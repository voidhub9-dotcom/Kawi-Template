<div align="center">

<img src="https://api.iconify.design/lucide/flame.svg?color=%23FF4B9A" width="60" height="60" alt="Lucide flame" />

# KawiXD

**A single-file Roblox client UI. An Airflow foundation. A look of your own.**

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&amp;weight=500&amp;size=20&amp;duration=2800&amp;pause=1200&amp;color=FF4B9A&amp;center=true&amp;vCenter=true&amp;width=760&amp;height=48&amp;lines=Your+interface.+Your+colors.+Your+background.%3BAirflow+foundation.+Null+Fire+appearance." width="760" height="48" alt="Your interface. Your colors. Your background. Airflow foundation. Null Fire appearance." />

<p>
<img src="https://img.shields.io/badge/runtime-Luau-FF4B9A?style=flat-square" alt="Runtime: Luau" />
<img src="https://img.shields.io/badge/environment-client_executor-80E2EA?style=flat-square" alt="Environment: client executor" />
<img src="https://img.shields.io/badge/distribution-4_files-E6DEF3?style=flat-square" alt="Distribution: four files" />
<img src="https://img.shields.io/badge/appearance-v1-FF4B9A?style=flat-square" alt="Appearance profile version 1" />
</p>

[**Quick start**](#get-started) &nbsp;·&nbsp; [**Appearance**](#make-it-yours) &nbsp;·&nbsp; [**Native API**](#native-api-reference) &nbsp;·&nbsp; [**Extended API index**](#extended-api-index) &nbsp;·&nbsp; [**AI guide**](llms.txt)

</div>

---

> **Built for client executor scripts—not a Roblox Studio installation.** Load `Source.lua`, create a window, and build with the native Airflow-style API. Use `CreateKawiXDWindow` when you also want the Null Fire appearance methods.

<table>
<tr>
<td width="33%" valign="top">
<img src="https://api.iconify.design/lucide/panels-top-left.svg?color=%23FF4B9A" width="26" height="26" alt="Lucide panels-top-left" />
<h3>Keep the foundation</h3>
<p>Sidebar tabs, sub-tabs, split groupboxes, tabboxes, controls, and window-wide search. Familiar native methods, not a replacement widget API.</p>
</td>
<td width="33%" valign="top">
<img src="https://api.iconify.design/lucide/palette.svg?color=%23FF4B9A" width="26" height="26" alt="Lucide palette" />
<h3>Make it yours</h3>
<p>Null Fire, Null Ice, and Null Mono alongside native themes. Live palettes, image backgrounds, tint, dim, fit, and portable appearance profiles.</p>
</td>
<td width="33%" valign="top">
<img src="https://api.iconify.design/lucide/activity.svg?color=%23FF4B9A" width="26" height="26" alt="Lucide activity" />
<h3>Stay in motion</h3>
<p>Native window transitions, eased resizing, popup motion, and the draggable Dynamic Island minimize. Pin live statuses without building another overlay.</p>
</td>
</tr>
<tr>
<td valign="top">
<img src="https://api.iconify.design/lucide/sliders-horizontal.svg?color=%23FF4B9A" width="26" height="26" alt="Lucide sliders-horizontal" />
<h3>Controls with depth</h3>
<p>Toggles, sliders, steppers, dropdowns, keybinds, color pickers, editable tables, logs, readouts, dependencies, and tooltips.</p>
</td>
<td valign="top">
<img src="https://api.iconify.design/lucide/save.svg?color=%23FF4B9A" width="26" height="26" alt="Lucide save" />
<h3>State that travels</h3>
<p>Native flags, configs, share codes, and autoload. Separate JSON appearance import/export for a complete look, including extra background styling.</p>
</td>
<td valign="top">
<img src="https://api.iconify.design/lucide/smartphone.svg?color=%23FF4B9A" width="26" height="26" alt="Lucide smartphone" />
<h3>Fit the viewport</h3>
<p>Touch-aware controls, adaptive sizing, manual UI scale, and density presets. Viewport fitting—not physical DPI detection.</p>
</td>
</tr>
</table>

## Get started

### 1. Load the library

Load [`Source.lua`](Source.lua) directly in a compatible Roblox client executor. It returns the complete library, including the Airflow-derived core and the Null Fire appearance layer. This is not a Roblox Studio project: no ModuleScript installation, ReplicatedStorage setup, or LocalScript is required. The `.lua` filename contains Roblox Luau code.

The loading pattern matches the original Airflow docs: `loadstring(game:HttpGet(url))()`. Your executor must provide `loadstring` and client HTTP access. File configs, clipboard actions, and URL/file images depend on the corresponding executor APIs; do not assume every executor supports them.

### 2. Create your first window

Run this in the Roblox client executor you use for an experience you own or have permission to test:

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/voidhub9-dotcom/Kawi-Template/main/Source.lua"))()

local Window = Library:CreateKawiXDWindow({
    Name = "My Hub",
    ConfigurationSaving = { FolderName = "MyHub" }, -- Enabled is not a persistence switch
})

local Main = Window:CreateTab({
    Name = "Main",
    Icon = "layout-grid",
})

local Controls = Main:CreateGroupbox({
    Name = "Controls",
    Side = "Left",
})

local Enabled = Controls:CreateToggle({
    Name = "Enabled",
    Flag = "MyHub_Enabled",
    CurrentValue = true,
    Callback = function(value)
        print("Enabled:", value)
    end,
})

Controls:CreateSlider({
    Name = "Intensity",
    Min = 0,
    Max = 100,
    Increment = 5,
    CurrentValue = 65,
    Suffix = "%",
})

Window:CreateAppearanceTab({ Name = "Appearance", Icon = "palette" })
Window:SelectTab(Main)
```

### 3. Explore the showcase

[`Example.lua`](Example.lua) is a standalone KawiXD showcase with the complete library embedded. Run it separately; it does not need a second copy of `Source.lua`. Its demo controls change the interface only. It demonstrates selected native controls and the appearance editor, not every native element.

```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/voidhub9-dotcom/Kawi-Template/main/Example.lua"))()
```

### Window defaults

`CreateKawiXDWindow(options)` uses the native window factory and adds appearance methods. Its defaults are `Name = "KawiXD"`, `DefaultTheme = "Null Fire"` when no theme is supplied, and an explicit `ConfigurationSaving = { Enabled = false, FolderName = "KawiXD" }` option when no configuration options are supplied. **Important:** the source does not read `ConfigurationSaving.Enabled`; this supplied option does not disable native persistence or file APIs. Native window options remain available. Plain `Library:CreateWindow(options)` is still the native factory: it does not attach the appearance methods and does not inject the `Null Fire` default. On a fresh library instance the native palette is `Midnight`; the native title and config folder default to `KawiXD`. Previously selected library themes and a saved player default can affect the starting palette.

`CreateNullFireWindow` remains a backward-compatible alias. `Library.KawiXD` and `Library.NullFire` refer to the same metadata table, reporting version `1.0.0`.

## Make it yours

**Start with a palette. Add a background. Export the complete look.** These methods are attached by `CreateKawiXDWindow`; native controls stay unchanged.

### Pick a palette

| Preset | Character |
| :--- | :--- |
| `Null Fire` | ![Null Fire](https://img.shields.io/badge/-%23FF4B9A-FF4B9A?style=flat-square) Pink accent on dark surfaces; the enhanced factory default |
| `Null Ice` | ![Null Ice](https://img.shields.io/badge/-%2380E2EA-80E2EA?style=flat-square) Cyan accent on dark surfaces |
| `Null Mono` | ![Null Mono](https://img.shields.io/badge/-%23E6DEF3-E6DEF3?style=flat-square) Neutral monochrome palette |

```lua
Library:SetTheme("Null Ice")

local ok, err = Library:RegisterTheme("My Palette", {
    Accent = "#6AE2F0",
    AccentDark = Color3.fromRGB(40, 140, 160),
})

if ok then
    Library:SetTheme("My Palette")
else
    warn(err)
end
```

`RegisterTheme(name, palette)` returns `true`, or `false, error`. The name must contain non-whitespace text and be at most 64 characters; supply at least one color. Unspecified colors are filled from the current theme. Use native palette keys only: `Background`, `Surface`, `Surface2`, `Surface3`, `Stroke`, `StrokeHover`, `Accent`, `AccentDark`, `Text`, `Muted`, `Success`, `Warning`, and `Error`.

### Style a background

```lua
local ok, err = Window:SetBackgroundStyle({
    Source = "Deep Violet",
    Transparency = 0.25,
    Tint = "#FFFFFF",
    ScaleType = "Crop",
    Dim = 0.2,
})

if not ok then
    warn("Background unchanged:", err)
end

local style = Window:GetBackgroundStyle()
-- Clear the image explicitly:
-- Window:SetBackgroundStyle({ Source = "None" })
```

| Option | Accepted values |
| :--- | :--- |
| `Source` | Preset name, accessible Roblox image asset ID, supported image URL, local file, or `"None"` |
| `Transparency` | Number from `0` to `1` |
| `Tint` | `Color3` or `#RRGGBB` |
| `ScaleType` | `"Crop"`, `"Fit"`, `"Tile"`, or `"Stretch"` |
| `TileSize` | `{ X = 256, Y = 256 }`; each dimension from `1` to `4096` |
| `Dim` | Number from `0` to `1` |

Built-in background presets: **Deep Violet**, **Blood Red**, **Cyanic**, **Amber Glow**, **Bloomings**, and **Lavender Pink**. These are image presets, separate from color themes.

Invalid or unresolved sources leave the previous background intact. `GetBackgroundStyle()` returns a detached, normalized table with a hex-string tint.

> **Image compatibility:** An accessible Roblox image asset ID is the portable recommendation. Direct web images and local files depend on environment-specific file/custom-asset APIs and are not portable to every executor. An accepted asset ID can still fail to display because of permissions, moderation, or an incorrect image/decal ID. No upload picker is included.

### Export and restore a look

```lua
local snapshot = Window:GetAppearance()
local json, exportErr = Window:ExportAppearance()

if json then
    -- Store or transfer the JSON yourself, then restore it explicitly:
    local ok, applyErr = Window:ApplyAppearance(json)
    if not ok then
        warn(applyErr)
    end
else
    warn(exportErr)
end

-- A snapshot table works too:
-- local ok, err = Window:ApplyAppearance(snapshot)
```

Profiles contain **version, theme, background style, UI scale, adaptive sizing, density, and corner radius**. `GetAppearance()` returns a detached JSON-safe snapshot; `ExportAppearance()` returns JSON or `nil, error`; `ApplyAppearance(tableOrJSONString)` validates the profile before applying it and returns `true`, or `false, error`.

Appearance import/export is explicit: profiles are not automatically written to disk and do not include control flags, credentials, or gameplay state. Use native configs separately for flagged controls. Native theme files do not capture every background-style field; use `ExportAppearance()` for the complete appearance snapshot.

### Add the appearance editor

```lua
Window:CreateAppearanceTab({ Name = "Appearance", Icon = "palette" })

-- Equivalent library-level form:
-- Library:CreateAppearanceTab(Window, { Name = "Appearance" })
```

This optional tab adds the native theme manager, background controls, and profile import/export. Use a window returned by `CreateKawiXDWindow`.

### Fit different screens

```lua
Window:SetAdaptiveSize(true)
Window:SetUIScale(1.15) -- Requested multiplier; clamped to 0.6–1.5

print(Window:GetUIScale())
```

Adaptive sizing is enabled by default and fits the window to the viewport, including touch screens. This is **viewport-based scaling**, not a physical display-DPI measurement. `GetUIScale()` reports the requested multiplier; `Window.Scale.Scale` is the fitted render scale.

> **Shared versus per-window:** Themes, density, and corner radius are shared by windows from the same library instance. Background styling is per-window. Importing an appearance profile can therefore recolor sibling windows.

## Files

**One library. One standalone showcase. Two documentation files.**

Exactly four files make up this distribution:

| File | Purpose |
| :--- | :--- |
| [`Source.lua`](Source.lua) | Complete library, including the appearance layer |
| [`Example.lua`](Example.lua) | Standalone UI showcase with the library embedded |
| [`Readme.MD`](Readme.MD) | Installation, examples, API reference, and MIT license |
| [`llms.txt`](llms.txt) | Compact API guidance for AI coding assistants |

No documentation site, build step, or extra asset folder is required. To customize the library, edit `Source.lua`; `Example.lua` embeds its own copy, so keep that copy in sync if you also customize the standalone demo.

## Native API reference

The reference below follows the preserved original Airflow README, with library variables, file names, and KawiXD-specific native defaults corrected. All examples use the `Library` returned by the executor loader above. `CreateWindow` provides the native API; `CreateKawiXDWindow` additionally attaches the appearance API documented above. Use `Library.Flags`, `Library.Theme`, and `Library.Touch`—there is no separate `Airflow` global to load.

Element handles use `:Set()` / `:Get()` where applicable, not `:SetValue()`. Constructors also support forms without the `Create` prefix. Use unique flags for saveable values, keep yielding work out of inline callbacks, and call `Window:LoadAutoload()` after building your controls when using native configs.

### Reference contents

[Window](#window) · [Home](#home) · [Tab](#tab) · [Sub Tab](#sub-tab) · [Groupbox](#groupbox) · [Tabbox](#tabbox) · [Visibility](#visibility) · [Tooltips](#tooltips) · [Search](#search) · [Section](#section) · [Divider](#divider) · [Label](#label) · [Status](#status) · [Status List](#status-list) · [Paragraph](#paragraph) · [Button](#button) · [Button Row](#button-row) · [Toggle](#toggle) · [Slider](#slider) · [Stepper](#stepper) · [Progress](#progress) · [Dropdown](#dropdown) · [Order List](#order-list) · [Input](#input) · [Keybind](#keybind) · [Color Picker](#color-picker) · [Image](#image) · [Table](#table) · [Log](#log) · [Notification](#notification) · [Confirm](#confirm) · [Flags](#flags) · [Configs](#configs) · [Icons](#icons) · [Fonts](#fonts) · [Theme](#theme) · [Coloured text](#coloured-text)

## Conventions

Every constructor also works without the `Create` prefix. `Tab:Toggle` is the same as `Tab:CreateToggle`. Every element handle also has `Destroy()`, which removes the card, its listeners and its flag, and `SetVisible(bool)` / `IsVisible()`. Every constructor takes `Visible = false` to start hidden (see [Visibility](#visibility)) and `Tooltip` to explain itself on hover (see [Tooltips](#tooltips)).

---

## Window

> The root container. Sidebar with tabs and your profile, a content area with search, the close button and the notification stack.

```lua
local Window = Library:CreateWindow({
    Name = "KawiXD",
    LoadingSubtitle = "My Hub",
    Icon = "wind",
    ToggleUIKeybind = "RightControl",
    Size = UDim2.fromOffset(760, 520),
    MinSize = Vector2.new(480, 360),
    MaxSize = Vector2.new(1100, 800),
    MaxNotifications = 4,
    KeepOnScreen = true,
    OpenButton = { Title = "KawiXD", Icon = "wind" },
    ToggleButton = { Platform = "Mobile", Icon = "layout-grid" },
    Backdrop = { Weather = "Snow", Tint = 0.45 },
    Profile = true,
    Search = true,
    Loading = {
        Enabled = true,
        Title = "KawiXD",
        Text = "Starting",
        Steps = { "Preparing interface", "Loading icons", "Almost there" },
        Duration = 1.6,
    },
    Disclaimer = {
        Title = "Before you start",
        Text = "Use at your own risk. We are not responsible for bans.",
        Id = "risk-v1",
    },
    ConfigurationSaving = {
        Enabled = true,
        FolderName = "MyHub",
    },
    Home = {
        Tier = "Free",
        Discord = "dsc.gg/myhub",
        Website = "myhub.com",
    },
    Parent = game:GetService("CoreGui"),
})

Window:Toggle(false)
```

Drag any empty area to move it and the grip in the bottom-right corner to resize it. While resizing, the top-left corner stays put and the size follows the pointer through a spring, so it glides and settles instead of snapping. The window only renders through a CanvasGroup while it fades in or out, so resizing never re-renders it into a texture. It scales itself down on small screens and stays inside the viewport. With **adaptive size** (on by default) it is drawn for a 1080p screen and scales with the resolution: 1x on 1080p, about 1.35x on 1440p, up to 1.75x on 4K, and a little smaller on small laptops, so it covers the same share of any monitor. Touch screens only use the fit. `UIScale` multiplies on top.

The button in the top-right minimizes the window into a Dynamic Island: a black pill hanging from the top centre of the screen. Press and pull it to move it anywhere: it folds to the pill and lifts while carried, and a drop near the top centre snaps it home. Its spot is saved in the `ConfigurationSaving` folder, and when it opens near an edge the wide card slides inward to stay on screen. Compact, it shows the logo and a small equalizer meter that dances while toggles are running, with the running count beside it. With toggles running and a [status](#status) pinned, it splits like two iOS Live Activities: the pill shows the first pinned status and the meter buds off into its own little circle beside it. Hover it and it springs open into a card with the current tab, how many toggles are on, up to six pinned [statuses](#status) with live values, and the key that reopens the window. A notification sent while minimized opens the island for a few seconds to show it, coloured by its `Type`, then folds back (the usual toast still appears too). Click or tap it (or press the hide key) and it unfolds back into the window.

The toggle button is a small rounded square floating on the left edge. Tapping it minimizes the window, tapping it again restores it, and it also brings back a window hidden with the hide key. Drag it anywhere. Its border lights up in the accent colour while the window is folded away. By default it only shows on touch devices; `Platform = "Both"` shows it on PC too.

The sidebar is an inset rounded rail: the logo on top, then one tile per tab with its icon over its name, with a highlight that glides to the selected tile, an accent pill beside it, and fades at the ends when the list scrolls. The selected tile scrolls into view. The bottom shows the player's headshot, display name and the current game. Clicking it opens the home tab.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"KawiXD"` | Title in the sidebar header. Also names the ScreenGui. |
| `LoadingSubtitle` | string | — | Small line under the title. |
| `Icon` | string \| number \| table | Native logo asset (theme tinted) | Lucide name, asset id, or `{ Image, RectOffset, RectSize, Tint }`. See [Icons](#icons). |
| `ToggleUIKeybind` | string \| KeyCode | `"RightControl"` | Hides and shows the window. `"RightShift"`, `"LeftAlt"`, `"Insert"`, `"F1"`, or an `Enum.KeyCode`. |
| `Size` | UDim2 | `760 × 520` | Starting size. |
| `MinSize` | Vector2 | `480 × 360` | Smallest size the resize grip allows. |
| `MaxSize` | Vector2 | unlimited | Largest size the resize grip allows. |
| `SaveSize` | boolean \| string | `true` | Save the window's exact size (in pixels, not the UI scale) in configs, under a hidden `__WindowSize` flag. A string renames the flag; `false` leaves size out of configs. |
| `MaxNotifications` | number | `4` | Oldest toast is dismissed past this. |
| `KeepOnScreen` | boolean | `true` | Nudge the window back inside the viewport after a drag, resize or screen change. |
| `Transparent` | boolean | `false` | See-through window body and sidebar. |
| `Background` | string | — | Background image behind the window content. Same sources as `SetBackground`. |
| `BackgroundTransparency` | number | `0.35` | How much of the theme background colour shows through the image, 0 to 1. |
| `DragStyle` | string | `"Outline"` | What follows the pointer while dragging; the window glides into it on release. `"Outline"`, `"Brackets"`, `"Ghost"`, `"Frame"`, or `"Off"` to drag the window itself. `DragSkeleton = false` still means `"Off"`. |
| `IslandStyle` | string | `"Show on Hover"` | How the minimized island shows the session card: `"Show on Hover"` or `"Always Show"` (kept open while minimized). |
| `CornerRadius` | number | `10` | The window's corner radius in pixels, 0 to 20. Every other rounded corner scales with it. |
| `OpenButton` | boolean \| table | touch-only devices without a toggle button | Floating pill that reopens the window. `true` / `false` to force, `{ Title, Icon }` to customise. |
| `ToggleButton` | boolean \| table | `{ Platform = "Mobile" }` | Square button that minimizes and restores the window. `false` removes it. |
| `ToggleButton.Platform` | string | `"Mobile"` | `"Mobile"` shows it on touch devices only, `"Both"` on PC and mobile. |
| `ToggleButton.Icon` | string \| number \| table | `"layout-grid"` | Any [icon](#icons). |
| `ToggleButton.Enabled` | boolean | `true` | `false` builds it hidden, to show later with `SetToggleButton(true)`. |
| `ToggleButton.Position` / `Size` | UDim2 / number | left edge / `56` touch, `50` PC | Starting position and side length. |
| `Backdrop` | boolean \| table | `{ Weather = "Snow" }` | Black tint over the game while the window is up, with weather drifting through it. It fades out when the window is minimized or hidden and sweeps back in with a gust on restore. `false` removes it. |
| `Backdrop.Weather` | string | `"Snow"` | `"Snow"`, `"Rain"`, `"Hell Fire"` (embers rising from a red glow), `"Sakura"` (pink petals that flip as they drift down), `"Fireflies"` (glowing specks that wander, pulse and fade), `"Matrix"` (falling columns of shifting green glyphs) or `"None"` for the tint alone. |
| `Backdrop.Tint` | number | `0.45` | Tint strength, `0` to `1`. |
| `Backdrop.Dim` | boolean | `true` | `false` starts with the tint off and only the weather showing. |
| `Backdrop.Mode` | string | `"Screen"` | `"Screen"` drifts the weather across the whole screen, `"UI"` keeps it inside the window behind its content. |
| `Backdrop.Density` / `Speed` | number | `1` / `1` | Particle count and fall speed multipliers. |
| `Backdrop.Enabled` | boolean | `true` | `false` builds it off, to turn on later with `SetBackdrop(true)`. |
| `AdaptiveSize` | boolean | `true` | Scale the window with the screen resolution (see above). Players can switch it in the [theme manager](#theme). |
| `IslandDraggable` | boolean | `true` | `false` pins the minimized island to the top centre. |
| `UIScale` | number | `1` | Size of the whole window, `0.6` to `1.5`. The window still shrinks further when it wouldn't fit the screen. Players can change it in the [theme manager](#theme). |
| `Density` | string | `"Default"` | `"Compact"`, `"Default"` or `"Comfortable"`: the spacing between cards, groupboxes and groupbox rows. Shared by every window, like the theme. |
| `Profile` | boolean | `true` | Player card at the bottom of the sidebar. |
| `Search` | boolean | `true` | Search box in the top-right of the content area. See [Search](#search). |
| `Loading` | boolean \| table | `true` | Loading card before the window morphs in. `false` skips it. |
| `UnsupportedExecutor` | table \| false | on | When the executor is off `SupportedExecutors` (window or `Home` option) or, without a list, lacks the file, clipboard or request functions, the loading card turns into a warning with **Exit** and **Continue anyway** before the window opens. Shown even with `Loading = false`. Ticking **Don't ask again on this executor** before Continue saves the executor's name to `unsupported_skip.txt` in the `ConfigurationSaving` folder, and the warning is skipped while that executor is used (a different executor, or resetting the folder, brings it back). The tick box only shows when the executor can write files. `{ Title, Text, Block = true }` changes the wording or drops Continue (and the tick box); `false` turns it off. |
| `Loading.Title` | string | `Name` | Title on the card. |
| `Loading.Text` | string | `LoadingSubtitle` | First status line. |
| `Loading.Steps` | table | 3 built-in lines | Status lines cycled over the duration. |
| `Loading.Duration` | number | `1.6` | Seconds before the window appears. |
| `Disclaimer` | string \| table | — | Custom notice shown on the loading card after the executor warning, before the window opens; the player must press **I understand** to continue or **Exit** to close the script. Shown even with `Loading = false`. A string is just the text; a list of them shows one card after another. See the fields below. `Disclaimers` works too. |
| `Disclaimer.Title` / `Text` | string | `"Disclaimer"` / — | Heading and body. Long text scrolls inside the card. |
| `Disclaimer.Subtitle` | string | — | Small coloured line under the title. |
| `Disclaimer.Icon` / `Color` | string / Color3 | `"info"` / accent | Badge icon (any Lucide name or asset id) and its tint, e.g. `Color3.fromRGB(240, 176, 108)` for a warning look. |
| `Disclaimer.AcceptText` / `DeclineText` | string | `"I understand"` / `"Exit"` | Button labels. `DeclineText = false` drops Exit so the card can only be acknowledged. |
| `Disclaimer.Remember` | boolean | `true` | Offers a **Don't show again** tick box (when the executor can write files). Ticked, the disclaimer's `Id` is saved to `disclaimers.txt` in the `ConfigurationSaving` folder and it is skipped next time. `false` shows it on every run. |
| `Disclaimer.RememberText` | string | `"Don't show again"` | Tick box label. |
| `Disclaimer.Block` | boolean | `false` | `true` leaves only **Exit** (no accept button, no tick box), for a hard stop such as a missing requirement. It is never remembered. |
| `Disclaimer.Id` | string | hash of title and text | Key saved by the tick box. Without it, rewording the disclaimer shows it again; set an `Id` (and bump it) to control that yourself. |
| `Disclaimer.Callback` | function | — | Called with `true` on accept or `false` on Exit. |
| `ConfigurationSaving` | table | — | See [Configs](#configs). |
| `Home` | boolean \| table | `{}` | The built-in first tab. `false` removes it. See [Home](#home). |
| `Theme` / `DefaultTheme` | string \| table | — | Starting theme, same as `Library:SetDefaultTheme`. A default the player saved in the theme manager wins. See [Theme](#theme). |
| `Parent` | Instance | `gethui()` / CoreGui | Where the ScreenGui goes. Falls back to PlayerGui. |

### Handle

| Member | Description |
| --- | --- |
| `.Open` | Whether the window is shown. |
| `.CurrentTab` | The selected tab. |
| `.Tabs` | Array of tabs. |
| `.Home` | The home tab, unless `Home = false`. |
| `.SearchBox` | The search TextBox. |
| `Toggle(open?)` | Show, hide, or flip. Restores the window when minimized. |
| `Minimize()` / `Restore()` / `SetMinimized(bool)` | Fold into the island and back. |
| `.Minimized` / `.Island` | Whether it's minimized, and the island itself (also `.MiniBar`). |
| `GetMinimizeOnStart()` / `SetMinimizeOnStart(bool)` | "Minimize UI on Start": saved with the config settings; when on, the window folds into the island once right after it opens. `Tab:CreateMinimizeOnStart(opts?)` adds the toggle by hand; any groupbox named **Menu** gets it automatically, above its first button. |
| `SetIslandDraggable(enabled)` / `ResetIslandPosition()` | Lock the island in place, or send it back to the top centre and forget the saved spot. |
| `SetAdaptiveSize(enabled)` / `GetAdaptiveSize()` | Turn resolution scaling on or off. Eases to the new size. |
| `SetSize(Vector2, instant?)` / `GetSize()` | Resize to an exact size in pixels, kept within `MinSize` and `MaxSize`. Configs save and load it. |
| `SetToggleButton(enabled)` | Show or hide the toggle button. |
| `SetToggleButtonPlatform(platform)` | `"Mobile"` or `"Both"`. |
| `SetToggleButtonIcon(icon)` | Swap its icon. |
| `.ToggleButton` | The toggle button, when it was built. |
| `SetBackdrop(enabled)` | Turn the tint and weather on or off. |
| `SetWeather(name)` / `.Weather` | `"Snow"`, `"Rain"`, `"Hell Fire"`, `"Sakura"`, `"Fireflies"`, `"Matrix"` or `"None"`. `.Weather` reads `"Ember"` for hell fire. |
| `SetBackdropTint(amount)` | Tint strength, `0` to `1`. |
| `SetDim(bool)` | Turn the tint on or off. The weather keeps running. |
| `SetWeatherDensity(n)` / `SetWeatherSpeed(n)` | Particle count and speed multipliers. |
| `SetKeybind(keyCode)` | Change the hide key. Updates the chip on the home tab. |
| `SetKeepOnScreen(enabled)` | Turn the viewport clamp on or off. |
| `SetDragStyle(style)` / `GetDragStyle()` | Set or read the drag style (see `DragStyle`). `SetDragSkeleton(enabled)` still works as an on/off switch. |
| `SetIslandStyle(style)` / `GetIslandStyle()` | Set or read the island style (see `IslandStyle`). |
| `SetTransparent(enabled)` / `.Transparent` | See-through window on or off. |
| `SetBackground(source)` / `.Background` | Background image. `source` is a preset name (`Library.BackgroundPresets`: Deep Violet, Blood Red, Cyanic, Amber Glow, Bloomings, Lavender Pink), an image asset id or `rbxassetid://` link (an Image id, not a Decal id), an http(s) image link (downloaded once to `<FolderName>/backgrounds/cache`, needs `writefile` and `getcustomasset`), or an image file dropped into `<FolderName>/backgrounds`. `nil` or `"None"` removes it. Yields while a link downloads; returns `ok, err`. |
| `SetBackgroundTransparency(value)` / `ListBackgrounds()` | Image transparency, 0 to 1; presets plus the files in the backgrounds folder. |
| `SetWeatherMode(mode)` / `.WeatherMode` | `"Screen"` or `"UI"`. |
| `SetHideName(hidden)` / `SetHideAvatar(hidden)` | Hide the player's name or headshot everywhere, same as the home switches. |
| `SetUIScale(n)` / `GetUIScale()` / `.UIScale` | Window size, `0.6` to `1.5`. Eases to the new size and nudges the window back on screen. |
| `SetDensity(mode)` / `GetDensity()` | `"Compact"`, `"Default"` or `"Comfortable"`. Respaces every window live; same as `Library:SetDensity(mode)`. Returns the mode it applied. |
| `Library:SetCornerRadius(pixels)` / `GetCornerRadius()` | The window's corner radius, 0 to 20 px (default 10); every rounded corner scales with it and eases to the new size. Returns the radius it applied. |
| `SelectTab(tab)` | Switch tabs from code. |
| `CreateTab(opts)` | See [Tab](#tab). |
| `Rejoin()` / `ServerHop()` / `JoinLowestServer()` | Teleport to this server, a random open one, or the emptiest one. |
| `CopyToClipboard(text, what?)` | Copy and show a toast. |
| `Notify(opts)` | See [Notification](#notification). |
| `Confirm(opts)` / `Dialog(opts)` | See [Confirm](#confirm). |
| `SaveConfig / LoadConfig / DeleteConfig / ListConfigs` | See [Configs](#configs). |
| `Destroy()` / `Unload()` | Fade out, disconnect everything, remove the gui. `Library:Destroy()` unloads every window. |

---

## Home

> A built-in first tab: the player card with privacy switches, live stats, the current game with server actions, an executor check, and your community links.

```lua
Home = {
    Name = "Home",
    Title = "Welcome to My Hub!",
    Welcome = "Welcome back,",
    Tier = "Premium",
    TierIcon = "crown",
    Expiry = os.time() + 3600 * 12,
    Stats = { "Players", "Friends", "Execs", "Session", "FPS", "Ping" },
    SupportedExecutors = { "Potassium", "Wave", "Volt" },
    Discord = "dsc.gg/myhub",
    Website = "myhub.com",
    Links = {
        { Icon = "youtube", Title = "Showcase", Text = "youtube.com/@myhub", Button = "Copy Link" },
    },
    HideName = false,
    HideAvatar = false,
    Features = true, -- automatic feature list; a table writes your own, false hides it
    Pages = {
        {
            Name = "Changelog",
            Icon = "scroll-text",
            Entries = {
                { Title = "v1.3", Tag = "Latest", Changes = { "Sub tabs", "Groupboxes" } },
                { Title = "v1.2", Date = "Aug 30", Content = "Plain text instead of bullets." },
            },
        },
        { Name = "Info", Icon = "info", Content = "Wrapped text in a card." },
        { Name = "Custom", Icon = "wrench", Build = function(page) page:Button({ Name = "Hi" }) end },
    },
}
```

Stats refresh once a second and pause while the window is hidden or another tab is open. When `Pages` is set, the home tab gets sub tabs: an overview page with the cards above, then one per page.

The **Feature list** card opens a searchable list of the script's features over the window. By default it's automatic: every toggle, slider, dropdown, input, keybind, colour picker, stepper, button and order list, grouped by tab, with the sub tab and groupbox under each name. Hidden elements, hidden tabs and the config and theme managers are left out. Picking a feature closes the list and jumps to it, like search does. To write the list yourself, pass `Features` a table:

```lua
Features = {
    Title = "What's inside",
    List = {
        { Name = "Combat", Icon = "swords", Items = {
            "Auto Parry", -- names that match a control jump to it
            { Name = "Kill Aura", Desc = "Hits everything in range", Tag = "New" },
        } },
        { Name = "Coming soon", Icon = "clock", Items = { { Name = "Auto Raid", Tag = "Soon" } } },
    },
}
```

Bare items (strings or tables without `Items`) gather into one group. `Features = false` removes the card. `Window:ShowFeatures()` opens the list from anywhere.

The game card has Rejoin, Server Hop, Copy Job ID, Copy Universe and Join Lowest Server. The executor card names the executor, says whether it is supported, and shows the hide key. The **Name** and **Profile** switches hide the player's name and headshot on the home tab and in the sidebar.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` / `Desc` / `Icon` | string | `"Home"`, `"house"` | The tab itself. |
| `Title` | string | `"Home"` | Page heading. |
| `Welcome` | string | `"Welcome back,"` | Line above the display name. |
| `Tier` | string \| false | `"Free"` | Badge on the player card. `false` hides it. |
| `TierIcon` | string | window icon | Icon in the badge. |
| `Expiry` | number \| string \| function | — | Under the badge. A unix time counts down (`11h 57m`), a string is shown as is, a function is called every second. |
| `Stats` | table | six shown above | Any of `"Players"`, `"Friends"`, `"Execs"`, `"Session"`, `"FPS"`, `"Ping"`, `"Executor"`, `"Game"`, `"Region"`, `"Time"`, `"ServerAge"`, `"Memory"`. |
| `StatColors` | boolean | `true` | Tint `FPS`, `Ping` and `Memory` green, amber or red by how healthy they are (FPS 50+ / 30+, ping under 90 / 180 ms, memory under 1.5 / 3 GB). |
| `StatsFolder` | string | config folder | Where the execution counter is stored. |
| `TimeFormat` | string | `"%H:%M"` | `os.date` format for the time stat. |
| `SupportedExecutors` | table | — | Names checked against the executor. Without it, the card checks for the file, clipboard and request functions. |
| `Discord` / `Website` | string | — | Link cards with a copy button. |
| `DiscordTitle` / `WebsiteTitle` | string | `"Join the community"` / `"Supported games"` | Card titles. |
| `Links` | table | — | More link cards: `{ Icon, Title, Text, Button, Copy, Callback }`. |
| `HideName` / `HideAvatar` | boolean | `false` | Start with the privacy switches on. |
| `Features` | table \| false | automatic | The feature list card. A table takes `Title`, `Desc` (card text, instead of the count), `Icon`, `Button` and `List`. |
| `Features.List[n]` | table \| string | — | A group `{ Name, Icon, Items }`, or a bare item. |
| `Items[n]` | string \| table | — | `{ Name, Desc, Tag, Icon, Callback }`. `Callback` runs when it's picked. |
| `OverviewName` / `TabIcon` | string | `"Overview"` / `"layout-grid"` | The first sub tab when `Pages` is set. |
| `Pages` | table | — | Extra sub tabs. |
| `Pages[n].Name` / `Icon` | string | — | The sub tab button. |
| `Pages[n].Content` | string | — | Wrapped text in a card. |
| `Pages[n].Entries` | table | — | Cards with `Title`, `Tag` or `Date`, and `Changes` (a list) or `Content`. |
| `Pages[n].Build` | function | — | `function(page, list)`. `page` is a sub tab, so every element constructor and `Groupbox` work on it. |

---

## Tab

> A sidebar button and a page with its icon and title.

```lua
local Tab = Window:CreateTab({
    Name = "Main",
    Desc = "Movement and actions",
    Icon = "zap",
    EmptyText = "Nothing here yet",
})

local Tab = Window:CreateTab("Main", "zap")
```

The first tab created is selected automatically. When there are more tabs than fit in the sidebar, the hidden end fades out and a small chip shows a chevron and how many tabs are past that end. Pressing it scrolls toward them; it leaves once you reach the end. An empty tab shows its icon with `EmptyText`. Elements added straight to a tab stack as full-width cards. Groupboxes go into two columns underneath them.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Tab"` | Sidebar label and page title. |
| `PageTitle` | string | `Name` | Page heading when it should differ from the sidebar label. |
| `Desc` | string | — | Muted line under the page title. |
| `Icon` | string \| number \| table | — | Sidebar and page icon, accent-tinted. |
| `EmptyText` | string | `"Nothing here yet"` | Shown while the tab has no elements. |

### Handle

Every `Create*` element constructor below, `CreateSubTab`, `CreateGroupbox` / `AddLeftGroupbox` / `AddRightGroupbox`, `CreateTabbox` / `AddLeftTabbox` / `AddRightTabbox`, `SelectSubTab(subTab | name | index)`, `.CurrentSubTab`, `.Name` and `.Window`.

---

## Sub Tab

> A row of pills under the page title. Each pill has its own page, and switching slides between them.

```lua
local Farm = Window:CreateTab({ Name = "Farm", Icon = "swords" })

local MobFarm = Farm:CreateSubTab({ Name = "Mob Farm" })
local BossFarm = Farm:CreateSubTab({ Name = "Boss Farm", Icon = "skull" })

MobFarm:CreateToggle({ Name = "Auto Farm", Callback = function(v) end })
Farm:SelectSubTab("Boss Farm")
```

The first sub tab is selected automatically. Once a tab has sub tabs, add elements and groupboxes to the sub tabs, not the tab. The pill row scrolls sideways when it overflows, with the same fade and chip as the sidebar at whichever end has more pills.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Page n"` | Pill label. |
| `Icon` | string \| number \| table | — | Optional icon in the pill. |
| `EmptyText` | string | `"Nothing here yet"` | Shown while the page is empty. |

### Handle

Same as a tab: every element constructor and the groupbox constructors.

---

## Groupbox

> A titled, collapsible card. Groupboxes fill two columns and stack into one when the window is narrow.

```lua
local Mobs = MobFarm:AddLeftGroupbox({ Name = "Mob Farm", Icon = "crosshair" })
local Other = MobFarm:AddRightGroupbox("Other Features", "sparkles")
local Auto = MobFarm:CreateGroupbox({ Name = "Movement", Icon = "move", Collapsed = true })

Mobs:CreateToggle({ Name = "Auto Farm Mobs", Callback = function(v) end })
Mobs:CreateDropdown({ Name = "Mobs", Options = { "Bandit", "Wolf" } })
Mobs:CreateButton({ Name = "Teleport to mob" })
Mobs:CreateLabel("Status: idle")

Auto:Expand()
```

Inside a groupbox, elements are compact rows without their own card. Dropdowns and inputs take the same share of the row so their boxes line up, and buttons fill the width. Click the header to collapse it. The pop-out button beside the chevron lifts the groupbox into a floating panel you can drag anywhere by its header; it keeps working while you switch tabs or minimize, and a slot in its column (or the same button) docks it back. Without `Side`, each new groupbox goes to the column with fewer boxes.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Groupbox"` | Header title. |
| `Icon` | string \| number \| table | — | Accent icon on the right of the header. |
| `Side` | `"Left"` \| `"Right"` \| 1 \| 2 | balanced | Column. |
| `Collapsed` | boolean | `false` | Start collapsed. |
| `PopOut` | boolean | `true` | Show the pop-out button. |
| `PoppedOut` | boolean | `false` | Start popped out. |
| `Visible` | boolean | `true` | Start hidden. |

### Handle

| Member | Description |
| --- | --- |
| every element constructor | Adds a row to the groupbox. |
| `Collapse()` / `Expand()` / `SetCollapsed(bool)` | Animate closed or open. |
| `IsCollapsed()` | Current state. |
| `PopOut()` / `Dock()` / `IsPoppedOut()` | Float the groupbox in its own draggable panel, or fly it back to its column. |
| `SetTitle(text)` | Rename the header. |
| `SetVisible(bool)` / `IsVisible()` | Hide or show the whole card. Its column closes the gap. |
| `Destroy()` | Remove the groupbox and its elements. |

---

## Tabbox

> A groupbox whose header is a row of tabs. Each tab holds its own rows; only the selected one shows.

```lua
local Filters = MobFarm:AddLeftTabbox({ Name = "Filters" })   -- or AddRightTabbox / CreateTabbox({ Side = ... })
local Include = Filters:AddTab("Include", "plus")
local Exclude = Filters:AddTab({ Name = "Exclude", Icon = "minus" })

Include:CreateToggle({ Name = "Rare Items" })
Exclude:CreateToggle({ Name = "Common Items" })

Filters:SelectTab("Exclude") -- tab, name or index
```

Each tab works like a groupbox for adding elements. The tabbox has `SelectTab`, `.Current`, `.Tabs`, `SetVisible`, `IsVisible`, `SetTitle` and `Destroy`; each tab has `Select`, `SetTitle` and `Destroy`. Tab buttons share the header width evenly. Search finds elements inside any tab and switches to it.

## Visibility

Any element or groupbox can be hidden and shown again. A hidden row takes no space, so its groupbox shrinks and grows with it.

```lua
local Charge -- declared first so the toggle's callback can reach it
local Hold = Box:CreateToggle({ Name = "Hold Skills", Flag = "HoldSkills", Callback = function(v) Charge:SetVisible(v) end })
Charge = Box:CreateSlider({ Name = "Charge Distance", Range = { 5, 60 }, Visible = false, Flag = "ChargeDistance" })
```

- Search never reveals something you hid, and clearing the search leaves it hidden.
- Hidden elements keep their flag. They still save, load and run callbacks, so loading a config with `HoldSkills` on shows `Charge`. Visibility itself is not saved.
- Hiding an open dropdown or colour picker closes it, and hiding a keybind stops a capture.
- A hidden pinned status leaves the minimized island until it is shown again.

### Depends on

Instead of wiring callbacks, give an element a `DependsOn` rule and it shows only while the rule passes. Rules are rechecked ten times a second, so they follow clicks, config loads and changes made from code.

```lua
Box:CreateSlider({ Name = "Undercut %", Range = { 1, 50 }, Flag = "Undercut",
    DependsOn = { Flag = "PriceMode", Value = "Undercut" } })

Box:CreateSlider({ Name = "Max Bid", Range = { 100, 10000 }, Flag = "MaxBid",
    DependsOn = "AutoBid", DependsMode = "Disable" })
```

| Rule | Passes when |
| --- | --- |
| `"Flag"` | The flag is on: a toggle that's on, a dropdown with a pick, a non-zero number, a non-empty text or a bound key. |
| `{ Flag = "Mode", Value = "Percent" }` | The flag equals `Value`. `Value` can be a list of accepted values; a multi dropdown passes when it holds any of them. |
| `{ Flag = "AutoBid", Not = true }` | The opposite of the rule. |
| `{ "AutoSell", { Flag = "Mode", Value = "Fixed" } }` | Every rule in the list passes. |
| `function() return ... end` | The function returns true. |

`DependsMode = "Disable"` dims the element and blocks input instead of hiding it. `SetDependsOn(rule, mode?)` changes the rule later; `nil` removes it. A hidden element keeps its flag, and still saves and loads like any hidden element.

Any element can also be switched off by hand: `Disabled = true` in its options, or `SetDisabled(bool)` and `IsDisabled()` on its handle.

---

## Tooltips

Every element takes `Tooltip`: a string, or `{ Title, Text, Icon }` for a card with a heading and an icon.

```lua
Box:CreateToggle({ Name = "Kill Aura", Flag = "KillAura", Tooltip = "Hits every mob in range" })
Box:CreateSlider({
    Name = "Range",
    Range = { 5, 50 },
    Tooltip = { Title = "Range", Text = "Studs from your character. Higher can get you flagged.", Icon = "triangle-alert" },
})

Toggle:SetTooltip("New text") -- nil or false removes it
```

It is bare text with a thin dark outline, no background, with the icon and title on top when given. It rises in after a short hover and follows the pointer, flipping to the other side near the screen edge. Moving straight from one element to another swaps the card without the wait. Any click or key press hides it, as does switching tabs or hiding the window. On touch screens a half-second press shows it above the finger and lifting hides it; a finger that starts scrolling doesn't. `GetTooltip()` returns the current value.

---

## Search

The search box in the top-right searches the whole window as you type: tabs, sub tabs, groupboxes and controls from every tab, best matches first (names that start with the query, then word starts). Picking a result opens its tab and sub tab, expands a collapsed groupbox, scrolls the control to the middle of the page and lights it up: the control pops, a soft accent glow blooms around it, a sheen sweeps across it and a bright spot runs round its border, then it breathes once and fades. Switching tabs clears the box.

---

## Section

> An uppercase heading with a rule to the card edge.

```lua
local Section = Tab:CreateSection("Movement")

Section:Set("Movement (beta)")
```

### Handle

| Member | Description |
| --- | --- |
| `Set(text)` | Replace the heading. |

---

## Divider

> A 1px line, optionally with a caption in the middle.

```lua
Tab:CreateDivider()
Tab:CreateDivider({ Text = "share" })
```

---

## Label

> A single muted line. Can refresh itself.

```lua
local Label = Tab:CreateLabel({
    Text = "Players: 12",
    Color = Library.Theme.Muted,
    UpdateRate = 1,
    Update = function()
        return "Players: " .. #game.Players:GetPlayers()
    end,
})

local Label = Tab:CreateLabel("Players: 12")

Label:Set("Players: 13")
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Text` | string | `""` | The line. A bare string works too. |
| `Color` | Color3 \| string | muted | Text colour: a Color3, `"#rrggbb"` or a theme key such as `"Success"`. |
| `Update` | function | — | Called on a timer; its return value becomes the text. Supports [coloured text](#coloured-text). |
| `UpdateRate` | number | `1` | Seconds between `Update` calls. |

### Handle

| Member | Description |
| --- | --- |
| `Set(text)` | Replace the line. [Coloured text](#coloured-text) works. |
| `Get()` | The current text. |
| `SetColor(color)` | Recolour the whole line. |
| `SetUpdateRate(seconds)` | Change the timer, when `Update` was given. |

---

## Status

> Read-only key and value lines, in six styles. Built for groupboxes.

```lua
local Floor = Group:CreateStatus({ Name = "Floor", Value = 1, Pin = true })
Floor:Set(2)

Group:CreateStatus({ Name = "Exp", Value = "7859/10740", Style = "Bar" })
Group:CreateStatus({ Name = "Server", Value = "Healthy", Style = "Badge", Tone = "Success" })
Group:CreateStatus({ Name = "Bot", Style = "Dot", Update = function()
    return "Farming", "Success"
end })

local Run = Group:CreateStatuses({ "Points", "Hearts", "Map" }, { Style = "Row" })
Run.Hearts:Set(3)

-- Coloured values: a theme tag, a whole-value colour, or a Color3 tone.
Group:CreateStatus({ Name = "Ping", Style = "Row", Update = function()
    local Ms = math.floor(game.Players.LocalPlayer:GetNetworkPing() * 1000)
    return Ms < 100 and "<Success>" .. Ms .. " ms</Success>" or "<Error>" .. Ms .. " ms</Error>"
end })
Group:CreateStatus({ Name = "Mode", Value = "Aggressive", Style = "Row", Color = "Warning" })
Group:CreateStatus({ Name = "Shield", Value = "Up", Style = "Badge", Tone = Color3.fromRGB(120, 180, 255) })
```

| Style | Looks like |
| --- | --- |
| `Plain` | `Floor: 3`, muted key then the value. The default. Long values wrap and grow the line. |
| `Row` | Key on the left, value on the right. |
| `Badge` | Value in a pill tinted by `Tone`. |
| `Dot` | A pulsing dot tinted by `Tone`, then key and value. |
| `Bar` | Key and `current / max` with a progress bar. `"7859/10740"` strings, `Set(current, max)`, or a 0–1 number all work. |
| `Stat` | Small key over a large value. |

A changed value flashes the accent colour briefly. With `Update`, the function runs every `UpdateRate` seconds: its first return is the value, and a second return sets the max (a number) or the tone (a string or Color3). Keys and values are rich text, so [coloured text](#coloured-text) works anywhere in them, and pinned statuses keep their colour on the minimized island.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | — | The key. |
| `Value` | any | `"-"` shown | The value. `nil` shows `Placeholder`. |
| `Style` | string | `"Plain"` | See above. |
| `Tone` | string \| Color3 | `"Accent"` | Tints the badge, dot and bar. Any theme colour name (`"Success"`, `"Warning"`, `"Error"`, `"Muted"`…), a Color3 or `"#rrggbb"`. |
| `Color` | string \| Color3 | text colour | Colours the whole value in the `Plain`, `Row`, `Dot`, `Bar` and `Stat` styles. Same forms as `Tone`. `ValueColor` works too. |
| `Max` | number | — | Max for `Bar`. |
| `Prefix` / `Suffix` | string | — | Text around the value. |
| `Placeholder` | string | `"-"` | Shown while the value is `nil`. |
| `Update` / `UpdateRate` | function / number | — / `1` | Refresh on a timer. |
| `Wrap` | boolean | `true` | `Plain` only. `false` keeps the value on one line. |
| `Pin` | boolean | `false` | Also show it on the minimized island. |
| `Pulse` / `Flash` | boolean | `true` | The `Dot` pulse and the change flash. |

### Handle

| Member | Description |
| --- | --- |
| `Set(value, max?)` / `Get()` | Change or read the value. |
| `SetTone(tone)` / `SetName(name)` | Recolour the tint or rename. |
| `SetColor(color)` | Colour the whole value; `nil` goes back to the text colour. |
| `SetUpdateRate(seconds)` | When `Update` is set. |
| `SetWrap(enabled)` | `Plain` only. `false` stops wrapping, `true` turns it back on. |
| `Tab:CreateStatuses(entries, shared?)` | Several at once. Entries are names or option tables; `shared` fills missing options. Returns the handles by name. |

---

## Status List

> A read-only block of rows that grows up to `MaxRows`, then scrolls inside itself. Built for groupboxes: hotbar skills, boss timers, a queue.

```lua
local Skills = Box:CreateStatusList({
    Name = "Hotbar",
    MaxRows = 5,
    EmptyText = "no skills on the hotbar yet",
    UpdateRate = 0.5,
    Update = function()
        return {
            "Z Compound Eye Hexagon (on target, up to 3s)",
            { Text = "X True Flutter", Value = "charges 3s" },
            { Text = "B Illusory Light", Value = "cooldown 12s", Tone = "Warning" },
        }
    end,
})
Skills:Set({ "one row", "another row" })
```

A plain string is one muted line that wraps. A table `{ Text, Value?, Tone? }` puts `Text` on the left and `Value` on the right, like the `Row` status style. `Tone` (or `Color`) is a theme colour name, a Color3 or `"#rrggbb"` and tints the value, or the text when there is no value. Text and values are rich text, so [coloured text](#coloured-text) tags colour just part of a row, and theme tags repaint when the theme changes.

Rows are reused between refreshes, and unchanged rows are skipped, so it never flickers. The scroll position survives a refresh. The mouse wheel scrolls the list, and at its top or bottom edge the page scrolls instead. `Update` only runs while the list is on screen: not while the window is hidden or minimized, another tab or sub tab is open, or the list or its groupbox is hidden. Search matches the list's `Name`, not its rows.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | — | Optional small muted heading above the rows. Omit it for no heading. |
| `Rows` | table | `{}` | Initial rows. |
| `MaxRows` | number | `5` | Rows shown before the list scrolls. |
| `EmptyText` | string | `"Nothing yet"` | One muted line shown when there are no rows. |
| `Update` / `UpdateRate` | function / number | — / `1` | Timer refresh. The return value is the row list. Returning `nil` keeps the current rows. |
| `Visible` | boolean | `true` | Start hidden. |

### Handle

| Member | Description |
| --- | --- |
| `Set(rows)` | Replace all rows. |
| `Get()` | The current rows, as a copy. |
| `Clear()` | Remove all rows. The `EmptyText` shows. |
| `SetName(text)` | Change the heading. |
| `SetUpdateRate(seconds)` | When `Update` is set. |
| `SetVisible(bool)` / `IsVisible()` / `Destroy()` | Shared by every element. |

---

## Paragraph

> A card with a heading and wrapped body text.

```lua
local Paragraph = Tab:CreateParagraph({
    Title = "About",
    Content = "Longer text that wraps across several lines.",
})

Paragraph:Set("Updated body")
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Title` | string | `""` | Heading. |
| `Content` | string | `""` | Body. Wraps and grows the card. |

### Handle

| Member | Description |
| --- | --- |
| `Set(text)` | Replace the body. |

---

## Button

> A full-width card that ripples on click.

```lua
local Button = Tab:CreateButton({
    Name = "Reset character",
    Desc = "Respawns at the last spawn point",
    Icon = "refresh-cw",
    Style = "Primary",
    Callback = function()
        print("clicked")
    end,
})

Button:SetText("Respawn")
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Button"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `Icon` | string \| number \| table | — | Leading icon. |
| `Style` | string | — | `"Primary"` fills the card with the accent colour. |
| `Confirm` | boolean \| string | — | Two-step click: the first click shows `"Click again to confirm"` (or your text) in the warning colour, and a second click within `ConfirmTimeout` runs the callback. |
| `ConfirmTimeout` | number | `3` | Seconds before an armed button resets. |
| `HoldToConfirm` | boolean \| number | — | Hold to run: the button fills while pressed and runs when full. `true` is one second, a number sets the seconds. Letting go early or sliding off cancels. |
| `Callback` | function | — | Runs on click. |

### Handle

| Member | Description |
| --- | --- |
| `SetText(text)` | Replace the label. |
| `Disarm()` | Reset an armed `Confirm` button. |

---

## Button Row

> Equal-width buttons side by side.

```lua
Group:CreateButtonRow({
    { Name = "Save", Callback = function() end },
    { Name = "Load", Callback = function() end },
})
```

Each entry takes `Name`, `Callback` and `Style` (`"Primary"` for the accent fill, `"Danger"` for red text). The handle has `SetText(index, text)` and `.Buttons`.

---

## Toggle

> Switch a boolean on and off.

```lua
local Toggle = Tab:CreateToggle({
    Name = "Auto sprint",
    Desc = "Hold shift to run",
    CurrentValue = true,
    Flag = "AutoSprint",
    Callback = function(Value)
        print("Auto sprint:", Value)
    end,
})

Toggle:Set(false)
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Toggle"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `CurrentValue` | boolean | `false` | The initial state. The callback fires once on creation if `true`. |
| `Flag` | string | — | The save key. |
| `Callback` | function | — | Runs with the new value on every change. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current state. |
| `Set(value, skipCallback?)` | Set the state. Pass `true` as the second argument to skip the callback. |
| `Get()` | The current state. |

---

## Slider

> Pick a number in a range.

```lua
local Slider = Tab:CreateSlider({
    Name = "Walk speed",
    Desc = "Studs per second",
    Range = { 16, 100 },
    Increment = 1,
    Suffix = " sps",
    CurrentValue = 16,
    Flag = "WalkSpeed",
    Callback = function(Value)
        print("Walk speed:", Value)
    end,
})

Slider:Set(50)
```

Click the value chip to type an exact number.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Slider"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `Range` | table | `{ 0, 100 }` | `{ min, max }`. |
| `Increment` | number | `1` | Snap size. Its decimals set how the value is shown. |
| `Suffix` | string | `""` | Appended to the value chip. |
| `CurrentValue` | number | min | The initial value. |
| `Flag` | string | — | The save key. |
| `Callback` | function | — | Runs with the new value on every change, including while dragging. |
| `OnRelease` | function | — | Runs with the value when a drag ends. Use it for work too heavy to repeat every frame. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current value. |
| `.Dragging` | Whether the knob is being dragged. |
| `Set(value, skipCallback?)` | Set the value. Slides with a small overshoot. |
| `Get()` | The current value. |

---

## Stepper

> A number with − and + buttons.

```lua
local Stepper = Tab:CreateStepper({
    Name = "Fall threshold",
    Desc = "Distance before damage",
    Range = { 0, 100 },
    Increment = 5,
    Suffix = " studs",
    CurrentValue = 50,
    Flag = "FallThreshold",
    Callback = function(Value)
        print("Threshold:", Value)
    end,
})

Stepper:Set(75)
```

Hold either button to repeat.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Stepper"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `Range` | table | `{ 0, 100 }` | `{ min, max }`. |
| `Increment` | number | `1` | Step per press. Its decimals set how the value is shown. |
| `Suffix` | string | `""` | Appended to the value. |
| `CurrentValue` | number | min | The initial value. |
| `Flag` | string | — | The save key. |
| `Callback` | function | — | Runs with the new value on every change. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current value. |
| `Set(value, skipCallback?)` | Set the value. Snapped to the increment and clamped to the range. |
| `Get()` | The current value. |

---

## Progress

> A read-only bar from 0 to 1.

```lua
local Progress = Tab:CreateProgress({
    Name = "Health",
    Desc = "Live from the humanoid",
    CurrentValue = 1,
    Color = Library.Theme.Success,
    Format = function(Fraction)
        return math.floor(Fraction * 100) .. " hp"
    end,
    Callback = function(Fraction)
        print("Health:", Fraction)
    end,
})

Progress:Set(0.5)
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Progress"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `CurrentValue` | number | `0` | The initial fraction. |
| `Color` | Color3 \| string | accent | Fill colour: a Color3, `"#rrggbb"` or a theme key. |
| `TextColor` | Color3 \| string | accent | Colour of the percentage on the right. |
| `Format` | function | percentage | Returns the label text for a fraction. [Coloured text](#coloured-text) works. |
| `Callback` | function | — | Runs on `Set` unless skipped. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current fraction. |
| `Set(value, skipCallback?)` | Set the fraction. Eases the fill. |
| `SetColor(color)` | Change the fill colour. Eases. |
| `SetTextColor(color)` | Change the percentage's colour; `nil` goes back to the accent. |
| `Get()` | The current fraction. |

---

## Dropdown

> Pick one option, or several, from a searchable popup.

```lua
local Dropdown = Tab:CreateDropdown({
    Name = "Mobs",
    Desc = "Farmed in order",
    Options = { "T1", "T2", "T3" },
    CurrentOption = { "T1" },
    MultipleOptions = true,
    Flag = "Mobs",
    Callback = function(Options)
        print("Mobs:", table.concat(Options, ", "))
    end,
})

Dropdown:Set({ "T1", "T3" })
```

Clicking the chip unfolds a popup out of it, floating over the window under the chip, or above it when there's no room below. It follows the window while open and closes on an outside click, `Esc` or a tab switch. The chip lights up on hover and takes an accent outline while open; a picked value reads in full colour and `None` stays muted. A multi pick shows two names and a count (`Apple, Pear  +3`). The popup has a search box (it says how many options there are on long lists), **Select all** / **Clear all** in multi mode, and rows that highlight on hover. Picked rows rest on a faint accent tint. A single-pick list marks its value with an accent bar on the left and a check on the right; a multi-pick list ticks square checkboxes. Typing in the search lights up the matching part of each option in the accent colour. Select all only picks the rows matching the search. Clicking a selected row unchecks it. The page behind stays put while the popup is open, so wheel and swipe input always scroll the list. A single-select list opens scrolled to its current value, and the list shrinks to fit short windows. On touch, rows are taller and a swipe that scrolls the list never selects a row.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Dropdown"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `Options` | table | `{}` | The rows. |
| `CurrentOption` | string \| table | — | The initial selection. A table in multi mode. |
| `MultipleOptions` | boolean | `false` | Rows toggle independently and the callback receives a list. |
| `Searchable` | boolean | `true` | Show the search box. |
| `SearchAfter` | number | `0` | Only show search when there are more rows than this. |
| `MaxRows` | number | `6` | Rows visible before the list scrolls. |
| `NoneText` | string | `"None"` | Chip text with nothing selected. |
| `EmptyText` | string | `"None"` | Chip text when there are no options. |
| `AllowNone` | boolean | `true` | `false` stops a single dropdown from unchecking its value. |
| `PopupWidth` | number | `210` | Minimum popup width. It grows to the chip width. |
| `Stacked` | boolean | `false` | Inside a groupbox: the chip spans the full row with the name above it. Leave `Name` out for a bare chip. |
| `Flag` | string | — | The save key. |
| `Callback` | function | — | Runs with the selection on every change. `nil` when unchecked. |

### Handle

| Member | Description |
| --- | --- |
| `.Open` | Whether the popup is showing. |
| `Set(value, skipCallback?)` | Select a value, or a list in multi mode. |
| `SetOptions(options, settings?)` | Replace the rows. `settings` is `{ KeepSelection = true, Silent = false }`: picks are kept by default, and `Silent = true` skips the callback. A boolean works as `KeepSelection`. A pick only counts while its option is in the list, so if the new rows change the value (a config's saved picks becoming real options, or picks dropped), the callback runs with it unless silent. Saving keeps picks whose option is missing right now. |
| `GetOptions()` | A copy of the rows. |
| `Refresh(options, keepSelection?, skipCallback?)` | The older form of `SetOptions`: picks are dropped unless `keepSelection` is true. |
| `SetOpen(open)` | Show or hide the popup. |
| `Get()` | The current selection. |

---

## Order List

> An always-open list the player puts in order.

```lua
local Order = Tab:CreateOrderList({
    Name = "Boss Order",
    Desc = "Top boss is farmed first",
    Items = { "Rui", "Akaza", "Doma", "Kokushibo" },
    MaxRows = 6,
    Flag = "BossOrder",
    Callback = function(Order)
        print("First:", Order[1])
    end,
})

Order:Set({ "Doma", "Rui" }) -- Doma, Rui, then the rest in their current order
```

There's nothing to click open: the rows sit in the element. Drag a row to move it, and the others slide out of its way. On PC the whole row drags; on touch only the grip on the left does, so a swipe across the rows still scrolls. The up and down arrows on each row move it one place. Past `MaxRows` the list scrolls inside itself, and holding a dragged row near its top or bottom edge scrolls it along. The page behind stays put while a row is held. The callback runs once per drop or arrow press, not while dragging.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | — | The label above the list. |
| `Desc` | string | — | Hint text under the label. |
| `Items` | table | `{}` | The rows, in their starting order. |
| `MaxRows` | number | `6` | Rows visible before the list scrolls. |
| `Numbered` | boolean | `true` | Show each row's position. |
| `Arrows` | boolean | `true` | Show the up and down buttons. |
| `EmptyText` | string | `"Nothing to order"` | Shown when there are no items. |
| `Flag` | string | — | The save key. Saves the order. |
| `Callback` | function | — | Runs with the new order on every change. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current order. |
| `Set(order, skipCallback?)` | Reorder the items to match `order`. Items it leaves out keep their order after the ones it names. Names not in the list are remembered and applied when `Refresh` brings them in, so a saved order survives a list that fills in later. |
| `Refresh(items, keepOrder?, skipCallback?)` | Replace the items. Items that were already there keep the player's order and new ones go to the end. Pass `keepOrder` as `false` to take `items` as given. |
| `Get()` | The current order, a list. |

---

## Input

> A text box that grows with what you type.

```lua
local Input = Tab:CreateInput({
    Name = "Player name",
    Desc = "Partial names work",
    Icon = "user",
    PlaceholderText = "type here",
    CurrentValue = "",
    Numeric = false,
    Flag = "PlayerName",
    Callback = function(Text, EnterPressed)
        print("Input:", Text, EnterPressed)
    end,
})

Input:Set("Pookie")
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Input"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `Icon` | string \| number \| table | — | Icon inside the box. |
| `PlaceholderText` | string | `""` | Shown while empty. |
| `CurrentValue` | string | `""` | The initial text. |
| `Numeric` | boolean | `false` | Parses numeric text, including supported separators/suffixes; invalid edits revert to the last valid text and skip the callback. `Get()` and callbacks return a number or nil in numeric mode. |
| `Flag` | string | — | The save key. |
| `Callback` | function | — | Runs on focus loss or a non-silent programmatic `Set`. Receives text (or a number in numeric mode) and whether Enter was pressed. |

### Handle

| Member | Description |
| --- | --- |
| `Set(text, silent?)` | Replace the text; `true` skips the callback. Numeric mode validates/parses it. |
| `Get()` | Current text in normal mode; parsed number or nil in numeric mode. |

---

## Keybind

> Bind an action to a key.

```lua
local Keybind = Tab:CreateKeybind({
    Name = "Toggle sprint",
    Desc = "Press to flip the toggle",
    CurrentKeybind = "F",
    Flag = "SprintKey",
    Callback = function(Key)
        print("Pressed:", Key.Name)
    end,
    OnChanged = function(Key)
        print("Rebound to:", Key.Name)
    end,
})

Keybind:Set(Enum.KeyCode.G)
```

Click the chip and press a key to rebind. Escape cancels.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Keybind"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `CurrentKeybind` | string \| KeyCode | — | The initial key. |
| `Flag` | string | — | The save key. |
| `Callback` | function | — | Runs when the key is pressed and no text box has focus. |
| `OnChanged` | function | — | Runs when the user rebinds it. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current KeyCode, or `nil`. |
| `.Listening` | Whether the chip is waiting for a key. |
| `Set(keyCode, skipCallback?)` | Rebind. Pass `true` to skip `OnChanged`. |
| `Get()` | The current KeyCode. |

---

## Color Picker

> Pick a colour.

```lua
local ColorPicker = Tab:CreateColorPicker({
    Name = "Highlight colour",
    Desc = "Applied to every highlight",
    Color = Color3.fromRGB(235, 199, 246),
    Flag = "HighlightColor",
    Callback = function(Color)
        print("Colour:", Color)
    end,
})

ColorPicker:Set(Color3.fromRGB(150, 220, 170))
```

The panel has a saturation/value square, a hue bar, a hex box and an RGB readout.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"Color"` | The label. |
| `Desc` | string | — | Hint text under the label. |
| `Color` | Color3 | accent | The initial colour. |
| `Flag` | string | — | The save key. |
| `Callback` | function | — | Runs with the new colour on every change, including while dragging. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current colour. |
| `.Open` | Whether the panel is expanded. |
| `Set(color, skipCallback?)` | Set the colour. Animates the cursors. |
| `SetOpen(open)` | Expand or collapse. |
| `Get()` | The current colour. |

---

## Image

> A picture card: an optional title, the image with rounded corners, and an optional caption.

```lua
local Banner = Tab:CreateImage({
    Name = "Map",
    Image = 1234567890, -- asset id, rbxassetid:// or rbxthumb:// link, web link, file, background preset or "Avatar"
    Height = 160,
    Caption = "Spawn island",
})

Banner:SetImage("https://example.com/map.png")
```

A placeholder icon shows until the image has loaded, then the picture fades in. Sources are the same as `SetBackground` on the [window](#handle): an image asset id (an Image id, not a Decal id), an `rbxassetid://` / `rbxthumb://` link, an http(s) link (downloaded once, needs `writefile` and `getcustomasset`), a file in `<FolderName>/backgrounds`, or a background preset name. `"Avatar"` shows the player's headshot.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | — | Title above the image. Leave out for just the image. |
| `Desc` | string | — | Hint text under the title. |
| `Image` | string \| number | — | The picture. |
| `Height` | number | `160` | Height of the picture, 40 to 600. |
| `Caption` | string | — | Line over the bottom of the picture, on a dark fade. |
| `ScaleType` | string | `"Crop"` | `"Crop"`, `"Fit"`, `"Stretch"`. |
| `Color` | Color3 | white | Tint. |

### Handle

| Member | Description |
| --- | --- |
| `.Value` | The current source. |
| `SetImage(source)` / `Set(source)` | Swap the picture. `nil` clears it. Yields while a link downloads; returns `ok, err`. |
| `Get()` | The current source. |
| `SetCaption(text)` / `SetTitle(text)` | Change the caption (`nil` hides it) or the title. |
| `SetScaleType(name)` / `SetColor(color)` | Change how it fills the card, or its tint. |

---

## Table

> Rows under a header, sortable by column. With `Rank` it is a leaderboard.

```lua
local Board = Tab:CreateTable({
    Name = "Leaderboard",
    Rank = true,
    Columns = {
        "Player",
        { Name = "Kills", Align = "Right", Width = 0.2 },
        { Name = "Cash", Align = "Right", Width = 0.25, Format = function(v) return "$" .. v end },
    },
    Rows = {
        { "Builderman", 42, 12500 },
        { "Roblox", 57, 9800, Highlight = true },
    },
    SortBy = "Kills",
    MaxRows = 8,
    Callback = function(row, index)
        print(row[1], index)
    end,
})

Board:AddRow({ "Guest", 12, 300 })
Board:UpdateRow(2, { "Roblox", 60, 10200, Highlight = true })
```

A search box sits above every table and filters the rows as you type, matching any cell's text; while it filters, a count of the matching rows shows on its right. Ranks and medals keep their place in the full board, so a filtered leaderboard still shows each player's real rank. `Search = false` removes the box. Click a header to sort by it: numbers go high to low first and text A to Z, a second click flips it, and a third goes back to the order you gave. An arrow marks the sorted column. `Rank = true` adds a `#` column numbered by the order on screen, with gold, silver and bronze badges for the top three. Rows alternate shading and light up on hover. A highlighted row gets an accent tint, accent text and a bar on its left, for marking the player. `UpdateRow` flashes the row it changed. Past `MaxRows` the body scrolls; with fewer rows the card shrinks to fit.

A row is a list of values in column order, or a table keyed by each column's `Key` (its name by default). Numbers get thousands separators unless the column has a `Format`.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | — | Title above the table. |
| `Desc` | string | — | Hint text under the title. |
| `Columns` | table | — | Column names, or `{ Name, Key, Width, Align, Format, Color, Sortable }`. `Width` above 1 is pixels, up to 1 a share of the width; columns without one split what's left. `Align` is `"Left"`, `"Center"` or `"Right"`. `Format(value, row)` returns the text to show. `Color` is a Color3, `"#rrggbb"`, a theme key (`"Success"`) or `function(value, row)` returning one. `Sortable = false` locks a column. |
| `Rows` | table | `{}` | The rows. Put `Highlight = true` in a row to mark it, and `Colors = { [key or column number] = color }` to colour single cells. Cell text is rich text, so [coloured text](#coloured-text) works. |
| `Rank` | boolean | `false` | Add the `#` column with medals. |
| `Highlight` | function | — | `function(row, index)` returning `true` to mark a row, for example the player's own. |
| `SortBy` / `SortDescending` | string \| number / boolean | — / `true` | Starting sort: a column name, key or number. |
| `Sortable` | boolean | `true` | `false` turns header sorting off for every column. |
| `MaxRows` | number | `8` | Rows shown before the body scrolls. |
| `RowHeight` | number | `26` (`32` touch) | Height of a row. |
| `EmptyText` | string | `"Nothing here yet"` | Shown with no rows. |
| `Search` | boolean | `true` | The search box above the table. |
| `SearchPlaceholder` / `NoMatchText` | string | `"Search"` / `"No rows match"` | Text in the empty box, and shown when the search matches nothing. |
| `Callback` | function | — | `function(row, index)` when a row is clicked. `OnRowClick` works too. |

### Handle

| Member | Description |
| --- | --- |
| `.Rows` | The rows, in the order you gave. Indexes below refer to this list, not the sorted view. |
| `SetRows(rows)` / `Set(rows)` | Replace every row. Cheap enough to call every second for a live board. |
| `GetRows()` / `Get()` | The rows. |
| `AddRow(row, index?)` | Add a row at the end or at `index`. Returns its index. |
| `UpdateRow(index, row)` | Replace a row and flash it. |
| `RemoveRow(index)` / `Clear()` | Remove one row or all of them. |
| `Sort(column?, descending?)` | Sort from code. `Sort()` goes back to the given order. |
| `SetColumns(columns)` | Rebuild the header and clear the sort. |
| `SetMaxRows(n)` / `SetTitle(text)` | Change the visible row count or the title. |
| `SetSearch(text)` | Fill the search box from code; `""` clears it. |

### Editable tables

> Give a column a `Type` and its cells become editors: rows get added and removed in the table, and `Get()` hands back plain row tables.

```lua
local Rules = Tab:CreateTable({
    Name = "Price Rules",
    Columns = {
        { Name = "Item", Type = "Text", Placeholder = "Item name" },
        { Name = "Sell", Type = "Number", Min = 0, Integer = true, Align = "Right", Width = 0.22 },
        { Name = "Buy", Type = "Toggle", Align = "Center", Width = 0.14 },
        { Name = "Mode", Type = "Dropdown", Options = { "Market", "Auction", "Trade" } },
    },
    Rows = { { Item = "Golden Egg", Sell = 500, Buy = false, Mode = "Market" } },
    Flag = "PriceRules",
    OnChanged = function(rows) end,
})

for _, rule in ipairs(Rules:Get()) do
    print(rule.Item, rule.Sell, rule.Buy, rule.Mode)
end
```

`Text` and `Number` cells are text boxes that commit when they lose focus. A number takes the same shorthand as inputs (`1.5k`), is clamped to `Min` and `Max`, rounds with `Integer = true`, and goes back to its old value when the text isn't a number. `Toggle` cells are switches. `Dropdown` cells open a short list of `Options` (a list, or `function(row)` returning one). Any column without a `Type` stays plain text. `Editable = true` turns editing on without typed columns, for just the add and remove controls.

New rows come from `NewRow` (a table, or a function returning one), else from each column's `Default`, else off, `Min` or `0`, the first option, or `""`. They're keyed by column `Key` (the name by default). A `Flag` saves the rows with the config; loading one replaces them.

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Columns[i].Type` | string | — | `"Text"`, `"Number"`, `"Toggle"` or `"Dropdown"`. |
| `Columns[i].Options` / `Min` / `Max` / `Integer` / `Default` / `Placeholder` | — | — | Per-type settings as above. |
| `Columns[i].Searchable` / `SearchAfter` / `SearchPlaceholder` / `MaxRows` | boolean / number / string / number | — / — / `"Search"` / `6` | Dropdown cells: a search box at the top of the list (`Searchable = true`, or once there are more than `SearchAfter` options) that filters as you type; Enter picks the first match. `MaxRows` is how many options show before the list scrolls. |
| `OnChanged` | function | — | `function(rows)` after any edit, add or remove, and after `SetRows` unless it's called with `silent = true`. |
| `NewRow` | table \| function | — | The row the Add button inserts. |
| `AllowAdd` / `AllowRemove` | boolean | `true` | The Add row button under the table, and the remove column at the end of each row. |
| `AddText` | string | `"Add row"` | Text on the Add button. |
| `Flag` | string | — | Save the rows with the config. |

`NewRow()` on the handle returns a fresh row without adding it.

---

## Log

> A capped, scrolling list of timestamped lines, for a history the latest status line would overwrite.

```lua
local Activity = Tab:CreateLog({ Name = "Activity", MaxEntries = 100, MaxRows = 6 })

Activity:Push("Bought <Accent>Golden Egg</Accent> for 480", "Success")
Activity:Push("Trade declined", "Warning")
Activity:Clear()
```

New lines go at the bottom. While you're scrolled to the end the log follows them; scroll up and it stays put. Past `MaxEntries` the oldest line drops off. Lines wrap, and the text is rich text, so [coloured text](#coloured-text) works. `CreateFeed` is the same element.

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` / `Desc` | string | — | Title and hint. |
| `MaxEntries` | number | `100` | Lines kept. |
| `MaxRows` | number | `6` | Lines shown before it scrolls. |
| `Timestamps` | boolean | `true` | A muted time before each line. |
| `TimeFormat` | string | `"%H:%M:%S"` | `os.date` format for it. |
| `EmptyText` | string | `"Nothing logged yet"` | Shown with no lines. |

| Member | Description |
| --- | --- |
| `Push(text, color?)` | Add a line. `color` is a Color3, `"#rrggbb"` or a theme key (`"Success"`, `"Error"`, `"Muted"`). Also `Add` and `Log`. |
| `Clear()` | Remove every line. |
| `Get()` | Copies of the lines, oldest first: `{ Text, Color, Time }`. |
| `SetMaxEntries(n)` / `SetTitle(text)` | Change the cap or the title. |

---

## Notification

> A toast in the bottom-right corner.

```lua
local Notification = Library:Notify({
    Title = "Loaded",
    Content = "5 tabs ready",
    Icon = "check",
    Type = "Success",
    Duration = 4,
})

local Notification = Window:Notify({ Title = "Window specific" })

Notification:Dismiss()
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Title` | string | `"Notification"` | Bold first line. |
| `Content` | string | — | Wrapped body. |
| `Icon` | string \| number \| table | — | Icon before the title. |
| `Duration` | number | `4` | Seconds before it dismisses itself. |
| `Type` | string | `"Info"` | `"Info"`, `"Success"`, `"Warning"` or `"Error"`. Tints the title. |

### Handle

| Member | Description |
| --- | --- |
| `Dismiss()` | Close it now. |

---

## Confirm

> Ask before doing something.

```lua
Tab:CreateButton({
    Name = "Unload",
    Callback = function()
        Library:Confirm({
            Title = "Unload?",
            Content = "The window closes and everything is restored.",
            Icon = "power",
            ConfirmText = "Unload",
            CancelText = "Keep",
            Callback = function()
                Window:Destroy()
            end,
            OnCancel = function()
                print("Kept")
            end,
        })
    end,
})

Library:Dialog({
    Title = "Choose",
    Content = "Pick one.",
    Icon = "list",
    CloseOnBackdrop = true,
    Buttons = {
        { Title = "Later", Callback = function() end },
        { Title = "Now", Variant = "Primary", Callback = function() end },
    },
})
```

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Title` | string | `"Are you sure?"` | Heading. |
| `Content` | string | — | Wrapped body. |
| `Icon` | string \| number \| table | — | Icon before the heading. |
| `ConfirmText` | string | `"Confirm"` | Primary button. |
| `CancelText` | string | `"Cancel"` | Secondary button. |
| `Callback` | function | — | Runs when confirmed. |
| `OnCancel` | function | — | Runs on cancel or a backdrop click. |

`Dialog` builds the same card with any number of buttons. `Variant = "Primary"` gives a button the accent fill. `CloseOnBackdrop = false` forces a button press.

---

## Flags

> Read and write any element by its save key.

```lua
print(Library.Flags.AutoSprint:Get())
Library.Flags.WalkSpeed:Set(50)
```

Toggles, sliders, steppers, dropdowns, inputs, keybinds and colour pickers created with a `Flag` are stored on `Library.Flags`. Flags are also what configs save.

---

## Configs

`ConfigurationSaving.FolderName` selects the executor folder. `Enabled` is accepted in examples but is not read by this implementation; do not rely on `Enabled = false` to suppress writes. `SetIgnoreFlags` excludes named flags from config saving/loading, and `SetLoadingOrder` controls application order; see the extended index.

> Save every flagged element to a file, load it back, and pick one to autoload.

```lua
local Window = Library:CreateWindow({
    Name = "KawiXD",
    ConfigurationSaving = { Enabled = true, FolderName = "MyHub" },
})

local Settings = Window:CreateTab({ Name = "Settings", Icon = "settings" })
Settings:CreateConfigManager({ Name = "Configs", Side = "Left" })

-- create the rest of your tabs and elements

Window:LoadAutoload()
```

The config manager is a groupbox with, from top to bottom:

- a **config name** box and the config picker
- **Create** / **Save**, **Load** / **Delete**, **Set autoload** / **Clear autoload**, **Rename** / **Reset**
- a status line: `loaded: <name> | autoload: <name>`
- **Autoload mode**: *All accounts* or *This account*
- **Refresh list**
- a **share** section: **Copy code** puts the current settings on the clipboard as a code, and **Import code** applies a pasted code and saves it. It's saved under the name in the name box, or else the name inside the code (with ` (2)`, ` (3)`... added rather than overwriting a config you already have).

Save with nothing picked creates a config from the typed name. **Rename** renames the picked config to the typed name and moves the loaded name and autoloads with it. **Reset** puts every flagged element back to the value it was created with and deletes the script's whole `FolderName` folder (configs, saved themes, the default theme, autoload, settings, execution count), after a confirm. Names can't contain `\ / : * ? " < > |`.

`LoadAutoload` can run before every element exists. Values for flags that no element has claimed yet are held and applied as soon as an element with that flag is created, and saving writes them back, so a config never loses settings for elements that only exist some of the time (a game-specific tab, say).

### File format

A config file and a share code are the same readable JSON, so a code is just the file's contents:

```json
{"Folder":"MyHub/Game","Name":"farm","Version":1,"Config":"{\"AutoFarm\":{\"Value\":true,\"Type\":\"Toggle\"},\"Speed\":{\"Value\":40,\"Type\":\"Slider\"},\"EspColor\":{\"Value\":{\"Hex\":\"ff5a5a\"},\"Type\":\"ColorPicker\"},\"Targets\":{\"Value\":[\"Boss\",\"Mob\"],\"Type\":\"Dropdown\"},\"Pick\":{\"Type\":\"Dropdown\"}}"}
```

- `Folder` is the window's `FolderName`. Importing a code made for another folder asks first, and then only applies the flags that match by name and type.
- `Config` is the flags as their own JSON string. Each flag is `{ "Value": ..., "Type": ... }`. Colours are `{ "Hex": "rrggbb" }`, keybinds are key names (`"RightShift"`), and a dropdown with nothing picked has no `Value`.
- Old `airflow:...` base64 codes and older config files (bare flag tables, colours as RGB arrays) still load, and are rewritten in the new format on the next save.

Configs only change when you press **Create** or **Save** (or call `SaveConfig`); nothing is written automatically. The autoload mode lives in `<folder>/configsettings.txt`, apart from the configs, so loading a config never flips it. *This account* keeps the autoload in `autoload_<UserId>.txt`, so other accounts on the same PC don't load it. Switching modes moves the current autoload across.

Requires `writefile` / `readfile`.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `FolderName` | string | `"KawiXD"` | Folder in the executor workspace. Can be nested, like `"MyHub/Game"`; missing folders are made. |
| `FileName` | string | none | Optional config used when `SaveConfig` / `LoadConfig` get no name. With none set, there is no default config: only configs you create exist. |

`CreateConfigManager` takes `Name`, `Icon`, `Side` and `Placeholder`. Called on a groupbox it adds its rows there instead of making its own.

### Handle

| Member | Description |
| --- | --- |
| `Window:SaveConfig(name?)` | Write `<folder>/<name>.json`. Returns `ok, err`. |
| `Window:LoadConfig(name?, skipCallbacks?)` | Apply a saved config and mark it loaded. |
| `Window:DeleteConfig(name)` | Remove the file. |
| `Window:RenameConfig(name, newName)` | Rename a config, carrying the loaded name and autoloads along. Refuses to overwrite. |
| `Window:ConfigExists(name)` | Whether `<folder>/<name>.json` exists. |
| `Window:ResetConfig(skipCallbacks?)` | Put every flagged element back to its starting value. |
| `Window:ClearWorkspace()` | Delete the script's `FolderName` folder and everything in it. Returns `false` if some files could not be removed. |
| `Window:ListConfigs()` | Saved names, sorted without regard to case. |
| `Window.LoadedConfig` | Name of the loaded config, or `nil`. |
| `Window:ExportConfig(name?)` | Share code (the config JSON) for a saved config, or for the current settings when `name` is `nil`. |
| `Window:DecodeConfig(code)` | Read a code without applying it. Returns `flags, { Folder, Name, Version }`, or `nil, err`. |
| `Window:ImportConfig(code, saveAs?, force?)` | Apply a code. `saveAs` is a name, `true` for the name inside the code, or `nil` to only apply it. Codes for another `Folder` fail unless `force`. Returns `ok, err, savedName`. |
| `Window:SetAutoload(name?, scope?)` / `GetAutoload(scope?)` / `LoadAutoload(skipCallbacks?)` | The config loaded on start. `nil` clears it. `scope` is `"Global"` or `"Account"`, defaulting to the current mode. |
| `Window:SetAutoloadMode(mode)` / `GetAutoloadMode()` | `"Global"` (all accounts) or `"Account"` (this account). |
| `Window:OnConfigChanged(fn)` | Runs `fn` after a load, delete, import or autoload change. Returns a disconnect function. |
| `Tab:CreateConfigManager(opts)` | Returns `Create / Save / Load / Delete / Rename / Reset / SetAutoload / ClearAutoload / ToggleAutoload / SetAutoloadMode / Export / Import / Refresh`. |

---

## Icons

> Any lucide icon or your own image, anywhere an `Icon` is accepted.

```lua
Library:PreloadIcons()

Window:CreateTab({ Name = "Main", Icon = "zap" })
Tab:CreateInput({ Name = "Key", Icon = "lucide:key-round" })

local Window = Library:CreateWindow({ Name = "My Hub", Icon = 132608042600488 })
Window:CreateTab({ Name = "Custom", Icon = "rbxassetid://132608042600488" })
Tab:CreateButton({ Name = "Tinted", Icon = { Image = 132608042600488, Tint = true } })
Tab:CreateButton({
    Name = "Sprite",
    Icon = { Image = "rbxassetid://122605056588923", RectOffset = Vector2.new(325, 775), RectSize = Vector2.new(24, 24) },
})
```

| Form | Treated as |
| --- | --- |
| `"zap"` / `"lucide:zap"` | Lucide icon, tinted by the theme. |
| `132608042600488` / `"132608042600488"` / `"rbxassetid://…"` / `"rbxthumb://…"` | Your own image, shown in its own colours. |
| `{ Image, RectOffset, RectSize, Tint }` | Your own image or a sprite. `Tint = true` lets the theme colour it like a lucide icon. |

Custom images keep their colours through theme changes and are drawn 35% larger than their slot, since uploaded images usually carry transparent padding. A table icon can set its own `Scale` (`Scale = 1` for the exact slot size). On tabs and sub tabs, a custom icon shows the selection by going from dimmed to full opacity instead of changing colour. The default bird logo is still tinted with the accent.

Names resolve through the [Footagesus/Icons](https://github.com/Footagesus/Icons) list, fetched once on first use; `Library:PreloadIcons()` fetches it up front.

---

## Fonts

> Download a font once and use it everywhere.

```lua
Library:LoadFont({ Name = "ValleySans" })

Library:LoadFont({
    Name = "MyFont",
    Folder = "OuroFlowFonts",
    Weights = {
        Regular = "https://example.com/MyFont-Regular.ttf",
        Medium = "https://example.com/MyFont-Medium.ttf",
        SemiBold = "https://example.com/MyFont-SemiBold.ttf",
    },
})
```

Call it before `CreateWindow`. The TTFs are saved to the folder on first run and reused after that. Needs `writefile`, `isfile` and `getcustomasset`; without them the default Builder Sans stays.

### Properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | — | Family name. `"ValleySans"` uses the built-in URLs. |
| `Folder` | string | `"OuroFlowFonts"` | Where the TTFs and family file are saved. |
| `Weights` | table | preset | `Regular`, `Medium`, `SemiBold`, `Bold` → TTF URL. |

---

## Theme

The native presets below remain available alongside `Null Fire`, `Null Ice`, and `Null Mono`. `CreateKawiXDWindow` requests `Null Fire` unless you pass `Theme` or `DefaultTheme`; a saved player default still takes precedence.

> Colours, fonts and assets. Themes switch live: every themed colour in the window fades to the new one.

```lua
Library:SetTheme("Midnight")
Library:SetTheme({ Accent = Color3.fromRGB(128, 160, 246), Background = "#0F121A" })

Library:SetDefaultTheme("Synthwave") -- the script's starting theme
local Window = Library:CreateWindow({ Name = "KawiXD", DefaultTheme = "Synthwave" }) -- same thing

Settings:CreateThemeManager({ Name = "Themes", Side = "Right" })

Library.ThemePresets.Neon = { Accent = Color3.fromRGB(0, 255, 170) }

local Family = "rbxasset://fonts/families/BuilderSans.json"
Library.Fonts.Regular = Font.new(Family, Enum.FontWeight.Regular)
Library.Fonts.Medium = Font.new(Family, Enum.FontWeight.Medium)
Library.Fonts.Bold = Font.new(Family, Enum.FontWeight.SemiBold)

Library.Assets.Logo = "rbxassetid://103859712365480"
Library.Assets.Glow = "rbxassetid://8992230677"
Library.Assets.Shadow = "rbxassetid://6014261993"
```

Presets: `Midnight` (default), `Nebula`, `Synthwave`, `Sakura`, `Velvet`, `Rose`, `Crimson`, `Sunset`, `Amber`, `Gold`, `Cyber`, `Toxic`, `Matcha`, `Emerald`, `Aurora`, `Ocean`, `Frost`, `Abyss`, `Mono`, and the themed set `Halloween`, `Haunted`, `Christmas`, `Valentine`, `Lunar`, `Tropical`, `Dracula`, `Coffee`. `SetTheme` takes a preset name or a table of any keys below, as `Color3`, `"#RRGGBB"` or `{ r, g, b }`. Pass `true` as the second argument to skip the fade.

The theme manager is a groupbox with a **Preset** picker, **Weather** and **Weather Mode** pickers, **Dim** and **Transparent** switches, a **Drag Style** picker, an **Adaptive Size** switch (on by default; scales the window with the screen resolution), a **UI Scale** slider (applied when you let go of it), a **Density** picker, a **Corner Radius** slider (0 to 20 px; every corner eases to the new radius), a name box and **Create** to save the current colours, a **Theme** picker for saved themes, **Save** / **Load**, **Delete** / **Set Default**, the current default, and colour pickers for the main colours (`Customize = false` hides them). On start the window applies the player's default (set with **Set Default**, a preset or a saved theme); without one it applies the script's default from `Library:SetDefaultTheme` or the `Theme` window option. Themes are saved in `<config folder>/themes`.

### Properties

| Name | Used for |
| --- | --- |
| `Background` | Window, toast and dialog fill. |
| `Surface` | Chips, text boxes, popups. |
| `Surface2` | Element cards, groupboxes, option rows. |
| `Surface3` | Toggle pill off, tracks, buttons, selected tab. |
| `Stroke` | Outlines at rest. |
| `StrokeHover` | Outlines on hover, focus, open. |
| `Accent` | Highlights, primary buttons, checkboxes, progress bars. |
| `AccentDark` | Text on accent surfaces. |
| `Text` / `Muted` | Primary and secondary text. |
| `Success` / `Warning` / `Error` | Notification title tints, status tones and [coloured text](#coloured-text). |
| `Fonts.Regular` / `Medium` / `Bold` | Body text / titles and chips / emphasis. |
| `Assets.Logo` / `Glow` / `Shadow` | Sidebar mark, glow decal, drop shadow. |

### Handle

| Member | Description |
| --- | --- |
| `Library:SetTheme(nameOrTable, instant?)` | Apply a preset or colours live. |
| `Library:GetTheme()` | Copy of the current colours. |
| `Library:SetDefaultTheme(nameOrTable)` / `GetDefaultTheme()` | The script's starting theme. Call it before or after `CreateWindow`; it applies right away unless the player saved their own default. |
| `Library.ThemePresets` | The presets, by name. Add your own. |
| `Window:SaveTheme(name)` / `LoadTheme(name)` / `DeleteTheme(name)` / `ListThemes()` | Saved themes. `LoadTheme` also accepts a preset name. |
| `Window:SetDefaultTheme(name?)` / `GetDefaultTheme()` | The player's saved default, applied on start. Wins over the script default. |
| `Tab:CreateThemeManager(opts)` | `Name`, `Icon`, `Side`, `Customize`, `Colors = { { key, label } }`, `Weather` (`false` hides the weather dropdown), `Dim` (`false` hides the dim toggle), `Transparent` (`false` hides the toggle), `DragStyle` (`false` hides the drag style picker), `IslandStyle` (`false` hides the Dynamic Island picker), `CornerRadius` (`false` hides the corner radius slider), `AdaptiveSize` (`false` hides the adaptive size switch), `Scale` and `Density` (`false` hides the UI scale slider or the density picker), `Background` (`false` hides the background image dropdown, id/link box and opacity slider). The weather dropdowns cover the weather and its mode, screen-wide or inside the window. Configs save the theme (palette, preset or theme name, weather, dim, transparent, drag style, island style, corner radius, adaptive size, UI scale, density, background image and opacity) under one hidden flag, `__Theme` by default; `Flag` renames it, `Flag = false` leaves the theme out of configs. |

`Library.Touch` is `true` on touch-only devices; cards, chips and hit areas are larger there automatically.

---

## Coloured text

> Colour any part of a status, status list row, table cell, progress label, label or paragraph.

```lua
Status:Set("<Success>Online</Success> · 3 players")             -- a theme key as a tag
Status:Set(Library.Colorize("12 ms", "Success"))                 -- the same, built for you
Status:Set(Library.Colorize("Boss", Color3.fromRGB(255, 90, 90))) -- any Color3 or "#rrggbb"
Status:Set('<font color="#ff5a5a">raw</font> rich text')          -- plain Roblox rich text

Group:CreateStatus({ Name = "Mode", Value = "Aggressive", Style = "Row", Color = "Warning" })
Skills:Set({ { Text = "Dash", Value = "<Error>cooldown</Error> 4s" } })
Board:SetRows({ { "Roblox", 57, Colors = { [2] = "Success" } } })
```

Every theme colour works as a tag: `<Accent>`, `<Success>`, `<Warning>`, `<Error>`, `<Muted>`, `<Text>` and the rest of the [theme keys](#theme), in any case. Theme tags are resolved when the text is drawn and drawn again when the theme changes, so `<Success>` follows the palette; a `Color3` or hex colour stays fixed. Tags that aren't theme keys (`<b>`, `<i>`, `<font>`, `<stroke>`…) pass straight through to Roblox rich text.

Whole-value colours take the same forms everywhere: a theme key string, a `Color3`, `"#rrggbb"` or `{ r, g, b }`. Status `Color` and `Tone`, status list `Tone` / `Color`, table column `Color` and row `Colors`, progress `Color` / `TextColor` and label `Color` all accept them. The home tab tints its `FPS`, `Ping` and `Memory` stats by health on its own (`StatColors = false` turns that off).

| Member | Description |
| --- | --- |
| `Library.Colorize(text, color)` | Wraps `text` in a colour. A theme key gives a tag that follows the theme; anything else is baked in. `Library:Colorize(...)` works too. |

## Extended API index

The walkthrough above shows the standard options and usage. This index adds **source-exact signatures, return values, aliases, and less-visible helpers**. Receiver names matter: a `Library` method, native `Window` method, enhanced window method, manager method, and element handle are not interchangeable. Underscore-prefixed implementation helpers and Roblox Instance methods are not supported library API.

**Behavior to know:** `ConfigurationSaving.Enabled` is never read by this source. The enhanced factory supplies `Enabled = false` as an option, but that is **not a file-write kill switch**. Native config methods, remembered UI settings, and hidden size flags remain available when executor file APIs exist. Appearance export itself is explicit JSON generation and does not write a file.

<details>
<summary><strong>Library, window, container, config, theme, and background methods</strong></summary>

### Library

| Signature | Behavior / return | Verified details |
|---|---|---|
| `Library:Window(options)` | Creates and returns a native `Window`. | `Library.CreateWindow` is an alias. The options normalizer maps `Name` → `Title`, `LoadingSubtitle` → `Subtitle`, and `ToggleUIKeybind` → `Keybind`; a string `Keybind` is converted with `Enum.KeyCode[key]`. |
| `Library:CreateWindow(options)` | Alias of `Library:Window`; returns a native window. | It does not install the KawiXD appearance layer or force a theme. |
| `Library:CreateKawiXDWindow(options)` | Creates and returns a window with the KawiXD appearance layer installed. | Defaults `DefaultTheme` to `Null Fire` only when no theme is supplied. `CreateNullFireWindow` is an alias. |
| `Library:CreateAppearanceTab(window, options)` | Creates and returns an appearance-editor tab for the supplied window. | The appearance methods must already be installed; intended for a window from `CreateKawiXDWindow`. |
| `Library:Notify(options)` | Forwards to the most recently created window and returns its notification handle, or `nil` if there is no window. | `options.Text`/`Message` normalize to `Content`; `Image` normalizes to `Icon`. |
| `Library:Confirm(options)` / `Library:Dialog(options)` | Forwards to the most recently created window and returns that window method's result, or `nil` with no window. | These forwarders are real source methods. |
| `Library:LoadFont(options)` | Downloads configured font files, registers custom assets, updates `Library.Fonts`, and returns `true`; returns `false` when required file/custom-asset APIs are unavailable. | `Name` selects a preset (currently `ValleySans`); `Weights` may supply a weight map. |
| `Library:PreloadIcons()` | Loads and caches Lucide icons; returns the loaded table, or `false` after warning when loading fails. | Requires executor HTTP and `loadstring`. |
| `Library:SetDensity(mode)` | Sets shared layout density; use `Window:GetDensity()` to read it. | Accepted modes are `Compact`, `Default`, and `Comfortable` (case-insensitive); invalid input is replaced by `Default`. There is no `Library:GetDensity()` method. Setter returns the selected mode. `Window:SetDensity` forwards to this method and `Window:GetDensity` returns the shared mode. |
| `Library:SetCornerRadius(pixels[, instant])` / `Library:GetCornerRadius()` | Sets/gets the shared corner radius. | Input is rounded and clamped to **0–20 pixels**. Setter returns the settled integer radius; `instant` selects immediate vs tweened repaint. |
| `Library:SetTheme(theme[, instant])` / `Library:GetTheme()` | Applies a preset name or color table / returns a detached current color table. | A string must name an existing `ThemePresets` entry; a table is accepted. Invalid type/name returns `false`; successful set returns `true`. |
| `Library:SetDefaultTheme(theme)` / `Library:GetDefaultTheme()` | Sets/gets the default theme value. | `theme` may be a preset **name string**, a palette **table**, or `nil`; setter returns `true` or the result of applying the theme. A saved player default can take precedence when a window is created. |
| `Library:RegisterTheme(name, colors)` | Registers a merged named theme; returns `true`, or `false, error`. | Validation and color conversion are performed by the implementation; unknown/invalid entries are rejected. |
| `Library:Colorize(text, color)` | Returns rich-text markup, or the original text when the color cannot be resolved. | `color` may be a theme tone name, `Color3`, or supported color string. It does not display text. |
| `Library:Destroy()` / `Library:Unload()` | Destroys all windows created by the library. | `Unload` is an alias. |
| `Library.Flags` / `Library.Windows` / `Library.Theme` / `Library.ThemePresets` / `Library.Touch` | Public state tables/flag registries exposed by the source. | These are live implementation tables, not detached snapshots. |

### Window: navigation, visibility, sizing, and presentation

| Signature | Behavior / return | Verified details |
|---|---|---|
| `Window:Tab(options[, icon])` | Creates and returns a tab. | `Window.CreateTab` is an alias. |
| `Window:SelectTab(tab)` | Selects the supplied tab object and transitions to it. | The body accepts a tab object; it does **not** resolve a name or numeric index. It resets search and closes popups. Passing an unsupported value is not a documented API contract. |
| `Window:Toggle([open])` | Sets `Open` to the supplied boolean when given; otherwise toggles it. | No documented return. |
| `Window:Minimize()` / `Window:Restore()` / `Window:SetMinimized(value)` | Minimizes/restores or sets minimized state. | `SetMinimized` uses the supplied truth value; no documented return. |
| `Window:SetIslandDraggable(enabled)` / `Window:ResetIslandPosition()` | Enables island dragging / resets the remembered island position. | No documented return. `IslandDraggable = false` also locks it at construction. |
| `Window:SetKeepOnScreen(enabled)` | Sets `KeepOnScreen` to `enabled ~= false` and clamps when enabled. | No documented return; default is enabled. |
| `Window:SetKeybind(key)` | Replaces the window keybind. | Constructor options accept a string key name and convert it to `Enum.KeyCode`; the setter stores the supplied value directly, so use an `Enum.KeyCode` (or `nil`) rather than relying on setter string conversion. |
| `Window:SetAdaptiveSize(enabled)` / `Window:GetAdaptiveSize()` | Enables/gets adaptive viewport fitting. | Getter returns boolean; setter has no documented return. |
| `Window:SetUIScale(value)` / `Window:GetUIScale()` | Sets/gets UI scale. | Setter clamps to **0.6–1.5**; getter returns the requested scale, while adaptive fitting can additionally affect rendered scale. |
| `Window:GetSize()` / `Window:SetSize(size[, instant])` | Gets current pixel size / applies a `Vector2` size subject to window constraints. | `instant` controls resizing animation. `SaveSize` is handled by the configuration manager when configured. |
| `Window:SetDragStyle(style)` / `Window:GetDragStyle()` | Sets/gets drag skeleton style. | Accepted styles are exactly **`Outline`, `Brackets`, `Ghost`, `Frame`, `Off`**. Any other value falls back to `Outline`; setter returns the settled style. `DragSkeleton = false` maps to `Off`. |
| `Window:SetIslandStyle(style)` / `Window:GetIslandStyle()` | Sets/gets minimized-island presentation. | Accepted styles are `Show on Hover` and `Always Show`; invalid input falls back to `Show on Hover`; setter returns the settled style. |
| `Window:SetDragSkeleton(enabled)` | Compatibility on/off wrapper for drag style. | `false` selects `Off`; `true` restores `Outline` only when currently off. No documented return. |
| `Window:SetTransparent(enabled)` | Sets the window's transparent presentation mode. | Separate from appearance-layer image transparency; no documented return. |
| `Window:SetToggleButton(enabled)` / `SetToggleButtonPlatform(platform)` / `SetToggleButtonIcon(icon)` | Controls the floating toggle button, its platform restriction, and icon. | No documented return. |
| `Window:SetHideName(hidden)` / `SetHideAvatar(hidden)` | Sets profile-name/avatar visibility flags. | Source uses strict `hidden == true`; no documented return. |
| `Window:Rejoin()` / `ServerHop()` / `JoinLowestServer()` | Starts the corresponding asynchronous teleport operation. | No documented return; requires teleport/network capability. |
| `Window:CopyToClipboard(text[, label])` | Uses executor clipboard support and displays a result notification. | Returns a boolean; requires `setclipboard` or an equivalent. |
| `Window:ShowFeatures()` | Shows/selects the native feature surface. | No documented return. |
| `Window:SetIgnoreFlags(flags)` | Adds flag names to the ignore set used while applying configs. | `flags` is expected to be an array/table; no documented return. |
| `Window:SetLoadingOrder(order)` | Replaces the config-application type order when `order` is a table; otherwise clears the override. | No documented return. |
| `Window:SetSidebarWidth(value)` | Sets the sidebar width through the function installed when the sidebar is built. | `value` is converted with `tonumber` (default `188`) and floored/clamped to **150–300 px**, further limited by available body width (`body width / scale - 300`) when that is smaller; the effective lower bound remains 150. Returns nothing. |
| `Window:Destroy()` / `Window:Unload()` | Disconnects listeners, removes registrations, and destroys the window. | `Unload` is an alias; repeated destruction is guarded. |

### Window: notifications and dialogs

| Signature | Behavior / return | Verified details |
|---|---|---|
| `Window:Notify(options)` | Creates a toast and returns `{ Dismiss = function() ... end }`. | `Text`/`Message` normalize to `Content`; `Image` to `Icon`; `Type` selects notification color; `Duration` defaults to 4 seconds. |
| `Window:Dialog(options)` | Opens a modal and returns a dialog object with `Close()`. | `Buttons` entries use `Title` or `Name`, optional `Variant`, and `Callback`; `OnCancel` runs on backdrop cancellation when `CloseOnBackdrop ~= false`. A new dialog closes the previous one. |
| `Window:Confirm(options)` | Builds a two-button dialog and returns the dialog handle. | Uses `Content` (normalized from `Text`/`Message`), `ConfirmText`, `CancelText`, `Callback`, and `OnCancel`. |

### Window: native file configs and autoload

`ConfigurationSaving.Enabled` is not read by the implementation; it does not disable these methods or file operations.

| Signature | Behavior / return | Verified details |
|---|---|---|
| `Window:OnConfigChanged(handler)` | Registers a config-change callback and returns a disconnect function. | Callback errors are protected by dispatch. |
| `Window:ConfigExists(name)` | Returns boolean. | Requires a valid name and available file APIs; forbidden characters are `\\ / : * ? " < > |`. |
| `Window:SaveConfig([name])` | Writes current flags; returns `true` or `false, error`. | Uses `ConfigName`; missing both returns `false, "no config name"`. |
| `Window:LoadConfig([name[, silent]])` | Reads/applies a config; returns `true` or `false, error`. | Uses `ConfigName`, updates `LoadedConfig`, and fires listeners. |
| `Window:DeleteConfig(name)` | Deletes a config; returns `true` or `false, error`. |
| `Window:RenameConfig(name, newName)` | Copies, deletes, and updates references; returns `true` or `false, error`. | Rejects an existing destination or invalid name. |
| `Window:ListConfigs()` | Returns sorted config basenames without `.json`; returns `{}` when listing is unavailable. |
| `Window:ResetConfig([silent])` | Restores flagged elements to creation defaults; returns `true`. |
| `Window:ClearWorkspace()` | Removes the complete config workspace; returns boolean. |
| `Window:ExportConfig([name])` | Returns encoded JSON or `nil, error`. | With a name reads that file; without one encodes current flags. |
| `Window:DecodeConfig(code)` | Returns `flags, { Folder, Name, Version }`, or `nil, error`. | Does not apply the config. |
| `Window:ImportConfig(code[, saveAs[, force]])` | Applies decoded flags; returns `true, nil, savedName` or `false, error`. | `saveAs=true` uses embedded `Name`; a string saves under that name; omitted/nil applies without writing; `force=true` permits a different embedded folder. |
| `Window:GetAutoloadMode()` / `SetAutoloadMode(mode)` | Gets/sets `Global` or `Account`; setter returns `true` or `false, error`. | Any mode other than `Account` is treated as `Global`. |
| `Window:GetAutoload([scope])` / `SetAutoload(name[, scope])` | Gets/stores or clears an autoload name. | Scope is `Global` or `Account`; getter with no scope checks Account then Global. Setter returns `true` or `false, error`. |
| `Window:GetMinimizeOnStart()` / `SetMinimizeOnStart(enabled)` / `LoadAutoload([silent])` | Gets/sets persisted minimize-on-start; loads configured autoload. | Setters/load return the underlying boolean/error results. |

### Window: native themes and backgrounds

| Signature | Behavior / return | Verified details |
|---|---|---|
| `Window:SaveTheme(name)` / `LoadTheme([name[, instant]])` / `DeleteTheme(name)` / `ListThemes()` | Theme file save/load/delete/list operations. | Return values come from the file operation; list returns names. |
| `Window:GetDefaultTheme()` / `SetDefaultTheme(name)` | Gets/sets the window default theme selection. | Source signature accepts a **name**; library-level setter accepts a name or table. |
| `Window:SetBackground(source)` / `GetBackground()` / `SetBackgroundTransparency(value)` / `ListBackgrounds()` | Sets/gets native background source, transparency, or preset names. | No unsupported source forms are inferred here. |
| `Window:SetBackdrop(enabled)` | Enables/disables the backdrop. | Accepted input is a boolean-like value; source stores `enabled ~= false`. Returns nothing; does nothing if no backdrop was built. |
| `Window:SetBackdropTint(amount)` | Sets backdrop tint amount. | Numeric input is clamped to **0–1**; defaults to `0.45` when nonnumeric. Returns nothing. |
| `Window:SetDim(enabled)` | Enables/disables the black dim layer while leaving weather running. | This is a boolean switch (`enabled ~= false`), **not an amount**. Returns nothing. |
| `Window:SetWeatherMode(mode)` | Selects weather placement. | `UI`, `Window`, and `Inside` (case-insensitive) select `UI`; every other input selects `Screen`. Returns nothing. |
| `Window:SetWeather(name)` | Selects weather type. | Accepted canonical types: `Rain`, `Snow`, `Ember`, `Sakura`, `Fireflies`, `Matrix`; aliases include `embers/fire/hellfire`, `petals/cherryblossom`, `firefly`, and `matrixrain/code` (case-insensitive). Returns nothing. |
| `Window:SetWeatherDensity(value)` | Sets weather particle density. | Numeric value is clamped to **0–3**; nonnumeric defaults to `1`. Returns nothing. |
| `Window:SetWeatherSpeed(value)` | Sets weather animation speed. | Numeric value is clamped to **0.1–3**; nonnumeric defaults to `1`. Returns nothing. |

### Tab (container receiver)

| Signature | Behavior / return | Verified details |
|---|---|---|
| `Tab:Groupbox(options[, icon])` | Creates and returns a groupbox. | `CreateGroupbox`/`AddGroupbox` aliases; `AddLeftGroupbox` and `AddRightGroupbox` force a side. Calls from nested containers delegate to the parent tab. |
| `Tab:Tabbox(options)` | Creates and returns a tabbox. | `CreateTabbox`/`AddTabbox` aliases; left/right variants force a side. |
| `Tab:SubTab(options[, icon])` / `Tab:SelectSubTab(sub[, instant])` | Creates/selects sub-tabs. | Selection accepts a sub-tab object, title/name, or 1-based index; `instant` skips transition. `CreateSubTab`/`AddSubTab` alias the constructor. |
| `Tab:CreateMinimizeOnStart([options])` | Returns the window's built-in minimize-on-start control, creating it once. |
| `Tab:SetBadge()` / `Tab:GetBadge()` | Compatibility stubs. | Setter warns once and does nothing; getter returns `nil`. |
| `Tab:ButtonRow(options)` / `ConfigManager(options)` / `ThemeManager(options)` | Creates and returns the corresponding native container/control. | These are source-defined convenience constructors. |
| `Tab:Status(options)` / `Statuses(entries[, shared])` / `StatusList(options)` | Creates and returns native status displays. |
| `Tab:Image(options)` / `Table(options)` / `Log(options)` | Creates and returns the corresponding native display container. | `CreateImage`/`AddImage`, `CreateTable`/`AddTable`, and `CreateLog`/`AddLog`/`Feed`/`CreateFeed`/`AddFeed` are aliases. |

### Groupbox, tabbox, and pages

| Signature | Behavior / return | Verified details |
|---|---|---|
| `Groupbox:PopOut()` / `Dock()` / `IsPoppedOut()` | Floats/docks the groupbox or returns its boolean popped-out state. |
| `Groupbox:SetCollapsed(value)` / `Collapse()` / `Expand()` / `IsCollapsed()` | Sets/toggles collapsed state or returns boolean state. |
| `Groupbox:SetTitle(text)` / `SetVisible(value)` / `IsVisible()` / `Destroy()` | Updates title, visibility, reports visibility, or destroys the groupbox and children. |
| `Tabbox:AddTab(nameOrOptions[, icon])` / `Tabbox:SelectTab(page)` | Adds/returns a page or selects a page object. | `nameOrOptions` may be a string/options table; `CreateTab` aliases `AddTab`. `SelectTab` is page-object based in the source, not documented as name/index resolution. |
| `Page:Select()` / `Expand()` / `Collapse()` / `IsCollapsed()` / `SetTitle(text)` / `Destroy()` | Selects/expands, collapses (compatibility no-op), reports non-current state, updates title, or destroys the page. |
| `Tabbox:SetTitle(text)` / `IsVisible()` / `SetVisible(value)` / `Destroy()` | Updates title, reports/toggles visibility, or destroys the tabbox and pages. |

### Verified aliases

`Library.CreateWindow = Library.Window`; `Library.CreateNullFireWindow = Library.CreateKawiXDWindow`; `Library.Unload = Library.Destroy`; `Window.CreateTab = Window.Tab`; `Window.Unload = Window.Destroy`; `Tab.CreateGroupbox = Tab.Groupbox`; `Tab.AddGroupbox = Tab.Groupbox`; `Tab.CreateSubTab = Tab.SubTab`; `Tab.AddSubTab = Tab.SubTab`; `Tab.CreateLog`/`AddLog`/`Feed`/`CreateFeed`/`AddFeed` alias the log constructor; `Tab.CreateImage`/`AddImage`, `CreateTable`/`AddTable`, and `CreateLeaderboard` alias their constructors; `tabbox.CreateTab = tabbox.AddTab`.

Element-handle contracts are indexed in the next expandable section.

</details>

<details>
<summary><strong>Every element handle, normalization aliases, managers, and appearance contracts</strong></summary>

### Rules shared by native elements

- Every public `Tab:Foo(...)` constructor is also available as `Tab:CreateFoo(...)`; this alias is generated for every non-underscore `Tab` method. The same constructors are exposed by groupboxes through the groupbox forwarding layer. `Section` and `Divider` are valid constructors despite accepting a string shorthand.
- `Visible = false` is honored at construction. Every finished element has `SetVisible(bool)`, `IsVisible()`, `SetDisabled(bool)`, `IsDisabled()`, `SetDependsOn(rule, mode?)`, `SetTooltip(tip)`, `GetTooltip()`, and `Destroy()`. `Destroy()` is idempotent, disconnects listeners, removes the element from its tab, removes its flag if it still owns that flag, and destroys its GUI frame. `SetVisible`/`SetDisabled` are no-ops after destruction.
- `Tooltip` is a string or `{Title, Text, Icon}`; `SetTooltip(nil)`/`false` clears it. `DependsOn` uses the library flag dependency rules; `DependsMode = "Disable"` disables rather than hides when the rule is unmet. `SetDependsOn(nil)` removes the dependency.
- Option normalization accepts the documented long names and the native aliases shown below. For table options, unknown fields are retained in the option table, so shared options such as `Flag`, `Visible`, `Disabled`, `DependsOn`, `DependsMode`, and `Tooltip` can be combined with each constructor.
- Setters that implement a second `silent`/`skipCallback` argument document it below; do not assume every setter has one. Where a control compares old and new effective values, unchanged values do not invoke that control callback. Callback failures are isolated by the library.

### Text and non-interactive elements

#### Section

`Tab:Section(textOrOptions) -> handle` accepts a string or `{Name=..., Title=..., Visible=...}`. Text is uppercased. `handle:Set(text)` replaces and uppercases the heading. The README's string example is accurate; the table form and visibility are otherwise easy to miss.

#### Divider

`Tab:Divider(nil|string|{Text=..., Name=..., Visible=...}) -> handle`. With a caption it renders centered text and two rules; without a caption it renders a line. `handle:Set(value)` exists only as a useful operation for a captioned divider (it still changes the line-less divider handle harmlessly, but there is no text node).

#### Label

`Tab:Label(string|{Text, Color, Update, UpdateRate, Visible, ...}) -> handle`.

- `Text` is rich text; `Color` accepts `Color3`, `#RRGGBB`, or a theme key.
- `Update()` is polled immediately in a spawned loop and then every `max(tonumber(UpdateRate), 0.05)` seconds (default 1); a successful non-`nil` return replaces the text. Errors warn and polling continues.
- `Set(text)`, `Get() -> string` (the rendered rich-text source), `SetColor(color)`, and, when `Update` was supplied, `SetUpdateRate(seconds)` are public.

#### Paragraph

`Tab:Paragraph({Title=...|Name=..., Content=..., Visible=...}) -> handle`; `Title` is normalized from `Name`. `Set(text)` replaces only the body; there is no public title setter.

#### Button

`Tab:Button(options) -> handle`, with `Title -> Name` and `Description -> Desc` aliases. `Name`, `Desc`, `Icon`, `Style="Primary"`, `Callback`, `Confirm`, `ConfirmTimeout`, and `HoldToConfirm` are consumed by the body. `SetText(text)` changes the label. Confirm-gated buttons additionally expose `Disarm()`; it cancels the armed state and restores the original label. A compact/touch layout changes appearance but not the handle contract.

#### Button row

`Tab:ButtonRow(entries) -> handle` (also `CreateButtonRow`). Each entry is `{Name, Callback, Style}`. The returned handle has `SetText(index, text)` and `.Buttons`; `.Buttons` contains the per-button GUI/button handles. This constructor is present in the native implementation even though it is not a standalone `Tab:` definition in the element list.

### Value controls

#### Toggle

`Tab:Toggle(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `CurrentValue`/`Value -> Default`. `Default` is true only for literal `true`. A true initial value invokes `Callback(true)` once during construction. `Set(value, silent?)` coerces with `value == true`, so truthy non-boolean values are **off**, not truthy; `Get() -> boolean`; `.Value` mirrors the state.

#### Slider

`Tab:Slider(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `CurrentValue`/`Value -> Default`, `Increment -> Step`; `Range={min,max}` also fills missing `Min`/`Max`. Defaults are `Min=0`, `Max=100`, `Step=1`. Values are numeric, clamped and snapped to the increment; the initial value is snapped too. `Set(value, silent?)`, `Get() -> number`, `.Value`, and `.Dragging` are public. `OnRelease(value)` runs once when pointer dragging ends (not for ordinary `Set`). Clicking the value chip opens an exact-number editor; nonnumeric typed input is ignored.

#### Stepper

`Tab:Stepper(options) -> handle` uses the same aliases and range/step defaults as Slider. `Set(value, silent?)` converts with `tonumber(value) or Min`, then snaps and clamps; `Get() -> number`; `.Value`. Holding +/- repeats after about 0.4 seconds. There is no `OnRelease` hook. The visible suffix is formatting only and is not included in the numeric value.

#### Progress

`Tab:Progress(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `CurrentValue`/`Value -> Default`. Value is clamped to `[0,1]` (including the initial value). `Color` controls fill; `TextColor` controls the formatted value text; both accept `Color3`, hex, or theme key. `Format(fraction) -> string` controls the right-hand label and supports rich text. `Set(value, silent?)`, `Get() -> number`, `.Value`, `SetColor(color)`, and `SetTextColor(color)` are public. Passing nil to `SetTextColor` returns it to the accent color. Theme changes re-render the formatted label.

#### Dropdown

`Tab:Dropdown(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `CurrentOption`/`Value -> Default`, `MultipleOptions -> Multi`, `Values -> Options`.

- Single mode stores one option (a table default is reduced to its first item); multi mode stores a list (a scalar default is wrapped in a one-item list). `Set(value, silent?)` accepts a scalar in either mode; multi mode wraps it, and nil clears. `Get() -> scalar|nil` in single mode, or a **new array** in multi mode.
- `Refresh(newOptions, keepSelection?, silent?)` replaces options. `keepSelection` defaults to false in this method; when true, selected values are retained. Callback runs only if the effective selection changed unless silent.
- `SetOptions(newOptions, settings)` is the newer alias for Refresh and **keeps selection by default**. `settings` may be a boolean or `{KeepSelection=bool|keepSelection=bool, Silent=bool|silent=bool}`. `GetOptions() -> new array copy`.
- `SetOpen(bool)` opens/closes the popup. `.Open` reflects it. `Options`, `Searchable` (default true unless explicitly false), `SearchAfter`, `SearchPlaceholder`, `MaxRows`, `PopupWidth`, `AllowNone`, `NoneText`, and `EmptyText` affect the popup. Multi mode has Select all/Clear all actions. Unknown selected values are retained for config saving and can become effective when options are refreshed; this is why `Set`/`Get` and `Refresh` can differ from the currently visible rows.

#### Input

`Tab:Input(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `PlaceholderText -> Placeholder`, `CurrentValue`/`Value -> Default`. `Set(value, silent?)` sets text and invokes the callback immediately unless silent (unlike typing, which commits on focus loss); `Get() -> string` in normal mode. With `Numeric=true`, text is parsed as a number including commas, spaces, `$`, `_`, `kg`, `/s`, and suffixes `k/m/b/t/qa/qi`; `Get() -> number|nil`, invalid typed/set text reverts to the last valid text, and the callback receives `(number, enterPressedOrFalse)`. Normal mode callback receives `(text, enterPressedOrFalse)`. Numeric config saving preserves the original text spelling through the internal save path.

#### Keybind

`Tab:Keybind(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `CurrentKeybind`/`Value -> Default`. A string default is converted with `Enum.KeyCode[string]`; `.Value` is the selected `Enum.KeyCode|nil`, `.Listening` is public state, `Set(keyCode, silent?)` changes it and calls `OnChanged(keyCode)` unless silent, and `Get() -> Enum.KeyCode|nil`. Clicking enters listening; Escape cancels. Outside listening, the main `Callback(keyCode)` runs only for an unprocessed matching key. Hiding the element cancels listening.

#### Color picker

`Tab:ColorPicker(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `Color`/`CurrentValue`/`Value -> Default`. Default is a `Color3` (the implementation passes it to `Color3.toHSV`; invalid types are not normalized). `Set(color, silent?)` requires a Color3, updates the picker, and calls `Callback(Color3)` unless silent; `Get() -> Color3`; `.Value`; `SetOpen(bool)` and `.Open` expose the expanded panel. Hex input accepts optional `#` and exactly six hex digits; invalid input restores the current uppercase `#RRGGBB`. RGB/HSV edits call the callback continuously while dragging.

#### Order list

`Tab:OrderList(options) -> handle`; aliases: `Title -> Name`, `Description -> Desc`, `Options`/`Values -> Items`. `MaxRows` defaults to 6 and is clamped to at least 1; `Numbered` and `Arrows` default true; `EmptyText` defaults to `"Nothing to order"`. Items are copied into draggable rows. `Set(list, silent?)` reorders existing items and remembers unknown values for a later `Refresh`; `Get() -> new array`; `Refresh(items, keepOrder?, silent?)` replaces the item set, preserving current order by default and appending new items. Drag completion and arrow nudges call `Callback(currentArray)`; `Set`/`Refresh` also call it unless silent. Duplicate values are supported, but order preservation is value-based.

### Appearance wrapper attached by `CreateKawiXDWindow`

These methods are **not** attached by plain `Library:CreateWindow`; they are installed by `Library:CreateKawiXDWindow(options)` (alias `CreateNullFireWindow`). The wrapper's `CreateAppearanceTab(options)` is also attached to the returned window; `Library:CreateAppearanceTab(window, options)` is the equivalent library-level form and asserts that the window is an appearance-enabled KawiXD window.

- `Window:GetBackgroundStyle() -> detached table` returns `Source`, `Transparency`, `Tint` (uppercase hex), `ScaleType`, `TileSize={X,Y}`, and `Dim`. Native nonpositive tile offsets are reported as the useful default `{256,256}`.
- `Window:SetBackgroundStyle(style) -> true | false, error` validates before changing anything; success returns only `true` (not a style table). `Source=false` means `"None"`; numeric image IDs must be nonnegative integers; `Transparency`/`Dim` are `[0,1]`; `Tint` is Color3 or `#RRGGBB`; `ScaleType` is exactly `Crop|Fit|Tile|Stretch`; tile dimensions are `1..4096`. An unresolved/invalid native source returns `false,error` and leaves the previous background intact. `GetBackgroundStyle` returns a normalized detached table.
- `Window:GetAppearance() -> detached JSON-safe table` returns `{Version=1, Theme, Background, UIScale, AdaptiveSize, Density, CornerRadius}`. Theme colors are hex strings. It is not a control/config snapshot.
- `Window:ExportAppearance() -> jsonString | nil,error` JSON-encodes the snapshot; it does not write a file.
- `Window:ApplyAppearance(tableOrJSONString) -> true | false,error` accepts JSON up to 131072 bytes or a table. It validates version (only 1), theme colors, background, UIScale `0.6..1.5`, boolean AdaptiveSize, known Density, and CornerRadius `0..20` before applying. It can recolor sibling windows because theme/density/radius are library-shared. `Version` is optional for partial profiles; when present it must be `1`. A destroyed window returns `false,"Window is destroyed"`.

### Verified native aliases and correction summary

The important source-level corrections are: `Increment` is normalized to `Step`; `Range` fills `Min`/`Max`; `CurrentOption`/`MultipleOptions`/`Values` are dropdown aliases; `Input` and `Keybind` return parsed numeric/Enum values rather than always strings; dropdown `SetOptions` keeps selection by default while `Refresh` does not; dropdown save state retains currently unavailable selections; ColorPicker exposes `SetOpen`/`.Open`; Progress exposes both color setters; OrderList preserves unknown remembered order; and all handles inherit dependency, disabled, tooltip, visibility, and idempotent destruction behavior.

### Additional native elements present later in Source.lua

#### Status and Statuses

`Tab:Status(options) -> handle` also has `CreateStatus` and `AddStatus` aliases. Normalization includes `Title->Name`, `Text/Content/CurrentValue/Default->Value`. Public options include `Name`, `Value`, `Style` (`Plain`, `Row`, `Badge`, `Dot`, `Bar`, `Stat`), `Tone`, `Color`/`ValueColor`, `Max`, `Prefix`, `Suffix`, `Placeholder`, `Update`, `UpdateRate`, `Wrap`, `Pin`, `Pulse`, and `Flash`. The handle supports `Set(value, max?)`, `Get()`, `SetTone(tone)`, `SetName(name)`, `SetColor(color)`, `SetUpdateRate(seconds)`, and `SetWrap(bool)`; update callbacks can return `(value, maxOrTone)`. `Tab:Statuses(entries, shared?)` / `CreateStatuses` returns handles keyed by entry name; entries may be names or option tables and shared options fill missing fields.

#### StatusList

`Tab:StatusList(options) -> handle` has `CreateStatusList` and `AddStatusList` aliases. `Title->Name` is normalized. `Rows` accepts strings or `{Text, Value, Tone|Color}` rows; `MaxRows`, `EmptyText`, `Update`, `UpdateRate`, and `Visible` are consumed. The returned handle has `Set(rows)`, `Get()` (copy), `Clear()`, `SetName(text)`, `SetUpdateRate(seconds)`, plus shared handle methods. `Update` returning nil leaves rows unchanged. Rows are reused and only update while the list is shown.

#### Image

`Tab:Image(options) -> handle` (aliases `CreateImage`, `AddImage`). Media-card options are `Name`/`Title`, `Desc`/`Description`, `Caption`, `Image`, `ScaleType` (`Crop` default, or any valid `Enum.ScaleType` name), `Color` (initial image tint), and shared options such as `Visible`, `Flag`, `Tooltip`, and dependencies. `Image` may be a numeric asset id, `avatar`/`headshot` (local player's thumbnail), a preset/URL/file accepted by the window image resolver, `"None"`, `""`, or nil.

- `SetImage(source) -> true | false, error`: nil/empty/`"None"` hides the image and returns true; numeric ids become `rbxassetid://<floor(id)>`. A superseding call returns `false, "replaced by a newer image"`; resolution failure returns `false,error`. `Set` is the exact alias (`handle.Set = handle.SetImage`).
- `Get() -> original source|nil` returns the last source argument, not the resolved URI. `SetCaption(text)` stringifies non-nil text (nil becomes empty) and hides the caption when empty. `SetScaleType(name)` applies a valid enum name and retains the current scale for an invalid name. `SetColor(color)` uses a Color3 or resets to white. `SetTitle(text)` stringifies text and updates the title when present.

#### Table

`Tab:Table(options) -> handle` (aliases `CreateTable`, `AddTable`, `CreateLeaderboard`); aliases `Title->Name`, `Description->Desc`, `Data->Rows`, `OnRowClick->Callback`. Options include `Name`, `Desc`, `Columns`, `Rows`, `Rank`, `RowHeight`, `MaxRows` (minimum 1; default 8), `Search` (default true), `SearchPlaceholder`, `EmptyText`, `Sortable` (default true), `Editable`, `AllowAdd`/`AllowRemove` (default true when editable), `AddText`, `NewRow`, `SortBy`, and `SortDescending` (default true when `SortBy` is supplied). A column may specify `Name`/`Title`, `Key`, `Width` (pixels >1, share 0..1), `Align`, `Format(value,row)`, `Color`, `Sortable`, and editable `Type`, `Options`, `Min`, `Max`, `Integer`, `Default`, `Placeholder`, `Searchable`, `SearchAfter`, `SearchPlaceholder`, `MaxRows`. A column with `Type` makes the table editable.

Public methods: `SetColumns(columns) -> nil`; `SetRows(rows, silent?) -> nil` (scalar rows become `{scalar}`; editable rows are cloned; `OnChanged(handle.Rows)` runs only when editable and not silent); `Set` is its exact alias; `GetRows() -> handle.Rows` and `Get` are exact aliases returning the live rows table; `AddRow(row, position?) -> new row count`; `UpdateRow(index,row) -> true|false`; `RemoveRow(index) -> true|false`; `Clear() -> nil`; `Sort(columnKeyOrIndex?, descending?) -> nil` (nil key restores supplied order); `SetTitle(text) -> nil`; `SetMaxRows(count) -> nil` (minimum 1); `NewRow() -> row table`; and `SetSearch(text) -> nil`. Row clicks call `Callback(row,index)` when tappable. Cell edits and add/remove operations call `OnChanged(handle.Rows)` only in editable mode.

#### Log

`Tab:Log(options) -> handle` (aliases `CreateLog`, `AddLog`, `Feed`, `CreateFeed`); aliases `Title->Name`, `Description->Desc`, `Max->MaxEntries`, `Limit->MaxEntries`. Options include `MaxEntries` (minimum 1; default 100), `MaxRows`/`Lines` (minimum 1; default 6 visible lines), `Timestamps` (default true), `TimeFormat` (default `%H:%M:%S`), `EmptyText`, and shared options. `Push(text,color?) -> entry` appends `{Text=string, Color=color, Time=os.time()}` and returns that entry; color may be Color3, `#rrggbb`, or a theme key. Old entries are pruned from the front to `MaxEntries`; `Add` and `Log` are exact aliases. `Clear() -> nil` removes all entries; `Get() -> new array` returns oldest-first detached `{Text,Color,Time}` tables; `SetTitle(text) -> nil`; `SetMaxEntries(count) -> nil` clamps to at least 1 and prunes immediately.

### Config and theme manager handles

`Tab:ConfigManager(options) -> manager` (alias `CreateConfigManager`) returns a manager table, not an element handle. Options are `Name`/`Title`, `Icon`, `Side`, `Rows`, and `Placeholder`. Methods: `Refresh() -> nil`; `Create(name) -> nil`; `Save(name?) -> nil`; `Load(name?) -> nil`; `Delete(name?) -> nil` (confirmation-gated); `Rename(name?, newName) -> nil`; `Reset() -> nil` (confirmation-gated); `SetAutoload(name?) -> nil`; `ClearAutoload() -> nil`; `ToggleAutoload(name?) -> nil`; `SetAutoloadMode(mode) -> nil` (`Account` or global); `Export(name?) -> code|string?` (code on success, otherwise nil); and `Import(code) -> nil`. Name-less operations use the selected item. Mutating methods notify and do not expose the underlying window boolean/error pair.

`Tab:ThemeManager(options) -> manager` (alias `CreateThemeManager`) returns a manager table. Options include `Name`/`Title`, `Icon`, `Side`, `Menu`, `MenuName`, `MenuIcon`, `MenuSide`, `Weather`, `Dim`, `Transparent`, `DragSkeleton`/`DragStyle`, `IslandStyle`, `AdaptiveSize`, `Scale`, `Density`, `CornerRadius`, `Background`, `Customize`, `Colors`, `Flag`, and `Placeholder`. Methods: `Refresh() -> nil`; `Create(name) -> nil`; `Save(name?) -> nil`; `Load(name?) -> nil`; `Delete(name?) -> nil` (confirmation-gated); and `ToggleDefault(name?) -> nil`.

When `Flag ~= false` (default), ThemeManager registers `Library.Flags[flag]` where `flag` is the supplied string or `"__Theme"`. This hidden config handle has `Get() -> map` and `Set(value) -> nil`. `Get` returns `{Name, Colors, Weather, WeatherMode, Dim, Transparent, DragStyle, IslandStyle, CornerRadius, UIScale, AdaptiveSize, Density, Background, BackgroundTransparency}`; disabled sections are nil, `Colors` maps theme keys to hex strings, and false booleans remain false. `Set` ignores non-tables, applies supplied `Colors` and recognized look fields, and leaves omitted fields unchanged.

### Library-level transient UI utilities

`Library:Notify(opts)`, `Library:Confirm(opts)`, and `Library:Dialog(opts)` forward to the newest window and return that window method's result (or nil when there is no window). These are not tab elements and are documented here only to record the verified public utility signatures; their window-owned implementations return the transient notification/dialog handles where applicable.

</details>

## Executor compatibility

This library targets a Roblox client executor, as in the original Airflow documentation. Basic loading needs `loadstring` and `game:HttpGet`; persistent configs need file APIs such as `readfile` and `writefile`. Clipboard buttons use `setclipboard` when available. URL/file image backgrounds additionally need the supported request, file, and custom-asset APIs. The built-in unsupported-executor warning can offer **Continue anyway**; that is not a guarantee that every feature will work.

Themes, density, and corner radius are shared by windows from one library instance; backgrounds are per-window. Adaptive sizing fits the viewport and is not physical display-DPI detection. This documentation correction does not claim a fresh runtime test or universal executor compatibility.

## Credits and scope

README visuals use the official [Lucide icon set](https://github.com/lucide-icons/lucide), distributed through [Iconify](https://iconify.design/) under Lucide’s [ISC license](https://github.com/lucide-icons/lucide/blob/main/LICENSE). The animated headline uses [Readme Typing SVG](https://github.com/DenverCoder1/readme-typing-svg). These are externally hosted image embeds, not JavaScript or CSS animation inside the README, and add no repository files. Image blocking or host downtime may hide the decoration; all setup instructions and API text remain readable. The headline is decorative, not a runtime recording of the library.

KawiXD builds on **[Airflow UI by PookiePepelsss](https://github.com/PookiePepelsss/Airflow-UI)**, using the selected base from **[joustingmatch/-3](https://github.com/joustingmatch/-3)** at revision `2cf70e5`. The native layout and behavior are retained; the core changes are branding, with appearance features provided by the extension. Attribution is retained here; the full native library is included in `Source.lua`.

All four files in this repository are distributed under the MIT license below. Native image assets, icons, and custom fonts may fetch upstream resources when used; externally hosted resources are not bundled in these four files and may have their own terms.

## License

The MIT license applies to `Source.lua`, `llms.txt`, `Readme.MD`, and `Example.lua`.

```text
MIT License

Copyright (c) 2026 voidhub9-dotcom

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
