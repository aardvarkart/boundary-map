# Conference Finder: setup guide

A free app that tells you which St. Vincent de Paul conference serves an address. Works on iPhone, Android and desktop, installs to the home screen like an app, and lets approved admins draw and update boundaries from inside the app with a normal email sign-in. Changes go live instantly. Total cost: $0.

Two free services do the work: **Firebase** (Google) stores the boundaries and handles sign-in, and **GitHub Pages** hosts the app. Setup takes about 25 minutes, once.

## 1. Create the Firebase project (about 10 minutes)

1. Go to **console.firebase.google.com** and sign in with a Google account. Click **Create a project**, name it (e.g. "svdp-map"), and turn off Google Analytics when asked. No credit card is needed; the free "Spark" plan is plenty.
2. **Turn on sign-in:** in the left menu choose **Build → Authentication → Get started**. Under "Sign-in method", enable **Email/Password** and save. (Optionally also enable **Google** so admins can use their Google accounts.)
3. **Create the database:** choose **Build → Firestore Database → Create database**. Pick the location nearest you, choose **Start in production mode**, and create.
4. **Set the security rules:** open the **Rules** tab, delete what's there, paste the entire contents of `firestore.rules` from this folder, and click **Publish**. These rules make the map public to read but editable only by approved admins.
5. **Make yourself the first admin:** in the **Data** tab, click **Start collection**. Collection ID: `admins`. Document ID: your email address, all lowercase. Add one field: name `addedBy`, value `setup`. Save. (Every later admin can be added from inside the app.)
6. **Get the config:** click the gear icon → **Project settings**. Under "Your apps" click the **</>** (web) icon, name the app "Conference Finder", skip hosting, and click **Register app**. You'll see a block starting with `const firebaseConfig = {`. Copy everything between the braces.
7. Open `firebase-config.js` from this folder in any text editor (Notepad, TextEdit) and replace the placeholder values with the ones you copied. Save.

## 2. Put the app online with GitHub Pages (about 10 minutes)

1. Create a free account at **github.com**.
2. Click **+** → **New repository**. Name it `svdp-map`, keep it **Public**, click **Create repository**.
3. Click **uploading an existing file**, drag in *everything* from this folder (including the `icons` folder and your edited `firebase-config.js`), and click **Commit changes**.
4. Go to **Settings → Pages**. Set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**, and **Save**.
5. After a minute or two, refresh. Your link appears at the top: `https://yourname.github.io/svdp-map/`.
6. **Allow sign-in from that address:** back in Firebase, go to **Authentication → Settings → Authorized domains → Add domain** and add `yourname.github.io`.

Open the link, tap **Admin**, choose **Create account** with the email you added in step 1.5, and you're in.

## 3. Add your boundaries

- **Draw:** search an address to move the map, tap **Draw a new area**, then tap around the boundary. Points snap to neighboring borders so shared edges line up. Fill in the name, parish, help line, email and notes. Everything saves as you type.
- **Import:** if your diocese or council has parish boundary files, use **Import file**. It accepts GeoJSON and KML (Google Earth and Google My Maps both export KML).
- **Reshape:** open an area and tap **Reshape boundary**. Drag points to move them, drag a faint midpoint to add one, right-click or long-press a point to remove it. Tap **Done** to save.
- **Add admins:** Admin → **Admins** → enter their email. They then create their own account on the sign-in screen with that same email.

## 4. Install it on a phone

- **iPhone:** open the link in Safari → Share → **Add to Home Screen**.
- **Android:** open the link in Chrome → menu → **Install app**.
- **Desktop:** Chrome and Edge show an install icon in the address bar.

## Good to know

- **The map is public.** Anyone with the link can look up addresses and see conference names, phone numbers and notes. Use help lines, not personal numbers. (Only admins can edit.)
- **Sharing a lookup:** add `?address=123 Main St, Springfield IL` to the link to open the app with that address already checked.
- **Backups:** use **Export** now and then to download a copy of all boundaries.
- **Lost password:** use "Forgot password?" on the sign-in screen. To remove an admin, use the Admins list in the app, or Authentication in the Firebase console.
- **Free limits:** Firebase's free plan allows 50,000 reads a day, far beyond what a conference lookup tool will use. Map tiles are from OpenStreetMap; address search uses Photon and Nominatim. All free for a nonprofit's normal use.
- **Want it in the App Store later?** Apple charges $99/year and Google Play $25 once. PWABuilder.com can wrap this same app for the stores without rewriting it.
