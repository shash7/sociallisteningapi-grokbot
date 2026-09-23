# SocialListeningAPI plugin for Grok Bot and Cursor

This plugin connects Grok Bot and Cursor to the hosted SocialListeningAPI MCP server. It searches
public social posts, Google results, and Instagram discovery data. Searches use your
SocialListeningAPI workspace credits. The plugin contains connection settings only; search tools
run on the hosted MCP server.

**Status:** Pre-release. The static OAuth client metadata is live. Cursor and Grok Bot sign-in still
need a live connection check before marketplace submission.

## What you need

- A SocialListeningAPI account with an active workspace and available credits.
- Grok Bot or Cursor with access to plugins.

Sign in through the SocialListeningAPI OAuth screen when prompted. The plugin does not ask you to
put an API key in chat or in this repository. OAuth grants access to search using your workspace
credits.

## Install and connect

After marketplace approval, open **Plugins** in Grok Bot or **Customize** in Cursor, find
**SocialListeningAPI**, and select **Install** or **Add**. Complete the browser sign-in and approve
the SocialListeningAPI workspace shown on the consent screen. Then check that the server lists its
tools.

For a local Cursor check before submission, copy this repository into
`~/.cursor/plugins/local/sociallisteningapi` and reload Cursor. The copy must include
`.cursor-plugin/plugin.json` and `mcp.json`. Local plugin loading in Cursor does not verify the
Grok Bot marketplace install, so check Grok Bot separately before publishing.

The MCP URL is `https://api.sociallisteningapi.com/mcp`. The connection uses a public, static
OAuth client ID at
`https://api.sociallisteningapi.com/.well-known/oauth-client/sociallisteningapi-cursor`.
The ID is not a secret. The OAuth scope is `mcp`. Each user signs in to their own
SocialListeningAPI workspace.

## Try it

Start with a free metadata call:

> List SocialListeningAPI's supported sources, credit costs, and known limits.

Then try one search after checking its credit cost:

> Search public Reddit posts for "social listening tools". Show relevant results with source links.

Ask for a particular source when you need one. Each social post search calls one source. For
example, searching Reddit and LinkedIn makes two requests and uses the sum of their credit costs.

## Tools and credits

| Tool or request | Credit cost for a successful request |
| --- | ---: |
| `get_supported_sources` | 0 |
| Facebook post search | 7 |
| LinkedIn post search or profile posts | 2 |
| Reddit comment search | 2 |
| Other current MCP searches and lookups | 1 |

Failed requests use 0 credits. Search results include remaining workspace credits. Use
`get_supported_sources` for the current route list, result types, costs, and source-specific limits.

The MCP can search public posts on LinkedIn, X, Reddit, Facebook, Hacker News, TikTok, and YouTube.
It also searches Google results and public Instagram users, hashtags, and places. Other tools fetch
Instagram and X profiles, X user posts and conversations, Reddit post comments, and LinkedIn
profile posts. Instagram search does not return posts. Reddit post search and Reddit comment search
are separate tools.

## Current limits

Results depend on public source availability and may miss matching posts. Search does not provide
complete historical coverage. The MCP does not provide continuous monitoring, scheduled alerts,
reply automation, native sentiment analysis, or lead scoring. Discourse search is available through
the SocialListeningAPI HTTP API but is not exposed by this MCP. Normalized results are returned by
default; `raw: true` adds the provider response.

Grok Bot or Cursor produces summaries from the returned data. Check source URLs and dates before
using a summary in a report.

## Links

- [MCP overview and setup](https://sociallisteningapi.com/mcp)
- [SocialListeningAPI app](https://app.sociallisteningapi.com)
- [Cursor plugin format](https://cursor.com/docs/reference/plugins)
- [Cursor MCP OAuth configuration](https://cursor.com/docs/mcp)

## Release checks

1. [x] Deploy the SocialListeningAPI OAuth client metadata endpoint.
2. [x] Confirm the metadata URL returns the client ID and Cursor redirect URLs.
3. [ ] Install this plugin in Cursor and complete OAuth with a test workspace.
4. [ ] Connect in Grok Bot, list supported sources, and run one approved paid search.
5. [x] Publish this repository publicly.
6. [ ] Submit the repository URL for marketplace review.

This repository is licensed under the [MIT License](LICENSE).
