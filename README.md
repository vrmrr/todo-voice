# todo-voice

Two small pages for the [Sukoon](https://github.com/vrmrr/gmauto) phone app (every ask handled, peace of mind):

- `voice.html` (**Add Task**, teal-to-green 🎤 icon): a one-tap voice button.
- `launcher.html` (**Sukoon**, blue-to-teal ✓ icon): a home-screen icon that opens Sukoon straight away. Google's
  own page can only show a grey "G" icon, because Google controls its page head.

`icons/` holds the icons (SVG sources and PNGs at 180, 192 and 512 px, plus maskable versions);
`manifest-todo.json` and `manifest-voice.json` describe the two home-screen apps.

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

The manifests deliberately have no `start_url`: the home-screen icon then opens the page exactly as it was added,
including `#app=<your link>`, so the link works even where home-screen apps get their own empty storage (iPhone).

## Use

In the Sukoon app, tap ⚙︎ → **📲 Home-screen icons** → **✓ Sukoon** or **🎤 Add Task**; the page opens with your link
filled in. Then **Add to Home Screen**. (Or open `https://vrmrr.github.io/todo-voice/launcher.html` or `…/voice.html`
and paste your app link once.) Full guide: `docs/phone-setup.md` in the main repo.
