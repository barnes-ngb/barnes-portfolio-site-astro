---
layout: ../../layouts/BaseLayout.astro
title: "Directive Engine"
description: "Align reality to intent → generate installer-ready directives."
---

# Directive Engine
**One-liner:** Convert nominal ↔ as-built deltas into **installer-ready directive cards** (move/rotate/index), with visualization and verification.

[directive-engine](https://directive-engine.vercel.app/)

![Directive Engine Screenshot](../../public/images/Directive-Engine.png)

- Demo video (60–90s): **(add link)**

- Repo: **(add link)**
- Contact: **barnes.ngb@gmail.com**

---

## The problem
When something is off in the field, the hardest part is not detecting it — it’s expressing the correction in a **field-executable format** that’s:
- unambiguous,
- constrained by what’s physically allowed,
- and verifiable after adjustment.

## What the demo shows
1) Load nominal + as-built dataset  
2) Compute correction deltas  
3) Generate directive cards  
4) Visualize corrections (gizmo/axes)  
5) Export directives (JSON/CSV)  
6) Verify closure with a before/after metric

## Directive card example
**Part:** `P-0132`  
**Action:** translate + rotate index  
**Frame:** part-local (or site grid)  
**Verify:** after deviation < tolerance

## Roadmap
- Step ordering / dependencies (anchors → part → verification)
- Confidence scoring + “needs review” flags
- Tolerance heatmaps / clustering
- Optional: AR overlay as a *skin*, not the core
