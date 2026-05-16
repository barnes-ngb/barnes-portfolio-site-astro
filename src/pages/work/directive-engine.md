---
layout: ../../layouts/BaseLayout.astro
title: "Directive Engine"
description: "Pixels to atoms — a directive engine that bridges detection and execution for field teams, with installer-language directives and pass/fail verification."
---

<div class="title-block">
  <div class="title-block__id">work / instrument 01 · rev 2</div>
  <span class="status-chip status-chip--deployed">deployed</span>
</div>

<div class="page-header">
  <h1 class="page-header__title">Directive Engine</h1>
  <p class="page-header__subtitle">Pixels to atoms — a directive engine that bridges detection and execution for field teams. Deviations in, installer-language directives out, with pass/fail verification of closure.</p>
</div>

<div class="metadata-strip">
  <span><span class="metadata-strip__label">built </span>2025</span>
  <span><span class="metadata-strip__label">stack </span>ts · three.js · vite</span>
  <span><span class="metadata-strip__label">tol </span>±2.0mm</span>
  <span><span class="metadata-strip__label">stage </span>v0.2</span>
</div>

<p><a href="https://directive-engine.vercel.app/" target="_blank" rel="noopener">Open live demo</a> · <a href="https://github.com/barnes-ngb/directive-engine" target="_blank" rel="noopener">Repository</a> · <a href="mailto:barnes.ngb@gmail.com">Contact</a></p>

<figure class="figure">
  <img src="/images/Directive-Engine.png" alt="Directive Engine viewer showing the toy_facade_v1 fixture with deviation highlights." />
  <figcaption class="figure__caption">fig 01 · directive engine viewer — toy_facade_v1 fixture</figcaption>
</figure>

<div class="section-header">
  <div class="section-header__index">01 · problem</div>
  <h2>Problem</h2>
</div>

When something is off in the field, the hardest part is not detecting it — it's expressing the correction in a field-executable format that's:

1. Unambiguous — a directive an installer can execute with a wrench. *"Translate +3.2mm along slot S2"*, not *"translate +3.2mm in part-frame Y."*
2. Constrained — respects what the part is *physically allowed* to do: named pivots, slots, and indexed bolt patterns, not abstract axes.
3. Verifiable — pass/fail closure check after adjustment. Did the residual drop inside tolerance?

<div class="section-header">
  <div class="section-header__index">02 · signal</div>
  <h2>Inputs</h2>
</div>

Two inputs feed the engine: a nominal model (design intent — 3D geometry plus named features) and an as-built scan (field reality — point cloud or survey data).

Data format: JSON contracts for as-built poses, constraint metadata (joints, slots, indexed patterns), and directive outputs. Schemas live in the repo; the engine output is identical with or without named features declared — features are pure presentation metadata.

<div class="section-header">
  <div class="section-header__index">03 · calibration</div>
  <h2>Calibration and constraints</h2>
</div>

The engine operates on a calibrated frame: as-built poses expressed in a shared world coordinate system, with each part's pose represented as `T_world_part` (translation + quaternion). The v0.2 demo runs on the synthetic `toy_facade_v1` fixture — a 12-panel subsection with deviations designed to exercise the contract end-to-end.

Worst deviation on the fixture: ~8mm before apply, <1mm after apply (within the ±2.0mm tolerance). The geometry and deviations are synthetic — designed to exercise the contract — but the engine math (DOF projection, indexed rotation quantization, status logic) is real and unit-tested. The same primitives generalize to larger installs.

Each part declares its kinematic features — the things an installer can actually adjust. The engine projects raw deviations onto these features, so corrections come out in the vocabulary of the hardware, not abstract axes.

<div class="artifact-card">
  <div class="artifact-card__header">
    <span class="artifact-card__id">panel p-05 · constraints</span>
  </div>
  <div><span class="artifact-card__field-label">j1 </span>pivot</div>
  <div><span class="artifact-card__field-label">s2 </span>slot (±10mm lateral)</div>
  <div><span class="artifact-card__field-label">p3 </span>index (4-position bolt pattern)</div>
</div>

Allowed motion: pivot about joint J1, slide along lateral mounting slot S2, and rotate to one of four discrete index positions on bolt pattern P3. Everything else is held by the structure. Corrections that don't fit are `clamped` or `blocked` — never silently rounded.

<div class="section-header">
  <div class="section-header__index">04 · action</div>
  <h2>Action format — directive card</h2>
</div>

The engine emits directive cards — structured correction instructions in installer language:

<div class="artifact-card">
  <div class="artifact-card__header">
    <span class="artifact-card__id">directive · p-05</span>
    <span class="status-chip status-chip--pending">pending</span>
  </div>
  <div><span class="artifact-card__field-label">action </span>translate −6.5mm along slot s2; rotate to index 0 on p3</div>
  <div><span class="artifact-card__field-label">frame  </span>part-local, features declared in <code>constraints.json</code></div>
  <div><span class="artifact-card__field-label">tol    </span>±2.0mm translation · ±1.0° rotation</div>
  <div><span class="artifact-card__field-label">verify </span>before/after deviation metric, status flips <code>pending → ok</code> within tolerance</div>
</div>

The mapping from engine math to physical features happens in `src/presentation/format-directive.ts`; the engine stays generic, the language stays installer-facing.

<div class="section-header">
  <div class="section-header__index">05 · verification</div>
  <h2>Verification loop</h2>
</div>

The live demo walks through the loop in five beats — detection, constraint, directive, apply, verify — on the synthetic `toy_facade_v1` fixture. Try it on desktop or mobile: <a href="https://directive-engine.vercel.app/" target="_blank" rel="noopener">open live demo</a> · <a href="/demo/">demo walkthrough</a>.

<div class="artifact-card">
  <div class="artifact-card__header">
    <span class="artifact-card__id">verification · toy_facade_v1</span>
    <span class="status-chip status-chip--deployed">pass</span>
  </div>
  <div><span class="artifact-card__field-label">before </span>~8mm worst-panel deviation</div>
  <div><span class="artifact-card__field-label">after  </span>&lt;1mm worst-panel deviation</div>
  <div><span class="artifact-card__field-label">tol    </span>±2.0mm</div>
</div>

1. Detection — as-built scene loads. Panels glow yellow or red where deviation exceeds tolerance.
2. Constraint — camera dollies to the worst panel. Allowed DOF surface as named features.
3. Directive — engine emits the correction as an installer-language card.
4. Apply (simulated) — panel animates to corrected pose. Status flips `pending → ok`.
5. Verify — camera returns to the wide shot. Before/after metric closes the loop.

<div class="section-header">
  <div class="section-header__index">06 · artifacts</div>
  <h2>Artifacts</h2>
</div>

<a href="https://directive-engine.vercel.app/" target="_blank" rel="noopener">Live demo</a> · <a href="https://github.com/barnes-ngb/directive-engine" target="_blank" rel="noopener">Repository</a> · <a href="/demo/">Demo walkthrough</a>

### Run it on your own scan

The repository ships with a small CLI that runs the engine against a real point cloud. It accepts an ASCII PLY or XYZ scan plus a nominal-parts JSON describing the part geometries, then prints the resulting directives in human-readable form to the console. The committed example files in `examples/` make this reproducible without any setup beyond cloning, and the end-to-end test suite exercises the same path against those files.

```bash
git clone https://github.com/barnes-ngb/directive-engine
cd directive-engine && npm install
npx tsx scripts/ingest-pointcloud.ts examples/minimal-scan.ply examples/minimal-parts.json
```

Expected output:

```
Parsed 20 points from examples/minimal-scan.ply
  P-01: t=[0.03, 500.00, 0.00]mm  confidence=70.0%
  P-02: t=[506.00, 500.00, 0.00]mm  confidence=70.0%
  P-01: No adjustment required (within tolerance). Status: ok. Tolerance: ±5.0mm.
  P-02: Translate -6.0mm along part-frame X. Status: pending. Tolerance: ±5.0mm.
```

Same primitives the demo uses, different input format. An in-browser interactive version is a planned next iteration; the CLI is the present way to verify the engine works on real input.

### Why this generalizes

The primitives — pose as `T_world_part` with a quaternion, DOF projection onto declared kinematic features, indexed-rotation quantization, tolerance clamping, before/after verification — are domain-agnostic. The directive engine is the *generation* half of the loop (deviation → instruction). For the *capture* half (as-built reality → deviation) in an aerospace-flavored deployment, see <a href="https://www.azahner.com/labs/surveylink/" target="_blank" rel="noopener external">SurveyLink</a>, a real-time link between as-designed models and as-built field data.

### Roadmap

- Real scan-data ingestion on top of the existing contract
- Step ordering / dependencies (anchors → part → verification)
- Confidence scoring with `needs_review` flags surfaced in the UI
- Tolerance heatmaps to spot systemic drift across a facade
- AR overlay as an output target — not the core product

<aside class="limits-callout">
  <div class="limits-callout__label">limits</div>
  <ul>
    <li>Synthetic fixture (<code>toy_facade_v1</code>) — real scan-data ingestion not yet wired in</li>
    <li>Single-part directives per beat (no multi-part dependency chains yet)</li>
    <li>Browser-only viewer (no native mobile app)</li>
    <li>Prototype: engine math is unit-tested, but the end-to-end loop hasn't been run against a field deployment</li>
  </ul>
</aside>
