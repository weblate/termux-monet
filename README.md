<p align="center">
<img src="https://user-images.githubusercontent.com/103902727/177491288-019d0ea4-69b6-4eac-8040-80227623e2d7.png">
</p>

<div align="center">
    <img src="https://github.com/DevMoxxie/termux-monet/workflows/Build/badge.svg"
      alt="Build_status" />
    <img src="https://github.com/DevMoxxie/termux-monet/workflows/Unit%20tests/badge.svg"
      alt="Testing_status" />
</div>

<div align="center">
    <img src="https://img.shields.io/static/v1?label=Android&message=12%2B&color=brightgreen&style=flat&logo=android"
      alt="Android_Version" />
    <img src="https://img.shields.io/badge/Updated-July 06, 2022-informational.svg?longCache=true&style=flat"
      alt="_time_stamp_" />
    <img src="https://img.shields.io/discord/641256914684084234.svg?label=&logo=discord&logoColor=ffffff&color=5865F2&link=https://discord.gg/HXpF69X"
      alt="_time_stamp_" />
</div>


<p align="center">
<img src="https://user-images.githubusercontent.com/103902727/177439838-40eceea5-90d7-4854-b1e4-8ce891326b0c.png" width=50% height=50%>
</p>

***
## ONLY `ANDROID 12+` IS SUPPORTED!
***

[Termux-Monet](https://github.com/DevMoxxie/termux-monet) is a modified fork of [Termux](https://github.com/termux/termux-app), an Android terminal application and Linux environment, with Monet Theming Implementations.

***
## Contents
- [Phantom Process Killer](#PhantomProcessKiller)
- [Nightly Releases](#Nightly)
- [Wikis](#Wikis)
- [Miscellaneous](#Miscellaneous)
- [Debugging](#Debugging)
- [Forking Instructions](#Forking)
***

## PhantomProcessKiller

**NOTICE:**
> **Termux is broken on Android 12+.** Android OS will kill any (phantom) processes greater than 32 (limit is for all apps combined) and also kill any processes using excessive CPU. You may get `[Process completed (signal 9) - press Enter]` message in the terminal without actually exiting the shell process yourself. Check the related issue [#2366](https://github.com/termux/termux-app/issues/2366), [issue tracker](https://issuetracker.google.com/u/1/issues/205156966), [gist with details](https://gist.github.com/agnostic-apollo/dc7e47991c512755ff26bd2d31e72ca8) and [this TLDR comment](https://github.com/termux/termux-app/issues/2366#issuecomment-1009269410) on how to disable trimming of phantom processes.

#### Deactivation Instructions (ADB):
- On an ADB console, paste the following commands on the following order:
```
adb shell "/system/bin/device_config set_sync_disabled_for_tests persistent"
```
```
adb shell "/system/bin/device_config put activity_manager max_phantom_processes 2147483647"
```
```
adb shell settings put global settings_enable_monitor_phantom_procs false
```

#### Deactivation Instructions (ROOT):
- On Termux (or any Terminal Emulator), paste the following commands on the following order:
```
su -c /system/bin/device_config set_sync_disabled_for_tests persistent
```
```
su -c /system/bin/device_config put activity_manager max_phantom_processes 2147483647
```
```
su -c setprop persist.sys.fflag.override.settings_enable_monitor_phantom_procs false
```

***A better deactivation method for Root is coming soon!***

***

## Nightly

> Termux-Monet application can be obtained on **Github** either from [`Github Releases`](https://github.com/DevMoxxie/termux-monet/releases) for **stable releases** or from [`Github Actions`](https://github.com/DevMoxxie/termux-monet/actions/workflows/debug_build.yml) for the latest **unstable releases**.

#### Releases (Stable)
 - The APKs for `Github Releases` will be listed under `Assets` drop-down of a release. These are automatically attached when a new version is released.

#### Nightly (Unstable)
 - The APKs for `Github Actions` will be listed under `Artifacts` section of a workflow run. These are created for each commit/push done to the repository and can be used by users who don't want to wait for releases and want to try out the latest features immediately. Note that for seeing action workflows, you **need** to be [**logged into a `Github` account**](https://github.com/login) for the `Artifacts` links to be enabled/clickable. If you are using the [`Github` app](https://github.com/mobile), then make sure to open workflow link in a browser like Chrome or Firefox that has your Github account logged in since the in-app browser may not be logged in. 

***

## Wikis

- [Termux Wiki](https://wiki.termux.com/wiki/)
- [Termux App Wiki](https://github.com/DevMoxxir/termux-monet/wiki)
- [Termux Packages Wiki](https://github.com/termux/termux-packages/wiki)

***

## Miscellaneous
- [FAQ](https://wiki.termux.com/wiki/FAQ)
- [Termux File System Layout](https://github.com/termux/termux-packages/wiki/Termux-file-system-layout)
- [Differences From Linux](https://wiki.termux.com/wiki/Differences_from_Linux)
- [Package Management](https://wiki.termux.com/wiki/Package_Management)
- [Remote Access](https://wiki.termux.com/wiki/Remote_Access)
- [Backing up Termux](https://wiki.termux.com/wiki/Backing_up_Termux)
- [Terminal Settings](https://wiki.termux.com/wiki/Terminal_Settings)
- [Touch Keyboard](https://wiki.termux.com/wiki/Touch_Keyboard)
- [Android Storage and Sharing Data with Other Apps](https://wiki.termux.com/wiki/Internal_and_external_storage)
- [Android APIs](https://wiki.termux.com/wiki/Termux:API)
- [Moved Termux Packages Hosting From Bintray to IPFS](https://github.com/termux/termux-packages/issues/6348)
- [Running Commands in Termux From Other Apps via `RUN_COMMAND` intent](https://github.com/termux/termux-app/wiki/RUN_COMMAND-Intent)
- [Termux and Android 10](https://github.com/termux/termux-packages/wiki/Termux-and-Android-10)

***

## Debugging

You can help debug problems of the `Termux` app and its plugins by setting appropriate `logcat` `Log Level` in `Termux` app settings -> `<APP_NAME>` -> `Debugging` -> `Log Level` (Requires `Termux` app version `>= 0.118.0`). The `Log Level` defaults to `Normal` and log level `Verbose` currently logs additional information. Its best to revert log level to `Normal` after you have finished debugging since private data may otherwise be passed to `logcat` during normal operation and moreover, additional logging increases execution time.

The plugin apps **do not execute the commands themselves** but send execution intents to `Termux` app, which has its own log level which can be set in `Termux` app settings -> `Termux` -> `Debugging` -> `Log Level`. So you must set log level for both `Termux` and the respective plugin app settings to get all the info.

Once log levels have been set, you can run the `logcat` command in `Termux` app terminal to view the logs in realtime (`Ctrl+c` to stop) or use `logcat -d > logcat.txt` to take a dump of the log. You can also view the logs from a PC over `ADB`. For more information, check official android `logcat` guide [here](https://developer.android.com/studio/command-line/logcat).

Moreover, users can generate termux files `stat` info and `logcat` dump automatically too with terminal's long hold options menu `More` -> `Report Issue` option and selecting `YES` in the prompt shown to add debug info. This can be helpful for reporting and debugging other issues. If the report generated is too large, then `Save To File` option in context menu (3 dots on top right) of `ReportActivity` can be used and the file viewed/shared instead.

Users must post complete report (optionally without sensitive info) when reporting issues. Issues opened with **(partial) screenshots of error reports** instead of text will likely be automatically closed/deleted.

##### Log Levels

- `Off` - Log nothing.
- `Normal` - Start logging error, warn and info messages and stacktraces.
- `Debug` - Start logging debug messages.
- `Verbose` - Start logging verbose messages.
##

***

## Forking

- Check [`TermuxConstants`](https://github.com/DevMoxxie/termux-monet/blob/master/termux-shared/src/main/java/com/termux/shared/termux/TermuxConstants.java) javadocs for instructions on what changes to make in the app to change package name.
- Keep targetSdk 28 to avoid login error `not exec("/data/data/com.termux/files/usr/bin/login"): Permission denied`.
- You also need to recompile bootstrap zip for the new package name. Check [building bootstrap](https://github.com/termux/termux-packages/wiki/For-maintainers#build-bootstrap-archives), [here](https://github.com/termux/termux-app/issues/1983) and [here](https://github.com/termux/termux-app/issues/2081#issuecomment-865280111).
- Currently, not all plugins use `TermuxConstants` from `termux-shared` library and have hardcoded `com.termux` values and will need to be manually patched.
- If forking termux plugins, check [Forking and Local Development](https://github.com/DevMoxxie/termux-monet/wiki/Termux-Libraries#forking-and-local-development) for info on how to use termux libraries for plugins.
- Enable github actions and do any commit to build termux. e.g. upload a placeholder file.
- Create empty releases. You don't need to manually upload termux apks, Github Actions will do all the job for you.
