# Setup guide (about 60-90 minutes, no credit card)

You need: a Google account, a GitHub account, and a computer with a browser.
Menu names in the Firebase console change from time to time; if a button has moved, look for the closest wording.

## 1. Create a Firebase project

1. Go to <https://console.firebase.google.com> and sign in with your Google account.
2. Click **Create a project** (or **Add project**) and give it a name, for example `nosql-chat-demo`.
3. **Turn off Google Analytics** (it is not needed and slows you down).
4. Stay on the free **Spark** plan. Never upgrade: the demo needs no paid feature.

## 2. Add a Web app and copy the config

1. On the project home page, click the **`</>`** (Web) icon.
2. Give the app a nickname (for example `chat`). Do **not** tick "Firebase Hosting".
3. Firebase shows a `firebaseConfig` object. Copy it. It looks like this:

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project",
  storageBucket: "your-project.firebasestorage.app",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef"
};
```

These values are public by design. They are not secrets.

## 3. Create the Firestore database

1. In the left menu: **Build > Firestore Database > Create database**.
2. Choose **Native mode** (the default).
3. Pick a region close to you (any region works).
4. Choose **Start in production mode** (not "test mode": test mode expires after 30 days).

## 4. Publish the security rules

1. Open the **Rules** tab of Firestore.
2. Delete everything in the editor and paste the content of `firestore.rules`.
3. Click **Publish**.

## 5. Paste your config into `index.html`

1. Open `index.html` in any text editor.
2. Find the line `// PASTE YOUR CONFIG HERE`.
3. Replace the placeholder values below it with the values you copied in step 2.
4. Save the file.

## 6. The `settings/room` document

The app creates it for you the first time the **host** opens the page (`?host=1`), with `open = false`.
If you prefer to create it by hand: in the **Data** tab, click **Start collection**, collection ID `settings`, document ID `room`, field `open`, type **boolean**, value `false`.

## 7. Test on your computer

Browsers do not run ES modules from `file://`, so use a tiny local server:

1. Open a terminal in the `nosql-chat-demo` folder.
2. Run: `python -m http.server 8000` (or `python3 -m http.server 8000`).
3. Open <http://localhost:8000/?host=1> in one tab (host).
4. Open <http://localhost:8000/> in a second tab (audience).
5. Check: the audience tab is locked ("Waiting for the host to open the chat..."). Click **Open chat to audience** in the host tab, then send messages from both tabs.

## 8. Deploy on GitHub Pages

1. On GitHub, create a new **public** repository, for example `nosql-chat-demo`.
2. Upload `index.html`, `firestore.rules`, `SETUP.md` and `README.md` (the **Add file > Upload files** button works).
3. Go to **Settings > Pages**. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, then **Save**.
4. Wait about 1 minute. Your link will be `https://YOUR-USERNAME.github.io/nosql-chat-demo/`.

(Alternative: drag the folder onto <https://app.netlify.com/drop>.)

## 9. Make the QR code

1. Open any free online QR code generator.
2. Paste the **public** link (without `?host=1`!).
3. Download the image and put it on your last slide.

## 10. Open the host link

On the presenter's laptop, open:

```
https://YOUR-USERNAME.github.io/nosql-chat-demo/?host=1
```

Bookmark it. Never show this link to the audience.
