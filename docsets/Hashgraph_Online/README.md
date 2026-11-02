# HOL Registry Broker & Standards Docset

The archive keeps its existing `Hashgraph_Online` filename for compatibility with installed Dash docsets.

## Author
- **GitHub**: [hashgraph-online](https://github.com/hashgraph-online)
- **Twitter/X**: [@HashgraphOnline](https://x.com/HashgraphOnline)

## About HOL

HOL develops open standards and registry infrastructure for AI agents and MCP servers. The Registry Broker supports agent discovery and registration, HCS-based identity, and encrypted agent communication.

**Documented Capabilities:**
- [Agent and MCP server discovery](https://hol.org/registry) across supported protocols
- Multi-protocol integration, including A2A, MCP, and ERC-8004
- HCS-14 Universal Agent IDs (UAIDs)
- Client-side encrypted agent communication
- Registry Broker and Standards SDK integrations for development tools

## Documentation Source

- **Main Docs**: https://hol.org/docs/registry-broker/
- **SDK Docs**: https://hol.org/docs/libraries/standards-sdk/
- **Standards**: https://hol.org/docs/standards/hcs-1
- **Live Registry**: https://hol.org/registry

## How to Generate the Docset

### Prerequisites

- Node.js 20+
- pnpm (or npm)
- sqlite3 (usually pre-installed on macOS/Linux)
- ImageMagick (for icon generation)

### Generation Steps

The generation script (`generate-docset.ts`) is included in this folder.

```bash
# Create a working directory and copy the script
mkdir hol-docset && cd hol-docset
cp /path/to/generate-docset.ts .

# Create package.json
cat > package.json << 'EOF'
{
  "name": "hol-docset-generator",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "generate": "pnpm exec tsx generate-docset.ts"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "tsx": "^4.0.0",
    "typescript": "^5.0.0"
  }
}
EOF

# Install dependencies
pnpm install

# Generate docset
pnpm run generate

# Create icons (requires ImageMagick)
# Download icon from https://hol.org or use the one from hcs-improvement-proposals repo
magick /path/to/Logo_Icon.png -resize 16x16 Hashgraph_Online.docset/icon.png
magick /path/to/Logo_Icon.png -resize 32x32 Hashgraph_Online.docset/icon@2x.png

# Create archive
tar --exclude='.DS_Store' -cvzf Hashgraph_Online.tgz Hashgraph_Online.docset
```

### What the Script Does

1. Fetches documentation pages from hol.org (Docusaurus-based)
2. Extracts main content and creates clean, readable HTML
3. Creates a SQLite index (`docSet.dsidx`) for Dash search
4. Generates an `Info.plist` with proper docset metadata

## Indexed Content

The docset includes:
- **Registry Broker Documentation** - Agent discovery, chat, registration
- **Standards SDK** - Core SDK for HCS standards
- **HCS Standards** - Protocol specifications and guidance (consult the live docs for the current list)
- **API Reference** - Complete API client documentation
- **Tutorials & Guides** - Getting started, MCP server setup, encrypted chat

## Known Issues

None currently. Please report issues at https://github.com/hashgraph-online/standards-sdk/issues

## Links

- **Website**: https://hol.org
- **GitHub**: https://github.com/hashgraph-online
- **npm**: `@hashgraphonline/standards-sdk`
- **Telegram**: https://t.me/hashinals
