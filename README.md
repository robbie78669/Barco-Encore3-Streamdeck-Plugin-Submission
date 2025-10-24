# Encore3 Stream Deck Plugin

This repository contains the necessary files to submit the Encore3 Stream Deck Plugin for Elgato Marketplace, developed by Robbie Bruce from Barco NV. This plugin provides a set of actions to control Barco Encore3 devices directly from an Elgato Stream Deck.

[Barco Encore3 Website](https://www.barco.com/en/product/encore3)

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Description](#description)

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

## Description

The Encore3 Streamdeck plugin enables an operator to interact with one or more Encore3 frames using various Encore3 actions.   

Each action in the Encore3 Stream Deck Plugin can be configured using its Property Inspector (PI). The PI is a web-based interface that appears in the Stream Deck software when you drag an action onto a key. It allows you to customize the behavior of the action by selecting Encore3 hosts, operators, sources, presets, and other relevant parameters.

For more information regarding Encore3, please visit [Barco's Encore product page](https://www.barco.com/en/product/encore3)

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

*   **All Trans** ![All Trans Key](/imgs/actions/allTrans/allTransKey.png)
    *   **Trans time (frames)**: Sets the transition duration in frames (e.g., 30 frames for a 1-second transition at 30fps).
*   **Cut** ![Cut Key](/imgs/actions/cut/cutKey.png)
    *   No additional action-specific settings.
*   **Change Source in Aux** ![Change Source in Aux Key](/imgs/actions/cutAux/cutAuxKey_PVW.png)
    *   **Aux**: Selects the auxiliary output to change the source on.
    *   **Source**: Selects the input source to assign to the chosen auxiliary output.
*   **Change Source in Layer** ![Change Source in Layer Key](/imgs/actions/cutLayer/cutLayerKey_PVW.png)
    *   **Screen Destination**: Selects the screen destination containing the layer.
    *   **Layer**: Selects the specific layer (e.g., 1A, 1B) within the chosen screen destination.
    *   **Source**: Selects the input source to assign to the chosen layer.
*   **Recall Preset** ![Recall Preset Key](/imgs/actions/recallPreset/recallPresetKey_PVW.png)
    *   **Preset**: Selects the preset to recall.
    *   **Recall to**: Choose whether to recall the preset to "Preview" or "Program".
*   **Recall Next Preset** ![Recall Next Preset Key](/imgs/actions/recallNextPreset/recallNextPresetKey.png)
    *   No additional action-specific settings.
*   **Cue** ![Cue Key](/imgs/actions/recallCue/recallCueKey.png)
    *   **Cue**: Selects the cue to recall.
    *   **Action**: Choose the action to perform on the cue: "Recall", "Pause", or "Stop".
*   **Freeze** ![Freeze Key](/imgs/actions/freeze/freezeKey.png)
    *   **Source**: Selects the input source to freeze.
*   **Unfreeze** ![Unfreeze Key](/imgs/actions/unfreeze/unfreezeKey.png)
    *   **Source**: Selects the input source to unfreeze.
*   **Use Input Backup** ![Use Input Backup Key](/imgs/actions/recallSourceBackup/recallSourceBackUp1Key.png)
    *   **Input**: Selects the primary input for which to activate a backup.
    *   **Backup**: Selects the specific backup source to use for the chosen input.
*   **Use Primary Input** ![Use Primary Input Key](/imgs/actions/resetSourceBackup/resetsourcebackupKey.png)
    *   **Input**: Selects the input for which to reset to its primary source.
*   **Change MVR Layout** ![Change MVR Layout Key](/imgs/actions/mvrLayoutChange/mvrLayoutChangeKey.png)
    *   **MVR Layout**: Selects the desired multiviewer layout.
*   **Recall MVR Preset** ![Recall MVR Preset Key](/imgs/actions/recallMvrPreset/recallMvrPresetKey.png)
    *   **MVR Preset**: Selects the multiviewer preset to recall.
*   **Aux Test Pattern** ![Aux Test Pattern Key](/imgs/actions/recallTestPatternOnAux/recallTestPatternAuxKey.png)
    *   **Aux**: Selects the auxiliary output to display the test pattern on.
    *   **Test Pattern**: Selects the specific test pattern to display (e.g., "100% Color Bars", "Black").
*   **Screen Test Pattern** ![Screen Test Pattern Key](/imgs/actions/recallTestPatternOnScreen/recallTestPatternScreenKey.png)
    *   **Screen**: Selects the screen destination to display the test pattern on.
    *   **Test Pattern**: Selects the specific test pattern to display.

