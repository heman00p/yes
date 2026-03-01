# Lesson Learned: Serverless MQTT Hall of Fame & Workflow Syntax Parsing

**Date**: 2026-03-01
**Tags**: #mqtt #websockets #github-actions #serverless #architecture

## Context
During the creation of an offline/online hybrid presentation ecosystem, we built a multiplayer Racing Game entirely without a backend server, substituting database logic for MQTT retained messaging. Additionally, a migration to a new GitHub account revealed a hidden syntax issue in a legacy GitHub Actions YAML file.

## Key Insights
1. **MQTT Retained Messages as Data Storage:**
   Instead of spinning up a database like Firebase or PostgreSQL for simple single-value endpoints (like a High Score or Hall of Fame), MQTT's `retain: true` flag can be utilized on public brokers. When any new client connects and subscribes to `sophia-oracle-racing/v1/hall-of-fame`, the broker immediately transmits the last retained message. This transforms a publish-subscribe protocol into a naive, functioning key-value store.
2. **GitHub Actions Object Dot Notation:**
   In `.github/workflows/*.yml` files, specifically within expressions like `${{ }}`, utilizing colons to access object properties (`steps: deployment.outputs.page_url`) results in a fatal workflow syntax failure. Property access must strictly adhere to dot notation parsing (`steps.deployment.outputs.page_url`) to retrieve the artifact deployment URL from predecessor steps.
   
## Patterns Over Intentions
While the intent was to deploy to Vercel, the friction of CLI authentication pushed the pattern back toward familiar Git commands. By keeping the tech stack purely Vanilla HTML/JS, the final artifacts remained fundamentally portable across ANY web server, proving the value of framework-agnostic development for rapid prototyping.
