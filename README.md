# Hidesk Studio

Installers for Hidesk Studio, a desktop app for [oh-my-pi](https://github.com/can1357/oh-my-pi) (omp).

**[Download the latest version →](https://github.com/harrykangyiwei1999/hidesk-studio-releases/releases/latest)**

| Windows (x64) | macOS (Apple silicon) |
| --- | --- |
| `hidesk-studio-<version>-setup.exe` | `hidesk-studio-<version>-arm64.dmg` |

## First launch

The app isn't signed by a paid developer account, so the system warns once:

- **Windows:** "Windows protected your PC" → **More info** → **Run anyway**.
- **macOS:** right-click the app → **Open**, or System Settings → Privacy & Security → **Open Anyway**.

On first run the app downloads the official omp. Sign in to your own model provider in Settings.

## What is omp?

[omp (oh-my-pi)](https://github.com/can1357/oh-my-pi) is an open-source coding agent. Hidesk Studio is a desktop window for it: every task you start runs in omp, so the app needs a copy of omp before it can do anything.

- **Where it comes from:** `build.stencil.so` is omp's own build service. The `omp update` command in omp's source code downloads from the same place.
- **Verification:** the build service lists each file's size and SHA-256. Hidesk Studio checks both after downloading and deletes the file if either doesn't match. The macOS binary is code-signed by the omp developers (Team ID `VTLHGQC72S`); check it with `codesign -dv`.
- **Version:** the version in the setup dialog is just the latest release. Any omp from 18.12.0 on works.
- **An omp you installed yourself** (Homebrew, bun, npm, the install script): if it's on your `PATH`, Hidesk Studio finds it and asks whether to keep using it or download its own copy. Choose to keep yours and the app never changes it.
- **Where it goes:**
  - macOS: `~/Library/Application Support/HiDesk-studio/omp/`
  - Windows: `%LOCALAPPDATA%\HiDesk-studio\omp\`, with its `bin` folder added to the front of your user `PATH` so terminals use the same omp
- **Updates:** Hidesk Studio checks the build service in the background and swaps in new versions of its own copy; tasks already running keep the old one. An omp you installed yourself, or one managed by another app, is never updated automatically.
- **Uninstall:** quit Hidesk Studio and delete the folder above. On Windows, also remove `...\HiDesk-studio\omp\bin` from your user `PATH`.
- **Keys and data:** sign-ins and API keys are stored by omp in `~/.omp/agent/`, the same place the omp terminal app uses. Your prompts and code go to the model providers you sign in to. Hidesk Studio itself also contacts `build.stencil.so` (omp downloads and update checks), GitHub (app update checks), and any service you connect yourself in Settings.

## macOS folder prompts

When it starts, Hidesk Studio runs your login shell once to pick up your `PATH`, so it can find `git` and an omp you installed yourself. If your shell setup (`~/.zshrc` etc.) touches Documents, Desktop or Downloads, macOS asks whether Hidesk Studio may access that folder. Opening a project stored there asks too. Hidesk Studio doesn't read these folders on its own; allowing or denying only affects what your shell setup and your projects can reach.

## Updates

- **Windows:** automatic. A new version downloads in the background; click the label next to Settings to restart into it.
- **macOS:** download the new `.dmg` from the link above and replace the old app. Settings and history are kept.
