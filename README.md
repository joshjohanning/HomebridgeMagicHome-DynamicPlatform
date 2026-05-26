
<p align="center">

<img src="https://github.com/Lethegrin/HomebridgeMagicHome-DynamicPlatform/blob/master/branding/logos/zackneticlogo.svg" width="150">

</p>


# Homebridge MagicHome Dynamic Platform
[![Donate](https://img.shields.io/badge/Donate-PayPal-%2300457C?style=for-the-badge&logo=PayPal)](https://paypal.me/joshuajohanning)
[![Discord](https://img.shields.io/badge/Chat-Discord-%237289DA?style=for-the-badge&logo=Discord)](https://discord.gg/c8xpmZSNZC)

### Join the [Official MagicHome Discord Channel](https://discord.gg/c8xpmZSNZC) for tech support and to chat with other MagicHome users

## About

> [!TIP]
> This is a drop-in replacement for the original [`homebridge-magichome-dynamic-platform`](https://github.com/Zacknetic/HomebridgeMagicHome-DynamicPlatform) plugin with explicit Homebridge 2 support. See [Migrating from `homebridge-magichome-dynamic-platform`](#migrating-from-homebridge-magichome-dynamic-platform) for setup steps.

A Homebridge plugin for a range of Magic Home Wi-Fi lights and LED controllers.

## Installation

Install from the Homebridge UI by searching for `@joshjohanning/homebridge-magichome-dynamic-platform`, or via the command line:

```bash
sudo hb-service add @joshjohanning/homebridge-magichome-dynamic-platform
```

## Use

* This plugin automatically detects MagicHome bulbs and controllers just like the Magichome app, and it should do so when you first run Homebridge. No more setting individual IP addresses per device.

* If a device has changed its IP Address, such as after a power outage, this plugin will update that device with the new IP on the next restart. Maintaining the device's associated timers, scenes, etc.

* If you'd like to remove an individual device, add the word 'delete' to any part of its name in Homekit and restart homebridge. This can be useful if you are intentionally taking a device offline or if you would simply like to reset it. Keep in mind, if it is still turned on during the homebridge restart, it will be detected and added again.

## User Interface

When the retical moves closer to the center of the color wheel, the saturation % drops. Once the retical passes the threshold (default 50%) it will switch to white mode or color and white mode depending on the device and config settings. See below for more details.

* **RGBWW 5 Channel LED Strip Controller (RGB and Two Whites)** In the color wheel, move the retical from cyan to red. This will transition the LEDs in this pattern:
```Color-Only>Color and Cold-White>Cold-White Only>Cold-White and Warm-White>Warm-White Only>Color and Warm-White>Color-Only```

* **RGBWW 5 Channel LED Lightbulb (RGB and Two Whites)** In the color wheel, move the retical from cyan to red. This will transition the LEDs in this pattern:
```Color-OnlyCold-White Only>Cold-White and Warm-White>Warm-White Only>Color-Only```

* **RGBWW 4 Channel LED Strip Controller (RGB and  One White)** In the color wheel, move the retical from cyan to red. This will transition the LEDs in this pattern:
```Color-Only>Color and White>White Only>Color and White>Color-Only```

* **RGBW 4 Channel LED Lightbulb (RGB and One White)** In the color wheel, move the retical from cyan to red. This will transition the LEDs in this pattern:
```Color-Only>White-Only>Color-Only```

* **RGB 3 Channel (RGB Only)** Normal RGB functionality.

## Configuration

Please setup your config in Config UI X under ```Plugins>Homebridge MagicHome Dynamic Platform>Settings.```
However the default settings should suffice. Please read below to learn more about the settings before changing anything.

### Settings

#### Pruning

* `pruneMissingCachedAccessories` - **true** / **false** "Prune" or remove accessories once they have been missing for n restarts. Associated names, timers, and scenes will be lost for those accessories.

* `restartsBeforeMissingAccessoriesPruned` - ***number*** The number of homebridge restarts that an accessory can be not seen before being pruned. Will not occur if `pruneMissingCachedAccessories` is set to false.

* `pruneAllAccessoriesNextRestart` - **true** / **false** "Prune" or remove all accessories next restart. Use this if you would like to remove all your magichome accessories next restart. Be sure to set to false after you restart otherwise the cached accessories and associated names, timers, and scenes will be lost.

#### White Effects

* `simultaniousDevicesColorWhite` - **true** / **false** Allow simultanious color and white LEDs on compatible devices.

* `colorWhiteThreshold` - **number** The saturation threshold from color-only to white-only for non-simultanious devices.

* `colorWhiteThresholdSimultaniousDevices` - **number** The saturation threshold from color-only to color and white for simulanious devices.

* `colorOffThresholdSimultaniousDevices` - **number** The saturation threshold from color and white to white only for simultanious devices.

#### Device Management

* `blacklistOrWhitelist` - **blacklist** / **whitelist** Whether the listed Unique IDs are blacklisted or whitelisted.

* `blacklistedUniqueIDs` - **Alphanumeric** Unique IDs of devices you wish this plugin to ignore/delete. Can be found in the Magichome app under "MAC Address" or in the logs under "Unique ID". **i.e. 6001940EDC1F**

## Migrating from `homebridge-magichome-dynamic-platform`

This package can be used as a drop-in replacement for the original [homebridge-magichome-dynamic-platform](https://www.npmjs.com/package/homebridge-magichome-dynamic-platform) plugin.

Existing Homebridge config entries can stay the same. Your existing HomeKit accessories should keep their identity as long as you do not delete cached accessories or remove/re-pair the Homebridge bridge.

### Safe migration steps

1. Back up Homebridge from the Homebridge UI.
2. Stop Homebridge:

   ```bash
   sudo hb-service stop
   ```

3. Remove the original plugin:

   ```bash
   sudo hb-service remove homebridge-magichome-dynamic-platform
   ```

4. Install this fork:

   ```bash
   sudo hb-service add @joshjohanning/homebridge-magichome-dynamic-platform
   ```

5. Start Homebridge:

   ```bash
   sudo hb-service start
   ```

6. Check the Homebridge logs:

   ```bash
   sudo hb-service logs
   ```

7. Verify your existing MagicHome lights still work in Apple Home.

### Important notes

Do not remove cached accessories from Homebridge unless you intentionally want HomeKit to recreate them. Removing cached accessories may break room assignments, scenes, and automations that reference those lights.

### Updating this fork

When a new version is published to npm, update it from the Homebridge UI, or run:

```bash
sudo hb-service add @joshjohanning/homebridge-magichome-dynamic-platform
sudo hb-service restart
```
