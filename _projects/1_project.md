---
layout: page
title: IRIS
description: Intelligent Retinal Imaging System (Flutter + FastAPI + Supabase + AWS EC2)
img: assets/img/projects/iris/hero.jpg
importance: 1
category: work
github: https://github.com/aywhoosh/IRIS
related_publications: false
---

IRIS is an end-to-end, AI-powered mobile app for ocular disease screening. You capture or upload a retinal image, authenticate via Supabase, and get a real-time diagnosis from a FastAPI inference API hosted on AWS EC2.

[![GitHub Repo](https://img.shields.io/badge/GitHub-aywhoosh%2FIRIS-181717?style=flat-square&logo=github)](https://github.com/aywhoosh/IRIS)
[![Stars](https://img.shields.io/github/stars/aywhoosh/IRIS?style=flat-square)](https://github.com/aywhoosh/IRIS)
[![Last commit](https://img.shields.io/github/last-commit/aywhoosh/IRIS?style=flat-square)](https://github.com/aywhoosh/IRIS)
[![License](https://img.shields.io/github/license/aywhoosh/IRIS?style=flat-square)](https://github.com/aywhoosh/IRIS/blob/main/LICENSE)

## Highlights

- **Highly available inference API** on AWS EC2 using **Docker + FastAPI**, built for high uptime and low-latency responses.
- **2 to 3 second classification responses** for a snappy scan-to-result loop.
- **Supabase-backed workflow**: auth, profiles, storage, and scan history.
- **Product-first UX**: guided capture and a playful processing animation that still feels clinical.

## Stack

- **Mobile:** Flutter (Dart)
- **Backend:** Python, FastAPI, TorchScript model serving
- **Auth + Data:** Supabase (Auth, Storage, DB)
- **Infra:** AWS EC2, Docker

## Architecture

1. Flutter app captures or uploads an image.
2. Supabase Storage stores the image and Supabase DB stores scan metadata.
3. FastAPI on AWS EC2 orchestrates inference.
4. TorchScript model returns a JSON diagnosis to the app.

## Repository map

```text
.
├── app/              # Flutter front-end
├── backend/          # FastAPI service (EC2 / container)
├── model_backend/    # Standalone model service (optional)
└── screenshots/
```

---

## Screenshots

**Setup tip (recommended):**

- Create `assets/img/projects/iris/` in this portfolio repo.
- Copy the screenshots from the IRIS repo (`IRIS/screenshots/`) into that folder.
- Duplicate one screenshot (suggestion: `home_and_camera.jpg`) as `hero.jpg` for the project card background.

### Authentication

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/iris/register.jpg" title="Register" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/iris/login.jpg" title="Login" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/iris/profile.jpg" title="Profile" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Supabase auth, a clean onboarding flow, and a simple profile and history area.
</div>

### Scan flow

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/iris/home_and_camera.jpg" title="Home + Camera" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/iris/processing_screen.jpg" title="Processing" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/iris/scan_result.jpg" title="Results" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Capture or upload, watch the processing animation, and land on results quickly.
</div>

### Details view

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/detailed_diagnosis.jpg" title="Detailed diagnosis" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/hero.jpg" title="Project card hero" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  A deeper breakdown for the diagnosis details, plus a hero image that looks good on the projects grid.
</div>

---

## Links

- Repository: [aywhoosh/IRIS](https://github.com/aywhoosh/IRIS)
- Screenshots folder: [IRIS/screenshots](https://github.com/aywhoosh/IRIS/tree/main/screenshots)
