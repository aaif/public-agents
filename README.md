# AAIF Public Agents

This repository contains public, reusable agent resources for AAIF, including skills, recipes, prompts, and agent-facing workflows.

## Repository Structure

```text
public-agents/
├── skills/
│   └── ...
├── recipes/
│   └── ...
├── prompts/
│   └── ...
└── docs/
    └── ...
```

## Contents

- `skills/` — Agent Skills for reusable domain expertise, brand guidance, workflows, and tool-specific instructions.
- `recipes/` — Repeatable agent workflows and task definitions.
- `prompts/` — Reusable prompts and prompt templates.
- `docs/` — Supporting documentation for contributors and users.

## Usage

Start with the relevant directory for what you need:

- Looking for installable agent capabilities? See `skills/`.
- Looking for repeatable workflows? See `recipes/`.
- Looking for reusable prompt templates? See `prompts/`.

## GitHub Actions Workflows

Manually-triggered workflows in `.github/workflows/` that call LLM APIs.

### `copilot-test-action`

Calls the **GitHub Models** inference API (`https://models.github.ai`) using the built-in `GITHUB_TOKEN`. Lists all available model IDs from the catalog, then sends a "hello world" prompt to whichever model you pick.

**Requirements:**
- The org must have **GitHub Models** enabled in **Org Settings → Models**. Without this, inference returns `403` even though the catalog endpoint works.
- Workflow uses the org-scoped endpoint (`/orgs/{org}/inference/chat/completions`).

**No secret setup required** — `GITHUB_TOKEN` is provided automatically.

### `gemini-test-action`

Calls the **Google Gemini API** directly with your own API key. Sends a "hello world" prompt to a configurable Gemini model and prints the response.

#### Setup: storing the Gemini API key

1. Get a key from [Google AI Studio](https://aistudio.google.com/apikey).
2. Add it as a repository secret named `GEMINI_API_KEY`:
   - Go to **Repo → Settings → Secrets and variables → Actions → New repository secret**
   - **Name:** `GEMINI_API_KEY`
   - **Secret:** *(paste the key)*
   - Click **Add secret**

That's it. The workflow reads it from `${{ secrets.GEMINI_API_KEY }}` and passes it via the `x-goog-api-key` header (never in the URL, so it won't appear in logs or referrer headers).

#### Running it

1. Go to **Actions → gemini-test-action → Run workflow**.
2. Pick a model (default `gemini-2.5-flash`; other options include `gemini-2.5-pro`, `gemini-2.0-flash`, `gemini-1.5-pro`, `gemini-1.5-flash`).
3. Click **Run workflow**.

The log will show the HTTP status, raw JSON response, and the extracted text output.

#### Scoping the secret

For tighter blast radius, you can store `GEMINI_API_KEY` in a [GitHub Environment](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment) instead of repo-wide secrets, then add `environment: <name>` to the job. Useful if you later want approval gates or want different keys for different branches.
