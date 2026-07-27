# Orbital Studios website

A single-page marketing site for Orbital Studios, a student-run web design studio. Plain HTML/CSS/JS. No build step, no Node, no npm. Just open the file or upload it to a host.

## Viewing it

Double-click `index.html`, or open it from your browser (`File > Open`). Styles, scripts, and fonts all load from `css/`, `js/`, and Google Fonts, so no server is required.

## Hosting it

Upload the whole `agency-site/` folder (or its contents) to any static host:

- **Netlify**: drag-and-drop the folder onto [app.netlify.com/drop](https://app.netlify.com/drop)
- **GitHub Pages**: push this folder to a repo and enable Pages in Settings
- **Cloudflare Pages / Vercel**: connect the repo, no build command needed
- **Plain shared hosting / FTP**: upload the files as-is, `index.html` is the homepage

Nothing to configure. It's just static files.

## Where to edit things

Everything lives in `index.html`. Edit the text directly in the markup (there's no separate content file since there's no build step to pull one into). Landmarks to look for:

| What | Section in `index.html` |
| --- | --- |
| Site name / logo | `<div class="nav-outer">` near the top |
| Hero headline, subheadline, CTA buttons | `<section class="hero">` |
| Trust strip (row under the hero) | `<div class="trust-strip">` |
| Mission / about paragraph | `<section id="about">` |
| Service cards | `<section id="services">` |
| "How it works" steps | the `.timeline` inside the process section |
| Testimonial quotes | `<section>` above Contact, `.testi-slide` blocks |
| Contact email, form heading | `<section id="contact">` |

Other things to customize:

- **Colors**: all defined as CSS custom properties at the top of `css/styles.css` (`--ice-*` for the blue accent, `--slate-*` for text). Change the hex values there to rebrand the whole site, light and dark mode both included.
- **Dark mode**: the site currently renders dark-only, no toggle in the nav. The theme-switching code still exists in `js/script.js` and the light palette in `css/styles.css` if you want to bring the toggle back.
- **Fonts**: loaded via the Google Fonts `<link>` tags in `<head>` (Inter). Swap the `href` and the `font-family` in `css/styles.css` to change the typeface.

## Receiving contact form submissions

The form submits to [Formspree](https://formspree.io) (free, no backend code needed). You just need to point it at your own form.

1. Sign up at [formspree.io](https://formspree.io) (free tier covers 50 submissions/month).
2. Click **New Form**, give it a name, and set the destination email.
3. Formspree gives you an endpoint like `https://formspree.io/f/abcdwxyz`. Copy it.
4. In `index.html`, find the `<form>` tag in the Contact section and swap in your own ID:
   ```html
   <form class="contact-form" id="contactForm" action="https://formspree.io/f/abcdwxyz" method="POST">
   ```
5. That's it. `js/script.js` already submits the form via `fetch`, so visitors see the "thanks, we'll be in touch" message in place, without a page reload or redirect.

Formspree sends a confirmation email the first time you submit the form for real. Click the link in it once to activate the form. After that, every submission lands directly in your inbox.

(Netlify Forms works similarly if you host on Netlify. Just add `data-netlify="true"` to the `<form>` tag instead and skip Formspree entirely.)
