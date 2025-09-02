
# LizardMorph MCP Server

A Model Context Protocol (MCP) server for processing lizard X-ray images and generating TPS (Thin Plate Spline) files for morphological analysis. This server uses the MCP C# SDK.

## Using the MCP Server from NuGet.org

To use the LizardMorph MCP server from NuGet.org, you must have the [.NET 10.0 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) (preview 6 or higher) installed.

Once the MCP server package is published to NuGet.org, you can configure it in your preferred IDE. Both VS Code and Visual Studio use the `dnx` command to download and install the MCP server package from NuGet.org.

- **VS Code**: Create a `<WORKSPACE DIRECTORY>/.vscode/mcp.json` file
- **Visual Studio**: Create a `<SOLUTION DIRECTORY>/.mcp.json` file

For both VS Code and Visual Studio, the configuration file uses the following server definition (replace the version if a newer one is available):

```json
{
	"servers": {
		"LizardMorph.MCP": {
			"type": "stdio",
			"command": "dnx",
			"args": [
				"LizardMorph.MCP",
				"--version",
				"0.2.0-beta",
				"--yes"
			]
		}
	}
}
```

## Configuring the MCP Server in Claude

To use the LizardMorph MCP server with Claude Desktop, add the following to your `claude_desktop_config.json` file:

```json
{
	"mcp_servers": {
		"LizardMorph.MCP": {
			"type": "stdio",
			"command": "dnx",
			"args": [
				"LizardMorph.MCP",
				"--version",
				"0.2.0-beta",
				"--yes"
			]
		}
	}
}
```

Make sure you have the [.NET 10.0 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) (preview 6 or higher) installed on your system.