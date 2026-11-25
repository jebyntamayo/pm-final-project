# Spotlight Curated Rail, Simplified PRD (StreamLine)

**Author:** Me · **Status:** Draft · **Target:** High-Fidelity Prototype · **Persona:** Tom, 52, a former StreamLine subscriber

## 1. The Big Picture
- **Vision:** To eliminate the "warehouse" feeling for StreamLine viewers like Tom by putting a trusted, human-picked shortlist in front of them, so every evening starts with something worth watching.
- **Press release:** Today, StreamLine launched Spotlight, a hand-picked rail at the top of the homepage where our curators choose a short list of films worth your evening. After years of adding thousands of titles, we heard the same thing from viewers who had stopped coming back: a bigger library didn't make their nights better, and "it became a warehouse." Spotlight changes that by putting a named human curator behind every pick, so you can skip the endless scroll and press play.

"We stopped asking viewers to search a catalog of 15,000 titles and started giving them something worth watching," said the StreamLine product team. Spotlight rolls out first as a pilot, with picks refreshed weekly, and it's built so that existing browsing stays exactly as it is for the viewers who love it.
- **Success metric:** Month 1 retention of Wanderers exposed to Spotlight: from about 65% to 74% or higher.
- **Guardrail:** Power Users' sessions per week: hold at 4.8×, with no more than a 5% drop.

## 2. The Details
### User stories
- As Tom, a former subscriber, I want a short list of films picked by a named curator so that I don't have to scroll through thousands of titles.
- As Tom, I want to see who chose each film so that I can trust the pick.
- As Tom, I want to start a pick in one or two taps so that my evening isn't spent deciding.
- As a Power User, I want my usual homepage rows to stay in place so that my browsing isn't disrupted.
- As a curator, I want to change the picks each week without engineering help so that the rail stays fresh.
### Screens to build
- Home: the existing homepage with the Spotlight rail near the top (5-8 picks, "This week's picks" header, curator byline), with the usual rows below it.
- Core: the pick detail screen, showing the film's artwork, the curator's name and one-line note, and a Play button.
- Confirmation: a "Now playing" screen confirming the pick has started, with an option to return to Spotlight for the next pick.
### Functional requirements
- The system must show the Spotlight rail in the top two positions of the homepage, above the existing rows.
- The system must display between 5 and 8 hand-picked titles, in the order the curator set.
- The system must show the curator's name on the rail and on each pick's detail screen.
- The system must let a user start playback within 2 taps of opening the homepage.
- The system must leave all existing homepage rows unchanged in content and order.
- The system must let a curator replace the picks through a config file, with no code deploy.
- The system must log rail impression, pick click, play start, and 30+ minute session events.
### Smart behaviors (Situation → Outcome)
- If a user taps a pick → the system opens its detail screen with the curator's note.
- If a user taps Play → the system starts playback and shows the confirmation.
- If a curator updates the picks → the rail shows the new set on the next page load.
- If the rail has fewer than 5 titles → the system hides the rail so a thin shelf doesn't appear.
- If a user is in the holdout group → the system doesn't show the rail.
- If a user finishes a pick → the system offers the next Spotlight title.
### Technical constraints
- No external API calls and no database; use mock data (a hard-coded list of 5-8 titles and curator names) and React useState only. No AI or personalized ordering, no login, no filters or mood picker, no payments, no real video playback (use a placeholder), and no more than 3 screens.

## 3. The Logistics
### Features out
- No AI or personalized ordering, no "Why You'll Love This" labels, no mood picker, no advanced filters, no curator profiles or follow, no Watch Party, no Offline Download, no Digest Email, no login or settings, no real video playback.
### Edge cases & safety guard
- Fewer than 5 titles in the rail → hide the rail instead of showing a thin shelf.
- A title is missing artwork or curator info → skip that card and keep the rest of the rail.
- A user is in the holdout group → don't show the rail at all.
- A curator picks the same title twice → show it once.
- Safety: never invent a curator, a curator note, or a title that isn't in the approved list; never reorder or remove the existing homepage rows.
### Decision log
- Removed the AI "Why You'll Love This" label and personalized queue to keep the rail human-curated, which is what Tom's quote asks for, and to avoid algorithmic work inside a 3-week sprint.
- Made the rail additive and moved the Digest Email to Next so that Power Users' sessions (4.8×) stay protected and the team stays focused on one build.
### Evals
- Accuracy: 100% of rail titles come from the curator's approved list, and 100% show a curator name.
- Time-on-task: a user can start playing a pick within 2 taps and under 30 seconds of opening the homepage.
- Safety: 0 changes to the existing homepage rows, and 0 rails shown to holdout users.

## MoSCoW scope
- **Must:** Human-picked rail near the top of the homepage, bypassing the algorithm; Short, fixed set of titles (5-8); Curator byline as the trust signal; Added to the homepage without replacing existing rows (protects Power Users); Tap to title page or play, mobile first; Titles editable weekly without a deploy; Feature flag with a holdout group; Tracking: impression, click, play start, 30+ min session
- **Should:** One-line curator note per title; Hidden Gem Badge tag; "This week's picks" header with refresh date; Placement variants to test Power Users impact
- **Could:** Add to watchlist from the rail; Rotating themes or multiple curators; Auto-expiry of old picks; Trailer previews
- **Won't (now):** AI or personalized ordering (A5) and "Why You'll Love This" labels (A2); Mood picker (A4), advanced filters (A9); Curator profiles (A7); Watch Party (A8), Offline Download (A10); Digest Email (A6, it's a Next item); Full curation CMS, ratings and reviews, localization

---
**Builder hook:** Build a working prototype based on this PRD. Use the User Story as the core flow, Functional Requirements as build constraints, and prioritize speed and clarity over visual complexity.
