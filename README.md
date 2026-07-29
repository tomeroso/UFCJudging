# Scorecard — score an MMA fight while you watch it

A single-page tool for keeping your own judge's scorecard during a fight. Hold a key while a fighter is in control, score each round under the 10-point must system, and see how your card reads at the final bell.


<!-- TODO: replace the URL above with your real Pages URL once deployed.
     TODO: add a screenshot — the scorecard mid-fight with a few rounds filled in. -->

No install, no server, no dependencies. One HTML file.

---

## How it works

| Key | Action |
|---|---|
| `Space` | Start / pause the round clock |
| `F` (hold) | Red corner in control |
| `J` (hold) | Blue corner in control |

Enter both fighters' names, pick 3 or 5 rounds, and start the clock. Hold `F` or `J` while that fighter is controlling the exchange — the meter fills toward whoever is holding. When the round ends, the app shows how the control time split and you assign the score: 10-9, 10-8, or 10-10. The scorecard fills in round by round and gives a final decision.

`F` and `J` are the home-row index-finger keys, so you can score without looking at the keyboard — which is the point, since you're supposed to be watching the fight.

## Design notes

**Control time is a prompt, not a verdict.** Judges weigh effective striking, effective grappling, aggression, and octagon control — control time is one input among several, and the app never scores a round for you. It reports what it measured and leaves the decision to you.

**One meter, not two.** The first version had a separate progress bar per fighter. But the question a judge is actually asking isn't "how much control did each fighter have," it's "who had more." A single bar splitting red against blue answers that in a glance, which matters when your attention is on the fight and not the screen.

**Hold, don't tap.** An earlier version incremented the bar on each `keydown` event, which meant the fill rate was really measuring the operating system's key-repeat interval rather than elapsed time — different on every machine. Control is now accumulated against a fixed tick between `keydown` and `keyup`.

**Red and blue corner** are the actual UFC convention, so the palette is the sport's own rather than something invented for the page.

## Running locally

Open `index.html` in a browser. That's it.

To deploy your own copy: fork, then Settings → Pages → deploy from the `main` branch.

## History

This started as an ASP.NET Web Forms project. The scoring logic was all client-side JavaScript, while Web Forms posts back to the server on every button click — which wiped that state on each interaction. The framework was working against what the app did. Rewriting it as a static page removed the conflict, cut the dependencies to zero, and made it hostable for free.

## Roadmap

- [ ] Persist the card to `localStorage` so a refresh doesn't lose it
- [ ] Per-round notes against the four official judging criteria, not control time alone
- [ ] Compare-to-the-judges mode: enter the official card for a real fight and diff it against yours
- [ ] Touch controls so it works on a phone

## Licence

MIT
