# @sero-ai/plugin-starling

Starling Bank dashboard for Sero — view balances, transactions, savings goals, and spending insights.

## Sero Plugin Install

Install in **Sero → Admin → Plugins** with:

```text
git:https://github.com/monobyte/sero-starling-plugin.git
```

Sero clones the source repo, installs its dependencies locally, builds the UI,
and then hot-loads the plugin into the sidebar.

## Pi CLI Usage

Install as a Pi package:

```bash
pi install npm:@sero-ai/plugin-starling
```

The agent gains a `starling` tool (status, clear) and a `/starling` command.
State is stored in `.sero/apps/starling/state.json` (global scope).

## Sero Usage

When loaded in Sero, the web UI mounts in the main app area with three screens:

1. **Login** — enter your Starling Personal Access Token and set a PIN
2. **PIN unlock** — returning users enter their PIN to decrypt the stored token
3. **Dashboard** — tabbed view with overview, transactions, savings, and settings

### Security Model

- **Token encryption:** your PAT is encrypted via Electron's safeStorage API
  (macOS Keychain). Only this app, on this machine, by the current OS user can
  decrypt it.
- **PIN lock:** a UX-level lock to prevent casual access. The salted hash is
  stored for verification, but the PIN is NOT the encryption key — safeStorage
  is the security boundary.

## Dashboard Tabs

| Tab | Description |
|-----|-------------|
| **Overview** | Balance cards, spending by category chart, daily trend, recent transactions |
| **Transactions** | Searchable, grouped by date |
| **Savings** | Goal cards with progress bars |
| **Settings** | Lock dashboard, forget account |

## State File

```
~/.sero-ui/apps/starling/state.json   (Sero — global scope)
.sero/apps/starling/state.json         (Pi CLI — workspace-relative)
```

## Required API Scopes

Create a Personal Access Token at [developer.starlingbank.com](https://developer.starlingbank.com) with:

- `account:read`
- `balance:read`
- `transaction:read`
- `savings-goal:read`
