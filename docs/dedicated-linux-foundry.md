---
id: dedicated-linux-foundry
title: "Dedicated Server: Foundry Dedicated Server Linux Setup"
description: Information about setting up an Foundry Dedicated Server on a Linux Dedicated Server from ZAP-Hosting - ZAP-Hosting.com documentation
sidebar_label: Foundry
services:
  - dedicated
---

import InlineVoucher from '@site/src/components/InlineVoucher';

## Introduction
Do you have a Linux Dedicated Server and you want to install the Foundry Dedicated server service on it? You are in the right place. In this guide, we will explain the step by step process of installing this service on your Linux server through the use of SteamCMD. We will be using Ubuntu in the examples, but the process should be very similar for other distributions.

:::tip
Did you know that you can install our **ZAP GS/TS3 Interface** directly onto your dedicated server, allowing you to setup game server services, with direct integration to your ZAP-Hosting dashboard, in just a few clicks! Learn more about the [GS/TS3 Interface](dedicated-linux-gs-interface.md).
:::

<InlineVoucher />

## Preparation

To begin with, connect to your Dedicated Server via SSH. Use our [SSH Initial Access](dedicated-linux-ssh.md) guide if you need help doing this.

You will also have to complete a first-time setup for SteamCMD if this is your first time using this on your Linux server. Please use our [SteamCMD Linux Setup](dedicated-linux-steamcmd.md) guide and ensure SteamCMD is fully setup before proceeding.

:::info Wine Compatibility Layer
Foundry currently does not offer a native Linux-based server build, which means that there is an extra preparation step necessary to run the Windows server build on Linux.

You have to complete a one-time installation of the **Wine** compatibility layer if this is your first time using this on your Linux server. Please use our quick [Wine Compatibility Layer Setup](dedicated-linux-wine.md) guide to set this up before proceeding.
:::

## Installation

Begin by logging in to your `steam` user and heading over to the root `home/steam` user directory to keep things organised.
```
sudo -u steam -s
cd ~
```

When logged in, you can start the installation process using the following command to easily start the installation through the use of SteamCMD directly to your `steam` user. By using the `+@sSteamCmdForcePlatformType windows` parameter, you forcefully ensure that the Windows binaries are installed.
```
steamcmd +@sSteamCmdForcePlatformType windows +force_install_dir '/home/steam/Foundry-Server' +login anonymous +app_update 2915550 validate +quit
```

Please be patient as the download completes, it can take some time for games with larger sizes. Once successful, you will see a success message appear confirming this.

## Configuration

By this stage, you have finished the setup for your Foundry server. You can perform further server configuration through a configuration file found within the directory of your server.

You will be able to adjust all configuration parameters by accessing and editing the **app.cfg** configuration file found in the root server directory.
```
nano /home/steam/Foundry-Server/app.cfg
```

See our Foundry [Server Configuration](foundry-configuration.md) guide to view all of the available options and what they each do.

## Starting & Connecting to your server

Now it is time to start your server. Head over to the main game directory and run the **FoundryDedicatedServerLauncher.exe** executable file using the command below. Ensure that you add the **xvfb-run** and **wine** commands to run it through the Wine compatibility layer.
```
xvfb-run wine /home/steam/Foundry-Server/FoundryDedicatedServer.exe
```

You should now see logs appear in your command prompt which signals that the start up was successful. If everthing occurs as expected, your server will be visible in the server list. Alternatively, you will be able to connect directly by using the bottom search bar on the server list and searching for: `[your_ip_address]:3724`.

## Conclusion

Congratulations, you have successfully installed and configured the Foundry server on your Dedicated Server! As a next step, we recommend looking over our [Setup Linux Service](dedicated-linux-create-gameservice.md) guide, which covers setting up your new dedicated game server as a service. This provides various benefits including automatic server launching on boot, automatic server updates, easy management and access to logs, plus much more!

If you have any further questions or problems, please contact our support team, who are available to help you every day!