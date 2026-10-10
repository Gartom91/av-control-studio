# Local HDMI operator panel

Starting with **1.5.4**, Raspberry Pi 3B, 4B and 5 automatically display the active project's operator panel when an HDMI monitor is connected. The clean image includes the graphics stack; the Runtime update includes the same verified, offline OS packages for existing controllers.

Publish a project from Studio, connect HDMI and a standard Linux/libinput-supported USB mouse, touchpad or touchscreen. Touchscreens generally require separate HDMI video and USB touch connections. Without a monitor, the graphics session is stopped. With multiple monitors, the last connected monitor displays the panel.

Since **1.5.5**, the panel requires an AV Control user account. It offers a themed onscreen keyboard and explicit, optional 30-day automatic sign-in. The session has operator permissions only, including when using an administrator account. **My account** changes the user's own password; **Sign out** returns to the login screen. There is no desktop, browser toolbar, project editor or connection chooser. Context menus, browser history gestures, file dialogs, downloads, new windows and external navigation are blocked. Page tabs and scrolling within the published panel remain available. See the [account guide](ACCOUNTS-AND-LOGIN-EN.md).

**Ctrl+Alt+F2** opens the tty2 system login console; **Ctrl+Alt+F1** returns to the panel. Some keyboards require Fn. Log in using your own OS account; the console is never automatically authenticated. SSH remains available.

Administrators can enable/disable automatic display and select an initial page under **Settings → Raspberry Pi configuration → Local HDMI panel**. Preferences survive restart and update. Missing pages fall back to the first page of the current project.

Reconnecting HDMI or restarting the view never replays prior commands. Configured project startup actions remain a separate Runtime feature. Lost momentary-button holds expire through the existing lease mechanism. Offline views reject new requests; the panel resumes after reconnecting.

Diagnostics: `systemctl status avcontrol-kiosk.service seatd.service getty@tty2.service`, `journalctl -u avcontrol-kiosk.service -b`, and `sudo libinput list-devices`. Do not share the private local session credential. Test specialist touchscreens and calibration separately.

The [Polish illustrated guide and 60-minute training module](PANEL-HDMI-PL.md) includes connection steps, settings, service shortcuts and hardware acceptance exercises. Software/ARM emulation results are reported separately from physical monitor, USB touch and keyboard verification.
