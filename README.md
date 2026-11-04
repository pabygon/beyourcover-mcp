<p align="center">
  <img src="logo.png" alt="BeYourCover" width="128" height="128">
</p>

# BeYourCover MCP server

AI book covers, Amazon KDP print wraps and audiobook covers for AI agents.

BeYourCover runs a hosted [Model Context Protocol](https://modelcontextprotocol.io) server. An agent connected to it can create a book, generate genre-aware cover concepts, edit them, remove the cover text, make a square audiobook cover, upscale to print resolution and build a complete KDP paperback or hardcover wrap with a print-ready PDF. It can also list and download the books, covers and wraps already in the account.

This repository holds the listing files for MCP directories. The server itself is a hosted service: there is nothing to install or run.

- **Endpoint:** `https://beyourcover.com/api/mcp` (Streamable HTTP)
- **Docs:** https://beyourcover.com/mcp
- **Official MCP Registry:** `com.beyourcover/book-cover-generator` ([manifest](https://beyourcover.com/server.json))

## Connect

**claude.ai and Claude Desktop.** Add `https://beyourcover.com/api/mcp` as a custom connector and approve the sign-in. OAuth 2.1 with dynamic client registration: there is nothing to paste.

**Claude Code**, with OAuth:

```bash
claude mcp add --transport http beyourcover https://beyourcover.com/api/mcp
```

or with an API key from the BeYourCover dashboard:

```bash
claude mcp add --transport http beyourcover https://beyourcover.com/api/mcp \
  --header "Authorization: Bearer byc_sk_..."
```

**Cursor, VS Code and other clients** that take a JSON config:

```json
{
  "mcpServers": {
    "beyourcover": {
      "url": "https://beyourcover.com/api/mcp"
    }
  }
}
```

**Gemini CLI:**

```bash
gemini extensions install https://github.com/pabygon/beyourcover-mcp
```

**A client that takes only a local command:** bridge with `mcp-remote`:

```bash
npx -y mcp-remote https://beyourcover.com/api/mcp
```

## What you need

Any BeYourCover account can connect and read the tool list. The tools need an active plan:

- an [API plan](https://beyourcover.com/book-cover-generator-api), from $49/month with 150 credits, for the MCP server and the REST API only; or
- a [workspace plan](https://beyourcover.com/for-publishers), Starter from $79/month with 150 credits.

Without a plan, every tool call returns a message that names the plan requirement. It is not an authentication error.

Credits: 1 per cover image. Reading, listing, downloads, exports, upscales, wrap text changes and the KDP wrap calculator are free. Each tool's description states its cost.

## Tools

22 tools. The full table, with the cost of each, is at https://beyourcover.com/mcp.

| Area | Tools |
| --- | --- |
| Generate | `generate_covers`, `generate_cover_from_reference`, `get_generation_status` |
| Edit | `edit_cover` (edit, variations, text removal, audiobook version, upscale), `replace_person_on_cover`, `upload_reference_image`, `import_cover` |
| Print | `create_full_wrap`, `get_wrap`, `update_wrap_text`, `extend_wrap_front`, `calculate_kdp_wrap` |
| Files | `download_cover`, `export_cover` |
| Library | `list_books`, `list_covers_for_book`, `update_book`, `set_cover_visibility`, `list_templates_for_genre`, `get_credit_balance` |
| Agency | `list_clients`, `create_client` |

Generation is asynchronous. A create tool returns a `jobId`, and the agent polls `get_generation_status` until the job finishes, usually within 1 to 3 minutes.

## Example prompts

- "Design a cover for my psychological thriller *The Last Passenger* by Mara Voss: a night train, a passenger who vanishes between stations."
- "Show me the covers I already made for my book and give me the download links."
- "Turn my favourite cover into a KDP paperback wrap: 6×9, 320 pages, with this blurb: …"
- "What size does the full wrap need to be for a 5.5×8.5 paperback with 240 pages on cream paper?"

## Links

- [Privacy policy](https://beyourcover.com/privacy-policy)
- [Terms of service](https://beyourcover.com/tos)
- [REST API docs](https://beyourcover.com/api-docs)
- [Support](https://beyourcover.com/contact): support@beyourcover.com

## License

The files in this repository are MIT licensed. The BeYourCover service is proprietary and its use is governed by the [terms of service](https://beyourcover.com/tos).
