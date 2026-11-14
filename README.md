# todo-voice

Two small pages for the [Sukoon](https://github.com/vrmrr/gmauto) phone app (every ask handled, peace of mind):

- `voice/` (**Add Task**, ink square with an aurora-gradient 🎤 icon): a one-tap voice button, styled to match
  the Sukoon app's design (`docs/design/sukoon-ui.html` and `docs/design/sukoon-brand.html` in the main repo).
  `voice.html` at the old location is only a redirect to `voice/` (keeps old install links and the app's own
  Settings button working) — moved into its own folder in v1.8.1 so Android treats it as a separate installable
  app, not a page inside Sukoon's installed scope.
- `launcher.html` (**Sukoon**, ink square with the leaf): a home-screen icon that opens Sukoon straight away, and
  the app's own splash screen while it loads. Google's own page can only show a grey "G" icon, because Google
  controls its page head.

`icons/` holds the icons (SVG sources and PNGs at 180, 192 and 512 px, plus maskable versions) and `leaf.svg`,
the logo symbol; `manifest-sukoon.json` and `manifest-addtask.json` describe the two home-screen apps.

Leaf artwork: Google Noto Emoji (Apache 2.0).

You tap, speak, and the page opens your own Sukoon app with your words (`…/exec?add=<text>`). The app's quick-add does
the rest (deadline, who asked, type).

Why it exists: the Sukoon app runs inside Google's Apps Script frame, which does not allow the microphone. This page runs
outside that frame, so the browser's speech recognition works.

## This repository holds no data

- No server, no database, no analytics, no external scripts, fonts or images (enforced by a Content-Security-Policy).
- Your app link is kept only on your phone: in the page address after `#` (never sent to any server) and in the
  browser's local storage.
- Only links to Google Apps Script web apps (`https://script.google.com/…/exec`) are accepted, so the page can't be
  pointed at anything else.
- Speech is turned into text by your phone's own speech service (Apple on iPhone, Google on Android), the same as the
  keyboard microphone. The text then goes, over HTTPS, to your own Sukoon app.

Each manifest has its own `id` and a `scope` naming a distinct folder (`/todo-voice/launcher` for Sukoon,
`/todo-voice/voice` for Add Task), so Android installs them as two separate apps instead of treating the
second as already covered by the first's scope. The manifests deliberately have no `start_url`: the home-screen
icon then opens the page exactly as it was added, including `#app=<your link>`, so the link works even where
home-screen apps get their own empty storage (iPhone).

## Use

In the Sukoon app, tap ⚙︎ → **📲 Home-screen icons** → **✓ Sukoon** or **🎤 Add Task**; the page opens with your link
filled in. Then **Add to Home Screen**. (Or open `https://vrmrr.github.io/todo-voice/launcher.html` or `…/voice/`
and paste your app link once.) Full guide: `docs/phone-setup.md` in the main repo.
