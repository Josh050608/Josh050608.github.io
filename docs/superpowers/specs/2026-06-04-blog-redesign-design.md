# Blog Redesign — Design Spec

- Date: 2026-06-04
- Status: Approved (pending final user review)

## Goal

Turn the default Astro blog template into Josh's personal blog: remove all
template/demo content and restyle to an elegant "editorial serif" look. The
homepage becomes a personal intro followed by featured posts.

## Decisions (validated with user)

- **Site title:** `muimi の blog`
- **Author:** Josh
- **Homepage layout (B):** intro section → ✨ featured posts → "查看全部文章 →" link
- **Visual style (A — editorial serif):** cream background `#faf8f3`, ink text,
  deep-green accent `#46604a`, serif headings, generous spacing.
- **Fonts:** Apple system sans stack — `-apple-system, BlinkMacSystemFont,
  "PingFang SC", system-ui, sans-serif` (macOS default 苹方/SF; graceful fallback
  elsewhere). Remove the now-unused Atkinson web font (astro.config + BaseHead).
- **Featured posts:** manual `featured: boolean` flag in post frontmatter; homepage
  lists posts where `featured: true`.
- **Social links:** GitHub (`Josh050608`) + email (`sbzzx050608@gmail.com`), in
  Header and Footer (replacing the Astro-org links).
- **Content cleanup:** delete the 5 demo posts (`first-post`, `second-post`,
  `third-post`, `markdown-style-guide`, `using-mdx`); keep `why-i-start-my-blog`
  and `hello-astro`.
- **Intro & About prose:** clearly-marked placeholders for now — Josh writes them later.

## Changes by file

1. `src/consts.ts` — `SITE_TITLE = "muimi の blog"`; `SITE_DESCRIPTION` = simple
   default tagline (e.g. "记录思考与生活"), editable.
2. `src/content.config.ts` — add `featured: z.boolean().default(false)` to the blog schema.
3. `src/pages/index.astro` — replace the template body with: intro section
   (greeting "你好，我是 Josh" + **placeholder bio** + GitHub/email links) →
   featured-posts list (filter `data.featured`) → "查看全部文章 →" link to `/blog`.
4. `src/styles/global.css` — restyle `:root` vars + base styles: cream bg, serif
   stack, deep-green accent, spacing/typography.
5. `src/components/Header.astro` — keep nav; replace Astro social links with GitHub + email.
6. `src/components/Footer.astro` — "© {year} Josh"; replace social links with GitHub + email.
7. `src/pages/about.astro` — replace Lorem ipsum with a **placeholder** About (Josh to fill);
   fix title/description.
8. `src/layouts/BlogPost.astro` — light touch so post date/title fit the new look.
9. Delete `src/content/blog/{first-post,second-post,third-post,markdown-style-guide}.md`
   and `using-mdx.mdx`.
10. Mark `why-i-start-my-blog` as `featured: true` so the homepage section isn't empty.

## Out of scope (for now)

- Josh's real intro/about prose (he writes it)
- CJK web fonts; tags; dark mode; comments; analytics

## Verification

- `npm run dev` preview + `npm run build` succeeds; then publish via the existing
  push → GitHub Actions flow. Confirm homepage, featured list, and a post all render.
