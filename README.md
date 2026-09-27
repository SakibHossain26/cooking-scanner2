# Cooking-scanner

Scan your ingredients — by typing them, or by taking/uploading a photo — and get a real recipe back, with the option to have it read aloud to you step by step.

This guide assumes you've never coded before and have none of this installed. Just follow the steps in order.

## Step 1: Download the project

1. Go to [github.com/SakibHossain26/cooking-scanner2](https://github.com/SakibHossain26/cooking-scanner2)
2. Click the green **`< > Code`** button, then click **"Download ZIP"**.
3. Find the downloaded ZIP file (usually in your Downloads folder) and extract it — right-click it and choose **"Extract All"** (Windows) or double-click it (Mac).
4. You should now have a folder called `cooking-scanner2-main`. Move it somewhere you'll remember, like your Desktop.

## Step 2: Install Node.js

This is the program that actually runs the app.

1. Go to [nodejs.org](https://nodejs.org)
2. Click the big green button that says **"LTS"** (it's the recommended version) to download it.
3. Open the downloaded installer and click **Next** through every screen, then **Install**, then **Finish**. The default settings are all fine — you don't need to change anything.
4. Restart your computer after it finishes installing (this matters — skipping this step causes confusing errors later).

## Step 3: Get your three API keys

The app talks to three outside services, and each one needs its own free key. Takes about 5 minutes total.

**1. Gemini key** (this is what looks at your photos and identifies ingredients)
- Go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
- Sign in with any Google account (Gmail account) you have.
- Click **"Create API key"**.
- A long string of letters/numbers appears — copy it somewhere safe (like a Notes app), you'll need it in Step 5.

**2. Spoonacular key** (this is what finds the actual recipes)
- Go to [spoonacular.com/food-api](https://spoonacular.com/food-api/console#Profile)
- Click **"Start Now"** or **"Sign Up"** and create a free account.
- Once logged in, your API key is shown right there on your profile/console page — copy it.
- Note: the free plan only allows 50 searches per day total, shared across whatever key you use.

**3. ElevenLabs key** (this is what reads the recipe out loud)
- Go to [elevenlabs.io](https://elevenlabs.io)
- Click **"Sign Up"** and create a free account.
- Once logged in, click your profile icon (top right) → **"Profile Settings"** → **"API Keys"**.
- Click to create a new key. It'll show a list of permissions/toggles — you only need to turn ON **"Text to Speech" → "Access"**. Leave every other toggle off.
- Copy the key it gives you.

You should now have three keys copied down somewhere. Don't paste them anywhere public (Discord, group chats, etc.) — treat them like passwords.

## Step 4: Add your keys to the project

1. Open the `cooking-scanner2-main` folder (the one from Step 1) in File Explorer / Finder.
2. Find the file named `.env.example`.
3. Copy it (Ctrl+C, Ctrl+V on Windows) and rename the copy to exactly `.env` — just that, nothing before or after it. Windows may warn you about changing a file extension; click Yes/Continue.
4. Right-click `.env` and open it with Notepad (or any plain text editor).
5. It'll look like this — replace each blank with the matching key you copied in Step 3:
   ```
   GEMINI_API_KEY=paste your Gemini key here
   MEALDB_API_KEY=1
   SPOONACULAR_API_KEY=paste your Spoonacular key here
   ELEVENLABS_API_KEY=paste your ElevenLabs key here
   ELEVENLABS_VOICE_ID=
   ```
   Leave `MEALDB_API_KEY` and `ELEVENLABS_VOICE_ID` exactly as they are — don't touch those two lines.
6. Save the file (Ctrl+S) and close it.

## Step 5: Run the app

1. Open the `cooking-scanner2-main` folder in File Explorer.
2. Click once in the address bar at the top (where the folder path is shown), type `cmd`, and press Enter. A black window (Command Prompt) will pop up already pointed at the right folder.
   - **Windows only, important:** if you use PowerShell instead of Command Prompt and see a red error mentioning "running scripts is disabled," that's a Windows security setting blocking it — just close it and use Command Prompt (the `cmd` trick above) instead.
3. In that black window, type this and press Enter:
   ```
   npm install
   ```
   Wait for it to finish (a minute or so, only needed the very first time).
4. Then type this and press Enter:
   ```
   npm start
   ```
5. Wait until you see a line like `Cooking scanner running at http://localhost:3000`.
6. Open your normal web browser and go to:
   ```
   http://localhost:3000
   ```
7. The app should load. Leave that black window open in the background the whole time you're using it — closing it shuts the app down.

## If something's not working

- **A red error mentioning a missing key**: open `.env` again and double-check all three keys were pasted in correctly (no extra spaces, nothing missing).
- **"Something went wrong" when finding a recipe**: the free Spoonacular plan caps out at 50 searches/day total — this resets the next day. If several people are testing with the same key, it runs out faster.
- **Photo scan doesn't find anything / seems stuck**: Google's Gemini service occasionally gets overloaded — the app automatically retries a couple of times on its own. If it still fails, wait a few minutes and try again; it's not something broken on your end.
- **PowerShell error about "running scripts is disabled"**: use Command Prompt instead (see Step 5).
