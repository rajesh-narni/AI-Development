# Claude Code & OpenRouter Integration Guide (Windows)

A step-by-step blueprint to configure **Claude Code** (both CLI and VS Code Extension) to route entirely through **OpenRouter's free tier**.

---

## 🛠️ Step 1: Install Claude Code on Windows

1. Open a new **PowerShell** window.
2. Install the native package globally by running:
   ```powershell
   winget install Anthropic.ClaudeCode
   ```
3. Restart your terminal, then verify the installation by typing:
   ```powershell
   claude --help
   ```

*(Note: If the command is not recognized, press `Win + R`, open `%USERPROFILE%\.local\bin`, copy that path, and add it manually to your system's User Environment Path variable).*

---

## 🔑 Step 2: Grab Your OpenRouter API Key

1. Navigate to the official [OpenRouter Dashboard](https://openrouter.ai).
2. Go to the **Keys** section and click **Create Key**.
3. Copy your unique token string (it will start with `sk-or-v1-...`).

---

## ⚙️ Step 3: Configure the Global Settings File

To make both your command line and your visual VS Code Extension route traffic together, you must update Claude's central configuration file.

1. Press `Win + R`, paste the following path, and hit **Enter**:
   ```text
   %USERPROFILE%\.claude\
   ```
2. Locate or create a file named exactly **`settings.json`**.
3. Open it with any text editor and paste the following complete structural block:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://openrouter.ai/api",
    "ANTHROPIC_AUTH_TOKEN": "sk-or-v1-YOUR-ACTUAL-OPENROUTER-KEY",
    "ANTHROPIC_API_KEY": "",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "openrouter/free"
  }
}
```

*⚠️ Important Details:*
* Swap `sk-or-v1-YOUR-ACTUAL-OPENROUTER-KEY` with your literal key string.
* Keep `"ANTHROPIC_API_KEY": ""` empty to bypass default Anthropic logins.
* Setting `"openrouter/free"` acts as an intelligent wildcard router to dynamic free endpoints without breaking on strict model naming constraints.
* Another free tier model is `"nvidia/nemotron-3-ultra-550b-a55b:free"`

---

## 💻 Step 4: Run via VS Code UI Extension Mode

1. Open your project folder inside **Visual Studio Code**.
2. Open the extensions marketplace (`Ctrl + Shift + X`) and install the official **Claude Code** extension.
3. Reload your active window (`Ctrl + Shift + P` -> type `Developer: Reload Window` -> press **Enter**).
4. Click the Claude Code icon on your left activity bar.
5. In the message window, type `/status` or `/model` to verify that your active base URL targets `openrouter.ai`.

---

## 📈 Step 5: Verification & Limits

* **Live Tracking**: Open the [OpenRouter Activity Wall](https://openrouter.ai/activity) in your browser to watch live credit tracking and processing tokens update in real time.
* **Daily Caps**: Free keys are limited to **50 requests per day**. Depositing a single \$10 balance down payment onto OpenRouter automatically scales your access tier to **1,000 requests per day** permanently for free models.
