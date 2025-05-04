---
layout: post
title: "PhantomOPSEC"
date: 2025-04-28
---

# PhantomOPSEC v1.0: Simple User Guide

## What is PhantomOPSEC?

PhantomOPSEC is a collection of tools that work together to protect your privacy and security on Windows computers. It hides your identity online by encrypting your traffic, changing how your computer appears on networks, and routing your connection through secure paths.

## Why Use PhantomOPSEC?

- Hide your real location and IP address
- Prevent tracking of your online activities
- Protect against network monitoring
- Maintain privacy during sensitive operations

## Getting Started

### What You Need:
- Windows 10 or 11 computer
- Administrator rights on your computer
- The following free tools:
  - ProtonVPN
  - Technitium MAC Address Changer
  - Simple DNSCrypt
  - Tor Browser
  - Socat64 for Windows

### Setting Up PhantomOPSEC:

#### Step 1: Install Required Tools
1. Download and install all the tools listed above from their official websites
2. Make sure you have administrator rights on your computer

#### Step 2: Set Up Your Protection Chain

Follow these steps in order:

1. **Change Your MAC Address**
   - Open Technitium MAC Address Changer
   - Select your network adapter
   - Click "Random MAC Address"
   - Click "Change Now"
   - Reconnect to your network

2. **Activate Your VPN**
   - Open ProtonVPN
   - Sign in to your account
   - Turn on Kill Switch (under Settings)
   - Connect to a server (choose a country far from your location)

3. **Secure Your DNS**
   - Open Simple DNSCrypt
   - Click "Enable DNSCrypt"
   - Select "Use Anonymized DNS"
   - Click Apply

4. **Set Up Tor**
   - Create a custom torrc file at C:\tor\torrc with these settings:
   ```
   ## === SOCKS & CONTROLPORT SETUP ===
   SocksPort 127.0.0.1:9050
   ControlPort 127.0.0.1:9051
   CookieAuthentication 1
   HashedControlPassword 16:AB38C2D76453A74560CA2BB8C1A7042072093276A3D701AD684053EC4C
   
   ## === SPEED & STABILITY ===
   AvoidDiskWrites 1
   ClientUseIPv4 1
   ClientUseIPv6 0
   DisableNetwork 0
   MaxCircuitDirtiness 600
   
   ## === ENTRY NODE RESTRICTIONS (OPTIONAL: SPEED BOOST) ===
   # EntryNodes {us},{de},{fr}
   # StrictNodes 1
   
   ## === GEOIP FILES (FIX RELATIVE PATH WARNINGS) ===
   GeoIPFile C:\Tor\Data\geoip
   GeoIPv6File C:\Tor\Data\geoip6
   
   ## === LOGGING (OPTIONAL) ===
   Log notice stdout
   ```
   
   - Create a batch file (tor.bat) to start Tor with your custom config:
   ```
   @echo off
   title Starting TOR with Custom torrc
   cd /d C:\tor
   
   echo [*] Launching TOR with torrc...
   start "" tor.exe -f "C:\tor\torrc"
   
   echo [✓] TOR launched using: C:\tor\torrc
   echo [✓] SocksPort: 127.0.0.1:9050
   echo [✓] ControlPort: 127.0.0.1:9051
   
   timeout /t 2 >nul
   exit
   ```
   
   - Run the batch file to start Tor

5. **Set Up SocksCap64**
   - Install SocksCap64
   - Configure it to use the Tor SOCKS proxy (127.0.0.1:9050)
   - Launch your browser or other applications through SocksCap64 to route traffic through Tor

## Verification Steps

After setting up, verify your protection is working:

1. **Check Your IP Address**
   - Go to a website like "whatismyip.com"
   - Confirm the IP shown is from your VPN, not your real location

2. **Verify DNS Is Secure**
   - Go to "dnsleaktest.com"
   - Run the standard test
   - Make sure the DNS servers shown are not your ISP's servers

3. **Test Your MAC Address**
   - Open Command Prompt
   - Type: `getmac /v`
   - Confirm your MAC address is different from your original one

## Common Issues and Solutions

### VPN Keeps Disconnecting
- Check your internet connection
- Try a different VPN server
- Make sure no firewall is blocking the VPN

### MAC Address Won't Change
- Disconnect from networks before changing
- Make sure you're running Technitium as administrator
- Try disabling/enabling your network adapter

### DNS Still Leaking
- Restart Simple DNSCrypt
- Check Windows settings to ensure DNS is set to 127.0.0.1
- Disable IPv6 if it's causing leaks

### Applications Not Working Through Tor
- Verify Tor is running (check for the process in Task Manager)
- Make sure SocksCap64 is properly configured to use port 9050
- Try launching different applications through SocksCap64 to test the connection

## Safety Reminders

- Always verify all protection layers are active before doing sensitive work
- Never use this setup for illegal activities
- Remember that extreme privacy measures can sometimes draw attention
- No privacy system is 100% perfect - always act with caution
