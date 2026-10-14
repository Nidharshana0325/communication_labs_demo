# Communication Lab - Experiment 1: Meet and Greet

A small web lesson that teaches Indian school students (about Class 6 to 8) to **introduce themselves in English**.
The student listens, repeats, answers questions, and speaks aloud. The page gives simple feedback.

This is **one experiment** of a bigger set (15 planned). It is shared here so that others can help improve it.

- **One file:** the whole lesson is `index.html`.
- **No build step, no install, no API keys, no database.**
- Works best in **Chrome or Edge** (the microphone needs them).

---

## 1. Try it

**Quick way (VS Code):** install the "Live Server" extension, right-click `index.html`, choose **Open with Live Server**.

**Node way:** install Node.js (version 18 or newer), then in a terminal inside this folder:

    node local-server.js

Open http://localhost:3000

> Why not just double-click `index.html`? The microphone only works on `localhost` or `https`, so use one of the ways above.

---

## 2. What is in this repo

| File | What it is |
|---|---|
| `index.html` | The whole experiment: text, pictures, activities, style and code |
| `local-server.js` | A tiny local server so the microphone works on your computer |
| `vercel.json` | Tells Vercel to serve this as a plain website (needed for the free live link) |
| `.gitignore` | Files Git should ignore |
| `README.md` | This guide |

---

## 3. What the student does

The lesson has **8 stages**:

1. Introduction
2. Learn
3. Sound Lab
4. Practice
5. Kind Words
6. Real-Life Situations
7. Skill Check
8. Summary

The student can pick **basic** or **intermediate** level. Progress is saved in the browser, so a student can close the page and continue later.

---

## 4. How `index.html` is organised

Open `index.html` and use **Ctrl+F** to jump to these markers.

| Search for | What is there | Touch it if you want to... |
|---|---|---|
| `COMMON BLOCK START` | The shared engine: page layout, **CSS look**, voice, microphone, saving, step runner | change colours, fonts, buttons, spacing |
| `EXPERIMENT 1: DATA` | All the lesson text: towns, hobbies, questions, quiz items, tips | change or add sentences and questions |
| `EXPERIMENT 1: PICTURES` | Drawings made with inline SVG (no image files) | redraw or add pictures |
| `EXPERIMENT 1: ACTIVITIES` | The activity types (`speak`, `quiz`, `order`) and the `STEPS` list | add or reorder steps, make new activity types |
| `<style>` near the end | Extra CSS only for this experiment (mouth pictures, animation) | style experiment-only parts |

Everything the page draws lives inside one container, `<div id="cl-exp01-root">`. All CSS classes start with `cl-` so they do not clash with anything else.

---

## 5. How a step works

The lesson is a list called `STEPS`. Each step is one screen:

    {
      stage: 4,                       // which of the 8 stages (1 to 8)
      title: 'My, your, her, his',    // heading on the screen
      line: 'Choose one answer.',     // the one-line instruction
      gate: 1,                        // 1 = student must finish before Next works
      hint: 'Answer all 3 questions to go on.',   // shown while Next is locked
      render: function (box, S) {     // draws the activity inside `box`
        quiz(box, S, D.poss);         // D.poss = questions kept in the DATA section
      }
    }

Activity helpers (all in the ACTIVITIES section):

- `speak(box, S, items)` - student says a sentence; the page listens and gives feedback
- `quiz(box, S, items)` - choose the correct answer
- `order(box, S, list)` - tap words in the right order

`S` is the helper for the current step. Useful calls: `S.fb(...)` shows feedback, `S.done()` unlocks the Next button, `S.pic(...)` shows a picture.

Text such as `{name}`, `{age}`, `{town}` is replaced with the student's own details by the function `T(...)`.

**The page starts here (last line of the script):**

    CLab.run({ id:'exp01', label:'Experiment 1 of 15', welcome:'...', steps:STEPS })

---

## 6. How voice and microphone work

**Computer voice** (`CLab.say`). In this order:

1. If the device has an **Indian English voice** (for example Microsoft Neerja in Edge), use it.
2. Otherwise play **Google's Indian English text-to-speech** as a sound file. This is an unofficial endpoint and may be limited by Google at any time.
3. If that fails, use any English voice the browser has.

**Microphone** (`CLab.listen`). Uses the browser's own speech recognition with `en-IN` (Indian English). Needs Chrome or Edge, and internet.

**Checking what the student said** (`CLab.compare`). Compares the heard words with the target sentence and gives one of three bands: *Clear*, *Almost clear*, *Try once more*. It forgives small mistakes (one letter off, or common sound-alike words listed in `conf`).

**Known weak spot:** a computer voice with a true Indian accent on *every* device is hard to guarantee without a paid service. Ideas welcome (see section 9).

---

## 7. Saving progress

Progress is saved in the browser's `localStorage`, under keys that start with `clab.exp01.`
No data leaves the device. To reset, clear site data in the browser.

---

## 8. Rules to keep when you change things

These keep the lesson good for young learners:

1. **Simple English.** Short sentences. Everyday words.
2. **Indian setting.** Indian names, towns, and situations.
3. **Be kind.** Feedback should encourage, never shame.
4. **One thing per screen.** Do not crowd a screen.
5. **Easy to read.** Large text, strong contrast, buttons big enough to tap on a phone.
6. **Accessible.** Keep `aria-label` on buttons and pictures, and keep it usable with a keyboard.
7. **No extra files if possible.** Pictures are inline SVG so the whole lesson stays in one file.
8. **No keys, no sign-in, no tracking.**

Please do not edit inside `COMMON BLOCK` unless your change is about the shared look or engine. Other experiments in the full project use the same block.

---

## 9. Ways you can help

- **UI:** make it look friendlier and cleaner on small phones and big screens
- **Pictures:** better SVG drawings and small animations
- **Voice:** a reliable Indian English voice on all browsers, without a paid key
- **Content:** more situations, more hobbies, more towns, Hindi or regional hints
- **Accessibility:** screen reader check, keyboard check, colour contrast
- **Testing:** try it on different phones and browsers and report what breaks

---

## 10. How to contribute

1. Click **Fork** on GitHub.
2. Clone your fork and make a branch: `git checkout -b my-change`
3. Edit `index.html`. Test it with `node local-server.js`.
4. Commit and push: `git add .` then `git commit -m "what you changed"` then `git push origin my-change`
5. Open a **Pull Request** and say what you changed and why. A screenshot helps.

Not sure where to start? Open an **Issue** and ask.

---

## 11. Deploy your own copy (free)

Vercel: push to GitHub, **Add New, Project**, import the repo, preset **Other**, no environment variables, **Deploy**.

Do not add a `server.js` or `package.json` file. Vercel would try to run it as a server and the site would show "Not found".

---

## 12. Status

Working prototype. Tested on desktop Chrome and Edge. More phone and browser testing is needed.
