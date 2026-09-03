# Escape Loop

A prototype of a **stakes layer** wrapped around a language-tutor conversation. The
learning loop on its own is a chat window and a number that goes up; the same loop
inside a casual-game shell is a scene where every answer moves something you can see.

Riz is ordering breakfast in a café in Kadıköy. Emre is behind the counter. The man
at the corner table is losing patience.

**Play it:** https://chris-w-k.github.io/turkish-proto/

## The mechanic

Two counters pulling opposite ways, both driven by the conversation:

- **Your order** is the progress bar. Every item you successfully ask for — çay, su,
  şeker, ekmek, börek, hesap — lands on the counter and stays there.
- **His patience** is the pressure. He takes **one step per turn, two if you answer
  wrong**. Nothing moves on a clock, so you can think for as long as you like.

Points scale with how much target language you had to produce unaided: comprehension
is worth +1, situational production +3. A hint costs half the points and removes one
wrong option. Three correct in a row surges — bonus point, and he gains no ground.

Past a third of his patience his hand drifts to his coat; past two thirds it's inside;
near the end you can see what he's holding. The loss is telegraphed three turns out.

### Endings

- **Out the door** — full order, paid up, Riz walks into the daylight.
- **He shoots** — cartoon violence, pixel blood. Default.
- **He takes the bag** — same tension, no gunfire. Toggle in the tuning panel; this is
  the one that would survive an under-12s age rating.

### Losing is a second chance

Get caught and the retry level is rebuilt from **only the words you missed**, with a
wider turn budget. It's spaced repetition wearing a rescue costume — the player never
sees a drill, they see another go, and they win it.

## What's faked, and what isn't

**Faked:** twelve hand-written turns, three tap-chips per answer, no model in the loop.

**Real:** the two counters, the point scale by interaction type, the surge rule, the
double cost of a miss, the rule-teaching repairs, the loss condition, and the
missed-atom retry construction. Those are the parts worth arguing about before anyone
builds an engine.

## Tuning

The panel beside the game changes order size, his patience and the starting head start,
and swaps the ending. Changes apply on the next run. Defaults are tuned so a player at
roughly 70% first-try accuracy finishes the order just as he arrives — the near-miss
band is the design target.

## Running it

One self-contained HTML file. No dependencies, no build step, no backend. Sound is
generated in the browser with WebAudio — square waves and filtered noise, no audio
files. Open `index.html`, or serve the folder with anything:

```bash
python3 -m http.server
```

## Notes

Browsers require a gesture before any audio can start, so the first tap on an answer
doubles as that gesture. There's a **Sfx** toggle in the top bar.

The player character is a simplified Riz, borrowed from
[long-way-home](https://github.com/chris-w-k/long-way-home).
