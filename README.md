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

## Deploying

It's a plain Express app, so any Node host works (Render, Railway, Fly.io, a VPS). Set `ANTHROPIC_API_KEY` as an environment variable on the host. Note there's no login or rate limiting, so anyone with the URL can spend your API credits; add auth before sharing it publicly.
