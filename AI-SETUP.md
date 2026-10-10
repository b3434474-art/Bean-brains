# Bean Brain: real AI meeting dialogue

The game keeps working in local mode without this backend. To turn on language-model-generated bot discussion, deploy the Edge Function and paste its URL into **AI backend URL** in the game.

## Important safety notes
- Never put an OpenAI API key in `index.html`, GitHub, or a browser setting.
- Keep `OPENAI_API_KEY` in Supabase Function Secrets only.
- AI API use can cost money. Have a parent/guardian help set up and monitor any API billing.
- The function has basic origin checking and a small in-memory rate limit; those are not a substitute for proper production abuse protection.

## Setup
1. In a Supabase project, create an Edge Function named `bean-brain-ai` and replace its generated `index.ts` with `supabase/functions/bean-brain-ai/index.ts` from this repository.
2. In the Supabase dashboard, open Edge Function Secrets and add `OPENAI_API_KEY` with the provider key. Optionally set `OPENAI_MODEL`; the default is `gpt-4o-mini`.
3. Deploy the function.
4. Copy its URL, usually `https://YOUR_PROJECT_REF.supabase.co/functions/v1/bean-brain-ai`.
5. Open Bean Brain, paste that URL into **AI backend URL**, and tap **Save AI endpoint**.
6. Start a match and trigger a meeting. The status will show whether AI dialogue connected. If it cannot connect, the game falls back to local character dialogue.

The endpoint only accepts requests with the exact GitHub Pages origin configured in the function. If you host the game somewhere else, update `allowedOrigin` in the function to that exact origin before deploying.
