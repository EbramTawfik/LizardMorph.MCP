
# LizardMorph MCP Server

A Model Context Protocol (MCP) server for processing lizard X-ray images and generating TPS (Thin Plate Spline) files for morphological analysis. This server uses the MCP C# SDK and provides automated landmark detection for lizard morphometric studies.

> 🌐 **Web Version Available**: For a UI web interface, check out the [LizardMorph Web Application](https://github.com/Human-Augment-Analytics/LizardMorph) 

## Prerequisites

### Required Dependencies
- [.NET 10.0 SDK](https://dotnet.microsoft.com/download/dotnet/10.0)
- **Predictor Model File**: Since the predictor model is too large for this platform, download it here: 
  **[Download better_predictor_auto.dat](https://gatech.box.com/s/qky0pu7hd3y0b8okvl3r7zgfiaj961vb)**
  
  Place the downloaded `better_predictor_auto.dat` file in the root directory of your project.

## Available Tools

The LizardMorph MCP server provides the following tools for lizard X-ray image analysis:

### 1. `check_status`
**Description**: Check server status and verify .NET dependencies for LizardMorph image processing.
- Verifies .NET runtime availability
- Checks ImageSharp library status
- Validates predictor model file
- Tests file system access and memory status

### 2. `process_images_folder`
**Description**: Process a folder of lizard X-ray images and generate TPS files with landmark predictions.

**Parameters**:
- `imagesFolder` (required): Full path to the folder containing images to process
- `predictorFile` (optional): Full path to the predictor .dat file (defaults to `./better_predictor_auto.dat`)
- `outputDirectory` (optional): Full path to the output directory where TPS files will be saved (defaults to `./output`)

**Supported Image Formats**: `.jpg`, `.jpeg`, `.png`, `.tif`, `.tiff`, `.bmp`

### 3. `process_single_image`
**Description**: Process a single lizard X-ray image and generate TPS file with landmark predictions.

**Parameters**:
- `imagePath` (required): Full path to the image file to process
- `predictorFile` (optional): Full path to the predictor .dat file (defaults to `./better_predictor_auto.dat`)
- `outputDirectory` (optional): Full path to the output directory (defaults to `./output`)

### 4. `process_image_with_landmarks`
**Description**: Process a single lizard X-ray image and generate an image with landmarks visualized as colored circles.

**Parameters**:
- `imagePath` (required): Full path to the image file to process
- `predictorFile` (optional): Full path to the predictor .dat file (defaults to `./better_predictor_auto.dat`)
- `outputDirectory` (optional): Full path to the output directory (defaults to `./output`)
- `pointRadius` (optional): Radius of landmark points in pixels (defaults to 3)
- `numbered` (optional): Whether to number the landmarks (defaults to false)

### 5. `process_folder_with_landmarks`
**Description**: Process a folder of lizard X-ray images and generate images with landmarks visualized as colored circles.

**Parameters**:
- `imagesFolder` (required): Full path to the folder containing images to process
- `predictorFile` (optional): Full path to the predictor .dat file (defaults to `./better_predictor_auto.dat`)
- `outputDirectory` (optional): Full path to the output directory where files will be saved (defaults to `./output`)
- `pointRadius` (optional): Radius of landmark points in pixels (defaults to 50)
- `numbered` (optional): Whether to number the landmarks (defaults to false)

### 6. `list_processed_images`
**Description**: List all processed images and TPS files available in an output directory.

**Parameters**:
- `outputDirectory` (optional): Path to the output directory to scan for processed files (defaults to `./output`)

## Output Files

The server generates the following types of output files:

- **XML files**: Contain raw landmark coordinate data
- **TPS files**: Thin Plate Spline format files compatible with morphometric analysis software
- **Landmark visualization images**: JPEG images showing detected landmarks as colored circles (when using landmark visualization tools)

## Usage Examples

1. **Check if the server is ready**:
   ```
   Use the check_status tool to verify all dependencies and the predictor model
   ```

2. **Process a single image**:
   ```
   Use process_single_image with the path to your lizard X-ray image
   ```

3. **Process multiple images**:
   ```
   Use process_images_folder with the path to your folder containing multiple X-ray images
   ```

4. **Visualize landmarks**:
   ```
   Use process_image_with_landmarks or process_folder_with_landmarks to generate images showing detected landmarks
   ```

## Using the MCP Server from NuGet.org

To use the LizardMorph MCP server from NuGet.org, you must have the [.NET 10.0 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) installed and the predictor model file downloaded.

**Important**: Before using the server, make sure to download the predictor model:
- **[Download better_predictor_auto.dat](https://gatech.box.com/s/qky0pu7hd3y0b8okvl3r7zgfiaj961vb)**
- Place the file in your working directory or specify its path when using the tools

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
				"0.5.0",
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
				"0.5.0",
				"--yes"
			]
		}
	}
}
```

Make sure you have:
1. The [.NET 10.0 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) installed on your system
2. Downloaded the predictor model file from the link above and placed it in your working directory

## Getting Started

1. **Download the predictor model**: [better_predictor_auto.dat](https://gatech.box.com/s/qky0pu7hd3y0b8okvl3r7zgfiaj961vb)
2. **Place the model file** in your project root directory
3. **Configure your MCP client** using the configuration above
4. **Use the `check_status` tool** to verify everything is working correctly
5. **Start processing images** using the available tools

## Technical Details

- **File format support**: Processes common image formats and generates both XML and TPS output files
- **Visualization capabilities**: Can generate annotated images showing detected landmarks
- **Batch processing**: Supports processing entire folders of images efficiently