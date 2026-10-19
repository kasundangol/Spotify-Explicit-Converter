# Spotify Clean Playlist Maker

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kasundangol10-star/Spotify-Explicit-Converter/blob/main/Spotify_Clean_Playlist_Maker.ipynb)

Make a clean (non-explicit) copy of a Spotify playlist you own. It runs in your browser on Google Colab, so there is nothing to install on your computer.

## How it works

Spotify often lists the explicit and clean versions of a song as two separate tracks. This notebook:

1. Reads every song in your playlist.
2. Keeps songs that are already clean.
3. For each explicit song, searches Spotify for the same title by the same artist that is not marked explicit.
4. Puts all the matches into a new private playlist named after the original, for example "My Playlist (Clean)".
5. Saves two text files: `clean_songs.txt` (what made it in) and `no_clean_version.txt` (songs with no clean version found).

Some songs simply have no clean version on Spotify, so expect some to come up empty.

## What you need

- A Spotify account
- A Google account (for Colab)
- A playlist **you own** (if it is someone else's, first copy its songs into a new playlist of your own: select all songs, Add to playlist, New playlist)

## One-time setup

1. Create an app at [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard).
   - Set the **Redirect URI** to exactly `http://127.0.0.1:8888/callback`
   - Tick **Web API**
   - Note: Spotify may require a Premium account to create and use developer apps. Check their current requirements.
2. Open the app's **Settings** and copy the **Client ID** and **Client secret**.
3. Click the **Open in Colab** badge above.
4. In Colab, click the **key icon** (Secrets) in the left sidebar and add two secrets:
   - `SPOTIFY_CLIENT_ID` with your Client ID
   - `SPOTIFY_CLIENT_SECRET` with your client secret
5. Switch on **Notebook access** for both.

Your credentials are stored in your own Google account, not in the notebook, so they are not shared with anyone who opens or copies it.

## Using it

1. Run the code cell.
2. Paste your playlist link when asked (in Spotify: Share, then Copy link to playlist).
3. Colab prints a login link. Open it and click **Agree**.
4. You land on a page that says it can't be reached. That is expected. Copy the full address from the address bar, paste it into the box in Colab, and press Enter.
5. Wait for it to finish. Open the folder icon on the left to see the saved text files.

Colab forgets your login when the session resets, so you repeat step 3 and 4 in each new session.

## Troubleshooting

- **`ModuleNotFoundError: No module named 'spotipy'`**: the session was reset. Run the cell again; the install line is at the top.
- **"Couldn't find your secrets"**: check the two secret names match exactly and Notebook access is switched on.
- **`INVALID_CLIENT: Invalid redirect URI`**: the Redirect URI in your Spotify app must be exactly `http://127.0.0.1:8888/callback`.
- **"Found 0 tracks"**: the playlist is probably not one you own. Make a copy of your own and use that link.
- **403 Forbidden when creating the playlist**: Spotify restricts what apps in Development Mode can do. The notebook still saves `clean_songs.txt` so you can add the songs by hand.

## Limitations

- Only songs with a clean version on Spotify can be swapped in.
- Matching is strict (same title and same main artist), so a few real clean versions may land in `no_clean_version.txt`. It is worth skimming.
- Spotify changes its developer API from time to time. If something breaks, please open an issue with the error message (never include your client secret).

## Security

Never paste your client secret into the notebook code, an issue, or a screenshot. If it is ever exposed, click **Rotate client secret** in your Spotify developer dashboard.

## Disclaimer

This is an unofficial project and is not affiliated with or endorsed by Spotify. It uses Spotify's public Web API and is subject to Spotify's Developer Terms.

## License

MIT. See the `LICENSE` file.
