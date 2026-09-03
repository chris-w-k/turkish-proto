# Escape Loop

A prototype of a **stakes layer** wrapped around a language-tutor conversation. The
learning loop on its own is a chat window and a number that goes up; the same loop
inside a casual-game shell is a scene where every answer moves something you can see.

**Level 1: Ordering at the Café.** Riz is ordering breakfast in a backstreet café in
Kadıköy. Emre is behind the counter. The man at the corner table is losing patience.

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
near the end you can see what he's holding. Whatever happens at the end, you had three
turns of warning.

### Endings

- **Out the door** — full order, paid up, and the man from the corner table turns out
  to have been reaching for something other than what you feared.
- **He shoots** — cartoon violence, pixel blood.
- **He takes the bag** — same tension, no gunfire. Set `CFG.soft = true` in the script
  to swap it in; this is the version that would survive an under-12s age rating.

### Losing is a second chance

Get caught and the retry level is rebuilt from **only the words you missed**, with a
wider turn budget. It's spaced repetition wearing a rescue costume — the player never
sees a drill, they see another go, and they win it.

## Sound

Everything is synthesised in the browser with WebAudio. There are no audio files.

The background bed is an 8-bar loop in **D Hicaz** — the makam whose augmented second
between E flat and F sharp is what makes it read as Turkish rather than as generic
chiptune. A 25% pulse wave carries the melody over a root-and-fifth drone, with a very
quiet darbuka pattern underneath. It ducks when the man from the corner table walks
over, swells when he produces the flowers, and cuts dead on the gunshot.

## What's faked, and what isn't

**Faked:** twelve hand-written turns, three tap-chips per answer, no model in the loop.

**Real:** the two counters, the point scale by interaction type, the surge rule, the
double cost of a miss, the rule-teaching repairs, the loss condition, and the
missed-atom retry construction. Those are the parts worth arguing about before anyone
builds an engine.

## Tuning

Near the top of the `<script>` block:

```js
var CFG = { goal:20, patience:16, start:2, soft:false };
```

Pressure is `turns + misses`; he arrives at `patience`. The defaults are tuned so a
player at roughly 70% first-try accuracy finishes the order just as he gets there —
the near-miss band is the design target, not an accident.

Music level is `MUS.vol`; the melody itself is the `MEL` array, in beats.

## Running it

One self-contained HTML file. No dependencies, no build step, no backend. Open
`index.html`, or serve the folder with anything:

```bash
python3 -m http.server
```

## Notes

Browsers require a gesture before any audio can start, so the **Start** button on the
title screen doubles as that gesture. There's an **Sfx** toggle in the top bar, which
mutes the music too.

The player character is a simplified Riz, borrowed from
[long-way-home](https://github.com/chris-w-k/long-way-home).
