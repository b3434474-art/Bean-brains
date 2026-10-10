# Bean Brain: Gemini-powered meeting dialogue

The game keeps working in local mode without this backend. To turn on Gemini-generated bot discussion, deploy the Edge Function and paste its URL into **AI backend URL** in the game.

## Knowledge rules

Each bean gets a separate Gemini request. Gemini receives that bean's own secret team, personality, current room, personal sightings, personal suspicions, and the public meeting chat. It receives only the other players' names—not their secret teams, private sightings, suspicions, or current rooms. Meeting statements are public claims, not guaranteed facts. Beans must not invent things they did not personally see.

## Important safety notes

- Never put a Gemini API key in `index.html`, GitHub, or a browser setting.
- Keep `GEMINI_API_KEY` in Supabase Function Secrets only.
- API use may cost money or be subject to quotas. Have a parent/guardian help with setup and billing.
- The function has basic origin checking and an in-memory rate limit; these are not a substitute for production abuse protection.

## Setup

1. In [Google AI Studio](https://aistudio.google.com/), check Gemini API access and create an API key with a parent/guardian's help.
2. In a Supabase project, create an Edge Function named `bean-brain-ai` and replace its generated `index.ts` with `supabase/functions/bean-brain-ai/index.ts` from this repository.
3. In the Supabase dashboard, open Edge Function Secrets and add `GEMINI_API_KEY` with your Gemini key. Optionally set `GEMINI_MODEL`; the default is `gemini-2.5-flash`.
4. Deploy the function.
5. Copy its URL, usually `https://YOUR_PROJECT_REF.supabase.co/functions/v1/bean-brain-ai`.
6. Open [Bean Brain](https://b3434474-art.github.io/Bean-brains/), paste that URL into **AI backend URL**, and tap **Save AI endpoint**.
7. Start a match and trigger a meeting. The status will show whether AI dialogue connected. If it cannot connect, the game falls back to local character dialogue.

The endpoint accepts requests only from the configured GitHub Pages origin. If you host the game somewhere else, update `allowedOrigin` in the function to that exact origin before deploying.
