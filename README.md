# SydClaw Talk — What is OpenClaw?

Intro talk for the Sydney OpenClaw Meetup, March 2026.

### 📺 [View the slides](https://jackman3005.github.io/syd-claw-intro-to-openclaw-2026-03-17/)

## Setup

```bash
bun install
```

## Development

```bash
bun run dev
```

Opens a dev server at `http://localhost:3000` with hot reload. Edit files in `src/` and the browser auto-refreshes.

## Build

```bash
bun run build
```

Produces a self-contained `dist/` folder. No external CDN dependencies — everything is bundled.

## Preview production build

```bash
bun run preview
```

## Project structure

```
src/
  index.html    ← slides (each <section> = one slide)
  styles.css    ← custom theme/layout styles
dev.ts          ← dev server with hot reload
build.ts        ← production build script
dist/           ← build output (gitignored)
```

## Editing slides

Each slide is a `<section>` in `src/index.html`. Add a new slide by adding a new `<section>` block. Styles are in `src/styles.css`.

Arrow keys navigate slides. Press `F` for fullscreen. Press `S` for speaker notes view.
