# ICS for Visual Studio: user guide

The Marketplace overview is a quick introduction. This guide covers editor behavior, settings, commands, recovery files, and current language-service limits.

## Installation and first use

ICS supports Visual Studio 2022 17.x and Visual Studio 2026 18.x on x64 Windows, with .NET Framework 4.8. The VSIX includes a self-contained Windows x64 converter; no separate .NET runtime installation is required.

Choose **Download** on the [Visual Studio Marketplace page](https://marketplace.visualstudio.com/items?itemName=lucid-programming.icsvisualstudio), close Visual Studio, run the downloaded VSIX, and reopen Visual Studio.

Open a `.cs` file and choose **Tools → ICS: Open C# as ICS**. A writable ICS view opens beside the C# source. To toggle the view, press **Ctrl+K**, release both keys, then press **Ctrl+I**. These are the Visual Studio bindings; VS Code uses a different second keystroke.

The control panel is available through **View → Other Windows → ICS** or **ICS: Open Control Panel**. Settings are under **Tools → Options → ICS → General**.

## Preview edits, saves, and recovery

Both panes can be edited. After a short pause, a successful C# edit refreshes ICS, or a successful ICS edit updates the paired C# buffer. Live in-memory synchronization is free. **ICS: Apply Preview to C#** validates and updates the C# buffer without saving it.

Automatic buffer updates do not by themselves save the C# file to disk. Save to persist your work; Pro's optional **Auto-save paired C#** can also save each successful live update. Incomplete input keeps the passive pane at its last verified version and marks it out of date. Synchronization resumes when conversion succeeds.

If both panes change independently, neither silently overwrites the other. **ICS: Resolve Preview Conflict** lets you choose which side to keep while retaining a local backup. **ICS: Refresh ICS Preview** refreshes a clean projection; **ICS: Revert Preview from C#** explicitly discards preview edits after confirmation.

Dirty projections can be retained as local recovery drafts. Recovery data contains plaintext source code and is stored under `%LOCALAPPDATA%\Lucid\ICS\VisualStudio\Recovery`, not beside project files. It is not uploaded automatically.

Conflict backups are pruned when the recovery store is used: the retention policy is 30 days, the newest 20 complete C#/ICS pairs, and normally 100 MB. The newest pair is kept even if it alone exceeds that size. This policy applies to conflict history, not every recovery draft. Unrestorable drafts are removed when detected.

Use **ICS: Open Preview Recovery Folder** to inspect recovery files. **ICS: Clear Preview Recovery Data** deletes drafts and conflict backups after confirmation; recover anything you need before clearing them. See the [Visual Studio privacy notice](../privacy/visual-studio.md).

## Other workflows

With Pro, **Display ICS only** redirects an activated C# editor to its writable ICS projection. Validated saves still write ordinary `.cs` files. **ICS: Toggle ICS View** switches the active file's view.

For standalone `.ics` files, **ICS: Sync Current File to C#** writes a paired `.cs` file. Pro's **Sync standalone ICS files on save** does this automatically when a standalone ICS file is saved. **Protect user C# files** asks before overwriting a C# file that lacks the configured generated-file marker.

Solution commands can generate C# from standalone ICS, validate standalone ICS, or export C# as ICS. **ICS: Export as ICS File** performs a one-time export without creating a live-linked preview.

## Language services and diagnostics

ICS editors provide syntax colorization, comment toggling, bracket matching, autoclosing, and region folding. The language client provides live diagnostics, hover, completion, Go To Definition, Find All References, and native **Format Document** support. Diagnostics appear in the editor and Error List.

Analysis runs locally on generated C#. The current language service does not load the containing project's full source and references, so types declared in other files or external assemblies may be unresolved. Results requiring full project context can be incomplete, and semantic diagnostics may include false positives.

**Enable diagnostics** defaults to `True`. Turning it off suppresses ICS diagnostics, including useful parse errors. **ICS: Show Conversion Diagnostics** remains available for explicit conversion checks.

## Settings reference

Open **Tools → Options → ICS → General**. Free live pairing works without configuration.

| Setting | Default | Effect |
| --- | --- | --- |
| Sync standalone ICS files on save | False | Pro: convert a saved standalone `.ics` file to paired C#. |
| Display ICS only | False | Pro: show ICS projections in place of raw C# editors. |
| Auto-save paired C# | False | Pro: save each successful live update; buffer synchronization is free. |
| Protect user C# files | True | Ask before overwriting C# without the generated-file marker. |
| Generated-file marker | `<auto-generated` | Marker used by that overwrite protection. |
| Remove braces | False | Remove eligible optional braces from regenerated C#; see below. |
| Remove if-condition parentheses | False | Omit eligible `if`-condition parentheses in ICS. |
| Match source line numbers | False | Enable line-number matching during conversion. |
| Spaces per tab | 0 | Logical tab width; 0 reads `tab_width` from the nearest `.editorconfig`. ICS output uses spaces. |
| Enable diagnostics | True | Show parser and generated-C# diagnostics. |

**Converter command** and **Converter arguments** are diagnostic/development overrides; leave them unchanged for the bundled converter. Changing conversion options refreshes open projections.

## Optional braces in regenerated C#

Structural C# braces disappear in the ICS view without enabling **Remove braces**. Turning it on changes the C# you get back: when you edit a preview, the statement or member you change is regenerated without eligible optional braces, such as those around a single-statement `if`. Braces needed to preserve valid C# and its meaning remain. C# outside the changed statement or member is returned exactly. The option is off by default.

An untouched ICS preview returns the original C# exactly. Enabling the option does not rewrite every C# file in a solution.

## Complete command reference

Commands are available under **Tools**; the control panel also exposes common actions.

| Command | Purpose |
| --- | --- |
| ICS: Open C# as ICS | Open a live, writable projection. |
| ICS: Toggle ICS View | Switch between C# and its ICS view. |
| ICS: Apply Preview to C# | Validate and update the paired C# buffer. |
| ICS: Resolve Preview Conflict | Review competing edits and choose which side to keep. |
| ICS: Refresh ICS Preview | Refresh a clean projection from C#. |
| ICS: Revert Preview from C# | Discard preview edits after confirmation. |
| ICS: Show Paired C# File | Open the source paired with the active projection. |
| ICS: Show Conversion Diagnostics | Publish conversion diagnostics to the Error List. |
| ICS: Copy Generated C# | Copy converted C# without modifying a file. |
| ICS: Format ICS Document | Format the current ICS buffer. |
| ICS: Sync Current File to C# | Convert a standalone ICS file to C#. |
| ICS: Generate C# for Solution ICS Files | Convert solution standalone ICS files to C#. |
| ICS: Validate Solution ICS Files | Validate solution standalone ICS files. |
| ICS: Convert Solution C# Files to ICS | Export solution C# files as standalone ICS. |
| ICS: Export as ICS File | Export one file without creating a live-linked preview. |
| ICS: Restart Converter | Restart the converter and restore open projection sessions. |
| ICS: Open Preview Recovery Folder | Inspect local drafts and conflict backups. |
| ICS: Clear Preview Recovery Data | Delete drafts and conflict backups after confirmation. |
| ICS: Open Control Panel | Open settings, preview actions, and licensing controls. |
| ICS: Report Issue | Prepare a local report for review before sharing. |
| ICS: Enter License Key | Activate ICS Pro. |
| ICS: Refresh License | Refresh the cached licence status. |
| ICS: Deactivate License | Release an activation before moving it. |
| ICS: Upgrade to Pro | Open the purchase page. |

Default shortcuts:

- **Ctrl+K**, then **Ctrl+I** — Toggle ICS View.
- **Ctrl+Alt+S** — Apply Preview to C#.
- **Ctrl+Alt+R** — Refresh ICS Preview.

Visual Studio's native **Format Document** command also formats ICS. Custom keyboard mappings or other extensions may override defaults.

## Licensing and privacy

Live in-memory pairing is free. Display-only mode, auto-save of paired C#, and standalone sync-on-save require Pro. See the [current pricing](https://lucid-programming.com/#pricing), [product terms](../TERMS.md), and [activation transfer policy](../LICENSE-TRANSFERS.md).

The extension can validate a saved licence automatically during initialization or a Pro-access check when no valid cached result is available. Activation, validation, and user-requested deactivation contact Lemon Squeezy; source code and project information are not included. A valid cached licence can cover temporary network failures for up to 30 days, but not beyond licence expiration. Explicitly invalid, disabled, or expired licences do not receive an offline window.

## Troubleshooting and reporting bugs

- **Preview out of date:** complete the syntax on the edited side. The other side retains its last verified text until conversion succeeds.
- **Conflicting edits:** use **ICS: Resolve Preview Conflict** rather than replacing one pane blindly.
- **Language service or converter stopped responding:** try **ICS: Restart Converter** and inspect **ICS: Show Conversion Diagnostics**.
- **Unresolved types in valid project code:** see the language-service limitations above; project-wide binding is not currently available.
- **Control panel does not open:** the current preview can report a missing parameterless constructor. Use **Tools → Options → ICS → General** for settings and the individual **Tools → ICS** commands instead.
- **Live update stalls after inserting a line:** check indentation. Mixed tabs and spaces can be interpreted at different widths; use spaces consistently in the ICS preview. The last good C# is retained if conversion fails.

Run **ICS: Report Issue** to prepare a scrubbed local report. Review it before copying anything to the [public tracker](https://github.com/Administrator-Lucid-Programming/ics-support/issues). Do not submit proprietary code, licence keys, paths, customer information, or other sensitive data.
