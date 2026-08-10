# Process overview

A reading-guide to how the work came together --- a map to your process, not an
essay about it. Markers read this file and follow its citations; they don't
trawl the repo for evidence you didn't point at, so if a moment mattered, cite
it.

This file is the shape; the course site's
[assessment page](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/topics/assessment/#what-you-submit)
is the requirement, and its
[word counts](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/topics/assessment/#word-counts)
cover every deliverable.

## What I built

A five-page static site for a fictional music school, "Harmony -- The Music
School", redesigned from a Wix wellness template into a calming,
purple/lavender-toned brand: a home page, a "Who We Are" story page with team
and testimonials, a music programmes page, a careers page, and an events page
-- built with plain HTML/CSS/TypeScript on Vite and iterated on through several
rounds of visual polish (branding, hero photography, navigation) checked
against the repo's automated build/lint/spec suite and real browser
screenshots at both the marked viewports.

## The moments that mattered

1. **Header brand mark: image crop hit a CLI bug, so I changed the approach
   instead of fighting the tool.** The original brand asset was a rectangular
   logo lockup; I wanted a square badge cropped out of it. Chaining
   `sharp-cli`'s `extract` and `trim` operations in one invocation
   (`extract ... -- trim 10`) failed with `bad extract area`, even though the
   same extract succeeded on its own. Rather than keep forcing the chained
   form, I ran `extract`, `trim`, and `resize` as three separate sequential
   invocations. At the same time I replaced the old image-only wordmark with a
   decorative badge image (`alt=""`) plus real HTML text for the school name
   and tagline, which is both more robust to the crop and more accessible than
   baking the name into a raster image. I confirmed the result with Playwright
   screenshots of the header across viewports before committing
   ([`3501239`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit2-p-venkatram/commit/3501239)).

2. **A layout bug that only showed up at narrow widths, caught by checking the
   phone viewport rather than assuming desktop was representative.** After the
   badge/text header change, the logo was visibly squeezed at tighter container
   widths -- a global `img { max-width: 100%; }` rule was fighting a flex child
   that had no `flex-shrink: 0`. Instead of just shrinking the logo or
   redesigning the header, I traced it to that specific interaction and fixed
   it at the source: `flex-shrink: 0` on the `.brand` container and
   `max-width: none` on `.brand-logo` to opt that one image out of the global
   rule. I verified it by screenshotting the header across a wide sweep of
   widths from 320px to 1920px, including the 390px viewport this crit is
   marked at, to confirm no distortion at any of them
   ([`3501239`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit2-p-venkatram/commit/3501239)).

3. **Nav bar gradient went through three rounds of feedback, and each round I
   re-checked the mobile dropdown, not just the desktop bar I was editing.**
   The nav background moved from a flat tint, to a darker cohesive gradient, to
   a lighter lavender-to-white left-to-right gradient, based on rounds of
   visual feedback. The part that wasn't obvious: the desktop nav and the
   mobile dropdown nav (triggered under the `(width <= 55rem)` breakpoint)
   share the same link styles but sit on very different backgrounds, so a color
   change tuned for the desktop gradient risked making the mobile dropdown's
   text illegible. Each iteration I opened the mobile menu specifically (not
   just resized the desktop view) and screenshotted it before treating the
   change as done
   ([`9705e86...01331c4`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit2-p-venkatram/compare/9705e86...01331c4)).

## Before you ship

`pnpm check:evidence` verifies your citations resolve to real commits, that the
current reflection entry is in `reflections/`, and that your `CLAUDE.md` is
there --- before a marker ever opens the file. It checks that your map is
traceable, not that it is good: the marker judges whether your small,
deliberately chosen set of moments shows real judgement and reflection. A green
check is not a substitute for that curation.

Images are deliberately not checked, because whether one renders is visible the
moment you look. Open this file on GitHub and look at it before you ship.
