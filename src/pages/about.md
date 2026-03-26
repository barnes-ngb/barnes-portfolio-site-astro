---
layout: ../layouts/BaseLayout.astro
title: "About"
description: "Software engineer building calibrated instruments for architectural fabrication — geometry tools, directive systems, and field verification pipelines."
---

# About

## Who I am

I've spent the last decade at [A. Zahner Company](https://www.azahner.com/) — one of the most technically demanding architectural metal fabricators in the country — building the software layer between design models and the shop floor.

I started as a project engineer managing $2–10M metal facade installations, translating architectural intent into fabrication instructions while standing between architects, CNC operators, and field crews. I kept running into the same problem: the gap between what was designed and what could actually be built was filled with spreadsheets, tribal knowledge, and manual translation.

So I started building tools to close that gap. A CNC automation platform adopted by 30+ engineers. A customer-facing 3D configurator. A real-time field verification system I personally deployed on-site. Fabrication constraint APIs that catch infeasible geometry before it reaches the shop.

I call these tools **instruments** — because like a good measuring instrument, they're precise, reliable, and transparent about what they're measuring. The philosophy below explains how I think about building them.

---

## Operating Principles

The instruments I build share common calibration standards:

<div class="directive-card">
  <h4 class="directive-card__title">Constraints-Aware</h4>
  <div class="directive-card__constraints">
    <span class="chip chip--clamped">DOF LIMITS</span>
    <span class="chip">DEPENDENCIES</span>
  </div>
  <p class="directive-card__action">Every correction lives within physical and procedural limits. No impossible instructions.</p>
</div>

<div class="directive-card">
  <h4 class="directive-card__title">Verification-First</h4>
  <div class="directive-card__constraints">
    <span class="chip chip--ok">PASS</span>
    <span class="chip chip--blocked">FAIL</span>
  </div>
  <p class="directive-card__action">Before/after metrics that prove the gap is closed. No "trust me" outputs.</p>
</div>

<div class="directive-card">
  <h4 class="directive-card__title">Field-Executable</h4>
  <div class="directive-card__constraints">
    <span class="chip">UNAMBIGUOUS</span>
    <span class="chip">REFERENCE FRAME</span>
  </div>
  <p class="directive-card__action">Clear steps in known coordinate systems. No interpretation required.</p>
</div>

> The best software for physical work acts like a good instrument: precise, reliable, and transparent about what it's measuring.

---

## Technical Specification

<div class="metric-grid">
  <div class="metric-card">
    <span class="metric-card__label">Languages</span>
    <span class="metric-card__value" style="font-size: 1.1rem;">Python, C#, TypeScript</span>
  </div>
  <div class="metric-card">
    <span class="metric-card__label">Approach</span>
    <span class="metric-card__value" style="font-size: 1.1rem;">Pragmatic Automation</span>
  </div>
</div>

**Domains:**
- Geometry pipelines (mesh/NURBS/point cloud)
- Tolerance analysis and deviation mapping
- Web 3D visualization (Three.js, browser-first)
- Field-to-model alignment workflows

---

## Current Instrument

Building the **Directive Engine**: a system that converts nominal ↔ as-built deltas into installer-ready directive cards with 3D visualization and verification loops.

<div class="artifact-bar">
  <a href="/demo/" class="btn btn--primary">Try the Demo</a>
  <a href="/work/directive-engine/" class="artifact-link">Case Study →</a>
</div>

---

## What I'm looking for

I'm exploring roles at the intersection of design, fabrication, and software — particularly at early-stage companies in AEC-prefab, modular construction, or manufacturing automation where my combination of architecture training, fabrication floor experience, and full-stack engineering creates real leverage.

I'm at my best when I'm building systems that other people can use repeatedly, working close to the physical problem, and helping grow the people around me.

[Resume (PDF) →](/resume.pdf) · [LinkedIn →](https://linkedin.com/in/barnesngb) · [Email →](mailto:barnes.ngb@gmail.com)

---

## Contact

<div class="artifact-bar">
  <a href="mailto:barnes.ngb@gmail.com" class="artifact-link">barnes.ngb@gmail.com</a>
  <a href="https://www.linkedin.com/in/barnesngb/" class="artifact-link">LinkedIn</a>
  <a href="https://github.com/barnes-ngb" class="artifact-link">GitHub</a>
</div>
