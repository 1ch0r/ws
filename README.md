## 🛡️ Walks Softly

A modular, research‑grade network and system anonymization framework. This project hardens a host from boot to shutdown, covering network, system, and hardware identifiers to resist correlation, fingerprinting, and leaks.

## ✨ Features

Boot & Pre‑Boot Protection

Fail‑closed firewall before network stack (boot_guard)

MAC randomization at boot (mac_random_boot)

DHCP option minimization (dhcp_spoof)

Boot environment validation (boot_env_check)

Intel ME/AMT network exposure mitigation (me_guard)

Network Stack Hardening

DNS redirection + encrypted DNS (dns_mask, dns_secure)

IPv6 suppression (ipv6_disable)

Route immutability (route_lock)

Global + per‑UID firewalling (firewall, egress_firewall)

Traffic Obfuscation

Statistical padding (traffic_pad)

Bandwidth normalization (traffic_shape)

Protocol‑mimicking decoys (decoy)

Jittered scheduling (time_fuzz)

Anonymization Paths

Transparent Tor routing (tor)

IP rotation (ip_rotation)

Pluggable transports (pluggable_transport, bridge_mode)

Multi‑hop VPN chaining (vpn_chain)

Geo‑fuzzing (geo_fuzz)

Application & Daemon Control

Outbound connection monitoring (conn_monitor)

Daemon whitelist enforcement (daemon_watch)

Policy orchestration (policy_engine)

Hardened IPC (ipc_server, ipc_client)

Hardware & Peripheral Hygiene

Wi‑Fi SSID/vendor IE suppression (wifi_harden)

Bluetooth/LTE hygiene (bt_lte_harden)

CPU/TPM ID masking (hw_id_mask)

Hostname/machine‑ID masking (id_mask)

GPU/USB/PCI descriptor masking (peripheral_mask)

System Data Hygiene

Memory scrubbing (memory_scrubber)

Constant‑time operations (sidechannel_guard)

Swap/hibernation protection (swap_guard)

Crash/core dump control (crash_guard)

Secure secret storage (secret_store)

Side‑Channel Mitigations

Clock skew & NTP normalization (time_guard)

Power/battery telemetry fuzzing (power_mask)

Resilience & Monitoring

Live audit state machine (audit)

Fail‑safe killswitch (killswitch)

Watchdog/heartbeat (watchdog)

Safe telemetry (telemetry_safe)

Config integrity & rollback protection (config_guard)


## 🔒 Threat Model

This suite mitigates:

Pre‑boot leaks (DHCP, NTP, captive portal)

DNS/IP leaks

TLS/QUIC fingerprinting

Timing correlation

Background daemon leaks

Hardware/radio identifiers

Memory remanence

Swap/hibernation leakage

Crash/core dump leaks

Intel ME/AMT network exposure

Boot environment tampering

Clock skew, power telemetry, peripheral fingerprints

Out of scope:Firmware/BIOS compromise, physical side‑channels (EM, acoustic, power analysis), and user operational security.

## 🧩 Design Philosophy

Fail‑closed by default: No traffic flows until anonymization paths are verified.

Defense in depth: Multiple layers (e.g., DNS redirection + encryption).

Modularity: Each threat vector has a dedicated module.

Resilience: Watchdogs, audits, and killswitches ensure safe fallback.

## ⚠️ Disclaimer

This project is a research‑grade anonymization framework. It significantly raises the bar against network and system correlation attacks, but cannot guarantee absolute anonymity against all adversaries.Firmware, hardware, and user behavior remain critical factors.

