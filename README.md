# Idea Lab

Turn a software idea into a sharper business hypothesis. Idea Lab investigates the customer’s job, compares alternatives, challenges the idea and narrows it into something you can test. Everything is in English, with three main tabs: **Workspace**, **Examples** and **How it works**.

[Try Idea Lab online](https://idea-lab-tau.vercel.app). Use your own OpenAI API key for research. Examples and How it works are available without a key.

![Workflow preview](preview.jpg)

- Choose **Automatic** or **Review each round**. Start with up to three rounds and extend an investigation to five rounds in total.
- Connect Jobs to Be Done, measurable requirements, competitors, counterideas and an evidence ledger.
- Learn from three worked examples featuring Uber Eats, Slack / Microsoft Teams and Calendly.
- Use an API online or an eligible subscription CLI locally, keep research in your browser and export an MVP implementation prompt.

## Quick start

Clone or download this repository. With Node.js 22 or newer installed, open the project folder and start the app:

```sh
git clone https://github.com/mcobo-cic/idea-lab.git
cd idea-lab
npm start
```

Open [http://localhost:3000](http://localhost:3000). The app has no npm dependencies. You can explore the worked examples immediately.

## Set up your AI in Settings

Open **Settings** and choose a provider. The online Vercel version uses the OpenAI API; local Node.js and Docker runs also support subscription CLIs.

- **OpenAI API:** enter your API key in the dedicated settings form and save it. Use the connection check to verify access without running a paid analysis. Research uses API billing; a ChatGPT subscription does not pay these API charges.
- **Codex / ChatGPT subscription, local only:** use an existing eligible ChatGPT login in the official Codex CLI installed alongside the server.
- **Claude subscription, local only:** use an existing eligible subscription login in the official Claude Code CLI installed alongside the server.

An installed CLI still needs a valid subscription login, available model access and quota. The app checks the reported login method when research starts. It does not silently switch a subscription provider to API billing.

**Local Node.js / Docker:** saved API credentials stay on the app server in `.data/settings.json`, with a private directory and owner-only file permissions. They are sent directly from Settings to the server, never saved in browser localStorage, returned in saved settings or included in research exports. A blank key field keeps the current key; the explicit remove action clears it and disables environment-key fallback. Restarting the app preserves saved settings. Keep this local server on your computer.

**Online Vercel:** each visitor supplies their own API key. Settings use an encrypted browser cookie that expires after 24 hours, with `HttpOnly` and `Secure` protections. The key is decrypted only on the server when needed and is never returned in settings responses, saved in localStorage or included in exports. Use Settings to remove the saved key. Online deployment setup is described below.

The connection check verifies authentication only. It does not promise that a particular model or research request will complete. Provider usage, plan limits and account permissions still apply.

## Use the Workspace

1. Describe the software idea, intended customer, market and what you want to learn.
2. Choose **Automatic** or **Review each round**. A new investigation starts with a budget of up to three rounds, with a maximum of five rounds across that investigation.
3. In Automatic mode, let the app continue while targeted research is useful. In Review each round mode, inspect the result and choose **Run round N** when you are ready. Continuing adds the next round to the same investigation and history.
4. Check the **analyzed idea**, the **proposed next idea**, what changed and what new information was found. Open the detailed JTBD, requirements, competition, counterideas and evidence when useful. A proposed direction still needs to be analyzed or tested.
5. When research reaches **Test** or **Stop**, gather a real finding before choosing **Refine with this finding**. Record what happened, its source and its limits; the app carries your observations and earlier findings into subsequent rounds.
6. Copy or download a test plan, including customer questions, or generate an MVP implementation prompt for the useful slice you want to build.

The latest **12 investigation groups**, including their completed rounds, are saved in this browser. Export JSON for a separate backup and import it to resume elsewhere. Browser profiles do not synchronize. Use **Resume** or **Retry** after an interruption to continue the investigation while keeping its saved rounds. An unfinished provider request may need to run again.

When you cancel, the app asks the active provider request to stop and keeps completed rounds. Provider usage already consumed remains consumed. Keep the app open during research. **Run round N**, Resume and Retry can make a new AI request; simply opening saved results does not.

## What the AI does

One selected AI provider performs two passes in each round, taking different research roles:

```mermaid
flowchart TD
  Idea[Your current idea] --> Customer[Pass 1: customer researcher]
  Customer --> Jobs[Jobs to Be Done and measurable requirements]
  Jobs --> Market[Pass 2: market researcher and skeptical reviewer]
  Market --> Alternatives[Competitors, counterideas and evidence]
  Alternatives --> Direction[Proposed direction and weakest assumption]
  Direction --> Decision{What would teach us something new?}
  Decision -->|Targeted research| Next[Continue or pivot within the round budget]
  Next --> Customer
  Decision -->|Customer behavior or payment needed| Test[Stop research and propose a real test]
  Decision -->|Fatal constraint or no useful next step| Stop[Stop and explain why]
```

The app carries the selected refinement, contrary evidence, source limits and observations from earlier rounds into the next round. Each result separates the idea actually analyzed from the proposed next direction, and explains what changed and whether any new evidence was found. Review each round pauses between these steps; Automatic continues within the chosen budget when further research is useful.

The budget is a maximum: the AI should stop earlier when another model response cannot resolve the decisive question. A Test or Stop decision asks for a real finding before re-examining the same premise. You can also use **Try a different direction** to select another proposed premise and research it in the same investigation. This changes the hypothesis; it does not establish demand. At the budget boundary, the app pauses so you can choose whether another round would be useful. The same investigation can contain at most five rounds.

A clever niche, few search results or repeated AI agreement does not establish demand. No loop can invent interviews, transactions or pilot results. Proposed success thresholds are experiment plans, not achieved results.

For the API path, source URLs are checked against URLs returned by native web search. Subscription CLI sources are labeled **provider-reported**; the app does not independently verify the CLI’s search transcript or whether every page supports every claim. A documented competitor capability can be a fact while demand for your concept remains a hypothesis.

## Learn from the Examples

Each case shows the broad starting idea, what existing products already do, the narrower business mechanism, who might pay, the biggest risk and a test that could kill the proposal. Opening an example starts at its first round. Choose **See round N** to follow its three-round learning path and inspect the details and sources. These are saved results: opening or stepping through them makes no AI call. You can also use an example’s suggested idea as a starting point for your own investigation.

- **Competing with Uber Eats:** move from another delivery app to a fixed weekly lunch-coordination service for three nearby offices. Compare configured group ordering and standing catering before assuming a gap.
- **Competing with Slack / Microsoft Teams:** move from another messenger to one shift-handover receipt, while keeping existing communication tools. Compare it with a shared checklist and require worker agreement.
- **Competing with Calendly:** move from paid booking links to preparation readiness for paid CV reviews. Keep the existing calendar and payment processor, and measure client friction alongside saved consultant time.

These are **curated worked examples with unvalidated demand**. They were authored as completed analysis walkthroughs; no customer interviews or pilots were performed. Product capabilities were checked on November 19, 2026 using [Uber Help](https://help.uber.com/en-GB/ubereats/restaurants/article/how-to-place-a-group-order?nodeId=886fdace-3cee-4658-9d3c-7cadfbec5280), [DoorDash Help](https://help.doordash.com/en-us/business/article/guide-to-group-orders), [Slack Help](https://slack.com/help/articles/203950418-Use-a-canvas-in-Slack), [Microsoft Support](https://support.microsoft.com/en-us/teams/shifts/schedule-staff-shifts), [Calendly Help](https://calendly.com/help/payments-faq) and [Google Calendar Help](https://support.google.com/calendar/answer/13762729?hl=en). Features and account eligibility can change.

## Test plan and MVP handoff

Copy or download a practical test plan from the saved research. It includes customer questions and the proposed experiment so you can gather a real finding before further refinement. The plan is assembled locally from the saved analysis; opening, copying or downloading it makes no AI call and does not run the experiment.

Generate, copy or download an implementation prompt from the chosen analysis. It includes the target customer, selected scope, linked JTBD and requirements, acceptance metrics, objections, validation experiment, credential handling, one-container setup and checks to run. A STOP decision gates building the rejected business.

The implementation prompt is also assembled from saved research without another AI call. Generating it does not execute it, build the MVP or deploy anything. Paste it into your preferred coding assistant when you are ready to implement the proposed test.

## Deploy to Vercel

The online version serves the same workspace, examples and explanation pages. Research uses each visitor’s OpenAI API key; the local subscription CLIs and `.data` credential file are not used online. Examples and How it works remain available without a key.

Import this repository into Vercel and add **`IDEA_LAB_SESSION_SECRET`** as a sensitive environment variable for each deployment environment you will use. Generate a value from at least 32 random bytes, for example:

```sh
node -e "process.stdout.write(require('node:crypto').randomBytes(32).toString('base64'))"
```

Keep the generated value in Vercel environment settings, outside the repository and public client configuration. Keep it stable across deployments in the same environment; changing it invalidates existing encrypted visitor cookies. Configure Preview as well as Production if both will accept saved visitor keys.

Do **not** configure an owner’s `OPENAI_API_KEY` on the public deployment. The online app requires a key from the individual visitor and does not use an owner-key fallback. There is no shared credential database: the encrypted cookie belongs to that browser and expires after 24 hours. API usage is billed to the account associated with the visitor’s key.

The deployment configuration uses Node.js 22, `npm run build:vercel` as the build command, `dist` for static output and `api/index.mjs` for API requests, with a 300-second function duration. Each research round is a separate request; a slow round can time out before the overall round budget is exhausted. Review the deployed `/api/status` and Settings connection check before running research.

Vercel Functions have a read-only application filesystem and temporary instance-local scratch space, so online settings use the encrypted session cookie rather than the local settings file. The configured duration fits the documented Hobby maximum with Fluid compute. See [Vercel runtime storage limits](https://vercel.com/docs/functions/runtimes#file-system-support), [function duration limits](https://vercel.com/docs/functions/configuring-functions/duration#duration-limits) and [deployment configuration](https://vercel.com/docs/project-configuration/vercel-json).

## Optional: subscription CLI setup

Install the official CLI in the same environment that runs the server and sign in there. The native CLI manages its own login; Idea Lab does not extract browser cookies or copy host tokens.

```sh
codex login
codex login status
```

ChatGPT sign-in provides eligible subscription access. See [OpenAI authentication](https://learn.chatgpt.com/docs/auth) and the [Codex CLI reference](https://learn.chatgpt.com/docs/cli/reference).

```sh
claude auth login
claude auth status --json
```

Claude Code supports eligible Pro, Max and Ultra subscriptions. See [Claude subscription setup](https://support.claude.com/en/articles/11145838-use-claude-code-with-your-pro-max-or-ultra-plan) and [programmatic Claude Code usage](https://code.claude.com/docs/en/headless).

Subscription subprocesses omit inherited API keys and token variables and require the official CLI to report a subscription login. Update the CLI if it rejects a safety or structured-output flag. Optional `CODEX_BIN`, `CLAUDE_BIN` and model settings are described in `.env.example`.

## Optional: run in one Docker container

Docker must be running. The image includes the UI, server and both official CLIs. Use dedicated named volumes for app settings and native CLI logins:

```sh
cd idea-lab
docker build -t idea-lab .
docker run --rm --name idea-lab -p 127.0.0.1:3000:3000 --mount type=volume,source=idea-lab-settings,target=/app/.data --mount type=volume,source=idea-lab-cli,target=/home/node idea-lab
```

Open the same local address and configure the API key through Settings. For a subscription provider, authenticate inside the running container using the supported provider flow:

```sh
docker exec -it idea-lab codex login --device-auth
docker exec -it idea-lab claude auth login
```

Follow the displayed browser instructions. Device login depends on account support. Keep these volumes private; they persist after the container is removed. Do not mount your host home directory or copy its credential files into the image. The app runs as a non-root user and includes a health check. To stop it, interrupt it or run `docker stop idea-lab`.

For a different local server settings directory, configure `IDEA_LAB_DATA_DIR`. On local runs, an optional `OPENAI_API_KEY` environment value is used when no saved choice overrides it. Settings can explicitly remove that fallback. To use environment configuration locally, copy `.env.example` to `.env` and restart; never include credentials in the image or source control.

## Verification and project files

```sh
npm test
```

Tests cover server and settings boundaries, mocked provider research, subscription preflight, credential isolation, process cancellation, evidence provenance, bounded iteration context, MVP prompt requirements and all nine example rounds. Test runs make no real model calls or quota charges. A live provider smoke check and a Docker build are separate checks; an installed CLI alone does not prove inference works.

```text
public/       English UI, tested loop runner, workflow helpers and curated examples
lib/          Analysis contracts, prompts and provider adapters
.data/        Private server settings, excluded from source and image
api/          Online Node.js API entrypoint
scripts/      Vercel static build helper
test/         Server, settings, provider and workflow tests
server.mjs    HTTP server and provider orchestration
Dockerfile    One-container runtime
vercel.json   Online build, API routing and function duration
.env.example  Configuration without credentials
```
