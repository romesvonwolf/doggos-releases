# DoggOS — the phone OS built for an AI agent

DoggOS turns an Android phone into a machine an AI agent can actually run. An always-listening
assistant ("Hey Doggo") holds a real-time voice conversation, operates the whole phone (open apps,
read the screen, tap, type, toggle settings, read notifications), and hands multi-step work to a
coding agent (Claude Code, OpenAI Codex or Cursor) living in a Linux computer *inside* the phone,
where it can build, install and test brand-new Android apps on the fly.

This repository is the complete DoggOS layer: the Core app, the companion apps (Doggo Agent, Omni
Scheduler, Doggo Panel, Wingman), the agent daemon and CLI that run in the on-device Linux VM, the
app-forge build loop, the skills library, the phone setup scripts and the branding.

**Open source, MIT licensed. Source only — there is no installer and no ready-made image yet.**

## Read this before you start

- **Advanced users only.** This is an operating-system replacement, not an app. You will unlock the
  bootloader, flash LineageOS and run root `adb` commands. If any of that is unfamiliar, stop here.
- **It wipes the phone.** Unlocking the bootloader performs a full factory reset. Back up first.
  Everything on the device is erased, and the warranty is almost certainly void afterwards.
- **One supported device today: Google Pixel 6a (`bluejay`).** Other Pixel 6 or newer devices should
  work if their official LineageOS 23 build enables the Android Virtualization Framework "Linux
  terminal"; nothing else is tested.
- **Bring your own accounts.** Voice uses an xAI (Grok) key; the coding agent uses your own Claude
  Code, Codex or Cursor subscription. No credentials are included.
- **No support promises.** Things change weekly. Expect to read the scripts you are about to run.

## Recommended way to install: let a coding agent drive it

The install is ~45 minutes of hands-on steps plus downloads and builds, most of it typed `adb`,
`fastboot` and PowerShell commands against a plugged-in phone. The fastest and least error-prone
route is to let a coding agent do the typing while you watch the phone:

1. Install Android platform-tools (`adb`, `fastboot`) and **scrcpy** on your PC. scrcpy mirrors the
   phone screen to the PC over USB so you — and the agent, through screenshots — can see what the
   phone is doing. `tools/mirror.ps1` wraps it.
2. Clone or unzip this repository and open it in Claude Code, Codex or Cursor.
3. Tell the agent: *"Read DISTRIBUTION.md and install DoggOS on the phone plugged in over USB. Stop
   and ask me before anything that wipes data or needs a confirmation on the phone screen."*
4. Confirm the bootloader unlock and the recovery-menu steps on the phone yourself when the agent
   reaches them. Everything else — flashing, sideloading, the VM provisioning, building Core and the
   apps, pairing — it can do from `DISTRIBUTION.md`.

Doing it by hand works too; `DISTRIBUTION.md` is the step-by-step reference in either case.

## What is in here

| Path | What |
|---|---|
| `android/core` | DoggOS Core (`com.doggos.core`): wake word, voice director, phone "hands", settings, Core API |
| `android/apps` | Doggo Agent, Omni Scheduler, Doggo Panel, Wingman — WebView apps over the shared shell |
| `vm/agentd`, `vm/cli` | The agent daemon and `doggos` CLI that run in the on-device Debian VM |
| `vm/appforge` | Build → install → launch → screenshot loop for apps the agent writes |
| `vm/skills` | SKILL.md playbooks the coding agent reads |
| `vm/provision.sh`, `device/phone` | VM provisioning and phone-side setup scripts |
| `tools` | PC-side build and deploy scripts (PowerShell) |
| `branding` | Boot animation and wallpaper generators |
| `DISTRIBUTION.md` | The full install procedure (Stage A), and the plan for a real ROM (Stage B) |

## Status

Stage A: the DoggOS layer applied over an official LineageOS 23 build with root `adb`. Stage B — a
signed LineageOS fork with everything baked in and an installer — is planned, not built.

Product page and donations: https://binarymonster.com/software/doggos
