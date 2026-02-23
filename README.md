# Claude Triage Robot

This repository is an example of how to use [Claude Code](https://claude.ai/code) as an automated triage assistant for remote servers and network equipment.

Claude can SSH into servers, query devices via SNMP, run network diagnostics, and report on the health of your infrastructure — all driven by natural language prompts.

## How It Works

1. **`hosts.md`** — describes your infrastructure: hostnames, platforms, access methods, and SNMP credentials. Claude reads this to know how to reach each device.
2. **`CLAUDE.md`** — instructs Claude on the repository purpose and how to interpret host entries.
3. **`.claude/`** — local configuration (not committed) that grants Claude permission to run SSH, SNMP, and network diagnostic commands without prompting each time.

## Getting Started

### 1. Clone and customise the host inventory

Edit [hosts.md](hosts.md) to reflect your own infrastructure. Follow the format already used — hostname, platform, access method, and SNMP details where applicable.

### 2. Set up Claude Code permissions

Copy the sample configuration files to a local `.claude` directory (this directory is gitignored and won't be committed):

```bash
cp -r sample-dot-claude/. .claude/
```

Then edit the files in `.claude/` to match your environment:
- Replace placeholder hostnames in `config.json` with your actual server addresses
- Replace placeholder domains in `settings.local.json` with your domains
- Remove any tools or permissions you don't need

See [sample-dot-claude/README.md](sample-dot-claude/README.md) for details on what each setting does.

### 3. Open the project in Claude Code

```bash
claude
```

Then type a natural language prompt to begin triage.

#### OR try one shot prompting

Try one shot (non interactive) prompting, with the permissions set correctly this provides good results, especially to intergreated into other tools as described in [Using AI for Automated Triage and Impact Analysis](https://kcsinclair42.substack.com/p/using-ai-for-automated-triage-and).
```
claude -p 'YOUR PROMPT HERE, SEE BELOW FOR EXAMPLES' --verbose
```
--verbose is a good option when debugging things, not normally needed.

## Required Expertise

To work effectively with this setup, familiarity with the following is helpful:

- **Linux** — for SSH-based server triage
- **Unifi** — for network equipment diagnostics
- **SNMP** — for querying routers, switches, and servers without SSH
- **macOS** — if any hosts run macOS

## Sample Prompts

The following are real examples of prompts and the responses Claude produced.

---

### Check internet link utilisation on a router

**Prompt:**
> can you please check the current utilisation of the internet link on router1, which is using ethernet port 5

**Response:**
```
Here are the results for router1 — Ethernet Port 5 (eth4):

| Metric              | Value                              |
|---------------------|------------------------------------|
| Interface           | eth4 (ifIndex 8)                   |
| Operational Status  | Up                                 |
| Link Speed          | 2500 Mbps (2.5 GbE)               |
| Sample interval     | 9.1 seconds                        |
| In (download)       | 4.60 Mbps (0.18% utilisation)     |
| Out (upload)        | 2.60 Mbps (0.10% utilisation)     |

The internet link on port 5 is operational and carrying very light traffic —
under 5 Mbps inbound and under 3 Mbps outbound, which is well under 0.2% of
the 2.5 Gbps link capacity.
```

---

### Check server performance and disk space

**Prompt:**
> please check on the general performance of server2 and verify how much free disk space it has

**Response:**
```
## server2 (server2.domain.com) — Linux

### CPU
4 CPUs, all reporting 1% load — essentially idle.

### Memory
|               | Size  | Used    | Free               |
|---------------|-------|---------|--------------------|
| Physical RAM  | 40 GB | ~7.3 GB | ~32.7 GB (82% free)|
| Swap          | —     | 0       | no swap in use     |

### Disk Space
| Filesystem          | Size    | Used    | Free    | Use%  |
|---------------------|---------|---------|---------|-------|
| / (root)            | 1.82 TB | 1.21 TB | ~623 GB | 66.6% |
| /data               | 112.7 GB| ~121 MB | ~112.6 GB| <1%  |

### Summary
server2 is performing well — CPU is nearly idle, memory usage is light,
and there's ~623 GB of free disk space on the main volume (~33% remaining).
```
