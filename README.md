Q-SYS Default Conference Room Template

Baseline UCI + Gain Auto-Mute + Shared Camera Control Framework

Overview

This repository contains a Q-SYS Designer baseline template intended to speed up development of standard conference room control systems.

It provides a reusable starting point that includes:

A prebuilt UCI navigation framework
A gain auto-mute utility with dynamic detection
A meter popup behavior for gain interaction
A shared multi-camera control framework for third-party plugins

This is a programming template, not a fully integrated AV system.

What This Template Does
UCI Navigation Framework
Multi-layer navigation (Audio / Video / Camera / Help)
Interlocked navigation buttons
Dynamic legends via UCI variables
Centralized configuration for:
Page name
Layer names
Default layer
Button mappings

Behavior:

Only one content layer visible at a time
Invalid selections fall back to Home
Easy to expand by adding entries to the config table
Gain Auto-Mute Utility

Automatically detects and manages gain components.

Detection Requirements:

gain
stepper.increase
stepper.decrease
stepper.time

Behavior:

Populates:
Controls.gainList
Controls.gainButtons
Dynamically attaches event handlers
Applies auto-mute logic:
Gain ≤ threshold → Mute ON
Gain > threshold → Mute OFF
Button disabled → Force unmute

Use Case:
Quickly expose and manage gain controls without manually mapping every component.

Meter Popup Behavior

Provides temporary meter visibility during gain adjustments.

Behavior:

Press gain stepper → Meter layer shows immediately
Release stepper → Timer starts
After delay → Meter layer hides

Configurable:

HIDE_AFTER controls delay duration
Shared Camera Control Framework

A structured approach to controlling multiple third-party cameras using a single UCI control set.

Camera System Design
Manual Camera Registration

Cameras are explicitly defined in script:

local C1 = Component.New("cam1")
local C2 = Component.New("cam2")

camTable = { C1, C2 }

Cameras are not auto-discovered. You must add them manually.

Shared Control Mapping

When a camera is selected, its controls are mapped into a shared control table:

Pan Up / Down / Left / Right
Zoom In / Out
Preset Recall 1–3

All UCI control buttons operate the currently selected camera only.

Camera Selection
Controlled via Controls.whichCamera
Interlocked button behavior
Rebinds control map on selection
Clears active control states when switching
Tracking Mode

Each camera maintains its own tracking state.

Controls:

cameraTrack[1] → Tracking ON
cameraTrack[2] → Tracking OFF

Behavior:

Tracking ON:
Enables auto tracking on camera
Hides manual PTZ controls
Tracking OFF:
Disables tracking
Restores manual controls
UCI Expectations

The script assumes:

Controls.whichCamera → one button per camera
Controls.cameraControls → matches control map order
Controls.cameraTrack[1/2] → tracking toggle
Camera plugin control names match script exactly
What This Template Does NOT Do

This is intentional.

No video routing logic
No source switching
No display control
No soft codec integration
No automatic camera discovery
No finalized DSP tuning

This is a starting framework, not a completed room.

How to Use
1. Duplicate the Template

Do not build directly on the base file—copy it per project.

2. Configure UCI

Update:

Page name
Layer names
Navigation labels
Visible UI groups
3. Validate Gain Components

Ensure gain blocks include required controls:

gain
mute
steppers
4. Add Cameras

For each project:

Create camera plugin components
Name them consistently (cam1, cam2, etc.)
Add to script
Update camTable
Match control names to plugin
5. Expand Per Project

Add whatever the room actually needs:

Routing logic
Display control
Codec integration
Automation logic
Network/API control
Script Modules
UCI Navigation
Layer switching
Interlocked buttons
Legend syncing
Gain Auto-Mute
Component detection
Auto mapping
Threshold-based mute logic
Meter Popup
Temporary meter display
Timer-based hide
Camera Control
Manual camera registration
Shared control mapping
Tracking state per camera
UI visibility management
Best Practices
Keep component naming consistent
Do not rely on auto-detection for cameras
Keep UCI control arrays aligned with script
Validate plugin control names
Use local variables in Lua
Avoid hardcoding values throughout scripts
Design Philosophy

Build once. Reuse everywhere.

This template exists to eliminate repetitive setup work and give you a clean, predictable starting point for every room.

It focuses on:

Speed
Consistency
Maintainability
Real-world usability
Version

v1.0 – Baseline Template

Notes

This template handles the repetitive front-end work:

UCI structure
Navigation logic
Gain handling
Camera control framework

Everything else should be layered on top per project.
