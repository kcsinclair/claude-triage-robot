# CLAUDE.md

This sample file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a documentation repository for the ORGANISATION Network and Server infrastructure. It contains information about servers, websites, and network equipment maintained by the PACK organisation.

## Repository Structure

- **README.md**: Overview of the repository and required expertise (Linux, Unifi, macOS)
- **hosts.md**: Inventory of network hosts with access details

## Host Documentation Format

When adding or updating host entries in `hosts.md`, follow this structure:

```markdown
# hostname
* hostname.domain.com (or domain)
* platform (linux, unifi uxg max, website, etc.)
* [optional] server role/purpose (e.g., kvm, application, database, monitoring, etc.)
* [optional] hosting information (for websites: "hosted on hostname")
* ssh available/not available (or "ssh available to hostname" for hosted services)
* snmp available/not available including the SNMP credentials
```

## Key Infrastructure Details

- **Access Methods**: Some devices support SSH access, others require network troubleshooting tools (ping, traceroute)
- **Platforms**: Infrastructure includes Linux servers, Unifi network equipment, and macOS systems
- **Current Hosts**:
  - server1 (server1.domain.com) - Linux, SSH available - KVM, application, database and website server, router for 192.168.XX.0
  - server2 (server2.domain.com) - Linux, SSH available - Development virtual machine, hosted on server1.
  - router1 (router1.domain.com)  - Unifi UXG Max, no SSH - Router for 192.168.1.0
  - switch1 (192.168.1.XX)  - Netgear switch for network
  - www.domain.com - Website hosted on server2, SSH available to server2
  

## Working with This Repository

This is a documentation-only repository with no build, test, or deployment commands. When updating:

1. Maintain consistent formatting in host documentation
2. Verify access information is current
3. Include platform and access method details for all hosts
