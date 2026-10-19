# 🚧 **Status: Work in Progress | Not Fully Tested**

This project is under active development. Features may be incomplete, unstable, or subject to change.

# Network Speed Combiner

Network Speed Combiner is a high-performance download manager for Windows, macOS, and Linux that downloads files over multiple internet connections concurrently. If your computer has Wi-Fi and a mobile phone tethered via USB (or Ethernet), Network Speed Combiner utilizes both connections simultaneously for the same download. It supports direct HTTP/HTTPS links, magnet links, and `.torrent` files, complete with queues, detailed chunk telemetry, and per-interface speed and data allowance controls.

## Features

- **Combine Multiple Networks**: Aggregates throughput from multiple network adapters (e.g. Wi-Fi + USB 4G/5G Tethering + Ethernet) without requiring VPNs, virtual NICs, or admin rights.
- **Dynamic Chunk Scheduling**: Files are split into dynamic blocks (up to 8 MB) distributed across streams. Faster networks automatically pick up more chunks.
- **Endgame Racing**: Prevents slow finishes by racing the last remaining chunks across idle connections.
- **Pause & Resume**: Safe partial resuming with ETag and Last-Modified integrity validation.
- **BitTorrent Multi-Homing**: WebTorrent integration pinning peers and trackers across available interfaces.
- **Interface Bandwidth & Data Limits**: Set total or per-network bandwidth caps and daily/weekly/monthly quotas.
- **Slow Mode & Overnight Scheduling**: One-click bandwidth throttle and time-window scheduling.

## How It Works

Operating systems typically route all network traffic through a single default gateway. Network Speed Combiner binds individual sockets to the local address of each active network adapter, pulling distinct ranges via HTTP `Range: bytes=...` requests concurrently.

```text
                    ┌── Wi-Fi (192.168.1.40) ──────┐
                    │                              │
File ──→ Split ─────┼── Ethernet (10.0.0.12) ──────┼──→ Assembled file
                    │                              │
                    └── USB tether (172.20.10.3) ──┘
```

## Getting Started

### Prerequisites

- Node.js 22+
- npm 9+

### Setup & Development

```bash
# Clone the repository
git clone https://github.com/VG31OP/network-speed-combiner.git
cd network-speed-combiner

# Install dependencies
npm install

# Start in development mode
npm run dev
```

### Building for Production

- **Windows Unpacked**:
  ```bash
  npm run build:unpack
  ```
- **Windows Installer**:
  ```bash
  npm run build:win
  ```
- **macOS**:
  ```bash
  npm run build:mac
  ```
- **Linux**:
  ```bash
  npm run build:linux
  ```

## Tech Stack

- **Framework**: Electron
- **Frontend**: React 19, TypeScript, Tailwind CSS v4, Base UI, Zustand, Lucide Icons
- **Bundler**: electron-vite
- **Networking**: Node.js `net`, `http`, `https`, `koffi`, WebTorrent

## License

MIT License. See [LICENSE](LICENSE) for details.
