# Photoglacier MCP server for ChatGPT and Claude

Photoglacier publishes no public API or official MCP server, checked 17 November 2026. Cotlet.dev connects ChatGPT, Claude and other AI agents to your own signed-in photographer account.

Source: [Photoglacier integration page](https://cotlet.dev/integrations/photoglacier-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=photoglacier).

## What can your AI agent do?

The live page describes 8 hosted tools: 3 reads and 5 writes.

| Tool | Purpose |
| --- | --- |
| `view_gallery_stats` | List galleries, views, favorites and downloads. |
| `export_favorite_filenames` | Copy client favorites for Lightroom. |
| `read_photo_comments` | Collect photo comments into an edit list. |
| `upload_gallery_media` | Upload gallery photos and video. |
| `customize_gallery_design` | Set cover, palette, font and layout. |
| `set_download_sizes` | Enable downloads and choose sizes. |
| `set_gallery_password_and_pin` | Set gallery protection and the email gate. |
| `share_gallery_link` | Publish a gallery and return its link. |

Read tools run immediately. All 5 write tools ask for confirmation by default; you can change this per tool.
The agent returns the gallery link for you to send. Review Boards, team seats, custom domains, billing and account settings stay outside these tools.
Favorite filename export, gallery passwords and download PINs require Starter or above; photo comments require Pro. Your Photoglacier plan and storage limits apply.

## What can I ask?

> Show my galleries and their views, favorites and downloads.

> Export favorite filenames for the Lakeside wedding gallery.

> Collect photo comments into an edit list.

> Prepare the gallery design and ask before saving.

> Enable High and Web downloads after I confirm.

> Publish the approved gallery and return its link for me to send.

## Connect ChatGPT and Claude

1. [Get access to Photoglacier](https://cotlet.dev/signup?app=photoglacier).
2. Enable Photoglacier in the console and sign in at `https://photoglacier.com/app/login` in your Cotlet.dev Cloud Browser.
3. In ChatGPT, add `https://cotlet.dev/mcp/v1/connect` in Settings > Apps & Connectors, with OAuth.
4. In Claude, add the same URL in Settings > Connectors > Add custom connector.

## Connect Codex and Claude Code

Create an API key in your Cotlet.dev console and set `COTLET_API_KEY` in your environment.

Codex:

```toml
[mcp_servers.cotlet]
url = "https://cotlet.dev/mcp/v1"
bearer_token_env_var = "COTLET_API_KEY"
```

Claude Code:

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

## Optional local MCP wrapper

Python 3.10+, standard library only. This repository provides seven generic browser helpers: `photoglacier_guide`, `photoglacier_status`, `photoglacier_open`, `photoglacier_read`, `photoglacier_click`, `photoglacier_type`, `photoglacier_close`.
These helpers are separate from the 8 hosted business tools described above. Listing helpers requires no key; calling them requires `COTLET_API_KEY`.

```bash
export COTLET_API_KEY="your-key"
python3 photoglacier_agent.py serve
```

For a local MCP client, use an absolute path:

```json
{"mcpServers":{"photoglacier":{"command":"python3","args":["/absolute/path/to/photoglacier_agent.py","serve"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Other commands: `connect`, `status`, `guide`, `read`, `tools`.
The `read` command opens the browser, reads the page and closes the browser session.

## Questions

**Does Photoglacier have an API or official MCP server?**

The Cotlet.dev integration page reports no public API, developer documentation, official MCP server or official ChatGPT or Claude connector, checked 17 November 2026.

**Does the agent email clients?**

No. It returns the gallery link for you to send.

**Which account does it use?**

Your own photographer account, within the features your Photoglacier plan allows.

**Is this official?**

No. Cotlet.dev is independent and is not affiliated with Photoglacier or nord3 digital e.U.

## Access and control

Use your own Photoglacier account. You complete sign-in yourself. Disable Photoglacier for agents, reset the browser or change your Photoglacier password to revoke access.
Cotlet.dev is independent and is not affiliated with Photoglacier or nord3 digital e.U.
