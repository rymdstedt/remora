# Remora 🐟

**Rides along with Wireshark.** Remora turns packet captures into a live, NOC-style picture of your network – who talks to whom, what protocols are flowing, and what looks suspicious.

![Remora dashboard](docs/screenshot.png)

## Download

**[⬇ Download the latest Remora for macOS](https://github.com/rymdstedt/remora/releases/latest)** – a universal app for Apple Silicon and Intel, macOS 12 or later.

1. Open the DMG and drag **Remora** into **Applications**.
2. The first launch is blocked because the app is not notarized by Apple. Open **System Settings › Privacy & Security**, click **Open Anyway**, then **Open**. This is only needed once.

## What it shows

- **KPIs** with sparklines: throughput, data volume, packets, active hosts, DNS lookups, alerts
- **Traffic flow** stacked by protocol – drag across it to zoom into a time range
- **Alerts & findings**: port scans, host sweeps, failed DNS lookups (NXDOMAIN), unencrypted HTTP, cleartext protocols, large uploads, traffic spikes
- **Network map** with animated packet flows – color shows the protocol, direction shows where the bytes go
- **Protocol mix, top talkers and a live event feed** (DNS lookups, TLS server names, HTTP requests, new hosts)
- **Tables** for conversations, DNS, TLS/SNI and HTTP

## Filtering

Click a protocol chip to show only that protocol, click again to hide it, once more to turn the filter off – combine as many as you like. Layer chips work like Wireshark display filters: `TCP` includes TLS and HTTP, `UDP` includes DNS and QUIC. Clicking a host, alert, talker or chart segment narrows every view to it; `Esc` clears all filters.

## Live capture

Opening `.pcap` / `.pcapng` files works out of the box – drop a file on the window, press **⌘O**, or use **Open With › Remora** in Finder.

Live capture uses Wireshark's `dumpcap`. Install [Wireshark](https://www.wireshark.org) and keep **Install ChmodBPF** checked so captures work without admin rights. Then pick an interface, optionally add a capture filter such as `port 53`, and press **Live**.

## Privacy

Everything runs locally. Captures are parsed on your Mac and never leave it, and the app opens no network ports.

## Known limitations

- No TCP reassembly: HTTP and TLS are read from the first segment (enough for request lines and server names).
- Server names inside QUIC (HTTP/3) are not decoded; DNS answers provide host names instead.
- Alerts are heuristics with fixed thresholds, not an intrusion detection system.
