# Fake Spotify Presence for Discord

A lightweight Python script that shows a custom **"Listening to Spotify"** rich presence on your Discord profile, with a persistent elapsed-time counter that only accumulates while the script is running.

## Features

- Custom activity name, song title and artist line (`details` / `state`)
- Optional clickable song line that opens a URL
- Optional cover image from your Discord application's art assets
- Persistent counter: time is saved every 15 seconds and resumed on the next run, so hours only add up while your PC is on
- Minimal resource usage (sleeps most of the time)
- Refuses to run if the `LICENSE` file is missing

> **Disclaimer:** Setting a fake activity is not a real Spotify integration and it does not affect your actual Spotify stats. Using custom/non-official presences violates Discord's Terms of Service and may result in your account being warned or banned. Use at your own risk. This project is not affiliated with Discord or Spotify.

## Requirements

- Python 3.9+
- The **Discord desktop application** (running and logged in)
- `pypresence`

## Installation

```bash
pip install pypresence
```

## Setup

1. Go to https://discord.com/developers/applications and click **New Application**.
2. Copy the **Client ID** from the *General Information* tab.
3. Open `fake_listening.py` and paste it into `CLIENT_ID`.
4. *(Optional)* Upload a cover image under **Rich Presence Art Assets** and set its key in `IMAGE_KEY` and its tooltip in `IMAGE_TEXT`.
5. Make sure the `LICENSE` file is in the same folder as the script.

## Usage

```bash
python fake_listening.py
```

On Windows you can also double-click `run.bat` (it starts the script in the background).

The script connects to the Discord client that is running on your machine and sets the activity on the account logged into it.

## Configuration

All settings are at the top of `fake_listening.py`:

| Variable | Description |
| --- | --- |
| `CLIENT_ID` | Your Discord application Client ID |
| `ACTIVITY_TYPE` | Type of activity (`LISTENING`, `PLAYING`, `WATCHING`, `COMPETING`) |
| `ACTIVITY_NAME` | What appears after "Listening to ..." |
| `DETAILS` | First line (e.g. song title) |
| `STATE` | Second line (e.g. artist name) |
| `DETAILS_URL` | URL opened when clicking the details line (`None` to disable) |
| `IMAGE_KEY` | Key of the uploaded art asset |
| `IMAGE_TEXT` | Tooltip text of the cover image |
| `INITIAL_SECONDS` | Seconds the counter starts from (e.g. `1000 * 3600` for 1000 hours) |

## How the counter works

- The elapsed counter is based on a `start` timestamp set in the past.
- The accumulated seconds are stored every 15 seconds in `%APPDATA%\FakeSpotify\progress.json`.
- On the next run, the counter resumes from the last saved value and keeps counting only while the script is active.

## License

Distributed under the MIT License. See `LICENSE` for more information.
