# todo-voice

One page, `voice.html`: a one-tap voice button for the [AI To-Do Assistant](https://github.com/vrmrr/gmauto) phone app.

You tap, speak, and the page opens your own To-Do app with your words (`…/exec?add=<text>`). The app's quick-add does
the rest (deadline, who asked, type).

Why it exists: the To-Do app runs inside Google's Apps Script frame, which does not allow the microphone. This page runs
outside that frame, so the browser's speech recognition works.

## This repository holds no data

- No server, no database, no analytics, no external scripts, fonts or images (enforced by a Content-Security-Policy).
- Your app link is kept only on your phone: in the page address after `#` (never sent to any server) and in the
  browser's local storage.
- Only links to Google Apps Script web apps (`https://script.google.com/…/exec`) are accepted, so the page can't be
  pointed at anything else.
- Speech is turned into text by your phone's own speech service (Apple on iPhone, Google on Android), the same as the
  keyboard microphone. The text then goes, over HTTPS, to your own To-Do app.

## Use

Open `https://vrmrr.github.io/todo-voice/voice.html` on your phone (Safari on iPhone, Chrome on Android), paste your
To-Do app link once, then **Add to Home Screen** as "Add To-Do". Full guide: `docs/phone-setup.md` in the main repo.
