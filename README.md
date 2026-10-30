# AI CAPTCHA — Verify you are a robot

An experimental **reverse CAPTCHA** concept: instead of asking visitors to prove they are human, the page asks them to solve structured, machine-style challenges and displays **ROBOT VERIFIED**.

## Live demo

If GitHub Pages is enabled for this repository, open:

https://lordlolqdh.github.io/ai-captcha/

## Features

- Mobile-first dark interface with a technical green status display
- Randomized logic, structured JSON, pattern and checksum challenges
- Retry feedback, session ID, attempts/solved counters and a local verification receipt
- No dependencies, build step, API key, database or server required
- All challenge checking happens in the browser; no answer data is transmitted

## Run it

Open `index.html` in a browser, or enable GitHub Pages in the repository settings and choose the `main` branch as the publishing source.

## Important security limitation

This is a **demo, not a security-grade CAPTCHA**. Because challenge answers are checked in client-side JavaScript, users can inspect the answers or modify the page. A successful result does not prove that the visitor is an AI agent. Do not use this prototype to protect accounts, payments, private content, or APIs.

For real integrations, verification must happen on a server: generate unpredictable challenges, keep expected answers secret, expire and consume each challenge once, and issue short-lived signed tokens only after verification. Even then, challenge solving alone cannot reliably prove that a client is an AI.

## Project status

Prototype v0.1 — front-end demo.
