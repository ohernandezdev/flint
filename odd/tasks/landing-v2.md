# Landing v2 + README refresh

## Objective

Make the Flint landing page (`docs/index.html`, served by GitHub Pages at
https://ohernandezdev.github.io/flint/) and the README good enough that someone
who lands on them stars the repo or downloads the app. Unslopped copy and design,
GSAP scroll motion with real 3D moments, a short product film, correct facts.

## Problem

- The page is a centered template: pill badge above the H1, six equal feature
  cards, uppercase tracked table headers, negative tracking on small text,
  trailing periods on headings, em-dash-heavy copy.
- Factual errors: the page claims "Universal (Apple Silicon & Intel)", but the
  v1.0.0 DMG ships `wimlib-imagex` and `libwim.15.dylib` as thin arm64 Mach-O
  (verified: magic `cffaedfe0c000001`; the `Flint` binary itself is fat
  `cafebabe00000002`). The Windows split step cannot run on Intel Macs.
  The comparison table marks Boot Camp Assistant as "Free & open source".
- README says "Notarized distribution … planned but not yet shipped" while the
  v1.0.0 release is signed and notarized by `.github/workflows/release.yml`.
- `docs/assets/demo.gif` shows a Finder dialog with personal file names and
  a mixed Spanish/English UI, and ends while still formatting.
- No `<head>`: no meta description, Open Graph, favicon or structured data.

## Scope

In: `docs/index.html`, new assets under `docs/assets/`, `README.md`, a 30 s film.
Out: the Swift app, CI, the release workflow.

## Constraints

- One heavy local process at a time (one headless browser, one render).
- No unverifiable claims. No stars/download counts in the page copy.
- `prefers-reduced-motion: reduce` → no scroll-driven or 3D motion, all content visible.
- Libraries only from CDNs with exact versions:
  - `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js`
  - `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js`
  - `three@0.160.0` from `https://cdn.jsdelivr.net/npm/three@0.160.0/` via an import map
    (`three` → `build/three.module.js`, `three/addons/` → `examples/jsm/`).
  - Fonts: Google Fonts Geist (400, 500, 600) and Geist Mono (400, 500).
- "motion" in the request is read as motion design; GSAP covers it. Adding the
  Motion library on top would be a second animation runtime doing the same job.

## Direction (unslop)

- **Product.** A free, open-source Mac app that turns a Windows or Linux ISO into a
  bootable USB stick without any chance of erasing the Mac's own disk.
- **Character.** careful, exact, a little dry.
- **World.** A desk at night with a half-built PC and a USB stick: hardware,
  device nodes, `diskutil` output. Cool ink neutrals.
- **Moments.** (1) A real-looking 3D USB stick in the hero (three.js, matte black
  body, brushed metal connector, the Flint power glyph). (2) A coded, faithful
  Flint window that steps through the four screens as you scroll. (3) The disk
  whitelist as a 3D stack of drives where everything but the USB stick drops out.
- **Signature.** Mono device chips in the app's own format: `/dev/disk9 · 61.87 GB · USB`.

## Tokens

Ink ramp. Light / dark:

| Role | Light | Dark |
|---|---|---|
| Deepest | `#eceff4` | `#07080d` |
| Page bg | `#f5f7fa` | `#0b0d14` |
| Card | `#ffffff` | `#11141c` |
| Raised | `#eceff4` | `#1a1e28` |
| Hairline | `rgba(17,24,39,0.08)` | `rgba(238,240,245,0.08)` |
| Hairline strong | `rgba(17,24,39,0.14)` | `rgba(238,240,245,0.14)` |
| Text primary | `#111827` | `#eef0f5` |
| Text secondary | `#4b5565` | `#a3a9b8` |
| Text muted | `#5d6678` | `#8a92a6` |
| Accent (fill, links) | `#0062d6` | `#3291ff` |
| On accent | `#ffffff` | `#07080d` |
| Danger | `#dc2626` | `#e5484d` |
| Positive | `#16a34a` | `#4cc38a` |

App mock window always uses the app's light look: window `#f6f6f6`, title bar
`#ececec`, card `#ffffff`, hairline `rgba(0,0,0,0.10)`, text `#1d1d1f`, secondary
`#6e6e73`, stepper dark `#111111`, check blue `#0a7cff`, danger `#e5352b`,
traffic lights `#ff5f57 #febc2e #28c840`.

Type: Geist for UI, Geist Mono for meta/chips/figures, `tabular-nums` on numbers.
H1 64/66px weight 500, letter-spacing -0.03em (mobile 40/44). H2 40/44 weight 500,
-0.02em (mobile 30/34). Lede 19/30 secondary, max 34rem. Body 16/26. Small 14/22.
Mono meta 12/16, letter-spacing 0.01em. Weights 400/500, 600 only for the wordmark.
No uppercase tracked labels, no italics, no negative tracking under 16px.

Spacing on a 4px grid. Wrap max 1200px, side padding 32px (16px under 640px).
Section padding 128px (80px under 640px). Radius: chips 6, buttons 10, cards 16,
windows 14 (inner 10). Easing `cubic-bezier(0.22,1,0.36,1)`; GSAP `power3.out`
for tweens, `none` for scrubbed timelines. Hover 160ms, entrances 480ms,
stagger 60ms.

## Exact copy (verbatim, in page order)

Straight apostrophes are fine; use the typographic `’` in rendered copy. No em
dashes in prose. No trailing periods on headings, buttons, labels, captions.

### Head
- `<title>`: `Flint · Bootable Windows and Linux USB maker for Mac`
- description: `Free, open-source Mac app that turns a Windows or Linux ISO into a bootable USB drive. It only lists external, removable drives, so your Mac’s own disk is never in the list.`
- og:title `Flint for Mac`, og:description = description, og:image `https://ohernandezdev.github.io/flint/assets/og.png` (1200×630), twitter:card `summary_large_image`, canonical `https://ohernandezdev.github.io/flint/`, theme-color light `#f5f7fa` dark `#0b0d14`, favicon `assets/icon.png`.
- JSON-LD `SoftwareApplication`: name Flint, operatingSystem `macOS 13 or later`, applicationCategory `UtilitiesApplication`, softwareVersion `1.0.0`, offers price `0` USD, license `https://www.gnu.org/licenses/gpl-3.0.html`, downloadUrl `https://github.com/ohernandezdev/flint/releases/latest`, url canonical. No ratings.

### Nav
Wordmark `Flint` (icon.png 24px + text 16px weight 600). Links: `How it works` (#how), `Safety` (#safety), `FAQ` (#faq). Right: secondary small button with GitHub mark `Star on GitHub` → https://github.com/ohernandezdev/flint. Under 720px the three links hide and only the wordmark and the button stay.

### Hero (split: text left, 3D USB stick right)
- H1: `Make a bootable USB on your Mac, without risking the wrong disk`
- Lede: `Flint writes Windows and Linux installers to a USB stick. Its drive list only shows external, removable drives, so your Mac’s own disk can’t be picked by mistake.`
- Primary: `Download for Mac` → https://github.com/ohernandezdev/flint/releases/latest
- Secondary: `Watch it work` → #film
- Meta (mono, muted): `v1.0.0 · macOS 13+ · Apple Silicon · Free, GPLv3`
- Under the stick, a mono chip: `/dev/disk9 · 61.87 GB · USB`

### Why (own section, narrow column, scrubbed word reveal)
- Small label: `Why it exists`
- Paragraph: `I bought parts for a new PC and needed a Windows installer on a USB stick. All I had was a Mac. The options were paying for one of the few apps that do this, or running an unsigned binary from a site I’d never heard of, as root, pointed at my disks. Neither felt right, so I wrote the one I wanted and made it free. I built it alongside an AI coding agent. That’s what made it realistic for one person to ship it with tests, a properly isolated privileged helper and a notarized release.`
- Sign-off (mono, muted): `Omar Hernandez, who wrote Flint`

### Film (#film)
- H2: `The whole flow in thirty seconds`
- Sub: `The same four screens you’ll see in the app, sped up. The real copy takes as long as your USB stick needs.`
- Video in a Mac window frame: `assets/flint-film.webm` + `assets/flint-film.mp4`, poster `assets/flint-film-poster.jpg`, `muted playsinline loop preload="none"`, aspect 16:9. Plays when ≥50% visible, pauses when not. A visible control to pause/play (button, label `Pause` / `Play`). Under reduced motion it does not autoplay; it shows the poster with a `Play` button.

### How it works (#how), pinned 3D story
- Label: `How it works`
- H2: `Four screens, then you’re done`
- Sub: `Flint reads the ISO first and picks how to write it. Windows installers get copied to a FAT32 drive. Linux images get written byte for byte.`
- Steps (number in mono + title + text):
  1. `Pick the ISO` — `Drop it on the window. Flint checks how the image boots before it touches anything, and tells you what it found.`
  2. `Pick the USB drive` — `Only external, removable drives show up. Your Mac’s internal disk isn’t hidden behind a filter, it never makes it into the list.`
  3. `Confirm` — `You see the exact drive name and size, and tick a box that says you understand it will be erased. The button stays off until you do.`
  4. `Let it write` — `Format, copy, split, finish. Every phase shows real bytes, speed and time left. Linux images skip straight to one raw write.`
- Window screens (text copied from the real app, English UI). Header row in every screen: `⏻ Flint` | stepper `1 ISO` `2 USB drive` `3 Confirm` `4 Create` (done steps show a white check in a black circle, current is black circle with number and bold label, future is grey outline) | `🌐 English` (globe as line icon, not emoji).
  - Screen 1 — title `Select your ISO`, sub `Choose the official .iso file. Nothing is modified yet.` File row: disc icon + `Win11_25H2_English_x64.iso` + right link `Change ISO…`. Card with three rows (blue check-badge icon, file icon, shield icon): `Windows installer detected — files copied to FAT32.` / `install.wim is 7.56 GB → will be split for FAT32.` / `Secure Boot compatible (2023 cert likely).` (these are UI strings, em dash allowed here). Button bottom-right `Continue` (black).
  - Screen 2 — title `Choose the USB drive`, sub `Only external USB drives are shown. The internal disk never appears.` One row: drive icon tile, `USB Flash Drive`, mono `/dev/disk9 · 61.87 GB · USB`, radio selected (blue). Buttons `Back` (text) / `Continue` (black).
  - Screen 3 — title `Confirm before erasing`. Card: red triangle + `Everything will be erased on:`; red drive icon, `USB Flash Drive`, `/dev/disk9 · 61.87 GB`. Field row: `USB name (FAT32):` input `WIN11` + `5/11`. Checkbox (checks itself as the step activates): `I understand all content on USB Flash Drive will be erased.` with `all` and `USB Flash Drive` in 600. Buttons `Back` / `Format and create USB` (red fill, white text, bolt icon; disabled look until the box is checked).
  - Screen 4 — title `Creating the USB…`. Overall bar. Status line `Copying sources/boot.wim`. Card with phases: `Format` (blue check), `Copy files` with right figure `NN %` and its own bar and mono line `163.6 MB of 906 MB (18 %) · 1.47 GB/s · 1 s left` (numbers scrub from 0 → 906 MB with scroll; speed fixed `1.47 GB/s`; left counts down), `Split install.wim` with mono sub-line `pieces under 3800 MiB each` once it activates, `Finalize`. Button `Cancel` text. At the end of the scrub, all four phases are checked and the title reads `USB ready`.

### Features (bento: row 1 = A spans 2 cols + B; row 2 = C, D, E)
- Label `What it does`, H2 `A small app with one job`
- A `Windows or Linux, it works out which` — `Flint reads the ISO’s boot records, the MBR signature and El Torito, and picks a method. Windows installers are copied to a FAT32 drive with install.wim split into pieces FAT32 can hold. Linux and other isohybrid images are written raw, the way their makers ship them. Anything it can’t make bootable is turned away before you start.` Inside A, a two-row mono table:
  - `Win11_25H2_English_x64.iso` → `FAT32 copy · install.wim split to fit`
  - `ubuntu-26.04-desktop-amd64.iso` → `raw write · byte for byte`
- B `Checks the SHA-256 if you ask` — `Paste the hash from the download page and Flint checks the file against it, and tells you if it doesn’t match.`
- C `Won’t start a write it can’t finish` — `Before a raw write it checks the stick is at least as big as the ISO, so you never end up with half an image.`
- D `Progress you can read` — `Bytes, percent, MB/s and time left for every phase, the raw write included. No endless spinner.`
- E `Warns about Secure Boot` — `If the ISO’s boot files predate mid-2024, they were likely signed only with Microsoft’s 2011 certificate and may not boot with Secure Boot on. Flint warns you before you start.`
- Icons: lucide-style inline SVG, 18px, stroke 1.5, secondary text color. One per card.

### Safety (#safety)
- Label `Safety`
- H2 `Erasing the wrong disk is the whole risk`
- Sub: `Flint erases drives and runs a helper as root. That’s the dangerous part, so these checks sit between you and the wrong disk.`
- 3D disk stack (pinned scrub on ≥960px, static list under it): caption `What macOS sees, and what Flint lists`. Four drive slabs, top to bottom, mono labels:
  - `disk0 · APPLE SSD AP1024Z · 1 TB · internal` → drops out with tag `internal disk`
  - `disk3 · Macintosh HD · APFS container` → drops out with tag `virtual`
  - `disk5 · Win11_25H2_English_x64.iso · disk image` → drops out with tag `disk image`
  - `disk9 · USB Flash Drive · 61.87 GB · USB` → stays, turns to face the reader, accent hairline, tag `listed`
- Safeguards list (tag in mono chip + title + text):
  - `S-1` `Only external drives get listed` — `A drive has to be external, physical and removable or ejectable to show up. The boot disk, disk images and virtual devices are dropped in code, before the interface ever sees them. Other external drives, like a backup disk, can appear, so unplug the ones you care about.`
  - `S-2` `You confirm by name and size` — `The confirm screen shows the exact drive and its size, and the erase button stays off until you tick the box.`
  - `S-3` `Checked again right before writing` — `The drive is looked up again just before the write, in case the stick changed while the window was open.`
  - `S-4` `The helper double-checks` — `The root helper checks on its own that the target is external and removable. It doesn’t take the app’s word for it.`
  - `S-5` `Failures stop cleanly` — `If a step fails, the build stops and tells you what happened instead of carrying on with a half-made drive.`
- Architecture (exploded 3D planes): top plane `Flint.app` / `runs as you`; connector label (mono) `XPC · code signature checked`; bottom plane (inverted: dark fill in light theme, light fill in dark theme) `FlintHelper` / `root · erase, unmount, raw write, eject`. Caption: `Copying, splitting and verifying run as you. The helper only touches the disk itself: it erases it, and for Linux images it also unmounts it, writes the image and ejects it.`

### Compare (#compare)
- Label `Compared`
- H2 `Why not use what’s already on your Mac?`
- Table (header row sentence case, no uppercase). Columns: `` (row label) | `Flint` | `balenaEtcher` | `WinDiskWriter` | `Boot Camp Assistant` | `Terminal (diskutil + dd)`
  - `Windows installer USB` | ✓ | `Writes it raw, won’t boot` | ✓ | `Older Intel Macs only` | `Doable, with wimlib and care`
  - `Linux ISO USB` | ✓ | ✓ | — | — | ✓
  - `Runs on Apple Silicon` | ✓ | ✓ | ✓ | — | ✓
  - `Internal disk can’t be picked` | ✓ | `Hidden by default` | `Didn’t check` | n/a | `Up to you`
  - `Free and open source` | ✓ | ✓ | ✓ | `Free, closed source` | `Built in, free`
- Footnote (muted, 13px): `Etcher writes Windows ISOs as raw images, which don’t boot on most PCs, and warns you about it. WinDiskWriter is Windows-only. Boot Camp Assistant doesn’t exist on Apple Silicon, and Intel Macs from 2015 on don’t use a USB stick for it. Flint’s Linux path is newer than its Windows one, see the FAQ.`
- Check marks: inline SVG check 16px, accent color, with visually hidden text `Yes`; dash with hidden text `No`.

### FAQ (#faq) — native `<details>`, no height animation
- H2 `Questions people ask`
- `Can it erase my Mac’s disk?` — `No. The drive list only contains external, physical, removable drives. Internal disks, disk images and virtual devices are filtered out in code, and the root helper checks the target again before it writes. Other external drives, like a backup disk, can show up, so unplug the ones you care about before you start.`
- `Why does macOS ask me to approve something in Login Items?` — `Erasing a disk needs root. Instead of running the whole app as root, Flint installs one small helper through SMAppService that only erases the disk and writes the image. macOS asks you to allow it once, in System Settings → General → Login Items. If you write a Linux ISO that sits in a protected folder like Downloads, macOS may also ask you to give the helper Full Disk Access; Flint links you straight to that setting.`
- `Which ISOs work?` — `Windows installer ISOs are tested end to end: Windows 11 25H2, including a real install from the stick. Linux and other isohybrid ISOs, such as Ubuntu, Fedora and Debian, are written raw. The detector is tested against Ubuntu 26.04, but booting from a Flint-made Linux stick hasn’t been confirmed on real hardware yet, so reports are welcome. ISOs that can’t be made bootable are rejected before anything is written.`
- `Does it work on Intel Macs?` — `Partly. Linux images work on both. Windows ISOs whose install.wim is over 4 GiB, which includes current Windows 11 images, need an Apple Silicon Mac for now: the wimlib tool bundled in v1.0.0 is arm64-only, so on an Intel Mac the build fails at the split step, after the drive has already been erased.` + link `Help fix it on GitHub` → https://github.com/ohernandezdev/flint/issues
- `How big does the USB stick need to be?` — `16 GB for Windows 11, and Flint warns you below that. For Linux, at least the size of the ISO.`
- `Does it phone home?` — `No. There is no account, no analytics and no network code in the app. It’s GPLv3, so you can check.`

### Final CTA
- H2 `Got an ISO and a spare USB stick?`
- Text `That’s everything you need. Flint is free and takes a minute to set up.`
- Primary `Download for Mac`, secondary `Star on GitHub`
- Mono meta: `Flint-1.0.0.dmg · 1.6 MB · signed and notarized`

### Footer
Wordmark; links `GitHub`, `Releases`, `License (GPLv3)`, `Security policy`, `Contributing`; line `Made by someone who’d rather not lose a disk to a typo`.

## Motion spec (GSAP 3.12.5 + ScrollTrigger; three.js 0.160.0)

Global: register ScrollTrigger; wrap everything in `gsap.matchMedia()` with
`(prefers-reduced-motion: no-preference)` and `(min-width: 960px) and (min-height: 720px)` contexts (shorter viewports get the static fallbacks).
Content is visible by default in CSS; JS sets initial states only inside the
no-preference context (no FOUC traps, no `opacity:0` in CSS).

1. **Hero load.** One entrance: H1, lede, buttons, meta fade + rise 12px, stagger 60ms, 480ms.
2. **Hero USB stick (three.js).** Procedural model:
   - Body `RoundedBoxGeometry(2.4, 0.34, 0.92, 6, 0.09)`, `MeshPhysicalMaterial` color `#1a1c21`, roughness 0.42, clearcoat 0.5, clearcoatRoughness 0.35.
   - Connector shell at +x: box 0.86 × 0.2 × 0.62, `MeshStandardMaterial` color `#c8ccd2`, metalness 1, roughness 0.28, with a fine brushed look via a generated anisotropic-ish canvas roughness map (horizontal noise lines). Two square holes on the top: 0.12 × 0.012 × 0.12 boxes color `#0a0b0d`. Inner plastic tongue visible at the mouth: box 0.84 × 0.06 × 0.56 color `#f2f2f2` slightly inset.
   - Power glyph decal on the top face: canvas texture of the Flint power symbol (circle arc + vertical line, like `assets/icon.png`), color `#e9ebef`, on a 0.42 × 0.42 plane 0.001 above the face, slightly toward −x.
   - Lanyard loop hole at −x end: dark cylinder r 0.07, `#0a0b0d`.
   - Activity LED: tiny box near the connector, emissive accent `#3291ff`, intensity 1.2 (steady, not blinking).
   - Lights: `RoomEnvironment` through `PMREMGenerator` (intensity 0.9) + one `DirectionalLight` from upper left (intensity 1.4). Fake contact shadow: plane below with a radial-gradient canvas texture, color `#000`, opacity 0.28 light / 0.6 dark.
   - Renderer: alpha, antialias, `ACESFilmicToneMapping`, exposure 1.0, `SRGBColorSpace`, DPR `min(devicePixelRatio, 2)`. Camera fov 28 at (0, 1.1, 6.2) looking at origin.
   - Pose: rotation (0.38, −0.62, 0.1). Pointer within the hero eases rotation by up to ±0.12 rad (lerp 0.08 per frame). ScrollTrigger scrub over the hero leaving the viewport: rotation.y += 1.2, rotation.x −= 0.2, position.y −0.5.
   - Render on demand (only when the pose changes), stop when the canvas is off screen (IntersectionObserver). Resize with ResizeObserver.
   - Fallback when WebGL fails or under reduced motion: `<img src="assets/usb-stick.webp" alt="Flint USB stick" width="1200" height="900">` in the same slot (the image is produced in T4; if missing, the slot is a plain raised surface).
3. **Why paragraph.** Split into word spans in JS; scrub opacity 0.18 → 1 word by word from `top 80%` to `bottom 60%`. Section container goes from `rotateX(10deg)` to `0` with perspective 1200px.
4. **Film window.** Window starts `rotateX(22deg) scale(0.9) translateY(48px)` and scrubs flat as it enters (`top bottom` → `top 30%`), perspective 1600px, transform-origin bottom center.
5. **How it works (pinned, ≥960px).** Grid: steps list left (5/12), window right (7/12). Pin the section for `+=300%`. One timeline, scrub 0.6:
   - Active step: title to primary, text visible; inactive steps: muted, text collapsed via opacity (no height animation; reserve space).
   - Between screens the window turns: `rotateY` 0 → −14deg while the current screen fades out (opacity, `translateZ(-60px)`), next screen fades in from `rotateY(14deg)` → 0. Perspective 1800px on the window wrapper.
   - Stepper in the window header advances in sync.
   - Screen 3 checkbox checks and the red button enables at 60% of its segment.
   - Screen 4: copy bar and figures driven by timeline progress (`onUpdate` writes numbers, tabular-nums); then Split activates, then Finalize, then title swaps to `USB ready`.
   - Under 960px: no pin; each step renders its own small static window screen (clone of the screen DOM) under its text, entering with a short fade + rise.
6. **Features bento.** Each card from `rotateX(-14deg) translateY(40px) opacity 0` to rest, scrub from `top 90%` to `top 60%`, staggered by 0.08 in timeline position. Pointer tilt on hover for fine pointers only, max 3deg, 160ms, no scale.
7. **Safety disk stack (pinned, ≥960px, `+=200%`).** Slabs start stacked in an isometric view (`rotateX(58deg) rotateZ(-38deg)`, 14px apart in Z). Scrub: stack explodes to 72px apart → each non-USB slab in turn shows its tag and drops (translateZ −240px, translateY 120px, opacity 0.12, desaturated) → the USB slab rotates to face the reader (`rotateX(0) rotateZ(0)`), scales to 1.04, accent hairline, tag `listed`. Safeguard list items highlight in sync (S-1 with the drop, S-2..S-5 as the scrub continues). Under 960px: static list of the four slabs with the three excluded ones struck through and muted.
8. **Architecture planes.** Two planes in isometric 3D start touching and separate in Z by 96px as the block scrubs through the viewport, the XPC line grows (scaleY 0 → 1, transform only).
9. **Compare table.** Wrapper from `rotateX(16deg) translateY(32px)` to flat, rows fade in staggered 40ms.
10. **Final CTA.** Heading words rise 12px with stagger when entering; nothing loops.

No `transition: all`, no animated width/height/top/left, no looping animations.
Hover: color/background changes 160ms; press `scale(0.98)`.

## Tasks

- [x] T1 Rebuild `docs/index.html` per direction, tokens, copy and motion spec (delegated writer, 2 rounds: build + 9 visual fixes; parent fixed hero camera/shadow clipping)
- [x] T2 Film: 30 s 1920×1080 HyperFrames film of the four-step flow → `docs/assets/flint-film.mp4` (997 KB) + `.webm` (987 KB) + poster + `flint-readme.gif` (2.47 MB). Contact sheet reviewed frame by frame; 0 leftover processes.
- [x] T3 README rewrite with honest facts, FAQ, Intel note, new GIF cut from the film (claims checked: XPC `setCodeSigningRequirement` in HelperClient/Helper main, no URLSession/http in App, real Win11 install in DOGFOODING.md, `package-wimlib.sh` exists)
- [x] T4 Assets: `og.png` 1200×630 (97 KB), `usb-stick.webp` WebGL fallback rendered from the live canvas, README GIF from the film; `demo.gif` removed (leaked Finder file names)
- [x] T5 QA: Playwright 1440×900 light/dark, 390×844, reduced motion. Round 2: console errors 0, horizontal overflow 0, text under 0.5 opacity in reduced motion 0, one h1, 0 img without alt. Every screenshot reviewed
- [x] T6 Red-team review (sonnet, read-only): 18 confirmed findings, 6 plausible. Fixed: USB-only claim (filter has no USB-bus check), invented split sizes, 8 GB min, Intel scope (>4 GiB wim, fails after erase), Linux never booted on hardware, helper scope (unmount/eject), DKIOCSYNCHRONIZECACHE, SHA-256 warns only, Secure Boot date heuristic, compare table (WinDiskWriter added, Etcher/Boot Camp cells), film heading, muted contrast, short-viewport pins, color-mix fallback, aria-pressed, apple-touch-icon. Film re-rendered with corrected split line. QA round 3: 0 errors in 4 contexts
- [ ] T7 Fix findings, commit, push, PR; repo issue for universal wimlib

## Route per task

T1 delegated (writer trigger: one large non-trivial file + asset wiring).
T2 delegated (per-action render worker). T3 inline (one file, facts already
gathered). T4–T5 inline bounded actions. T6 delegated reviewer.

## Acceptance

- Every claim on the page traces to code, the release, or DOGFOODING.md.
- 0 console errors on load and full scroll (desktop 1440×900, mobile 390×844).
- Reduced motion: every section readable, nothing stuck at opacity 0.
- No horizontal scroll at 390px. Lighthouse-style basics: title, description,
  OG image, alt text, focus rings, one `h1`.

## Progress / evidence

Branch `feat/landing-v2`. QA script and screenshots kept in the session scratchpad. Not fixed (app code, out of scope): DiskFilter has no USB-bus check; no arch guard before erasing on Intel.

## Next step

Merge the PR so GitHub Pages redeploys; then fix the two app issues above.
