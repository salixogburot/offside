# Changelog

All notable changes to the offside quiz (`index.html`) are logged here, newest first.

## 2026-10-24 – Ball beside the player

### Changed
- The ball now sits to the right of the player (next to the circle, or next to the badge at the figure's front foot) instead of underneath.
- The ball line («Ballinje») now goes through the ball itself, in the quiz and on the rule cards.
- The ball is drawn on top of the target/second-last markers so it is never covered.
- Below-player tags on the rule cards moved up slightly, since the ball no longer sits underneath.
- Checked: for every scene, the drawn ball is on the same side of the target player as in the offside logic, in both figure and circle mode.

## 2026-10-24 – Football

### Changed
- The ball is now drawn as a classic football (black centre pentagon, seams and partial pentagons along the edge) instead of a plain white circle. It is a reusable `<symbol id="fig-ball">` in the sprite, used for the ball on the pitch, the faded "ghost" ball after the pass, the rule cards and the legend.
- The ball rolls (rotates) during the pass animation; it turns a whole number of times, so it lands without a jump when the answer is shown.
- Ball radius increased from 11 to 14, and the ball sits slightly lower under the player so it does not cover the team badge.
- The ghost ball is now the same football at 40 % opacity.

## 2026-10-23 – Illustrated players

### Added
- Players can be shown as illustrated figures (new default) instead of circles/squares. A toggle under the pitch, «Vis spillere som: Figurer / Sirkler», switches instantly (in-memory only, nothing is stored) and also redraws the rule cards on the end screen.
- Attackers (and our own keeper) use the running girl from `attack.svg`; defenders and their keeper use the figure from `defend.svg`.
- Each figure keeps a small team badge at its feet (blue circle «A1», red square «D1», yellow square «K»), so teams are still told apart by both colour and shape. Badges are drawn on top of all figures so they are never hidden.
- Target and second-last-defender markers become ellipses around the whole figure in figure mode.

### Changed
- Both illustrations are embedded in `index.html` (still a single file with no external dependencies):
  - `attack.svg` (15 tiled PNGs, 568 KB) was cropped and flattened to one transparent 227×330 PNG (~54 KB) embedded as base64.
  - `defend.svg` is embedded as a vector `<symbol>`, with the path data copied exactly; only the shirt colour is set by a CSS variable – red for defenders, yellow for their keeper (the original is blue, the same as our team).
- Figures are drawn back to front (by y), and vertical positions are clamped slightly so a figure on the sideline (throw-in) is not cut off. Offside logic only uses x, so this does not affect any answers.
- `index.html` grew from ~42 KB to ~121 KB.

## 2026-10-23 – Throw-in scene

### Added
- New scene 8 «Innkast» (the quiz now has 9 questions): A1 throws in from the top sideline directly to A2, who is ahead of both the ball and the second-last defender (D1). Answer: not offside, because you can never be offside directly from a throw-in.
- Context line «Innkast! A1 står på sidelinjen og kaster ballen rett til A2.», question «Innkastet tas NÅ. Er A2 offside?», and ball line shown after the answer.

### Changed
- The former scene 8 (offside variation) is now scene 9.

## 2026-10-23 – Rule cards carousel on end screen

### Added
- The three rules on the end screen are now illustrated cards in a carousel («Regel 1 av 3» …), each with a mini pitch in the same style as the quiz and a short caption:
  1. Foran ballen og nest bakerste: shaded orange «Offsideområde», offside line and ball line; A2 tagged «Offside», A3 tagged «Ikke offside».
  2. Bare på motstandernes halvdel: defenders deep on our half, offside area starts at the highlighted midline, «Aldri offside her» on our half.
  3. Med i spillet: A2 in the offside area but the pass goes to A3 («Ikke med = OK»), plus chips «Målspark», «Innkast», «Hjørnespark».
- Carousel navigation: ‹ / › buttons, dot indicators, swipe (scroll-snap) on touch, and arrow keys when the carousel has focus. Resets to the first card every time the end screen opens.
- `rules` data array (separate from `scenes`) so rule cards can be edited without touching the logic.

### Changed
- The plain numbered rule list on the end screen is replaced by the carousel; the end screen is slightly wider (780 px max).
- Drawing helpers reused by the cards: `drawPass()` takes a marker id, `drawBall()` can skip the `id`, new `drawLabel()` helper.

## 2026-10-23 – Animated pass

### Added
- The pass is animated after the user answers: the ball rolls from the passer to the receiver (smooth ease-in-out, duration scales with pass length, max ~1.4 s).
- Status text «Du svarte «…». Se på pasningen …» while the ball is moving.
- A faint dashed "ghost" ball marks where the ball was when the pass was played.
- Respects `prefers-reduced-motion`: the animation is skipped and the answer is shown immediately.

### Changed
- The correct answer, offside line, ball line and explanation are shown only once the pass is received.
- After the reveal the ball stays with the receiver; the ball line still goes through the ball's position at the moment of the pass.
- Feedback now repeats the user's choice: «Du svarte «Offside». Fasit: Offside.»
- Hint text for the ball line changed to «…viser hvor ballen var da pasningen ble spilt».

## 2026-10-23 – First version (MVP)

### Added
- Single-file quiz `index.html` with inline CSS and JavaScript, no dependencies, no data storage.
- Start screen, 8 scenes with progress indicator («Spørsmål X av 8»), and end screen with score and the three main rules.
- Landscape SVG pitch (`viewBox 0 0 1000 600`), attacking left to right, with «Angrepsretning →» indicator, «Vårt mål» / «Deres mål» labels and a legend.
- Players distinguished by colour and shape: blue circles (our team), red squares (defenders), yellow square (their keeper), blue circle «K» (our keeper).
- Dashed pass arrow, yellow ring around the target player.
- After answering: orange offside line through the second-last opponent (plus orange ring), ball line or highlighted midline where relevant, and explanation text.
- `scenes` data array separate from logic; `isOffside()` checks each scene and logs `console.warn` if it disagrees with `correct`.
- Responsive layout: pitch above panel in portrait, side by side in landscape; the pitch always fits on screen. Buttons at least 56 px high.
- Scene 7 (goal kick) shows the context line «Målspark! Keeperen vår sparker ballen rett til A2.»
