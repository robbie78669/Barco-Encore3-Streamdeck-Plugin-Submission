# Encore3 Stream Deck Plugin

This repository contains the source code for the Encore3 Stream Deck Plugin, developed by Robbie Bruce from Barco NV. This plugin provides a set of actions to control Barco Encore3 devices directly from an Elgato Stream Deck.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Development](#development)
- [Architecture](#architecture)
- [Contributing](#contributing)
- [License](#license)

## Features

The plugin offers a variety of actions to streamline control over Encore3 systems:

*   **All Trans**: Transitions all layers from Preview to Program.
*   **Cut**: Immediately cuts all layers from Preview to Program.
*   **Change Source in Aux**: Changes a source within an Auxiliary output.
*   **Change Source in Layer**: Changes a source within a specific Layer.
*   **Recall Preset**: Recalls a saved Preset to either Preview or Program.
*   **Recall Next Preset**: Recalls the next Preset in the sequence to Preview.
*   **Cue**: Recalls a Cue.
*   **Freeze**: Freezes video for a selected input.
*   **Unfreeze**: Unfreezes video for a selected input.
*   **Use Input Backup**: Recalls a source backup.
*   **Use Primary Input**: Resets to the primary source input.
*   **Change MVR Layout**: Changes the layout of the multiviewer.
*   **Recall MVR Preset**: Recalls a multiviewer preset.
*   **Aux Test Pattern**: Recalls a test pattern for a given auxiliary output.
*   **Screen Test Pattern**: Recalls a test pattern for a given screen.

## Installation

To install the plugin, download the `com.barco.encore3.sdPlugin` package and double-click it. The Elgato Stream Deck software will handle the installation.

## Development

This project is a TypeScript-based Elgato Stream Deck plugin, bundled with Rollup.

### Prerequisites

*   Node.js (version 20 or higher recommended)
*   npm or yarn

### Setup

1.  Clone the repository:
    ```bash
    git clone https://github.com/robbie78669/encore3.git
    cd encore3
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```

### Building the Plugin

To build the plugin for distribution:
```bash
npm run build
```
This command compiles the TypeScript code and bundles it into `com.barco.encore3.sdPlugin/bin/plugin.js`.

### Watching for Changes

For development, you can use the watch script, which automatically rebuilds the plugin and restarts the Stream Deck application upon changes:
```bash
npm run watch
```

## Architecture

The plugin follows a standard Elgato Stream Deck plugin architecture:

*   **`com.barco.encore3.sdPlugin/`**: This directory contains the plugin's manifest, UI files, images, and the compiled JavaScript code.
    *   `manifest.json`: Defines the plugin's metadata, actions, and their properties.
    *   `ui/`: Contains HTML files for the Property Inspectors (UI that appears when configuring an action in Stream Deck).
    *   `imgs/`: Stores icons and images used by the plugin and its actions.
    *   `bin/plugin.js`: The compiled and bundled JavaScript code for the plugin.
*   **`src/`**: Contains the TypeScript source code.
    *   `plugin.ts`: The main entry point of the plugin, responsible for initializing and registering all actions with the Stream Deck client. It also handles global settings, including caching and restoring Encore3 frame connections.
    *   `actions/`: A directory containing individual TypeScript files for each Stream Deck action. Each file defines the logic for a specific action (e.g., `allTrans.ts`, `cut.ts`, `recallPreset.ts`).
    *   `device/`: Contains logic for communicating with Encore3 devices, including `emFrame.ts` for managing Encore3 frame data and connections.
    *   `common/`: Shared utilities, such as `settingsHandler.ts`.
    *   `utils.ts`: General utility functions, including a custom logger.
*   **Build Process**:
    *   The project uses **TypeScript** for type-safe development.
    *   **Rollup** is used as the module bundler, configured via `rollup.config.mjs`. It compiles `src/plugin.ts` into a single JavaScript file (`com.barco.encore3.sdPlugin/bin/plugin.js`), including source maps and minification (via Terser) for production builds.
    *   The `@elgato/streamdeck` SDK is used for interacting with the Stream Deck application.
*   **Device Communication**: The plugin establishes and manages connections to Encore3 frames (devices) using their IP addresses. These connections are persisted across Stream Deck restarts via global settings.

## User Guide: Property Inspectors

Each action in the Encore3 Stream Deck Plugin can be configured using its Property Inspector (PI). The PI is a web-based interface that appears in the Stream Deck software when you drag an action onto a key. It allows you to customize the behavior of the action by selecting Encore3 hosts, operators, sources, presets, and other relevant parameters.

### Common Elements

Most Property Inspectors share common configuration elements:

*   **Encore3 Host**: A dropdown to select the Encore3 frame (device) you want to control.
    *   **Add**: Click this button to reveal fields for adding a new Encore3 host.
        *   **IP Address**: Enter the IP address of your Encore3 frame.
        *   **Connect**: Attempts to connect to the entered IP address and add it to the list of available hosts.
        *   **Cancel**: Hides the "Add Host" fields.
    *   **Refresh**: Refreshes the list of available Encore3 hosts.
    *   **Remove**: Removes the currently selected Encore3 host from the list.
*   **Operator**: A dropdown to select the operator for the Encore3 system. This includes "All", "Super", and dynamically loaded operators from the Encore3 frame.
    *   **Password**: This field appears only when "Super" is selected as the operator, requiring a password for elevated privileges.
*   **Host IP**: (Read-only) Displays the IP address of the currently selected Encore3 host.
*   **Host ID**: (Read-only) Displays the unique ID of the currently selected Encore3 host.
*   **Status**: (Read-only) Shows the connection status to the selected Encore3 host.

### Action-Specific Configurations

Beyond the common elements, each action's Property Inspector provides specific settings. Below is a list of actions with their respective key icons and configuration options:

*   **All Trans** ![All Trans Key](com.barco.encore3.sdPlugin/imgs/actions/allTrans/allTransKey.png)
    *   **Trans time (frames)**: Sets the transition duration in frames (e.g., 30 frames for a 1-second transition at 30fps).
*   **Cut** ![Cut Key](com.barco.encore3.sdPlugin/imgs/actions/cut/cutKey.png)
    *   No additional action-specific settings.
*   **Change Source in Aux** ![Change Source in Aux Key](com.barco.encore3.sdPlugin/imgs/actions/cutAux/cutAuxKey_PVW.png)
    *   **Aux**: Selects the auxiliary output to change the source on.
    *   **Source**: Selects the input source to assign to the chosen auxiliary output.
*   **Change Source in Layer** ![Change Source in Layer Key](com.barco.encore3.sdPlugin/imgs/actions/cutLayer/cutLayerKey_PVW.png)
    *   **Screen Destination**: Selects the screen destination containing the layer.
    *   **Layer**: Selects the specific layer (e.g., 1A, 1B) within the chosen screen destination.
    *   **Source**: Selects the input source to assign to the chosen layer.
*   **Recall Preset** ![Recall Preset Key](com.barco.encore3.sdPlugin/imgs/actions/recallPreset/recallPresetKey_PVW.png)
    *   **Preset**: Selects the preset to recall.
    *   **Recall to**: Choose whether to recall the preset to "Preview" or "Program".
*   **Recall Next Preset** ![Recall Next Preset Key](com.barco.encore3.sdPlugin/imgs/actions/recallNextPreset/recallNextPresetKey.png)
    *   No additional action-specific settings.
*   **Cue** ![Cue Key](com.barco.encore3.sdPlugin/imgs/actions/recallCue/recallCueKey.png)
    *   **Cue**: Selects the cue to recall.
    *   **Action**: Choose the action to perform on the cue: "Recall", "Pause", or "Stop".
*   **Freeze** ![Freeze Key](com.barco.encore3.sdPlugin/imgs/actions/freeze/freezeKey.png)
    *   **Source**: Selects the input source to freeze.
*   **Unfreeze** ![Unfreeze Key](com.barco.encore3.sdPlugin/imgs/actions/unfreeze/unfreezeKey.png)
    *   **Source**: Selects the input source to unfreeze.
*   **Use Input Backup** ![Use Input Backup Key](com.barco.encore3.sdPlugin/imgs/actions/recallSourceBackup/recallSourceBackUp1Key.png)
    *   **Input**: Selects the primary input for which to activate a backup.
    *   **Backup**: Selects the specific backup source to use for the chosen input.
*   **Use Primary Input** ![Use Primary Input Key](com.barco.encore3.sdPlugin/imgs/actions/resetSourceBackup/resetsourcebackupKey.png)
    *   **Input**: Selects the input for which to reset to its primary source.
*   **Change MVR Layout** ![Change MVR Layout Key](com.barco.encore3.sdPlugin/imgs/actions/mvrLayoutChange/mvrLayoutChangeKey.png)
    *   **MVR Layout**: Selects the desired multiviewer layout.
*   **Recall MVR Preset** ![Recall MVR Preset Key](com.barco.encore3.sdPlugin/imgs/actions/recallMvrPreset/recallMvrPresetKey.png)
    *   **MVR Preset**: Selects the multiviewer preset to recall.
*   **Aux Test Pattern** ![Aux Test Pattern Key](com.barco.encore3.sdPlugin/imgs/actions/recallTestPatternOnAux/recallTestPatternAuxKey.png)
    *   **Aux**: Selects the auxiliary output to display the test pattern on.
    *   **Test Pattern**: Selects the specific test pattern to display (e.g., "100% Color Bars", "Black").
*   **Screen Test Pattern** ![Screen Test Pattern Key](com.barco.encore3.sdPlugin/imgs/actions/recallTestPatternOnScreen/recallTestPatternScreenKey.png)
    *   **Screen**: Selects the screen destination to display the test pattern on.
    *   **Test Pattern**: Selects the specific test pattern to display.

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for any bugs or feature requests.

## License

This project is licensed under the [LICENSE](LICENSE) file.
