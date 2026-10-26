# Connect Spotify to Solance

**English** · [Português (Brasil)](SPOTIFY.pt-BR.md) · [← Back to README](../README.md)

Solance shows music from **any** player without any setup. Connecting Spotify adds a **Spotify tab** where you can:

- search songs, artists, albums and playlists
- browse **your** playlists and liked songs
- play, add to queue, shuffle (including Smart Shuffle) and change the volume

It takes about **two minutes**, and you only do it **once**.

> ### Why do I need my own Client ID?
> Spotify asks every app that talks to its service to be registered. Instead of everyone sharing one registration (which has strict limits and would tie all users to one account), **you create your own tiny, free app** in Spotify's developer dashboard and give Solance its *Client ID*.
> - Nothing goes through anyone else's account or server.
> - The Client ID is **not a password**. There is no secret to share.
> - You sign in on Spotify's own page. Solance never sees your password.

## Before you start

- A Spotify account.
- **Playback control** (play, pause, volume, shuffle, queue) from third-party apps is a **Spotify Premium** feature. Searching and browsing your playlists don't depend on it.
- Spotify's developer rules change from time to time. If the dashboard asks for anything that isn't described here (for example, a Premium account or extra confirmations), follow its instructions.

---

## Step by step

### 1. Open the Spotify developer dashboard

Go to **<https://developer.spotify.com/dashboard>** and log in with your Spotify account. Accept the Developer Terms if it asks.

> In Solance you can jump there with the **Open Spotify dashboard** button.

### 2. Create an app

Click **Create app** and fill in:

| Field | What to type |
|---|---|
| **App name** | `Solance` (any name works) |
| **App description** | `Notch for Windows` (anything) |
| **Website** | leave empty |
| **Redirect URIs** | `http://127.0.0.1:5543/callback` → then click **Add** |
| **Which API/SDKs are you planning to use?** | tick **Web API** |

Then tick the box agreeing to the Developer Terms and click **Save**.

> **The Redirect URI must be exactly** `http://127.0.0.1:5543/callback`
> - use `127.0.0.1`, **not** `localhost`
> - `http`, not `https`
> - no trailing slash, no spaces
> - you must click **Add** (it appears as a row under the field) *and then* **Save**
>
> Solance has a **copy button** next to this address so you don't have to type it.

### 3. Copy the Client ID

Open your new app and go to **Settings** (button at the top right of the app page). Copy the **Client ID** — a code with **32 letters and numbers**.

> Don't copy the **Client secret**. Solance doesn't need it and will warn you if you paste it.

### 4. Paste it into Solance

1. Hover the top of your screen to open the notch.
2. Open the **Spotify** tab (the magnifier icon).
3. Paste the Client ID into the field and click **Connect to Spotify**.

<div align="center">
<img src="img/spotify-setup.png" alt="Solance Spotify setup screen" width="720"/>
</div>

### 5. Allow access

Your browser opens Spotify's page. Log in if needed and click **Agree**. You'll see a confirmation — you can close that tab.

Back in Solance, the Spotify tab now shows your playlists. Type something in the search box and click a song to play it.

<div align="center">
<img src="img/spotify-search.png" alt="Searching in the Spotify tab" width="720"/>
<br/><sub>Your playlists, cover art and name are blurred in this screenshot.</sub>
</div>

You can also set this up (or change it later) in **Settings → Spotify**.

---

## Troubleshooting

<details><summary><b>The browser says “INVALID_CLIENT: Invalid redirect URI”</b></summary>

The Redirect URI in your Spotify app doesn't match. Open your app → **Settings** → **Redirect URIs** and make sure there is exactly:

```
http://127.0.0.1:5543/callback
```

Remove any other versions (for example with `localhost`, `https` or a trailing `/`), click **Add** and then **Save**. Try connecting again.
</details>

<details><summary><b>“The Client ID has 32 letters and numbers…”</b></summary>

What you pasted isn't a Client ID. Copy the **Client ID** (32 characters) from your app's Settings page — not the Client secret, and not the app's name or URL.
</details>

<details><summary><b>“Port 5543 is busy”</b></summary>

Solance listens on `127.0.0.1:5543` for a few seconds while you sign in. Another program is using that port. Close the other program (or restart your PC) and try again.
</details>

<details><summary><b>I clicked “Agree” and nothing happens in Solance</b></summary>

Keep Solance **running** while you sign in (it waits for up to 4 minutes). If the page says it can't connect, check that Solance is open and that a firewall or security tool isn't blocking local connections to `127.0.0.1`.
</details>

<details><summary><b>“Spotify didn't allow this access for the app” / error 403</b></summary>

Spotify apps in development mode only accept accounts that are allowed on the app. If you use a **different Spotify account** than the one that created the app, open your app in the dashboard → **Settings → User management** and add that account's name and e-mail. Then **Disconnect** and **Connect** again in Solance.
</details>

<details><summary><b>Search works but music doesn't play</b></summary>

- Playback control needs **Spotify Premium**.
- Open the **Spotify desktop app** on this PC at least once. Solance plays on this PC and will try to open Spotify for you.
- If you see “Spotify didn't start playing”, open the Spotify app, press play on anything, and try again from Solance.
</details>

<details><summary><b>“Session expired. Connect again.”</b></summary>

Go to **Settings → Spotify → Disconnect**, then connect again (you won't need to create a new app — the Client ID stays saved).
</details>

<details><summary><b>The shuffle button doesn't turn on Smart Shuffle</b></summary>

Spotify doesn't offer Smart Shuffle to other apps. Solance presses the button in the **Spotify desktop app** for you, so that app must be open on this PC.
</details>

## Disconnect, start over or remove access

- **Disconnect from Solance:** *Settings → Spotify → Disconnect*. This deletes the saved sign-in from your PC.
- **Revoke access on Spotify:** go to <https://www.spotify.com/account/apps/> and click **Remove access** next to your app.
- **Delete the app:** in the developer dashboard, open your app → **Settings** → **Delete app**.
- **Reset Solance completely:** close it and delete the `%AppData%\Solance` folder.

## What Solance can and can't do with your account

- It **reads** your playlists and liked songs, **searches** the catalog and **controls playback** on your devices (play, queue, volume, shuffle).
- It does **not** change, create or delete your playlists, and it does **not** post anything.
- Your sign-in token is stored **encrypted with Windows** and can only be read by your Windows user.

---

*Spotify is a trademark of Spotify AB. Solance is an independent project and is not affiliated with, sponsored by or endorsed by Spotify.*
