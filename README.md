# TL;DL

A self-hosted web UI for downloading media from Telegram channels. Built to run as a Docker container on ZimaOS or any Docker-compatible server.

> 🤖 This project was built with [Claude](https://claude.ai) (Anthropic AI).

---

## Features

- 🔐 Telegram login via phone number + verification code
- 📡 Browse all your joined channels
- 🎬 List all videos in a channel with captions
- ☑️ Select all or individual videos to download
- ⬇️ Real-time download progress with per-file log
- 📋 Download queue — monitor multiple active downloads
- 💾 Persistent session — authenticate once, stays logged in

## Screenshots

| Login | Channels | Download Progress |
|-------|----------|-------------------|
| Phone + code auth | Browse and search channels | Live progress bar per download |

---

## Requirements

- Docker + Docker Compose
- A Telegram API ID and API Hash — get them free at [my.telegram.org](https://my.telegram.org)

---

## Setup

### 1. Get Telegram API credentials

1. Go to [https://my.telegram.org](https://my.telegram.org)
2. Log in with your phone number
3. Go to **API Development Tools**
4. Create an app — copy the `api_id` and `api_hash`

### 2. Configure

Edit `docker-compose.yml` and set your credentials:

```yaml
environment:
  - API_ID=your_api_id_here
  - API_HASH=your_api_hash_here
```

Optionally change the downloads volume to your media folder:

```yaml
volumes:
  - ./data:/data
  - /your/media/folder:/downloads
```

### 3. Build and run

```bash
docker compose up -d --build
```

Open your browser at `http://localhost:3000`

### 4. First login

1. Enter your Telegram phone number (with country code, e.g. `+521234567890`)
2. Enter the verification code sent to your Telegram app
3. Done — session is saved in `./data/credentials.json`

---

## ZimaOS Installation

1. SSH into your ZimaOS server
2. Clone this repo:
   ```bash
   git clone https://github.com/Darkomg/tldl.git
   cd tldl
   ```
3. Edit `docker-compose.yml` with your API credentials and media path
4. Build and start:
   ```bash
   docker compose up -d --build
   ```
5. Access the UI at `http://your-server-ip:3000`

---

## Project Structure

```
tldl/
├── server.js          # Express backend + WebSocket server
├── public/
│   ├── index.html     # Main UI
│   ├── style.css      # Dark theme styles
│   └── app.js         # Frontend logic
├── Dockerfile
├── docker-compose.yml
└── package.json
```

---

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PORT` | `3000` | Web UI port |
| `API_ID` | — | Telegram API ID (required) |
| `API_HASH` | — | Telegram API Hash (required) |
| `DATA_DIR` | `/data` | Directory for session credentials |
| `DOWNLOADS_DIR` | `/downloads` | Root directory for downloaded files |

---

## Notes

- Sessions are stored in `DATA_DIR/credentials.json` — keep this volume persistent
- Downloads are organized in subfolders inside `DOWNLOADS_DIR` by channel name
- The app supports downloading videos, but the backend can be extended for other media types
- Built with [GramJS](https://github.com/gram-js/gramjs) for Telegram client functionality

---

## Built With AI

This project was fully designed and coded using **Claude Sonnet** by [Anthropic](https://anthropic.com).  
Prompted and directed by **Orlando Gutiérrez**.
