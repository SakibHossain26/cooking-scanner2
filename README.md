# Cooking-scanner

Scan your ingredients — by typing them, or by taking/uploading a photo — and get a real recipe back, with the option to have it read aloud to you step by step.

## What you need before you start

- A computer (Windows, Mac, or Linux)
- [Node.js](https://nodejs.org) installed — download the "LTS" version, run the installer, click Next through everything (defaults are fine).
- [Git](https://git-scm.com/downloads) installed — same deal, click Next through everything.
- Three free API keys (see below). Nothing in the app works without these — they're what let it talk to Google's AI, the recipe database, and the voice service.

## 1. Get the code

Open a terminal (Windows: search "PowerShell" in the Start menu. Mac: search "Terminal"), then run:

```
git clone https://github.com/SakibHossain26/cooking-scanner2.git
cd cooking-scanner2
```

## 2. Get your API keys (one-time)

You need three. All free:

1. **Gemini** (identifies food in photos) — go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey), sign in with a Google account, click "Create API key".
2. **Spoonacular** (finds recipes) — go to [spoonacular.com/food-api](https://spoonacular.com/food-api/console#Profile), sign up for a free account, your key is on your profile page. Free accounts get 50 requests/day.
3. **ElevenLabs** (reads recipes aloud) — go to [elevenlabs.io](https://elevenlabs.io), sign up, go to Profile Settings → API Keys, create a new key. When it asks about permissions, only turn on **Text to Speech: Access** — leave everything else off.

## 3. Set up the project (one-time)

1. In your terminal, inside the `cooking-scanner2` folder, run:
   ```
   npm install
   ```
   (Downloads everything the app needs — takes a minute.)
2. Find `.env.example` in the project folder, make a copy of it, and rename the copy to exactly `.env`.
3. Open `.env` in any text editor (Notepad is fine) and paste your keys in:
   ```
   GEMINI_API_KEY=your-gemini-key-here
   MEALDB_API_KEY=1
   SPOONACULAR_API_KEY=your-spoonacular-key-here
   ELEVENLABS_API_KEY=your-elevenlabs-key-here
   ELEVENLABS_VOICE_ID=
   ```
   Leave `MEALDB_API_KEY` and `ELEVENLABS_VOICE_ID` exactly as shown above.
4. Save the file.

**Never share your `.env` file or paste its contents anywhere public** (Discord, GitHub, chat, etc.) — those keys work like passwords for your accounts. `.env` is already set up to be ignored by git, so it won't get uploaded by accident.

## 4. Run it

Every time you want to use the app:

1. Open a terminal in the `cooking-scanner2` folder.
2. Run:
   ```
   npm start
   ```
3. Wait for `Cooking scanner running at http://localhost:3000`.
4. Open that link in your browser.
5. When you're done, go back to the terminal and press `Ctrl+C` to stop it.

## Using the app

- Type ingredients into the box, or click "Take a photo" / "Upload a photo" to scan them instead.
- Click **Find my recipe**.
- Click **See the full recipe** for the full ingredient list and steps.
- Click the ▶ button to have it read the recipe aloud, one step at a time.

## If something's not working

- **Nothing loads / errors about a missing key**: double-check `.env` has all three real keys pasted in correctly, then stop (`Ctrl+C`) and restart (`npm start`).
- **"Something went wrong" when finding a recipe**: Spoonacular's free plan caps out at 50 requests/day — this resets daily.
- **Photo scan fails**: Gemini's servers occasionally get overloaded; the app automatically retries and falls back to a backup model, but if it's a widespread outage it may take a bit — try again in a few minutes.
