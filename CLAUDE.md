# Spelling App — Project Spec

## Overview
A kid-friendly spelling learning app built as a single-page React application. Kids select their profile, pick a lesson, and practice spellings through three modes: Practice, Dictate, and Type.

## Tech Stack
- **React** (single `.jsx` or `.html` file, self-contained)
- **Web Speech API** for text-to-speech (browser built-in, no external dependencies)
- **localStorage** for persistence (profiles + progress tracking)
- **Tailwind CSS** or inline styles for styling

## App Flow
```
Profile Select → Lessons List → Lesson View (3 tabs)
```

---

## Screens & Features

### 1. Profile Select Screen (App Entry)
- Shows existing kid profiles as tappable name cards
- "Add New" button → simple text input to type a name
- Delete option per profile (small X icon on each card)
- No passwords, no signup — just tap a name to enter
- Profiles stored in localStorage

### 2. Lessons List Screen
- Flat list of lessons: "Lesson 1", "Lesson 2", etc.
- Each lesson shows Type tab completion status for the current kid (checkmark if completed)
- Back/logout button to return to profile select

### 3. Lesson View Screen
- **Header:** Back button + Lesson title (e.g., "Lesson 1")
- **Tab bar:** Three tabs in this exact order: **Practice · Dictate · Type**
- **Card area:** Centered word card (large, prominent)
- **Word counter:** e.g., "3 / 10"
- **Navigation:** Prev (◀) and Next (▶) arrow buttons

#### Tab: Practice
- Card displays the **word in large text**
- Play button (🔊) to hear the word via Web Speech API
- Kid can replay as many times as they want
- Navigate between words with Prev/Next
- No tracking, purely passive learning

#### Tab: Dictate
- Card does **NOT** show the word — only the play button (🔊)
- Word counter shown (e.g., "Word 3 of 10")
- Kid listens, writes on physical paper, taps Next when ready
- **End screen:** After the last word, reveal ALL words in a list so parents can check against the paper
- No tracking

#### Tab: Type
- Card does **NOT** show the word — only the play button (🔊)
- Text input field below the card for typing the spelling
- Submit button to check the answer
- **If correct:** Green checkmark animation/highlight, "Next" button appears
- **If incorrect:** Red highlight, correct answer displayed on the card, "Next" button appears
- Kid manually presses "Next" to advance (NO auto-advance)
- **End screen:** Shows final score (e.g., "You got 7 out of 10")
- **Progress saved:** Mark lesson as completed for this kid profile in localStorage

---

## Lesson Data Structure

All lessons are defined in a single clearly marked section at the top of the code for easy editing.

```javascript
// ===== ADD YOUR LESSONS HERE =====
const LESSONS = [
  {
    name: "Lesson 1",
    words: ["apple", "house", "water", "happy", "school", "friend", "mother", "garden", "purple", "silver"]
  },
  {
    name: "Lesson 2",
    words: ["bridge", "church", "planet", "forest", "winter", "basket", "candle", "pocket", "rabbit", "sunset"]
  },
  // Add more lessons by copying the pattern above
];
// ===== END LESSONS =====
```

Include **2 starter lessons** with 10 words each. Choose common English words with moderate difficulty (suitable for ages 6-10).

---

## Progress Tracking

- **Only tracked for the Type tab**
- Per-kid, per-lesson completion stored in localStorage
- Data structure example:
```json
{
  "profiles": ["Ali", "Sara"],
  "progress": {
    "Ali": { "lesson_0": { "completed": true, "score": "8/10" } },
    "Sara": { "lesson_0": { "completed": false } }
  }
}
```
- Lessons List screen shows a checkmark (✅) next to completed lessons for the active kid

---

## Visual Style

- **Clean but friendly** — not overly cartoonish, not too minimal
- Soft, muted colors (light backgrounds, pastel accents)
- Rounded corners on cards and buttons
- Large, readable font for words on cards
- Big tap targets (kid-friendly)
- Subtle transitions/animations for feedback (correct/incorrect)
- Responsive — should work well on both tablet and phone screens
- No emojis overload, but a few tasteful icons (🔊 for play, ✅ for done)

---

## Audio / Speech

- Use `window.speechSynthesis` (Web Speech API)
- Speak the word in English
- Use a clear, moderate-speed voice
- Allow replaying the word by tapping the play button again
- In Type and Dictate modes, optionally auto-play the word when it first appears

---

## Key UX Details

1. **No auto-advance anywhere** — kid always presses Next manually
2. **Play button always visible** in all three tabs — kid can re-hear the word anytime
3. **Dictate end screen** shows numbered word list (1. apple, 2. house, ...) for parent checking
4. **Type feedback** stays on screen until kid presses Next — gives them time to study the correct spelling if wrong
5. **Keyboard should auto-focus** the input field in Type mode for quick typing
6. **Case-insensitive** comparison for Type mode answers

---

## File Structure
Single self-contained file. All code, styles, and data in one file for simplicity.

---

## Out of Scope (Not needed)
- No user accounts / authentication / signup
- No backend / server
- No database (localStorage only)
- No admin panel for managing lessons (edit the code directly)
- No word-by-word progress history
- No stars / badges / gamification
- No multi-language support
- No animations beyond simple feedback
