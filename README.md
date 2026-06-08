# IELTS Recovery Lab 🌱

A personal practice tool built to help improve IELTS band scores by training the correct spelling, grammar patterns, vocabulary, and listening paraphrases — without ever showing the wrong version.

> **Philosophy:** Don't collect mistakes. Collect correct patterns.

---

## Why This Exists

Most vocabulary apps are generic. This one only contains the exact words, phrases, and patterns *you* have personally missed in IELTS practice. That makes it far more effective than any off-the-shelf app.

After every practice test, you add what you missed — correctly spelled, correctly phrased. The app trains your memory on those specific gaps until they're mastered.

---

## Features

### 🏠 Dashboard
- At-a-glance stats: Total patterns, Mastered, Learning, New
- Recently added patterns with category badges and growth level

### ➕ Add Pattern
- Save only the **correct** version of a word or phrase
- Four categories: **Spelling**, **Grammar**, **Vocabulary**, **Paraphrase / Listening**
- Optional hint or note (e.g. "double letters", "means moved from place to place")
- All data saved to `localStorage` — no backend, no login

### 🎯 Daily Practice
- **See it → Hide it → Type it** — the word appears for 3 seconds, then disappears
- You type it from memory, building the correct neural path
- Filter by category to focus on weak areas
- Each session picks up to 15 patterns, prioritising lower streaks
- Correct answers build your streak; wrong answers reset it to zero

### 🌱 Garden (Progress View)
- Every pattern is a growing plant based on your streak:
  - 🌰 New (streak 0)
  - 🌱 Learning (streak 1–2)
  - 🌿 Growing (streak 3–6)
  - 🌳 Mastered (streak 7+)
- Progress bars show the breakdown across all levels

### ⚔ Weekly Boss Fight
- All your patterns, no hints, no previews
- Type them all from memory
- Score shown at the end, streaks updated
- Use this every Sunday as your weekly review

---

## Getting Started

No installation needed.

1. Download `ielts-recovery-lab.html`
2. Open it in any browser
3. Start adding patterns from your last IELTS practice test

That's it.

---

## How to Use It Well

**After every practice test**, open the app and add what you missed:

| What you missed | What to add | Category |
|---|---|---|
| Spelled *transfered* | `transferred` | Spelling |
| Forgot the article | `a quarter` | Grammar |
| Missed the paraphrase | `follow rules` (= "don't smoke") | Paraphrase |
| Didn't recall the word | `promptly` | Vocabulary |

**Every day**, run a practice session. 10–15 minutes is enough.

**Every Sunday**, run the Boss Fight. No hints. Full recall.

---

## Data Structure

Each pattern stored in `localStorage` looks like this:

```json
{
  "id": "abc123",
  "word": "transferred",
  "cat": "spelling",
  "note": "double letters",
  "streak": 4,
  "added": 1718000000000
}
```

Categories: `spelling` | `grammar` | `vocab` | `paraphrase`

---

## Roadmap / Planned Features

- [ ] Export / import patterns as JSON (for backup)
- [ ] Dark/light theme toggle
- [ ] Paraphrase pair training (see phrase → type its IELTS equivalent)
- [ ] Weekly streak history chart
- [ ] Django backend for multi-device sync
- [ ] Spaced repetition scheduling

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript (vanilla) |
| Storage | `localStorage` |
| Fonts | DM Serif Display, DM Mono, Outfit (Google Fonts) |
| Backend (planned) | Django + Django REST Framework |

No frameworks. No build tools. No dependencies. One file.

---

## Migrating to Django (Later)

When you're ready to add a backend, the migration is straightforward. The data model maps directly to a Django model:

```python
class Pattern(models.Model):
    CATEGORIES = [
        ('spelling', 'Spelling'),
        ('grammar', 'Grammar'),
        ('vocab', 'Vocabulary'),
        ('paraphrase', 'Paraphrase'),
    ]
    word    = models.CharField(max_length=200)
    cat     = models.CharField(max_length=20, choices=CATEGORIES)
    note    = models.TextField(blank=True)
    streak  = models.IntegerField(default=0)
    added   = models.DateTimeField(auto_now_add=True)
```

To export your existing data from the browser:

```js
// Run this in the browser console
console.log(localStorage.getItem('ielts_lab_v1'))
```

Paste the output into a migration script and POST it to your Django API.

---

## Contributing

This is a personal tool, but PRs and suggestions are welcome — especially if you're also preparing for IELTS and have ideas that would help.

---

## License

MIT — use it, modify it, share it freely.
