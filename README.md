# Nexon Interface - Cheat UI Library for Roblox Executors

**Nexon Interface** is the ultimate cheat UI library designed for Roblox executors. It provides a fast, efficient, and smooth user interface that lets you create windows, buttons, sliders, and toggles for your custom cheats. Whether you want to control in-game cheats, settings, or create a custom control panel, this library makes it easy to inject UI into any Roblox game.

**Note**: This library requires the use of an **exploit executor** like **Krnl**, **Synapse X**, or **ScriptWare**. You will not be able to use this library in Roblox Studio or in games that block external scripts.

## Features
- **Draggable Windows**: Easily create custom windows for your cheat menu or control panel.
- **Interactive Buttons**: Create buttons that trigger your custom cheat functions or game mods with smooth animations.
- **Toggle Buttons**: Make switches for enabling/disabling cheats or game modifications.
- **Sliders**: Add sliders to control cheat parameters, such as speed, jump power, or custom hacks.
- **Customizable UI**: Completely change the colors, sizes, and animations to suit your needs.

## How to Use Nexon Interface with an Executor

### Step 1: Set Up the Script in Your Executor

To get started, you need a Roblox executor (such as **Krnl**, **Synapse X**, or **ScriptWare**) installed on your PC. If you don’t have one, you will need to download and set it up.

1. **Get the Source Code**:
   - Copy the source code of **Nexon Interface** from the script provided in this document.
   
2. **Inject the Script**:
   - Open your Roblox game.
   - Open your **exploit executor** and inject it into the game.
   - In the executor, paste the **Nexon Interface** source code.

3. **Execute the Script**:
   - Execute the script by pressing the **Execute** button in your executor. 
   - This will load **Nexon Interface** into your Roblox game, and the UI elements will become accessible.

### Step 2: Using Nexon Interface to Create UI Elements

Once the script is successfully injected and running, you can start creating cheat UI elements like windows, buttons, and sliders. Below is a quick guide to using the most common functions.

#### Example: Creating a Window

You can create a draggable window where you can put your cheats or controls. Here’s how you can do it:

```lua
local NexonInterface = require(game:GetService("ReplicatedStorage"):WaitForChild("NexonInterface"))

local myWindow = NexonInterface:createWindow(game.Players.LocalPlayer.PlayerGui, "Cheat Menu", UDim2.new(0, 400, 0, 300), UDim2.new(0.5, -200, 0.5, -150))
