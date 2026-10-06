---
title: Smart Vinyl Player
---

# Smart Vinyl Player

**Sai Porumamilla** · User Interface I, Project 1

[**Try the live app**](https://sai-porumamilla.github.io/UI-Project_1/) · [Source code on GitHub](https://github.com/sai-porumamilla/UI-Project_1) · [Demo video](#demo-video)

![The master page: device UI on the left, testing panel on the right](images/overview.png)

## The project

A record player that keeps everything people love about vinyl, the physical record, the platter and the needle, while adding a digital display and sensors. A touchscreen faces forward on the front of the player, below the turntable and between the left and right speakers. Two physical knobs sit on top at the front right corner: one for volume and one for the playback mode (33⅓ RPM, 45 RPM or Bluetooth).

Sensors inside the player watch its own health: belt and platter speed, stylus cleanliness, air quality, vibration, audio clipping and tonearm level. They also recognize which song is playing. A companion phone app shows that health and turns the detected plays into a library and listening stats.

The mock-up has two interfaces, chosen from one master page:

1. **Player display**: the touchscreen on the front of the player.
2. **Companion app**: the phone app paired with the player.

Both interfaces are fixed at a **1.41 : 1** ratio, the ISO A-series paper ratio (√2). The display is landscape and the phone is portrait.

---

## Design

### Affordances and physical properties

> **TODO (Sai):** Describe the object's physical properties, referencing the Design of Everyday Things slides. For example: it's large and fixed, it sits on a shelf or console, it isn't portable, the tonearm invites being grabbed, the knobs invite turning, and the touchscreen faces you at standing height.

### Assumptions about the smart features

These are the sensing features the interface assumes. They should be feasible, but how they would be built is out of scope.

| Sensor | What it detects | How the UI uses it |
|---|---|---|
| Platter speed sensor | Whether the platter is turning and how far it is from 33⅓ or 45 RPM | Belt & platter speed card in the app |
| Stylus sensor | Debris build-up, tracked as hours played since the last cleaning | Stylus cleanliness card and stylus lifetime bar |
| Air quality sensor (PM2.5) on the side of the player | Whether the room is dusty | Air quality card, with a tip to keep the lid closed |
| Vibration sensor | Vibration reaching the platter, for example from nearby speakers | Vibration card |
| Audio clipping detector | Distortion from the stylus mistracking | Stylus clipping card |
| Tonearm level sensor | Whether the arm is parallel to the record | Tonearm level card |
| Tonearm proximity sensor | A hand reaching for the arm while the needle is down | Hands-off warning on the display |
| Song recognition | Which song and record are playing | Now Playing info and the app's listening history |
| Knob encoders | Volume and mode knob positions | Volume meter and mode overlays on the display |

### User needs and design requirements

> **TODO (Sai):** Check these against your interviews and add or adjust as needed.

| User need | Design requirement |
|---|---|
| Control playback without handling the tonearm and risking the record | The display offers play/pause, previous/next and scrubbing, and warns the user away from the arm while the needle is down |
| Know what is playing from across the room | When left alone, the display fades to large album art with the song, artist and album |
| Sing along | The display shows time-synced lyrics |
| Get clear feedback when turning a physical knob | The display shows the new volume on an arched meter, or the new mode's name and symbol |
| Know when the player needs care before sound quality suffers | The app gives one overall health rating plus a card per sensor, with a fix for anything Fair or Poor |
| Show off the collection, including special editions | The app has a collection view with vinyl colors and a filter for special editions |
| See listening habits | The app shows a day-by-hour heatmap, top artists and totals, built from automatically detected plays |

### Interviews

> **TODO (Sai):** The 3 interviews: your questions, who you talked to (no identifying details), what you learned, and how it changed the design. Add photos or video of them using a record player if you have them.

### Sketches

> **TODO (Sai):** Add images and short captions for:
> - 10-plus-10 sketches for 3 design challenges
> - The vanilla sketch of the interface
> - Storyboard
> - Hybrid sketch showing the interface on a real record player

### Feedback on the vanilla sketch

> **TODO (Sai):** Feedback from the 3 people who reviewed your vanilla sketch, and what you changed because of it.

---

## The interface

### Master page

A switch at the top chooses **Player display**, **Companion app** or **Side by side**. Below the device sits a front-view drawing of the player that highlights where the current interface lives. The **Testing UI** panel holds the project info, an info button that explains the simulation, and controls that stand in for physical actions.

![Side-by-side view, with the testing panel underneath](images/side-by-side.png)

**Testing UI controls**

| Control | What it simulates |
|---|---|
| Volume knob slider | Turning the physical volume knob |
| Mode knob (33⅓ RPM / 45 RPM / Bluetooth) | Turning the physical mode knob |
| Reach for tonearm | A hand near the tonearm while a song plays |
| Owner profile (Maya, Jordan, Sam, Pat) | Loads a different owner's sensor readings, collection and listening history into the app |

### Player display

**Now Playing.** Play/pause, previous/next, ±10-second skips and a scrub bar. A record peeks out behind the album art and spins at the selected speed, so 45 RPM visibly spins faster than 33⅓.

![Now Playing on the player display](images/display-playback.png)

**Idle mode.** If nobody touches the Now Playing screen for 8 seconds, it fades to large album art with the song, artist and album names, readable from across the room. One tap brings the controls back.

![Idle mode](images/display-idle.png)

**Synced lyrics.** The line being sung is highlighted and kept centered, Apple Music / Spotify style. Tapping a line jumps the song to it. Lyrics come from [LRCLIB](https://lrclib.net), a free synced-lyrics database.

![Synced lyrics](images/display-lyrics.png)

**Hands off the tonearm.** Lifting the needle mid-song can scratch the record, so the display steers people to a safer action:
- **Signifier:** while the needle is down, a strip along the bottom says not to lift the arm and to tap pause instead.
- **Feedback:** if the proximity sensor detects a hand near the arm, a full-screen warning appears with a large, pulsing pause button. Pausing dismisses it.

![Tonearm warning](images/display-needle-warning.png)

**Physical knobs.** The display reacts whenever either knob turns:
- **Volume knob:** an arched panel meter with the new value. The arc turns orange above 85.
- **Mode knob:** the mode's name and symbol. 33⅓ RPM is an LP disc, 45 RPM is a disc with the wide single-record centre, and Bluetooth uses the standard Bluetooth symbol.

| Volume knob | Mode knob |
|---|---|
| ![Volume meter](images/display-volume.png) | ![Mode overlay](images/display-mode.png) |

### Companion app

A mini player at the top controls the same player as the touchscreen. The header shows the connection and the current knob settings.

**Health.** One headline rating out of four tiers (**Excellent / Good / Fair / Poor**), computed from six sensors. Each sensor card shows its reading, its own tier and a four-segment bar. Anything Fair or Poor also shows how to fix it. The overall rating is the average of the sensors, but a single Poor sensor caps it at Fair so a serious problem can't hide behind good readings. Every tier pairs its color with a symbol and a label, so the rating doesn't depend on color alone.

| Excellent (Maya) | Poor (Pat) | Sensor cards |
|---|---|---|
| ![Excellent health](images/phone-health-excellent.png) | ![Poor health](images/phone-health-poor.png) | ![Sensor detail](images/phone-health-sensors.png) |

**Library.** The collection shows each record as a disc in its actual vinyl color, with special and limited editions starred and a filter to show only those. Insights shows hours listened, songs spun, the day streak, songs the player detected this session, a day-by-hour heatmap (hover a cell for the count) and top artists.

| Collection | Insights | Heatmap & top artists |
|---|---|---|
| ![Collection](images/phone-collection.png) | ![Insights](images/phone-insights.png) | ![Heatmap](images/phone-insights-heatmap.png) |

### Why a companion app (Option 2)

The touchscreen is for the moment of listening: it is big, glanceable and right next to the record. Health and history are different jobs. You check them occasionally, often when you're not near the player, and they need more room than a playback screen should give up. The phone handles those, and also works as a remote.

The two stay connected in both directions. The phone's play/pause and next buttons drive the player. The player's current song, playing state, knob settings and detected plays all show up on the phone. The **Side by side** view makes this visible.

### Why the sensor data matters (Option 3)

Most turntable problems are invisible until they audibly damage the sound or the records: a slipping belt, a dirty stylus, a tilted tonearm. The health screen turns them into one rating with specific fixes, so owners can act before it gets that far. The four owner profiles show the range:

| Profile | Situation | Health |
|---|---|---|
| Maya | Audiophile collector with a dedicated listening room | Excellent |
| Sam | First turntable, weekend afternoon listener | Good |
| Jordan | College dorm, with the player sharing a desk with a subwoofer | Fair: dusty air, high vibration, dirty stylus |
| Pat | Inherited player set up in a garage workshop | Poor: slipping belt, worn stylus, tilted arm, clipping |

The library and listening stats come from the same sensing. Because the player recognizes what is playing, collectors get stats.fm-style insights for physical records without logging anything.

---

## Implementation

- **Svelte 5 + JavaScript, built with Vite.** Components use Svelte 5's runes (`$state`, `$derived`, `$effect`).
- **One shared player state.** `player.svelte.js` holds a single audio element and one reactive state object: track, playing, time, volume, mode, owner profile and detected plays. The touchscreen, the phone and the testing panel all read and change this one object, which is what keeps the two devices in sync.
- **Physical inputs as events.** A knob turn or a hand near the tonearm sets a fresh event object in that state. The display watches for it and shows a timed overlay.
- **Lyrics.** Fetched at runtime from LRCLIB's free API and parsed from LRC format (`[mm:ss.xx] line`). LRC only times whole lines, so highlighting is line by line. A per-song offset can re-sync lyrics if they drift from the audio.
- **Data.** The four owner profiles, sensor thresholds and tier rule live in `scenarios.js`. Each heatmap is generated from that owner's peak listening hours.
- **Charts.** All hand-built with SVG and CSS, with no chart library: the volume meter, the health arc, the sensor bars, the heatmap and the top-artist bars. The health tiers use a fixed status palette, always paired with a symbol and a label.
- **Checks and hosting.** A small Node test (`npm test`) covers the lyric parsing and the health-tier logic. A GitHub Actions workflow tests, builds and deploys the app to GitHub Pages on every push.

---

## Future work

- **Letter-by-letter lyrics.** The original design highlighted lyrics down to each letter. That needs word- or syllable-level timing, which LRCLIB doesn't provide.
- **Real speed effects.** The mode knob changes the display and the platter animation but not the audio. A real 45 RPM setting would audibly speed up a 33⅓ record.
- **Health over time.** Readings are a snapshot per owner profile. A history view could show the stylus wearing and dust building up week by week, with reminders.
- **Phone → display sharing.** In Bluetooth mode, the phone could send its own album art and lyrics to the player's screen.
- **Offline fallback.** Lyrics and album art load from the internet. Caching them would keep the display working without a connection.

> **TODO (Sai):** Add anything you attempted but didn't finish, with screenshots.

---

## AI usage

> **TODO (Sai):** Describe how you used AI, in your own words.

For reference, here is what Claude Code (Anthropic's AI coding assistant) built in this project:
- The project's `CLAUDE.md` guidance file, from your spec and `REQUIREMENTS.md`
- Both device interfaces, the master page and the testing panel, from your design spec
- The four mock owner profiles
- Finding the LRCLIB lyrics source
- The GitHub Pages setup
- The screenshots on this page and a first draft of this write-up

The design decisions came from your spec: the 1.41 ratio, the two display pages, the tonearm warning, the knob behavior, the six sensors with four health tiers, and the library and insights.

---

## Demo video

> **TODO (Sai):** Embed or link a 2–3 minute demo with voiceover covering the project name, your name, the components and how it works.
