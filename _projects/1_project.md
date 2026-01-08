---
layout: page
title: IRIS
description: Few-shot ocular disease screening (Flutter + FastAPI + Supabase + AWS EC2)
img: assets/img/projects/iris/hero.jpg
importance: 1
category: work
github: https://github.com/aywhoosh/IRIS
---

<!--
Assets note (optional but recommended for best visuals):
1) Create folder: assets/img/projects/iris/
2) Copy these screenshots from the IRIS repo into that folder and keep the same names:
   - register.jpg, login.jpg, home_and_camera.jpg, processing_screen.jpg, scan_result.jpg, detailed_diagnosis.jpg, profile.jpg
3) Pick one screenshot (I recommend home_and_camera.jpg) and duplicate it as: hero.jpg
-->

<p class="lead">
IRIS is an end-to-end, AI-powered mobile app for ocular disease screening. You capture or upload a retinal image,
authenticate via Supabase, and the app calls a model back-end on AWS EC2 to return a real-time diagnosis, plus scan history and profiles.
</p>

<p>
  <a href="https://github.com/aywhoosh/IRIS" target="_blank" rel="noopener">
    <img alt="GitHub Repo" src="https://img.shields.io/badge/GitHub-aywhoosh%2FIRIS-181717?style=flat-square&logo=github">
  </a>
  <a href="https://github.com/aywhoosh/IRIS" target="_blank" rel="noopener">
    <img alt="Stars" src="https://img.shields.io/github/stars/aywhoosh/IRIS?style=flat-square">
  </a>
  <a href="https://github.com/aywhoosh/IRIS" target="_blank" rel="noopener">
    <img alt="Last commit" src="https://img.shields.io/github/last-commit/aywhoosh/IRIS?style=flat-square">
  </a>
  <a href="https://github.com/aywhoosh/IRIS/blob/main/LICENSE" target="_blank" rel="noopener">
    <img alt="License" src="https://img.shields.io/github/license/aywhoosh/IRIS?style=flat-square">
  </a>
</p>

<div class="row">
  <div class="col-md-8">
    <h2>What it does</h2>
    <ul>
      <li><strong>Supabase Auth & Profiles</strong>: login and patient metadata.</li>
      <li><strong>Guided capture & upload</strong>: camera and gallery workflows with focus guides.</li>
      <li><strong>Real-time diagnostics</strong>: TorchScript model served via FastAPI on AWS.</li>
      <li><strong>Rich results</strong>: condition, confidence, severity and recommendations, with scan history.</li>
      <li><strong>Animated UI</strong>: shader backgrounds, pulsating orbs, smooth transitions.</li>
    </ul>

    <h2>Why I built it</h2>
    <p>
      I wanted a project that feels like a real product: an intuitive mobile experience backed by a production-style inference API.
      The fun part is the details: the guided capture flow, the fast feedback loop, and the way the UI makes a medical workflow feel approachable.
    </p>

    <h2>Architecture</h2>
    <p>
      The high-level flow is straightforward and intentionally modular:
    </p>
    <ol>
      <li><strong>Flutter app</strong> captures or uploads an image.</li>
      <li><strong>Supabase Storage</strong> stores the image, and <strong>Supabase DB</strong> stores scan history.</li>
      <li><strong>FastAPI on AWS EC2</strong> performs inference orchestration.</li>
      <li><strong>TorchScript model</strong> returns a JSON diagnosis back to the app.</li>
    </ol>

    <h2>API surface</h2>

    <div class="table-responsive">
      <table class="table table-sm">
        <thead>
          <tr><th>Verb</th><th>Path</th><th>Purpose</th></tr>
        </thead>
        <tbody>
          <tr><td><code>POST</code></td><td><code>/api/upload</code></td><td>Store image and start processing</td></tr>
          <tr><td><code>GET</code></td><td><code>/api/status/{id}</code></td><td>Poll processing job</td></tr>
          <tr><td><code>GET</code></td><td><code>/api/history</code></td><td>List scans for logged-in user</td></tr>
        </tbody>
      </table>
    </div>

    <h2>Deployment notes</h2>
    <ul>
      <li>Inference runs behind a FastAPI service on an AWS EC2 instance.</li>
      <li>Docker and a reverse proxy (NGINX + SSL) are the intended production setup.</li>
      <li>End-to-end latency is tuned for a snappy user experience (single-digit seconds for classification).</li>
    </ul>

    <h2>Repo structure</h2>

    <pre><code>.
├── app/              # Flutter front-end
├── backend/          # FastAPI service (EC2 / container)
├── model_backend/    # Standalone model service (optional)
└── screenshots/
</code></pre>
  </div>

  <div class="col-md-4 mt-3 mt-md-0">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Stack</h5>
        <ul class="mb-0">
          <li>Flutter, Dart</li>
          <li>FastAPI (Python)</li>
          <li>Supabase (Auth, Storage, DB)</li>
          <li>AWS EC2</li>
          <li>TorchScript model serving</li>
        </ul>
      </div>
    </div>

    <div class="card mt-3">
      <div class="card-body">
        <h5 class="card-title">Links</h5>
        <ul class="mb-0">
          <li><a href="https://github.com/aywhoosh/IRIS" target="_blank" rel="noopener">Repository</a></li>
          <li><a href="https://github.com/aywhoosh/IRIS/blob/main/readme.md" target="_blank" rel="noopener">README</a></li>
          <li><a href="https://github.com/aywhoosh/IRIS/tree/main/screenshots" target="_blank" rel="noopener">Screenshots</a></li>
        </ul>
      </div>
    </div>
  </div>
</div>

<hr>

<h2>Screenshots</h2>

<h3>Authentication</h3>
<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/register.jpg" title="Register screen" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/login.jpg" title="Login screen" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Clean onboarding with Supabase authentication.
</div>

<h3>Main workflow</h3>
<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/home_and_camera.jpg" title="Home and camera screen" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/processing_screen.jpg" title="Processing animation" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/scan_result.jpg" title="Scan results" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Capture, upload, and get results with a playful UI that still feels clinical.
</div>

<h3>Details and profile</h3>
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/detailed_diagnosis.jpg" title="Detailed diagnosis view" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/projects/iris/profile.jpg" title="Profile screen" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  A deeper view for diagnosis details, plus a simple profile and history area.
</div>
