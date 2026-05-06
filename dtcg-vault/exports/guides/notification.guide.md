---
schema: foundry-guide-v1
title: Guide — Notification
component: notification
category: deployment
---

# Deployment Guide

## Overview
Inline messaging — informational, positive, caution, critical. Toast variant subsequent milestone.

## Technical Recipe

### HTML
```html
<aside class="ps-notif ps-notif--{{variant}}" role="status" aria-live="polite">
  <span class="ps-notif__title">{{title}}</span>
  <p class="ps-notif__body">{{body}}</p>
</aside>
```

### CSS
```css
.ps-notif{padding:var(--ps-space-4,12px) var(--ps-space-5,16px);border-left:4px solid;border-radius:var(--ps-corner-2,4px)}.ps-notif--info{background-color:var(--ps-support-info-bg,#eef3ff);border-color:var(--ps-support-info,#234ed8)}.ps-notif--positive{background-color:var(--ps-support-positive-bg,#e8f6ed);border-color:var(--ps-support-positive,#26823f)}.ps-notif--caution{background-color:var(--ps-support-caution-bg,#fff5e1);border-color:var(--ps-support-caution,#a87514)}.ps-notif--critical{background-color:var(--ps-support-critical-bg,#fceaea);border-color:var(--ps-support-critical,#a52323)}.ps-notif__title{display:block;font-weight:600;margin-bottom:var(--ps-space-2,4px)}.ps-notif__body{margin:0;font-size:.875rem;line-height:1.43}
```

## Accessibility
role='status' announces inline (aria-live='polite'). Critical notifications use role='alert' aria-live='assertive' for time-sensitive failures. Notifications never auto-disappear without an undo affordance.
