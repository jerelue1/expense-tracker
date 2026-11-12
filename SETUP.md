# Expense Tracker: one-time setup

About 15 minutes. Everything here is on free plans, and nothing asks for a credit card.

Replace `jerelue1` below with your GitHub username. Your site will be at `https://jerelue1.github.io/expense-tracker/`.

## 1. Create the Firebase project
1. Go to <https://console.firebase.google.com> → **Create a project** → name it `expense-tracker` → you can turn Google Analytics off → **Create**.
2. On the project home page, click the **Web** icon (`</>`) → nickname `expense-tracker` → **Register app**.
3. Copy the `firebaseConfig` values it shows (apiKey, authDomain, projectId, storageBucket, messagingSenderId, appId). These go into `index.html` (step 6).

## 2. Turn on sign-in
1. **Build → Authentication → Get started**.
2. **Sign-in method** tab → enable **Google**, choose your support email, then **Save**.
3. Also enable **Email/Password**, then **Save**. This is the fallback if the Google pop-up gets blocked on an iPhone/iPad home-screen app.
4. **Settings** tab → **Authorized domains** → **Add domain** → `jerelue1.github.io`.

## 3. Create the database
1. **Build → Firestore Database → Create database**.
2. Location: `asia-east2 (Hong Kong)` → **Next** → **Start in production mode** → **Create**.
3. Open the **Rules** tab, replace everything with the contents of `firestore.rules`, then **Publish**.
   This makes sure only you can read your own expenses.

## 4. Turn on the screenshot AI (Gemini)
1. **Build → AI Logic → Get started**.
2. Choose **Gemini Developer API** (the no-cost option) and follow the prompts to enable it.

## 5. Turn on App Check (Firebase requires it for the AI)
1. Enable the reCAPTCHA (Fraud Defense) API: <https://console.cloud.google.com/apis/library/recaptchaenterprise.googleapis.com?project=expense-20da1>. Free up to 10,000 checks a month.
2. Create a key: <https://console.cloud.google.com/security/recaptcha/create?project=expense-20da1>. Choose Website, domain `jerelue1.github.io`, and no checkbox challenge. Copy the **key ID**.
3. Firebase → **App Check → Apps** → your web app → **reCAPTCHA Enterprise** → paste the key ID → **Save**.
4. Put the key ID in `index.html` as `RECAPTCHA_SITE_KEY` (step 6).

## 6. Paste your keys into index.html
Near the top of `index.html`, replace the `PASTE_…` values:

```js
window.FIREBASE_CONFIG = {
  apiKey: "…",
  authDomain: "….firebaseapp.com",
  projectId: "…",
  storageBucket: "…",
  messagingSenderId: "…",
  appId: "…"
};
window.RECAPTCHA_SITE_KEY = "…";   // the reCAPTCHA Enterprise key ID
```

These values are safe to put in a public repo. The database rules and App Check are what protect your data.

## 7. Publish on GitHub Pages
Repo **Settings → Pages** → Source: **Deploy from a branch** → Branch `main`, folder `/ (root)` → **Save**.
The site is live in about a minute.

## Using it
- Sign in with the same account on your phone, iPad and laptop, and everything syncs automatically. It also works offline and syncs when you're back online.
- 📷 button: pick a screenshot (receipt, Octopus, PayMe, AlipayHK, bank app, delivery order…). It reads the amount, date, shop and category. Check them, then tap **Add**.
- On a laptop you can also **paste** a screenshot (Ctrl/Cmd + V) or **drag** it onto the page.
- On iPhone/iPad: Share → **Add to Home Screen** to open it like an app.

## If something goes wrong
- *"This website isn't allowed yet"*: redo step 2.4.
- *"App Check blocked the request"*: check that the domain in step 5.1 matches your site, and that the site key is pasted in step 6.
- *"The AI model name isn't available"*: Google retired the model. Change `AI_MODELS` near the top of `index.html` to current Gemini Flash models.
