# First run: AV Control on Raspberry Pi

**[Polski](PIERWSZE-URUCHOMIENIE-PL.md) · [English](FIRST-RUN-EN.md)**

Use this procedure for a new SD card prepared by **AV Control Imager** for Pi **3B, 4B or 5**. Update an existing installation using Runtime; writing its card with Imager erases it. The complete Polish training course remains one handbook; chapters 23–27 cover imaging, configuration, deployment, Player and updates.

## 1. Prepare the SD card

1. Download Imager from **Assets** in the [latest release](https://github.com/Gartom91/av-control-studio/releases/latest). The AV Control image and writing utility are included. Install Studio if you will design the project.
2. Connect an SD reader. The minimum card size is 8 GB; 16 GB or larger is recommended. Back up its existing contents.
3. Select **3B / 4B / 5** and check the target disk's number, capacity and volumes.
4. Set **Nazwa kontrolera** (controller name), default `av-control`. Give multiple controllers unique names, such as `room-a` and `room-b`. Use lowercase letters, digits and hyphens, up to 63 characters.
5. Choose an AV Control administrator password of at least 12 characters. The controller has no factory administrator password.
6. Configure the separate Linux account, default username `avoperator`. Imager initially proposes the same entered password for both accounts; you can choose a separate system password. Optional SSH access is disabled by default.
7. Ethernet uses DHCP. For Wi-Fi, enable configuration and enter the SSID, WPA2/WPA3 password and country. Pi 3B requires a 2.4 GHz network.
8. If you will access the controller by a fixed IP, reserve it in the router's DHCP settings and enter it in **Dodatkowe adresy certyfikatu** (additional certificate addresses). This field adds a certificate name/IP; it does not configure a static network address.
9. **Dołączenie do TechnikAV** is optional and disabled by default. Local control does not need it. Enabling it requires subsequently accepting the controller in your TECHNIKAV account.
10. Select **Przygotuj zapis karty**, check the summary and enter the required `WYMAŻ number` confirmation. Select **Wymaż i zapisz kartę SD**, confirm the correct target and Windows elevation prompt. This erases the selected disk.
11. Wait for writing, read-back verification and **Karta jest gotowa** (card ready). Do not remove the card during the operation.

## 2. Boot and find the controller

Insert the card into the Pi, connect Ethernet if used, and connect suitable power. First boot configures the Linux account, network, application administrator and HTTPS certificate. Wait for provisioning to finish; the pairing files are created afterwards.

| Imager setting | Interface address |
| --- | --- |
| Default name `av-control` | **https://av-control.local:8443/** |
| Custom name `room-a` | **https://room-a.local:8443/** |
| Known IP such as `192.168.1.50`, included in the certificate | **https://192.168.1.50:8443/** |

Use **HTTPS** and port **8443**. There is no universal fixed IP for a fresh image. `192.168.1.23` identifies one existing test installation; it is not the image's default address.

The `.local` name uses local-network mDNS. The computer and Pi need network connectivity; guest-network isolation or separate VLANs may block discovery and access. If the name does not resolve, look for the chosen hostname in your router's connected-device / DHCP lease list and read its IP. Access by that IP still requires certificate-name agreement; do not disable verification.

## 3. Read pairing details and trust the certificate

After successful first boot, the boot partition contains:

- **`AV-Control-parowanie.txt`**: actual URL, username `admin` and server certificate SHA256 fingerprint. It contains no password.
- **`AV-Control-CA.crt`**: public CA certificate for browser trust.

Read these through the local console / previously enabled SSH, or shut the Pi down correctly and read the card on a PC. Do not remove a live controller's card. With SSH configured, sign in using the Linux account, for example `avoperator`, and read:

```sh
cat /boot/firmware/AV-Control-parowanie.txt
```

**Studio / Player:** enter the HTTPS URL and exact SHA256 fingerprint from the pairing file. The apps verify the fingerprint, hostname and certificate validity. Their native connection does not require importing the CA into Windows.

**Browser:** import `AV-Control-CA.crt` from your own controller into the device/browser's trusted certificate authorities. On Windows, open the certificate, install it for the current user and choose **Trusted Root Certification Authorities**. A browser with a separate trust store also needs its own import. Trusting a CA trusts certificates that it issues: only import the file obtained from your own controller. Restart the browser and use the name in the pairing file. Do not export private `.key` files.

A certificate error when using an IP often means that IP was not included in the certificate. Use the covered `.local` name or configure the correct certificate addresses. Bypassing a browser warning is not completed pairing. Check the date on the PC and Pi; set an accurate clock for offline installations.

## 4. Sign in and check settings

Open the controller URL and sign in to AV Control as **`admin`**, using your Imager password. **`avoperator`** is the Linux / SSH account, not the default web account. Studio's local simulator credentials `admin` / `simulation` are not factory Pi credentials.

In **Ustawienia → Konfiguracja Raspberry Pi**, check the model, hostname, addresses, time, temperature, free storage and network interfaces. UART is enabled in the clean image without a serial console. Configure its device and protocol later in the project. Additional USB–Ethernet interfaces can be configured here, preferably bound to their MAC address.

Changing the controller name renews the server certificate. Update Studio / Player's URL and fingerprint. The configurator displays the new fingerprint and offers the public CA download. Network changes require confirmation after reconnecting; follow the displayed instructions before the rollback deadline.

## 5. Connect Studio and deploy a project

1. Select a controller connection in Studio instead of the local simulator. Enter an installation name, **Adres HTTPS kontrolera**, **Odcisk SHA256 certyfikatu z RPi**, `admin` and your password.
2. Create a project or open a neutral training example. Physical transports in the example are disabled. Set your ports, addresses and protocols before enabling them.
3. Add panel pages and bindings. Validate and test in the simulator.
4. Check that Studio is connected to the intended Pi. Publish through validation, staged preparation and activation. Saving a local project does not deploy it.
5. Open **Panel operatora** in the controller's browser interface, or connect standalone Player using the URL and fingerprint. It shows the Pi's active project. The engine continues running when Studio closes.

A new card has no installation project deployed. Waiting for a panel is expected until the first project is activated.

## 6. Accounts, login and local HDMI

An administrator creates a separate operator account in Settings. Operators change their own passwords; administrators manage accounts and their passwords. See the [account and keyboard guide](ACCOUNTS-AND-LOGIN-EN.md).

Panels require sign-in. **Loguj automatycznie na tym urządzeniu (30 dni)** (automatic login on this device for 30 days) is initially off and applies to that station. **Wyloguj z panelu** ends its remembered session. The virtual keyboard slides up when an input is selected; Shift and Alt provide extra characters. Physical keyboards also work.

Connect HDMI and a USB mouse, touchpad or touchscreen. Pi 3B uses HDMI; 4B / 5 use micro HDMI. Touch generally needs a separate USB connection: HDMI carries the picture. The clean image enables the kiosk when a monitor is detected. It shows sign-in and then the active panel, without Studio or the desktop. With no project it waits for a panel. Select the start page under **Konfiguracja Raspberry Pi → Panel lokalny HDMI**. **Ctrl+Alt+F2** opens the tty2 system sign-in console; **Ctrl+Alt+F1** returns to the kiosk. See the [HDMI guide](HDMI-PANEL-EN.md).

## 7. Updates and optional remote monitoring

Daily operation is local. GitHub update checks and hosted reporting need internet access and configuration. Configure Runtime's update policy in Settings, separately from Windows app updates. Runtime updates preserve the project and data; Imager prepares and erases a new card.

If TECHNIKAV enrollment was enabled, sign in to your **technikav.pl** account, select AV Control, compare the device identifier with the local controller and accept the installation. This account is separate from local `admin` and Linux `avoperator`. The hosting receives reports. Email requires its own recipient configuration and hosting schedule; entering project metadata does not enable email notifications.

## 8. Troubleshooting

| Symptom | Check |
| --- | --- |
| `.local` does not resolve | Power, cable / SSID, router DHCP list, correct hostname, same network and client isolation |
| HTTPS cannot connect | HTTPS, port 8443, completed provisioning; `avcontrol-setup.service` and `avcontrol.service` using console / SSH |
| Pairing files missing | First boot must finish; inspect `journalctl -u avcontrol-setup.service -b`; files do not exist before the first boot |
| Certificate rejected | Correct controller CA, covered hostname/IP, current fingerprint and accurate dates |
| Password rejected | Web: `admin` and Imager password; SSH: Linux account; simulator: separate credentials |
| Monitor waits for a panel | Project published and activated, with panel pages |
| Touch does not work | USB input connection, Linux HID detection, vendor driver / calibration requirements |

Do not include passwords, private keys or saved sessions in issue reports. Include the model, version, chosen hostname, provisioning stage and error message.

**Verification boundary:** this procedure was checked against Imager, first-boot provisioning, pairing and kiosk implementation. Package tests and emulation do not replace a clean physical SD boot or HDMI, touch and port tests on each Pi model. Consult the relevant release report for completed trials and their limits.
