---
layout: ../../layouts/BaseLayout.astro
title: "Instrument Template"
description: "Template for documenting instruments using the calibration-first approach: Problem → Signal → Calibration → Constraints → Action → Verification → Artifacts."
---

# Instrument Documentation Template

This template provides a consistent structure for documenting instruments (projects) using the calibration-first, field-runbook approach.

<div class="callout callout--info">
  <span class="callout__icon">📐</span>
  <div class="callout__content">
    <strong>Philosophy:</strong> Every project is an instrument with inputs, calibration requirements, constraints, action formats, and verification protocols. Document accordingly.
  </div>
</div>

---

## Template Structure

Copy the sections below when creating a new case study. Replace placeholder content with your specifics.

---

### 1. Hero Section

```html
<div class="instrument-hero">
  <div class="instrument-hero__status">
    <span class="chip chip--ok">STATUS</span>
    <span class="chip">TAG</span>
  </div>
  <h1 class="instrument-hero__title">[Instrument Name]</h1>
  <p class="instrument-hero__subtitle">[One-line description of what it does]</p>
</div>
```

**Status chip options:**
- `chip--ok` — Calibrated, deployed, verified
- `chip--pending` — In development, awaiting validation
- `chip--clamped` — Limited scope, constrained
- `chip--blocked` — Blocked, known issues
- `chip--review` — Needs review, marginal

---

### 2. Problem

Describe what problem this instrument solves. Focus on the gap between current state and desired state.

```markdown
## Problem

When [situation], the hardest part is not [obvious thing] — it's [harder thing] that's:

<div class="steps">
  <div class="step">
    <span class="step__number">1</span>
    <div class="step__content">
      <div class="step__title">[Requirement 1]</div>
      <div class="step__description">[Why this matters]</div>
    </div>
  </div>
  <!-- Add more steps as needed -->
</div>
```

---

### 3. Inputs (Signal)

What data does the instrument consume? Be specific about formats and sources.

```html
<div class="metric-grid">
  <div class="metric-card">
    <span class="metric-card__label">[Input Type]</span>
    <span class="metric-card__value">[Value/Description]</span>
    <span class="metric-card__unit">[Format/Source]</span>
  </div>
</div>
```

---

### 4. Calibration

How does the instrument align or validate its inputs? What metrics indicate good calibration?

```html
<div class="metric-grid">
  <div class="metric-card">
    <span class="metric-card__label">[Metric Name]</span>
    <span class="metric-card__value">[Value]<span class="metric-card__unit">[unit]</span></span>
    <div class="metric-card__status">
      <span class="chip chip--ok">PASS</span> [threshold description]
    </div>
  </div>
</div>
```

Include calibration warnings:

```html
<div class="callout callout--warning">
  <span class="callout__icon">⚠</span>
  <div class="callout__content">
    <div class="callout__title">Calibration Warning</div>
    If [condition], [consequence and recommended action].
  </div>
</div>
```

---

### 5. Constraints / DOF

What limits the valid solution space? Express as degrees of freedom or constraint tags.

```html
<div class="directive-card">
  <h4 class="directive-card__title">[Component/Context]</h4>
  <div class="directive-card__constraints">
    <span class="chip chip--clamped">[CONSTRAINT]</span>
    <span class="chip chip--ok">[FREE DOF]</span>
  </div>
  <p class="directive-card__action">[Explanation of what's allowed/not allowed]</p>
  <div class="directive-card__dof">DOF: X of Y</div>
</div>
```

---

### 6. Action Format

What does the instrument output? Show the structure of the directive/action/result.

```html
<div class="directive-card">
  <div class="directive-card__header">
    <h4 class="directive-card__title">[OUTPUT TYPE]: [ID]</h4>
    <span class="chip chip--pending">PENDING</span>
  </div>
  <div class="directive-card__constraints">
    <span class="chip">[ACTION TYPE]</span>
  </div>
  <p class="directive-card__action">
    <strong>Action:</strong> [Specific instruction]<br>
    <strong>Frame:</strong> [Reference frame]<br>
    <strong>Verify:</strong> [Verification criteria]
  </p>
  <div class="directive-card__dof">[Expected outcome metric]</div>
</div>
```

---

### 7. Verification Loop

How is success measured? Show the verification workflow.

```html
<div class="verification-panel">
  <div class="verification-panel__header">Verification Result</div>
  <div class="verification-panel__body">
    <div class="verification-panel__result">
      <span class="chip chip--ok">PASS</span>
      <span>[Metric]: <code>[value]</code> (tolerance: [threshold])</span>
    </div>
  </div>
</div>
```

Describe the verification steps:

```html
<div class="steps">
  <div class="step">
    <span class="step__number">1</span>
    <div class="step__content">
      <div class="step__title">[Step Name]</div>
      <div class="step__description">[What happens]</div>
    </div>
  </div>
</div>
```

---

### 8. Artifacts

Link to all external resources:

```html
<div class="artifact-bar">
  <a href="[URL]" class="artifact-link">Live Demo</a>
  <a href="[URL]" class="artifact-link">Repository</a>
  <a href="[URL]" class="artifact-link">Dataset</a>
  <a href="[URL]" class="artifact-link">Documentation</a>
</div>
```

---

### 9. Limits + Next Steps

Be honest about current limitations:

```html
<div class="callout callout--info">
  <span class="callout__icon">📋</span>
  <div class="callout__content">
    <div class="callout__title">Current Limits</div>
    <ul style="margin-bottom:0">
      <li>[Limitation 1]</li>
      <li>[Limitation 2]</li>
    </ul>
  </div>
</div>
```

Then list the roadmap as bullet points:

```markdown
**Roadmap:**
- [Next feature/improvement]
- [Future capability]
```

---

## Full Example

See the [Directive Engine case study](/work/directive-engine/) for a complete implementation of this template.

---

## Component Reference

| Component | Use |
|-----------|-----|
| `metric-card` | Display calibration values, readings |
| `chip chip--ok` | PASS, verified, deployed |
| `chip chip--pending` | In progress, awaiting |
| `chip chip--clamped` | Constrained, bounded |
| `chip chip--blocked` | Blocked, failed |
| `chip chip--review` | Needs attention |
| `callout--info` | Informational notes |
| `callout--warning` | Calibration warnings |
| `callout--error` | Error conditions |
| `directive-card` | Action/output format |
| `verification-panel` | PASS/FAIL results |
| `steps` | Sequential procedures |
| `artifact-bar` | External resource links |

---

[Back to Instrument Catalog →](/work/)
