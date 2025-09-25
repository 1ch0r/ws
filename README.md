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

---
===========================================================
📂 Project Structure
===========================================================

src/
├── main.c
├── config/              # Config parsing & validation
├── policy/              # Policy orchestration
├── ipc/                 # Hardened IPC
├── net/                 # Network, traffic, anonymity modules
├── utils/               # Shared utilities
├── include/             # Public headers
└── Makefile

===========================================================
🔄 Service Flow
===========================================================

[ Boot Phase ]
   |-- boot_env_check      (validate kernel cmdline, modules, bootloader)
   |-- boot_guard          (fail-closed nftables, block early leaks)
   |-- mac_random_boot     (randomize MAC before link-up)
   |-- dhcp_spoof          (minimal DHCP options, randomized IDs)
   |-- me_guard            (block Intel ME/AMT mgmt ports)
   v
[ Init Phase ]
   |-- policy_engine       (load trust model, orchestrate sequencing)
   |-- ipc_server          (secure IPC channel)
   |-- kernel_harden       (drop caps, seccomp, /proc hardening)
   |-- time_fuzz           (jittered scheduling)
   |-- sidechannel_guard   (constant-time ops, scrub primitives)
   |-- memory_scrubber     (register buffers, signal hooks)
   v
[ Network Bring-up ]
   |-- vpn_chain           (optional multi-hop VPN)
   |-- tor + ip_rotation   (transparent Tor routing, IP rotation)
   |-- pluggable_transport (obfs4, meek, snowflake)
   |-- bridge_mode         (bridge orchestration)
   |-- dns_secure + dns_mask (encrypted DNS + redirection)
   |-- firewall + egress_firewall (fail-closed global + per-UID)
   |-- route_lock          (prevent route tampering)
   v
[ Runtime Protection ]
   |-- traffic_pad/shape   (padding, bandwidth normalization)
   |-- decoy               (protocol-mimicking cover traffic)
   |-- fingerprint_defense (normalize TLS/QUIC hellos)
   |-- tls_enforcer        (TLS 1.3+, ECH, cipher policy)
   |-- protocol_sanitizer  (MTU, TCP timestamps, ICMP PMTU)
   |-- conn_monitor        (track outbound per-process)
   |-- daemon_watch        (block unauthorized daemons)
   |-- wifi_harden         (suppress SSID/vendor IEs)
   |-- bt_lte_harden       (radio hygiene)
   |-- hw_id_mask          (mask CPU/TPM IDs)
   |-- id_mask             (mask hostname, machine-id)
   |-- peripheral_mask     (mask GPU/USB/PCI descriptors)
   |-- time_guard          (normalize NTP, clock skew)
   |-- power_mask          (fuzz battery telemetry)
   |-- swap_guard          (disable/encrypt/wipe swap/hibernation)
   |-- crash_guard         (disable/scrub core dumps)
   |-- secret_store        (ephemeral secret storage)
   v
[ Monitoring & Resilience ]
   |-- audit               (state machine, captive portal safe mode)
   |-- killswitch          (fail-safe watchdog)
   |-- watchdog            (heartbeat, self-heal)
   |-- telemetry_safe      (anonymized metrics/logs)
   |-- config_guard        (signed configs, rollback protection)
   v
[ Shutdown Phase ]
   |-- memory_scrubber     (scrub sensitive buffers)
   |-- swap_guard          (wipe swap if enabled)
   |-- crash_guard         (scrub crash logs)
   v
[ System Halted Safely ]

===========================================================


---



## 🚀 Getting Started

Build

make

Run

sudo ./anonymizer

Configuration

Edit anonymizer.conf for runtime options.

Policies defined in anonymizer.policy.

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

This project is a research‑grade anonymization framework.It significantly raises the bar against network and system correlation attacks, but cannot guarantee absolute anonymity against all adversaries.Firmware, hardware, and user behavior remain critical factors.

