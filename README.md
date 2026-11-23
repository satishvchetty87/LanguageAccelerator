# Rewrite & Translate

A small web app with two tools:

1. **Tone rewriter**: paste English, pick a tone (professional, direct, friendly, casual, confident, empathetic, persuasive, formal, apologetic, concise) or type your own ("polite but firm"), and get a rewrite that sounds like a person wrote it.
2. **Telugu → English**: paste Telugu script, romanized Telugu ("nenu repu vastanu"), or Tenglish, and get natural English. You can optionally pick a tone for the English too.

Uses Claude (`claude-opus-5-5` by default) through the Anthropic API.

## Run it locally

Needs Node 18+ and an Anthropic API key from https://console.anthropic.com.

```bash
cd LanguageAccelerator
npm install
cp .env.example .env        # then put your key in .env
npm start
```

Open http://localhost:3000. Ctrl/Cmd + Enter submits.

To use a cheaper, faster model, set `CLAUDE_MODEL=claude-sonnet-5-5` in `.env`.

## How "human tone" is enforced

The system prompt in `server.js` (`HUMAN_STYLE`) bans common AI tells (delve, leverage, seamless, em-dashes, "I hope this email finds you well"), asks for plain words and varied sentence length, and forbids adding facts or sign-offs that weren't in the original. Edit that block to tune the voice.

## Password

Set `APP_PASSWORD` and the browser asks for a username and password before showing anything. Type anything as the username. After 20 wrong passwords from one IP, that IP is blocked for 15 minutes. When `NODE_ENV=production`, the app refuses to serve pages if `APP_PASSWORD` isn't set, so it can't go online unprotected by accident.

## Deploying to Render (free)

1. Merge the pull request into `main`.
2. Open https://render.com/deploy?repo=https://github.com/satishvchetty87/LanguageAccelerator and sign in with GitHub.
3. Render reads `render.yaml` and asks for two secrets: `ANTHROPIC_API_KEY` and `APP_PASSWORD`. Fill them in and click **Deploy**.
4. After a few minutes you get a link like `https://language-accelerator.onrender.com`.

The free plan sleeps after 15 minutes without visits, so the first load after a break takes about a minute.
