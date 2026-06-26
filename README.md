# Team Harmony — Collective Powerhouse

A static brand landing page for **Team Harmony**, a collective of three developers, designers, and strategists. The site showcases their services, case studies, development process, team, and client testimonials in a dark-themed, emerald-accented design.

---

## Features

- **10 sections**: Navbar, Hero, Core Values, Expertise, Case Studies, Process, Team, Testimonials, CTA Banner, Footer
- **Dark / Light theme toggle** with `localStorage` persistence
- **Fully responsive** across 5 breakpoints (1200px, 1024px, 768px, 480px, 375px)
- **Smooth scroll** navigation and scroll-to-top button
- **CSS animations**: fade-in on scroll, card hovers, icon effects, nav underline, custom scrollbar
- **24 service items** across 4 categories, **3 case studies**, **4 testimonials**, **3 team members**
- **Footer** with 4-column grid, social links, and encircled scroll-to-top arrow

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| **Markup** | HTML5 |
| **Styling** | CSS3 with custom properties |
| **Icons** | Boxicons 2.1.4 (CDN) |
| **Fonts** | Poppins (Google Fonts) |
| **Images** | Unsplash (team photos) |
| **Scripting** | Vanilla JavaScript (inline) |
| **Version Control** | Git |

No frameworks, build tools, or package managers.

---

## Color System

The design uses an **Emerald Noir** palette — a near-black backdrop with emerald green as the primary accent.

### Dark Mode (default)

| Token | Value | Usage |
|-------|-------|-------|
| `--color-dark-bg` | `#030712` | Page background |
| `--color-accent-emerald` | `#10b981` | Primary accent |
| `--color-accent-teal` | `#14b8a6` | Secondary accent |
| `--color-accent-gold` | `#f59e0b` | Tertiary accent |
| `--color-text-primary` | `#f8fafc` | Main text |
| `--color-text-secondary` | `#94a3b8` | Muted text |

### Light Mode

Overrides the dark palette with an off-white background (`#f8fafc`), dark text (`#0f172a`), and softer emerald glows.

---

## Project Structure

```
├── index.html          # Main landing page (all content)
├── style.css           # All styles (~1300 lines)
└── README.md           # This file
```

---

## Getting Started

Open `index.html` in any browser — no build step required.

```bash
# Clone the repo
git clone <repo-url>

# Open in browser
start index.html
```

---

## Git Workflow & Merge Conflict Case Study

This section documents a deliberate merge conflict that was created and resolved during development, serving as a reference for understanding Git's merge behavior.

### Scenario

Two branches modified the **same line** in `index.html` — the hero section heading — to different values:

| Branch | Change |
|--------|--------|
| `main` | `"Innovative Thinkers, Seamless Execution"` |
| `feature/conflict-branch` | `"Bold Visions, Powerful Results"` |

Both diverged from a common ancestor that had the original text: `"Creative Minds, Harmonious Solutions"`.

### Step-by-Step Walkthrough

#### 1. Create a feature branch

```bash
git checkout -b feature/conflict-branch
```

#### 2. Make a change on the branch

The hero heading was edited in `index.html`:

```html
<h1>Bold Visions, <span>Powerful Results</span></h1>
```

Committed:

```bash
git add index.html
git commit -m "Updated hero heading on conflict-branch"
```

#### 3. Switch back to main and make a different change to the same line

```bash
git checkout main
```

The same line was edited to a different value:

```html
<h1>Innovative Thinkers, <span>Seamless Execution</span></h1>
```

Committed:

```bash
git add index.html
git commit -m "Updated hero heading on main"
```

At this point, the commit graph looked like this:

```
* eddc102 (main) "Innovative Thinkers..."
| * 8d49401 (feature/conflict-branch) "Bold Visions..."
|/
* 68f0e52 (common ancestor) "Creative Minds..."
```

#### 4. Merge triggers the conflict

```bash
git merge feature/conflict-branch
```

Git's auto-merge algorithm found that **both sides changed the same region** of the same file with different content. It could not decide which to keep, so it halted with:

```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

#### 5. Conflict markers appear in the file

```diff
<<<<<<< HEAD
        <h1>Innovative Thinkers, <span>Seamless Execution</span></h1>
=======
        <h1>Bold Visions, <span>Powerful Results</span></h1>
>>>>>>> feature/conflict-branch
```

| Marker | Meaning |
|--------|---------|
| `<<<<<<< HEAD` | Start of **our** version (the branch being merged into — `main`) |
| `=======` | Separator |
| `>>>>>>> feature/conflict-branch` | End of **their** version (the branch being merged in) |

#### 6. Resolution

The team chose to **keep the HEAD (ours) version**. The conflict markers and the rejected code were removed:

```html
<h1>Innovative Thinkers, <span>Seamless Execution</span></h1>
```

#### 7. Stage and commit the resolution

```bash
git add index.html
git commit -m "Merge feature/conflict-branch into main (resolved - kept ours)"
```

The final merge commit has two parents, preserving the full history.

```
*   161fe52 (HEAD -> main) Merge feature/conflict-branch...
|\
| * 8d49401 (feature/conflict-branch) Updated hero heading on conflict-branch
* | eddc102 Updated hero heading on main
|/
* 68f0e52 Merge branch 'test-conflict'
```

### Key Takeaways

- A **merge conflict** occurs when two branches modify the same lines of the same file in different ways.
- Git marks the conflict in the file with `<<<<<<<`, `=======`, and `>>>>>>>` markers.
- Resolution requires **manual editing**: pick one version, merge both, or write something new — then remove the markers.
- After resolving, **stage** the file and **commit** to finalize the merge.
- The conflict is **not a bad thing** — it is Git's way of asking for human judgment when automation is not safe.
