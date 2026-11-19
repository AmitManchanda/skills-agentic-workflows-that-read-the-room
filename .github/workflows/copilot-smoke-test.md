---
name: copilot-smoke-test
description: Minimal Copilot SDK inference test.

on:
  workflow_dispatch:

permissions:
  contents: read
  copilot-requests: write

strict: true

engine:
  id: copilot
  copilot-sdk: true
  model: gpt-5.6

safe-outputs:
  noop:
---

# Copilot smoke test

Use noop with the reason "Copilot inference test succeeded".
