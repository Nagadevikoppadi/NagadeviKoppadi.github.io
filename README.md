# Nagadevi Koppadi — Personal Portfolio

A clean, single-file personal portfolio website for a 2025 B.Tech IT graduate, built with pure HTML, CSS, and vanilla JavaScript. No frameworks, no build tools — open the file and it works.

---

## Live Sections

| # | Section | Description |
|---|---|---|
| — | Hero | Full-screen introduction with name, title, quick info panel, and CTA buttons |
| 01 | About | Bio, background, and stats (certifications, projects, graduation year) |
| 02 | Skills & Expertise | 6 skill cards covering backend, frontend, ML/AI, testing, cybersecurity, and data analytics |
| 03 | Featured Projects | 3 highlighted projects with tech stack tags |
| 04 | Certifications | 5 industry certifications from Deloitte, Accenture, edX/IBM, and ZTCA |
| 05 | Education | Timeline of academic history from SSC through B.Tech |
| 06 | Contact | Email and LinkedIn links |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 |
| Styling | Custom CSS (no frameworks) |
| Fonts | Google Fonts — Playfair Display, DM Sans |
| Animations | Intersection Observer API |
| JavaScript | Vanilla JS (scroll spy + fade-in animations) |

---

## Project Structure

```
index.html
│
├── <head>
│   ├── Google Fonts import
│   └── <style> — all CSS (CSS variables, layout, components, responsive)
│
├── <nav>               — Fixed top navbar with smooth scroll links
├── .hero               — Two-column split hero (intro left + quick info right)
├── #about              — Dark-background bio section with stats
├── #skills             — 3-column skill card grid
├── #projects           — Numbered project list cards
├── #certifications     — 2-column cert card grid
├── #education          — Dark-background vertical timeline
├── #contact            — Centered contact section with link chips
├── <footer>            — Copyright line
│
└── <script>
    ├── IntersectionObserver  — triggers .fade-up → .visible animations
    └── Scroll spy            — highlights active nav link on scroll
```

---

## CSS Architecture

All styles live in a single `<style>` block using CSS custom properties:

```css
:root {
  --ink:        #0d0d0d;   /* primary text / dark backgrounds */
  --cream:      #ffffff;   /* white backgrounds */
  --rust:       #4a3f35;   /* accent — hover states, eyebrow labels */
  --mist:       #f5efe6;   /* warm beige — hero right, projects bg */
  --gold:       #b8996e;   /* gold accent — dark section headings, stats */
  --text-muted: #6b6258;   /* secondary text */
  --border:     #e2d9cc;   /* card and divider borders */
  --beige:      #f5efe6;   /* tag pill backgrounds */
}
```

Alternating section backgrounds create visual rhythm: `white → dark → white → beige → white → dark → beige`.

---

## JavaScript Features

### Fade-in Animations
Elements with class `.fade-up` start invisible (`opacity: 0, translateY: 30px`) and animate in when they enter the viewport:

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.classList.add('visible');
  });
}, { threshold: 0.12 });

document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
```

Staggered delays are set via inline `style="transition-delay: .Xs"` on sibling cards.

### Scroll Spy
The active nav link is highlighted based on which section is currently in view, using `getBoundingClientRect()` on each `section[id]`.

---

## Responsive Breakpoints

| Breakpoint | Changes |
|---|---|
| `≤ 900px` | Hero stacks to single column; sections reduce padding; project cards collapse; timeline removes date column; footer stacks vertically |
| `≤ 600px` | Skills grid goes single column; nav link gap reduces |

---

## Personalisation Guide

### Update Personal Info
All personal content is hard-coded in the HTML. Key areas to edit:

- **Name / title** — `.hero-name`, `.hero-title`, `.nav-logo`
- **Hero description** — `.hero-desc` paragraph
- **Quick info panel** — `.info-item` blocks (location, degree, interests, status)
- **About text** — `#about .about-text` paragraphs
- **Stats** — `.stat-num` / `.stat-label` pairs

### Add a Project
Copy and paste a `.project-card` block inside `#projects .projects-list`:

```html
<div class="project-card fade-up">
  <div class="project-num">04</div>
  <div class="project-info">
    <h3>Your Project Title</h3>
    <p>Brief description of what it does and how you built it.</p>
  </div>
  <div class="project-stack">
    <span class="tag">Tech 1</span>
    <span class="tag">Tech 2</span>
  </div>
</div>
```

### Add a Certification
Copy a `.cert-card` block inside `#certifications .certs-grid`:

```html
<div class="cert-card fade-up">
  <div class="cert-icon">🏅</div>
  <div class="cert-info">
    <h4>Certificate Name</h4>
    <span>Issuing Organisation</span>
  </div>
</div>
```

### Change the Accent Colour
Update `--rust` and `--gold` in `:root` to change the primary accent and gold highlight colours throughout the entire site.

---

## Getting Started

No installation or build step required:

```bash
# Simply open in a browser
open index.html

# Or serve locally
npx serve .
python -m http.server 8080
```

---

## Browser Support

Works in all modern browsers. The Intersection Observer API has broad support (Chrome, Firefox, Safari, Edge). No polyfills needed for modern targets.

---

## License

Free to use as a personal portfolio template. Replace all personal details (name, email, LinkedIn, projects) before deploying.
