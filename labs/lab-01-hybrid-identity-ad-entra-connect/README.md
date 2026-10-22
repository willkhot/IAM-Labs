# Lab 1 — Building a Hybrid Identity Lab: Active Directory on Hyper-V (Part 1)

## Overview

This is the first lab I built on my own instead of following a course video. In the [hybrid identity exercise](../../entra/lab-04-hybrid-identity/) I learned how a company connects its on-premises Active Directory to Microsoft Entra ID, but I couldn't try any of it because I didn't have an on-prem setup to practice on. So I built one. I'm still a student learning this, so I kept it simple and used the default settings where I could.

In this part I set up a small company network for my made-up company, **Bam Co.**, on my own PC using Hyper-V. I created two virtual machines, one running Windows Server 2022 and one running Windows 11. I turned the server into a **domain controller** for a new Active Directory domain called `bamco.internal`, then joined the Windows 11 machine to that domain.

The big takeaway is that Active Directory depends on **DNS**. The workstation couldn't find the domain until I pointed its DNS at the domain controller. Once I did, the join worked on the first try.

Part 2 will connect this domain to my Entra tenant with **Entra Connect**. See [To Be Continued](#to-be-continued) at the bottom.

## Objectives

- Create virtual machines in Hyper-V and install Windows Server 2022 and Windows 11
- Install Active Directory Domain Services and promote a server to a domain controller
- Create a new forest and domain
- Check that the domain and its DNS zone were created
- Point a workstation's DNS at the domain controller and join it to the domain

## Tools & Technologies

| Category | Tools |
|---|---|
| Virtualization | Hyper-V on Windows 11 |
| Server | Windows Server 2022 Standard Evaluation (Desktop Experience) |
| Workstation | Windows 11 Enterprise Evaluation |
| Roles | Active Directory Domain Services (AD DS), DNS Server |
| Tools | Hyper-V Manager, Server Manager, DNS Manager, Command Prompt |

## Lab Environment

| Machine | Role | OS | Memory | IP address |
|---|---|---|---|---|
| `BAM-DC01` | Domain controller and DNS server | Windows Server 2022 | 8 GB | `192.168.1.31` |
| `BAM-WS01` | Workstation | Windows 11 Enterprise | 4 GB | `192.168.1.33` |

```text
              Hyper-V host (my PC)
   ┌──────────────────────────────────────────┐
   │                                          │
   │   BAM-DC01                 BAM-WS01      │
   │   Windows Server 2022      Windows 11    │
   │   AD DS + DNS              domain member │
   │   192.168.1.31             192.168.1.33  │
   │        │                        │        │
   │        └──── External switch ───┘        │
   └──────────────────────────────────────────┘

   Domain: bamco.internal   (NetBIOS name: BAMCO)
```

---

## Task 1 — Create the Virtual Machines

I used the **New Virtual Machine Wizard** in Hyper-V Manager twice, once for each machine. The settings are mostly the same for both:

| Setting | BAM-DC01 | BAM-WS01 |
|---|---|---|
| Generation | Generation 1 | Generation 1 |
| Startup memory | 8 GB | 4 GB |
| Network | External switch | External switch |
| Virtual hard disk | 127 GB, dynamically expanding | 127 GB, dynamically expanding |
| Install from | Windows Server 2022 evaluation ISO | Windows 11 Enterprise evaluation ISO |

The last page of the wizard shows a summary before the VM is created:

![Hyper-V wizard summary for BAM-WS01](screenshots/01-hyperv-vm-summary.png)

> Both VMs are on an **external** switch, so they sit on the same network as each other and can also reach the internet. Both operating systems are free evaluation versions from the Microsoft Evaluation Center.

---

## Task 2 — Install the Operating Systems

### 2.1 Windows Server 2022

When setup asked which edition to install, I picked **Standard Evaluation (Desktop Experience)**. The "Desktop Experience" option installs the normal Windows desktop. Without it, the server only has a command line.

![Choosing the Windows Server edition](screenshots/02-server-2022-edition.png)

After the install finished and I set the Administrator password, the server opened **Server Manager**, which is where most of the setup happens.

![Server Manager dashboard](screenshots/03-server-manager-dashboard.png)

### 2.2 Windows 11

Windows 11 setup wants a Microsoft work or school account. Since this PC is going to join my own domain, I chose **Sign-in options → Domain join instead**, which let me create a local account.

![Windows 11 setup: Domain join instead](screenshots/04-windows-11-domain-join-instead.png)

After setup I renamed both machines from their random default names to `BAM-DC01` and `BAM-WS01`. I did this before installing Active Directory so I wouldn't have to rename a domain controller later.

---

## Task 3 — Set Up the Domain Controller

### 3.1 Point the server's DNS at itself

The domain controller is also going to be the DNS server for the domain, so it needs to use **itself** for DNS. In the network adapter's IPv4 properties I set the preferred DNS server to `127.0.0.1`, which just means "this machine".

![Setting the DNS server to itself](screenshots/05-dc-dns-points-to-itself.png)

### 3.2 Install the AD DS role

**Server Manager → Add roles and features.** On the **Server Roles** page I checked **Active Directory Domain Services** and accepted the extra management tools it asked to add.

![Adding the AD DS role](screenshots/06-add-ad-ds-role.png)

### 3.3 Promote the server to a domain controller

Installing the role doesn't create a domain yet. After it finished, Server Manager showed a warning flag with a link to **Promote this server to a domain controller**.

![Promote this server to a domain controller](screenshots/07-promote-to-domain-controller.png)

That opens another wizard. Since this is the very first domain, I chose **Add a new forest** and entered `bamco.internal` as the root domain name.

![Creating a new forest](screenshots/08-new-forest-root-domain.png)

> A **forest** is the top-level container in Active Directory, and a **domain** lives inside it. A brand new environment needs a new forest. I used `.internal` so the name can't clash with a real website on the internet.

On the next page I left the defaults and set a DSRM password:

| Setting | Value |
|---|---|
| Forest and domain functional level | Windows Server 2016 |
| Domain Name System (DNS) server | Yes |
| Global Catalog (GC) | Yes |
| DSRM password | Set (used to repair or restore Active Directory if it breaks) |

![Domain controller options](screenshots/09-domain-controller-options.png)

I clicked through the remaining pages with the defaults. The NetBIOS name was filled in as `BAMCO`. The prerequisites check passed with a couple of warnings, and I clicked **Install**. The server restarted on its own when it was done.

![Prerequisites check](screenshots/10-prerequisites-check-install.png)

### 3.4 Check that it worked

After the restart, **Server Manager → Local Server** shows the computer name `BAM-DC01` and the domain `bamco.internal` where it used to say `WORKGROUP`.

![Server is now a domain controller](screenshots/11-server-is-domain-controller.png)

**Tools → DNS** opens DNS Manager. The wizard created a forward lookup zone for `bamco.internal` and a host (A) record pointing `bam-dc01` to `192.168.1.31`. This is how other machines find the domain controller.

![DNS Manager showing the bamco.internal zone](screenshots/12-dns-manager-zone.png)

---

## Task 4 — Join the Workstation to the Domain

### 4.1 Find the domain controller's IP

On `BAM-DC01` I ran `ipconfig` to get its address:

```text
ipconfig
```

![ipconfig on the domain controller](screenshots/13-dc-ipconfig.png)

### 4.2 Point the workstation's DNS at the domain controller

This is the step that matters most. By default the workstation asks my home router for DNS, and the router has no idea what `bamco.internal` is. On `BAM-WS01` I went to **Settings → Network & internet → Ethernet → DNS server assignment → Edit**, switched it to **Manual**, and set the preferred DNS to `192.168.1.31`.

![Setting the workstation's DNS](screenshots/14-workstation-dns-setting.png)

I also turned off IPv6 on the workstation's network adapter so it would only use the IPv4 DNS server I had just set.

### 4.3 Test it

`ipconfig /all` confirmed the DNS server was now `192.168.1.31`, and a ping showed the workstation could reach the domain controller.

```text
ipconfig /all
ping 192.168.1.31
```

![DNS server confirmed and ping successful](screenshots/15-workstation-ping-dc.png)

### 4.4 Join the domain

**Settings → System → About → Domain or workgroup → Change.** Under **Member of**, I selected **Domain** and typed `bamco.internal`.

![Entering the domain name](screenshots/16-join-domain-name.png)

Windows then asked for an account that's allowed to join computers to the domain. I used the domain's Administrator account, written as `BAMCO\Administrator`.

![Entering domain credentials](screenshots/17-join-domain-credentials.png)

And it worked:

![Welcome to the bamco.internal domain](screenshots/18-welcome-to-domain.png)

`BAM-WS01` is now a member of `bamco.internal`. After a restart, domain accounts can be used to sign in to it.

---

## Things I Would Fix

- The domain controller is still getting its IP address from DHCP. I only changed its DNS setting, and the prerequisites check warned me about this. A domain controller should have a static IP, because the workstation finds the domain through that address. If my router gave the server a different address, the workstation's DNS setting would stop working. I'll set a static IP before Part 2.
- I joined the workstation using the domain Administrator account. That's fine for a lab, but from what I understand a real company wouldn't use its main admin account just to join a computer.

## What I Learned

- How to create VMs in Hyper-V and install Windows Server and Windows 11 from ISO files
- Installing the AD DS role is only step one. The server isn't a domain controller until it's promoted
- The difference between a forest and a domain, and why a new environment starts with a new forest
- Active Directory relies on DNS. The domain controller runs DNS for the domain, and clients have to use it as their DNS server to find the domain
- To actually check that things worked (Server Manager, DNS Manager, `ipconfig`, `ping`) instead of just assuming
- A domain controller needs a static IP. I missed that the first time

---

## To Be Continued

**Part 2: Connect Active Directory to Microsoft Entra ID with Entra Connect.**
*This section will be updated when Part 2 is done.*

---

> **Note:** Everything here runs on local virtual machines on my own PC. My host computer's name, my name and local account, file paths, the device and product IDs, and the network adapter's MAC address have been redacted from the screenshots. The IP addresses are private addresses on my home network, and all passwords shown are masked. `bamco.internal` is a made-up domain that only exists inside this lab.

[← Back to IAM Labs](../)
