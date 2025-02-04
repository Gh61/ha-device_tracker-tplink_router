# TPLink Router device tracker for Home Assistant
[![Validate with hassfest](https://github.com/Gh61/ha-device_tracker-tplink_router/actions/workflows/hassfest.yaml/badge.svg)](https://github.com/Gh61/ha-device_tracker-tplink_router/actions/workflows/hassfest.yaml)

The `tplink_router` platform for `device_tracker` integration allows you to detect presence by looking at connection devices to a [TP-Link](https://www.tp-link.com) wireless router.

It was part of the official `tplink` integration in the past but was [removed](https://github.com/home-assistant/core/pull/27936) from Home Assistant.

## Fork Updates

This fork has been updated to work with Home Assistant version 2022.7+

## Installation
Manual: copy `custom_components/tplink_router` folder into your `custom_components`.

<div class='note'>
TP-Link devices typically only allow one login at a time to the admin console.  This integration will count towards your one allowed login. Depending on how aggressively you configure device_tracker you may not be able to access the admin console of your TP-Link device without first stopping Home Assistant. Home Assistant takes a few seconds to login, collect data, and log out. If you log into the admin console manually, remember to log out so that Home Assistant can log in again.
</div>

## Configuration

To enable this device tracker, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
device_tracker:
  - platform: tplink_router
    host: YOUR_ROUTER_IP
    username: YOUR_ADMIN_USERNAME
    password: !secret tplink_router_password
```

Configuration variables:

- **host** (*Required*): The IP address of your router, e.g., 192.168.1.1.
- **username** (*Required*): The username of an user with administrative privileges, usually *admin*. The Archer D9 last firmware does not require a username.
- **password** (*Required*): The password for your given admin account.

For Archer C9 models running firmware version 150811 or later please use the encrypted password you can retrieve like this:

1. Go to the login page of your router. (default: 192.168.0.1)
2. Type in the password you use to login into the password field.
3. Click somewhere else on the page so that the password field is not selected anymore.
4. Open the JavaScript console of your browser (usually by pressing F12 and then clicking on "Console").
5. Type `document.getElementById("login-password").value;` or `document.getElementById("pcPassword").value;`, depending on your firmware version.
6. Copy the returned value to your Home Assistant configuration as password.

See the [device tracker integration page](https://www.home-assistant.io/integrations/device_tracker/) for instructions how to configure the people to be tracked.

For Archer D9 model the default IP is 192.168.1.1, the username is not necessary and you can leave that field blank.

## Supported devices

Devices originaly supported include the following:

- Archer C7 firmware version 150427
- Archer C9 firmware version 150811
- EAP-225 AP with latest firmware version
- Archer D9 firmware version 0.9.1 0.1 v0041.0 Build 160224 Rel.59129n

Additional devices added since the removal from Home Assistant:

- Archer C6 firmware version 1.3.6 Build 20200902 rel.65591(4555)
- TPLink N600 with latest firmware
- TPLink VR600 with latest firmware
- TL-WR840N
- TL-WDR4900

If your device is not in the list, you can still give it a try and let me know if it works or not, I'll update the documentation.

*Disclaimer*: I cannot add support for devices I don't own, unless you provide me with a list of HTTP requests leading to the page listing MAC address of connected devices, including authentication, and an example of the page.
