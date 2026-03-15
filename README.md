<p align="center">
    <h1 align="center">Process Priority Manager</h1>
    <h5 align="center">A Windows utility that automatically adjusts process priorities based on the currently prioritized application.</h5>
    <p align="center">
        <a href="https://www.patreon.com/cw/SenpaiGabriel">Support on Patreon</a>
    </p>
</p>

          ░██████                ░████████                   ░██ 
        ░██   ░██               ░██                         ░██  
       ░██        ░██████      ░██    ░██████   ░███████ ░██████ 
      ░██ ░████ ░██   ░██     ░█████      ░██ ░██         ░██    
     ░██   ░██ ░██   ░██     ░██    ░███████  ░██████    ░██     
    ░██   ░██ ░██   ░██     ░██   ░██   ░██       ░██   ░██ ░██  
    ░██████   ░██████      ░██    ░███████ ░███████     ░████   

## System requirements

Windows 10 or Windows 11.

## Shipped files

A packaged release should contain:

- `process_priority_manager.exe`
- `LICENSE`

Do not separate `process_priority_manager.exe` from `LICENSE`. The executable checks for the license file during setup.

## Installation

1. Keep `process_priority_manager.exe` and `LICENSE` in the same folder.
2. Run `process_priority_manager.exe`.
3. On first launch, the program will:
   - prompt you to accept the license terms
   - create the `resources` folder if needed
   - create or update `resources\settings.json`
   - offer to create a desktop shortcut if one does not already exist

If setup completes successfully, you can continue launching the program from the executable directly or from the created shortcut.

## Usage

Behavior:

- No arguments: runs setup when `resources\settings.json` is missing, otherwise starts the prioritizer.

The executable supports these modes:

- `--install`: runs setup explicitly.
- `--run`: starts the prioritizer directly.

## Settings

The application stores its runtime configuration in:

```text
resources\settings.json
```

The executable always uses its own folder as the application root. That means the `resources` directory is created next to the executable you run.

Default settings:

```json
{
  "window": "focused",
  "ignore_files": [],
  "target_files": [],
  "background_files": [],
  "build_file_process_trees": false,
  "target_priority": "High",
  "background_priority": "Low",
  "poll_interval_sec": 1.0,
  "refresh_process_tree_sec": 1.0,
  "errors_until_skip": 1,
  "verbosity": 2,
  "debug_mode": false,
  "i_agree_to_all_license_terms_of": "none"
}
```

### Setting reference

`window`

- Selects how the program decides which process should be treated as the active target.
- Valid values: `focused`, `visible`, `unminimized`, `cpu`
- Default: `focused`

`ignore_files`

- A list of executable paths that should be ignored by the manager.
- Default: `[]`

`target_files`

- A list of executable paths that should always be treated as target processes.
- Default: `[]`

`background_files`

- A list of executable paths that should always be treated as background processes.
- Default: `[]`

`build_file_process_trees`

- Controls how `target_files` interact with process trees.
- Default: `false`

`target_priority`

- Priority class applied to the focused or targeted process group.
- Default: `High`
- Valid values: `Low`, `Below Normal`, `Normal`, `Above Normal`, `High`, `Realtime`

`background_priority`

- Priority class applied to tracked background processes.
- Default: `Low`
- Valid values: `Low`, `Below Normal`, `Normal`, `Above Normal`, `High`, `Realtime`

`poll_interval_sec`

- Delay between each monitoring loop.
- Default: `1.0`

`refresh_process_tree_sec`

- How often the internal process-tree snapshot may be rebuilt.
- Default: `1.0`

`errors_until_skip`

- Number of repeated process access errors allowed before a process is skipped during refresh.
- Default: `1`

`verbosity`

- Controls how much status output is printed to the console.
- Default: `2`

`debug_mode`

- Enables extra debug logging about focus resolution, process grouping, and process-tree behavior.
- Default: `false`

`i_agree_to_all_license_terms_of`

- Stores the accepted license identifier.
- Current accepted value: `LicenseRef-Esotericks-NC-1.0`
- Default before acceptance: `none`

## Notes

- The program is intended for Windows only.
- The executable contains its application icon, so the shortcut uses the embedded icon from the `.exe`.
- The application may pause and keep the console open after certain startup failures so error output remains visible.

## License

This software is distributed with a required license file:

- `LICENSE`

Running or installing the program requires acknowledging all LICENSE terms.
