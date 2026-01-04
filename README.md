# 10 Ways to Ruin Your Proxmox Setup - And How Not To

This repository contains the source code for the book **"10 Ways to Ruin Your Proxmox Setup - And How Not To"**.

## 🚀 TL;DR: What You Will Learn
This guide bridges the gap between "it works" and "it works reliably." 

Most Proxmox tutorials show you how to click through the installer, but they don't tell you **why your VMs feel sluggish** on that shiny new RAIDZ pool, or **why your cluster locked up** when you unplugged one node.

**You will learn:**
1.  **Storage Architecture:** Why RAIDZ kills VM performance and why ZFS often needs less RAM than commonly claimed (when designed correctly)..
2.  **High Availability:** Why enabling HA on 2 nodes guarantees downtime (and how to fix it).
3.  **Operations:** How to backup correctly, why Docker belongs in a VM, and how to monitor the silence before the crash.

---

## 📖 Sneak Peek

### Why RAIDZ is (usually) a mistake for VMs
> "The counterintuitive result is that a RAIDZ vdev with six disks delivers random IOPS roughly equivalent to a single disk."

You'll learn why **RAIDZ** excels at large sequential files (Backups, ISOs) but crumbles under the random I/O of Virtual Machines. The guide explains why **Mirrored VDEVs (RAID 10)** are almost always the superior choice for VM workloads, even if it costs you some capacity.

### The "Host CPU" Trap
> "The 'host' CPU type is seductive because it makes intuitive sense... until you try to migrate."

Using the `host` CPU type gives maximum performance but breaks live migration between different CPU generations. The book guides you to the sweet spot (`x86-64-v2-AES` or `v3`) to balance performance with cluster compatibility.

---

## 🔍 Excerpt from Chapter 8
*From "Running Docker Directly on the Proxmox Host"*

> It starts innocently enough. You need a quick container for a small service... What could possibly go wrong?
>
> As it turns out, quite a lot.
>
> **The iptables Conflict**
> The most common and most frustrating issue involves iptables. Both Proxmox and Docker manipulate iptables rules to manage network traffic, and they don't coordinate with each other. Docker might insert rules that bypass Proxmox's firewall entirely, exposing services you thought were protected.
>
> **The Solution**
> Take the extra five minutes to create a Docker VM. Your future self, not debugging iptables rules at midnight, will thank you.

---

## 🛠 Building the Book

The book is written in **AsciiDoc**. To generate the PDF yourself:

### Prerequisites

```bash
# macOS (Homebrew)
brew install asciidoctor

# Or via Gems
gem install asciidoctor-pdf
```

### Compile

```bash
# Generate PDF
asciidoctor-pdf index.adoc -o "10_Ways_to_Ruin_Your_Proxmox_Setup.pdf"

# Generate HTML
asciidoctor index.adoc
```

## ☕️ Support

This project is free and open.
If this guide saved your weekend (or your cluster), consider buying me a coffee!

<a href="https://buymeacoffee.com/swamirama" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>