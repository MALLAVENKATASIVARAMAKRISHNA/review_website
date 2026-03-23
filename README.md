# AI Bootcamp Reviews Website

This repository contains a static review website for AI Karyashala bootcamp participants.

The project is intentionally simple:

- `index.html` contains the full application markup, styling, and client-side JavaScript.
- `student_images/` contains local student photo assets present in the repository.

## Project Overview

The website displays:

- overall average rating
- total number of reviews
- paginated review cards
- a random reviews view
- footer links to AI Karyashala pages

The application is a single-page static site with no framework, no build step, and no backend code in this repository.

## How It Works

The page loads the Supabase browser SDK from a CDN and creates a client in the browser.

It then fetches data from:

- Supabase table: `bootcamp_reviews`
- Supabase Storage bucket: `student-images`

Main runtime flow:

1. `getStats()` fetches ratings and total count.
2. `loadReviews(page)` fetches 9 reviews for the current page.
3. `loadRandomReviews()` fetches all reviews and picks 9 random entries client-side.
4. `displayReviews()` renders cards into the reviews grid.

## Repository Structure

```text
.
├── index.html
├── README.md
└── student_images/
```

## Data Source

Review data is not stored locally in this repository.

The frontend fetches it directly from Supabase using the client defined in `index.html`.

The current implementation includes:

- a public Supabase project URL
- a public Supabase anon key

This is normal for direct client-side Supabase usage, but access should be protected with correct Supabase Row Level Security policies.

## Deployment

Because the app is a static HTML page, it can be hosted on any static hosting platform, for example:

- GitHub Pages
- Netlify
- Vercel static hosting
- any basic web server

## Current Limitations

- The Supabase URL is visible in the client because the browser connects directly to Supabase.
- `loadRandomReviews()` is inefficient because it fetches the full review dataset before sampling.
- Review text is rendered with `innerHTML`, which can be unsafe if stored content is not sanitized.
- The local `student_images/` directory may be redundant if production images are always loaded from Supabase Storage.

## Recommended Improvements

- move database reads behind a backend endpoint if you want to avoid direct browser-to-Supabase access
- sanitize or safely render review text
- optimize random review loading
- document the required Supabase schema and storage setup

## Local Development

There is no build process. To run the project locally, serve the repository as a static site and open `index.html` in a browser.

If the page depends on live Supabase data, internet access and valid Supabase configuration are required.
