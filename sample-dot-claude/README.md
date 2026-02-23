# Sample `.claude` Configuration Files

This directory contains sample configuration files for Claude Code. These files define the permissions and settings for the Claude agent when working in this project.

## Usage

These are **sample files** and must be reviewed and customised before use. To activate them:

1. Review each file and update it to match your environment (hostnames, domains, etc.)
2. Copy the files to a `.claude` directory in your project root:

```bash
cp -r sample-dot-claude/.  .claude/
```

> The `.claude` directory is listed in `.gitignore` so your local settings will not be committed to the repository.

## Files

### `config.json`

Defines auto-approval rules — actions Claude can take without prompting you each time. This includes:

- **bash**: SSH commands to specific remote hosts (update with your actual hostnames)
- **read / write**: File access within the project directory (`**/*` covers all files)

### `settings.local.json`

Defines per-tool allow rules for Claude. This file grants permission to run specific commands such as:

- Network diagnostics: `ping`, `nc`, `dig`, `curl`
- SSH access
- SSL/TLS inspection: `openssl s_client`, `openssl x509`
- SNMP tools: `snmpget`, `snmpwalk`, `snmpbulkwalk`, `snmptrap`
- Web fetching from specific domains (update `yourdomain.com` etc. with your actual domains)

## Before Using

- Replace placeholder hostnames (`server1.domain.com`, etc.) in `config.json` with your actual server addresses
- Replace placeholder domains (`yourdomain.com`, `otherdomain.com`) in `settings.local.json` with domains relevant to your infrastructure
- Remove any tools or permissions that are not needed in your environment
