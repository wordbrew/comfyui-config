# ComfyUI Configuration

This repository contains configuration files for automated ComfyUI Docker deployments.

## Structure

```
comfyui-config/
├── README.md              # This file
├── custom_nodes.json      # List of custom nodes to install
└── workflows/
    └── *.json            # Workflow files (auto-discovered)
```

## Files

### `custom_nodes.json`
Contains a structured list of all custom nodes to be installed in ComfyUI. Each node includes:
- Repository URL
- Branch name
- Priority (installation order)
- System dependencies (if needed)
- Description

**Format:**
```json
{
  "version": "1.0",
  "updated": "2025-10-16",
  "nodes": [
    {
      "name": "ComfyUI-Manager",
      "repo": "https://github.com/ltdrdata/ComfyUI-Manager.git",
      "branch": "main",
      "priority": 1,
      "description": "Essential - ComfyUI Manager"
    }
  ]
}
```

### `workflows/index.json`
Lists all available workflow files in the workflows directory.

**Format:**
```json
{
  "version": "1.0",
  "updated": "2025-10-16",
  "workflows": [
    "my_workflow_1.json",
    "my_workflow_2.json"
  ]
}
```

### Workflow Files
Individual ComfyUI workflow JSON files that can be loaded into ComfyUI. Export these from ComfyUI and upload them here.

## Usage

This configuration is designed to be used with the ComfyUI Docker deployment system. The Docker image will:

1. Download `custom_nodes.json` during build/startup
2. Clone and install each custom node automatically
3. Download workflow files from the `workflows/` directory

## Configuration URLs

Use these base URLs in your Docker build:

**Custom Nodes:**
```
https://raw.githubusercontent.com/wordbrew/comfyui-config/main/custom_nodes.json
```

**Workflows:**
```
https://raw.githubusercontent.com/wordbrew/comfyui-config/main
```

## Adding Workflows

1. Export your workflow from ComfyUI (Save button → Export)
2. Upload the `.json` file to the `workflows/` folder
3. Edit `workflows/index.json` and add the filename to the `workflows` array
4. Commit and push

Example:
```json
{
  "workflows": [
    "my_new_workflow.json"  ← Add this line
  ]
}
```

## Updating Custom Nodes

To add/remove custom nodes:
1. Edit `custom_nodes.json`
2. Add or remove node entries
3. Commit and push
4. Rebuild your Docker image

## Updating

To update the configuration:
1. Edit the JSON files in this repository
2. Commit and push changes
3. Rebuild or restart your Docker container

The Docker system will automatically pull the latest configuration.

## Version

Current version: 1.0  
Last updated: 2025-10-16

---

**Repository maintained by:** [@wordbrew](https://github.com/wordbrew)