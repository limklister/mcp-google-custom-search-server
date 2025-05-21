# MCP Google Custom Search Server
[![smithery badge](https://smithery.ai/badge/@limklister/mcp-google-custom-search-server)](https://smithery.ai/server/@limklister/mcp-google-custom-search-server)

A Model Context Protocol (MCP) server that provides web search capabilities through Google's Custom Search API. This server enables Language Learning Models (LLMs) to perform web searches using a standardized interface.

## 🌟 Features

- Seamless integration with Google Custom Search API
- Model Context Protocol (MCP) compliant server implementation
- Type-safe implementation using TypeScript
- Environment variable configuration
- Input validation using Zod
- Configurable search results (up to 10 per query)
- Formatted search results including titles, URLs, and descriptions
- Error handling and validation
- Compatible with Claude Desktop and other MCP clients

## 📋 Prerequisites

Before you begin, ensure you have:

1. A Google Cloud Project with Custom Search API enabled

   - Visit [Google Cloud Console](https://console.cloud.google.com)
   - Enable the Custom Search API
   - Create API credentials

2. A Custom Search Engine ID

   - Visit [Programmable Search Engine](https://programmablesearchengine.google.com/)
   - Create a new search engine
   - Get your Search Engine ID

3. Local development requirements:
   - Node.js (v18 or higher)
   - npm (comes with Node.js)

## 🚀 Quick Start

### Installing via Smithery

To install Google Custom Search Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@limklister/mcp-google-custom-search-server):

```bash
npx -y @smithery/cli install @limklister/mcp-google-custom-search-server --client claude
```

### Manual Installation
1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/mcp-google-custom-search-server.git
   cd mcp-google-custom-search-server
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Create a .env file:

   ```bash
   GOOGLE_API_KEY=your-api-key
   GOOGLE_SEARCH_ENGINE_ID=your-search-engine-id
   ```

4. Build the server:

   ```bash
   npm run build
   ```

5. Start the server:
   ```bash
   npm start
   ```

## 🔧 Configuration

### Environment Variables

| Variable                | Description                       | Required |
| ----------------------- | --------------------------------- | -------- |
| GOOGLE_API_KEY          | Your Google Custom Search API key | Yes      |
| GOOGLE_SEARCH_ENGINE_ID | Your Custom Search Engine ID      | Yes      |

### Claude Desktop Integration

Add this configuration to your Claude Desktop config file (typically located at `~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "google-search": {
      "command": "node",
      "args": [
        "/absolute/path/to/mcp-google-custom-search-server/build/index.js"
      ],
      "env": {
        "GOOGLE_API_KEY": "your-api-key",
        "GOOGLE_SEARCH_ENGINE_ID": "your-search-engine-id"
      }
    }
  }
}
```

## 📖 API Reference

### Available Tools

#### search

Performs a web search using Google Custom Search API.

**Parameters:**

- `query` (string, required): The search query to execute
- `numResults` (number, optional): Number of results to return
  - Default: 5
  - Maximum: 10

**Example Response:**

```
Result 1:
Title: Example Search Result
URL: https://example.com
Description: This is an example search result description
---

Result 2:
...
```

## 🛠️ Development

### Project Structure

```
mcp-google-custom-search-server/
├── src/
│   └── index.ts          # Main server implementation
├── build/                # Compiled JavaScript output
├── .env                  # Environment variables
├── package.json          # Project dependencies and scripts
├── tsconfig.json         # TypeScript configuration
└── README.md            # Project documentation
```

### Available Scripts

- `npm run build`: Compile TypeScript to JavaScript
- `npm start`: Start the MCP server
- `npm run dev`: Watch mode for development

### Testing

1. Using MCP Inspector:

   ```bash
   npx @modelcontextprotocol/inspector node build/index.js
   ```

2. Manual testing with example queries:
   ```bash
   # After starting the server
   {"jsonrpc":"2.0","id":1,"method":"callTool","params":{"name":"search","arguments":{"query":"example search"}}}
   ```

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- Built with [Model Context Protocol (MCP)](https://github.com/anthropics/model-context-protocol)
- Uses Google's Custom Search API
- Inspired by the need for better search capabilities in LLM applications
