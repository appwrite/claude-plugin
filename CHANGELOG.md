# Change Log

## 0.3.0

* Updated: Rewrote the CLI skill as guidance rather than a command catalog, deferring flags to `appwrite <command> --help`
* Added: `Query` relationship, aggregation, grouping, join and builder examples in every SDK skill
* Fixed: plugin and marketplace homepages point at the current Claude Code docs page

## 0.2.0

* Breaking: Replaced local `appwrite-api` and `appwrite-docs` MCP servers with the hosted server at `https://mcp.appwrite.io/`
* Removed: `userConfig` from the plugin manifest, no longer needed with the OAuth-authenticated hosted MCP server
* Updated: Descriptions reference the hosted Appwrite MCP server
* Updated: SDK skills content refreshed
* Updated: LICENSE changed from MIT to the Appwrite BSD-style license

## 0.1.0

* Added: Initial release of the Appwrite plugin for Claude Code
