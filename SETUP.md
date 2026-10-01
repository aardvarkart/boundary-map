# Conference Finder: setup guide

A free app that tells you which St. Vincent de Paul conference serves an address. It runs on iPhone, Android and desktop, installs to your home screen like an app, and lets an admin draw and update boundaries from inside the app. Total cost: $0.

## 1. Put the app online (about 10 minutes, once)

1. Create a free account at **github.com**.
2. Click **+** (top right) → **New repository**. Name it something like `svdp-map`, choose **Public**, and click **Create repository**.
3. On the new repository page, click **uploading an existing file**. Drag in *everything* from this folder (including the `icons` folder) and click **Commit changes**.
4. Go to **Settings → Pages**. Under "Build and deployment", set Source to **Deploy from a branch**, Branch to **main** and folder **/ (root)**, then **Save**.
5. Wait a minute or two and refresh. Your link appears at the top, like `https://yourname.github.io/svdp-map/`. That's your app.

## 2. Create your admin key (once)

The app saves boundary changes back to your repository, so it needs a key that allows that.

1. On GitHub, click your profile photo → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Name it "Conference Finder", set an expiration (a year is reasonable; you can make a new one later).
3. Under **Repository access**, choose **Only select repositories** and pick `svdp-map`.
4. Under **Permissions → Repository permissions**, set **Contents** to **Read and write**.
5. Click **Generate token** and copy it.

Open your app, tap **Admin**, and paste the token. It's stored only on that device. Do this on each device you want to edit from. Anyone else who should be able to edit needs their own token (or you can share yours privately).

## 3. Add your boundaries

- **Draw:** search an address to move the map, tap **Draw a new area**, then tap around the boundary. New points snap to neighboring borders so shared edges line up. Fill in the name, parish, help line, email and notes.
- **Import:** if your diocese or district council has parish boundary maps, use **Import file**. It accepts GeoJSON and KML (Google Earth and Google My Maps both export KML).
- **Reshape:** open an area and tap **Reshape boundary**. Drag points to move them, drag a faint midpoint to add one, right-click or long-press a point to remove it.
- **Publish:** edits are saved on your device as you go. Tap **Publish** when you're ready; everyone sees the change within about a minute.

## 4. Install it on a phone

- **iPhone:** open the link in Safari → Share → **Add to Home Screen**.
- **Android:** open the link in Chrome → menu → **Install app** (or Add to Home screen).
- **Desktop:** Chrome and Edge show an install icon in the address bar. Or just bookmark it.

## Good to know

- **Everything you publish is public**, because the repository and site are public. Use conference help lines rather than personal phone numbers. (Private GitHub Pages sites require a paid plan.)
- **Sharing a lookup:** `https://yourname.github.io/svdp-map/?address=123 Main St, Springfield IL` opens the app and checks that address.
- **Backups:** every publish is saved in the repository's history, so you can always roll back. **Export** also downloads a copy.
- **Free services used:** GitHub Pages (hosting), OpenStreetMap and CARTO (map), Photon and Nominatim (address search). These are free for a nonprofit's normal use.
- **Want it in the App Store later?** Apple charges $99/year and Google Play $25 once. Tools like PWABuilder.com can wrap this same app for the stores without rewriting it.
