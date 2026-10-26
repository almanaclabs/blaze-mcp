# Installing the Blaze MCP server

Blaze is a hosted MCP server. Do not clone, build, or run anything, and do not ask the user for an API key.

1. Add this entry to the MCP settings file (for Cline, `cline_mcp_settings.json`):

   ```json
   {
     "mcpServers": {
       "blaze": {
         "type": "streamableHttp",
         "url": "https://app.blaze.ai/mcp"
       }
     }
   }
   ```

2. The server answers unauthenticated requests with `401` and an OAuth 2.1 challenge. The client registers itself
   (dynamic client registration) and opens a browser window. Ask the user to sign in to Blaze there and approve access.
   If they have no account, they can create one at https://www.blaze.ai (free trial).

3. Check the connection by calling `list_workspaces`. It returns the user's workspaces; every other tool except
   `search_fonts` needs one of the returned `workspace_key` values.

If the client can't do OAuth for remote servers, use the stdio bridge instead:

```json
{
  "mcpServers": {
    "blaze": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://app.blaze.ai/mcp"]
    }
  }
}
```
