# Spec Amendment — `.writing-footer` pattern

**Adds:** §2.9 to `VISUAL_SYSTEM.md` and a new component to `components.css`.
**Reason:** Every writing post needs a footer. Without a named pattern, each post drifts. This codifies one minimal, restrained footer to use across `/writing` and any future post-template page (lab entries, etc.).
**Date:** 2026-05-16
**Status:** Proposed for sign-off, then apply via Claude Code.

---

## What this changes

1. **`VISUAL_SYSTEM.md`** — adds a new §2.9 (Writing footer) and a one-line update to Phase 2 in §3.
2. **`components.css`** — appends the `.writing-footer` block.
3. **`src/pages/writing/pixels-to-atoms.md`** — the trailing `---` + sign-off block is replaced with the new pattern.

No tokens change. No other patterns change.

---

## 1 · Spec text to add to `VISUAL_SYSTEM.md`

Insert the following section between §2.8 (Lab entry) and §3 (Implementation plan):

````markdown
### 2.9 Writing footer

Closes every writing post (and any future post-template page like lab entries that read as authored pieces). Three jobs only: mark the end of the post, attribute it, point somewhere useful next.

```html
<footer class="writing-footer">
  <div class="writing-footer__end-mark">— end · entry 011 · 2026-05-13</div>

  <div class="writing-footer__byline">
    <div class="writing-footer__name">Nathan Barnes</div>
    <div class="writing-footer__role">
      Design-to-Fabrication Systems Engineer ·
      <a href="mailto:barnes.ngb@gmail.com" class="writing-footer__contact">barnes.ngb@gmail.com</a>
    </div>
  </div>

  <div class="writing-footer__see-also">
    <div class="writing-footer__see-also-label">see also</div>
    <ul class="writing-footer__see-also-list">
      <li class="writing-footer__see-also-item">
        <a href="/work/directive-engine" class="writing-footer__see-also-link">Directive Engine</a>
        <span class="writing-footer__see-also-tag">instrument 03</span>
      </li>
      <li class="writing-footer__see-also-item">
        <a href="/demo" class="writing-footer__see-also-link">Live demo</a>
        <span class="writing-footer__see-also-tag">browser</span>
      </li>
    </ul>
  </div>
</footer>
```

**Rules:**

- End-mark format: `— end · entry NNN · YYYY-MM-DD`. The em-dash + tracking-wider mono treatment matches figure captions. Entry number is the same one used in the title block at the top of the page; date is the post's published date.
- Byline is always present. Name + role + contact, in that order, in restrained sans.
- See-also is optional but should appear whenever the post has at least one meaningful related link. Don't pad with filler — three rows is plenty, two is fine, zero is acceptable.
- See-also items have two parts: a link on the left (the thing), a mono tag on the right (what kind of thing it is). Tag examples: `instrument 03`, `entry 010`, `browser`, `paper · acadia 2024`, `github`, `external`.
- No share buttons, no subscribe forms, no comments, no social row, no headshot. The footer is restrained on purpose.
- On lab pages (§2.8), the `.writing-footer` is not used — lab entries close more like log entries and need their own pattern when the time comes.
````

Then in §3 (Implementation plan), under **Phase 2 — Apply to existing pages**, update the writing post bullet:

```diff
- 5. `writing/*.md` — apply title block, metadata strip, figure pattern.
+ 5. `writing/*.md` — apply title block, metadata strip, figure pattern,
+    and close with .writing-footer (§2.9).
```

---

## 2 · CSS to append to `components.css`

Append at the end of the file (after `.summary-strip`):

```css
/* ============================================================
   Writing footer — closes writing posts.
   See VISUAL_SYSTEM.md §2.9.
   ============================================================ */

.writing-footer {
  margin-top: var(--space-6);
  padding-top: var(--space-5);
  border-top: var(--border-thin) solid var(--border);
}

.writing-footer__end-mark {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  letter-spacing: var(--tracking-wider);
  color: var(--ink-tertiary);
  margin-bottom: var(--space-5);
}

.writing-footer__byline {
  margin-bottom: var(--space-6);
}

.writing-footer__name {
  font-size: var(--text-base);
  font-weight: 500;
  color: var(--ink);
  margin-bottom: 2px;
}

.writing-footer__role {
  font-size: var(--text-sm);
  color: var(--ink-secondary);
}

.writing-footer__contact {
  color: var(--accent);
  border-bottom: var(--border-thin) solid var(--accent);
  text-decoration: none;
}

.writing-footer__contact:hover {
  border-bottom-color: var(--ink);
}

.writing-footer__see-also {
  margin-top: var(--space-5);
}

.writing-footer__see-also-label {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  letter-spacing: var(--tracking-wider);
  color: var(--ink-tertiary);
  margin-bottom: var(--space-2);
}

.writing-footer__see-also-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.writing-footer__see-also-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-2) 0;
  border-top: var(--border-thin) solid var(--border);
  gap: var(--space-3);
}

.writing-footer__see-also-item:last-child {
  border-bottom: var(--border-thin) solid var(--border);
}

.writing-footer__see-also-link {
  color: var(--ink);
  text-decoration: none;
  border-bottom: none;
  font-size: var(--text-base);
}

.writing-footer__see-also-link:hover {
  color: var(--accent);
}

.writing-footer__see-also-tag {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  color: var(--ink-tertiary);
  letter-spacing: var(--tracking-wide);
  white-space: nowrap;
}
```

---

## 3 · Replacing the existing trailing block in `pixels-to-atoms.md`

The current post ends (per Claude Code's audit, lines 113–120) with a markdown `---` rule, demo links, and a sign-off. That block should be replaced with raw HTML using the new pattern. Astro markdown pages allow raw HTML, so no template change is needed.

**Replace this kind of trailing block:**

```markdown
---

[Try the live demo](/demo) · [Read the case study](/work/directive-engine)

— Nathan Barnes / barnes.ngb@gmail.com
```

**With this:**

```html
<footer class="writing-footer">
  <div class="writing-footer__end-mark">— end · entry 011 · 2026-05-13</div>

  <div class="writing-footer__byline">
    <div class="writing-footer__name">Nathan Barnes</div>
    <div class="writing-footer__role">
      Design-to-Fabrication Systems Engineer ·
      <a href="mailto:barnes.ngb@gmail.com" class="writing-footer__contact">barnes.ngb@gmail.com</a>
    </div>
  </div>

  <div class="writing-footer__see-also">
    <div class="writing-footer__see-also-label">see also</div>
    <ul class="writing-footer__see-also-list">
      <li class="writing-footer__see-also-item">
        <a href="/work/directive-engine" class="writing-footer__see-also-link">Directive Engine</a>
        <span class="writing-footer__see-also-tag">instrument 03</span>
      </li>
      <li class="writing-footer__see-also-item">
        <a href="/demo" class="writing-footer__see-also-link">Live demo</a>
        <span class="writing-footer__see-also-tag">browser</span>
      </li>
    </ul>
  </div>
</footer>
```

The entry number and date in the end-mark should match the title block at the top of the post. If the post's title block reads `writing / 2026 · 01`, the end-mark reads `— end · entry 011 · 2026-05-13` (entry numbers are zero-padded to three digits; the year-prefix in the title block and the entry-NNN in the footer are two views of the same identifier — entry `011` is "post 11 of all time", `writing / 2026 · 01` is "first post of 2026").

If that dual-numbering feels redundant on review, simplify the end-mark to `— end · 2026-05-13` and use only the year-prefix in the title block. Either is fine — pick one and commit.

---

## 4 · Claude Code prompt to apply this amendment

Run in a fresh session in the site repo:

```
Read docs/visual-system/phase-2-writing-footer-amendment.md.
Also read docs/visual-system/VISUAL_SYSTEM.md to understand existing context.

Scope for this session:
1. Apply the spec text from §1 of the amendment to VISUAL_SYSTEM.md.
   Insert §2.9 between §2.8 and §3. Update the Phase 2 bullet in §3 per the diff.
2. Append the CSS from §2 of the amendment to src/styles/components.css.
3. Replace the trailing block in src/pages/writing/pixels-to-atoms.md per §3
   of the amendment. Use the published date and entry number consistent with
   the post's existing title block.

Hard rules:
- Use existing tokens. Do NOT introduce new CSS variables.
- Do not modify any other page in /writing this session — only pixels-to-atoms.
- Do not touch other components.
- Show me the diff for each of the three files before committing.
- If the existing trailing block has links I haven't anticipated (additional
  related posts, other instruments), include them as additional .see-also
  items rather than dropping them. If unsure, ask.

Definition of done:
- VISUAL_SYSTEM.md has §2.9 and an updated §3 Phase 2 bullet
- components.css has the .writing-footer block appended
- pixels-to-atoms.md renders with the new footer; npx astro build passes
- One commit on a new branch (suggested: visual-system/writing-footer)
```

---

## 5 · What this amendment does not cover

- **Lab entry footers.** The lab page (§2.8) uses a different content model — log-like entries, not authored essays. When `/lab` ships, a separate `.lab-entry-footer` may be needed (or the lab entries may not need a footer at all). Decide then, not now.
- **Pagination / archive nav.** `Previous: X` in the see-also list handles per-post backward navigation. A standalone archive page (`/writing/`) is a separate v1 question.
- **RSS / subscribe surface.** If you add a feed, the affordance lives in the site footer (global) or the writing index page, not in `.writing-footer`. The post footer stays restrained.
- **Open Graph / social card metadata.** Out of scope — that's `<head>` work, not visual system work.
