---
layout: page
title: IRIS
description: AI-powered mobile diagnostic tool for retinal disease screening
img: assets/img/projects/iris/hero.jpg
importance: 1
category: work
related_publications: false
github: "https://github.com/aywhoosh/IRIS"
---

Modern healthcare infrastructure struggles to provide timely ocular screening in underserved areas. IRIS addresses this by putting diagnostic-grade retinal imaging directly into clinicians' hands through a mobile-first application powered by few-shot learning.

The system handles the complete diagnostic workflow: capture or upload a retinal fundus image, run inference against a fine-tuned DenseNet121 backbone with Prototypical Networks, and return structured results with confidence scores and clinical recommendations—all within 2-3 seconds.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <div class="embed-responsive embed-responsive-16by9">
            <iframe class="embed-responsive-item" src="https://www.youtube.com/embed/2kp05iu2q0g" allowfullscreen></iframe>
        </div>
    </div>
</div>
<div class="caption">
    Complete diagnostic workflow demonstration
</div>

## Technical Architecture

The application separates concerns across three layers: a Flutter mobile client for capture and display, Supabase for authentication and persistent storage, and a FastAPI inference service running on AWS EC2.

When a user captures an image, it uploads directly to Supabase Storage while scan metadata writes to PostgreSQL. The mobile client then posts the image URL to the FastAPI endpoint, which retrieves the file, preprocesses it for the model, and runs inference using a TorchScript-serialized classifier. The API responds with structured JSON containing the predicted condition, confidence intervals, severity classification, and evidence-based recommendations.

This architecture keeps the mobile app lightweight while centralizing model updates and versioning on the backend. The EC2 instance runs inside a Docker container for consistent deployments, and the TorchScript format eliminates Python runtime overhead during inference.

## Model Design

The diagnostic model uses a two-stage approach: a DenseNet121 encoder pretrained on ImageNet extracts visual features, then Prototypical Networks perform few-shot classification across five ocular conditions (normal, diabetic retinopathy, glaucoma, cataracts, and age-related macular degeneration).

This design choice matters because annotated medical imaging datasets are small and expensive to produce. Few-shot learning lets the model generalize from limited examples per class while maintaining clinical accuracy. During inference, the model computes prototypical embeddings for each condition and classifies new images based on nearest-neighbor distance in feature space.

## Clinical Integration

The interface design prioritizes clinical usability. Guided capture overlays show proper positioning and lighting requirements. The processing state uses a pulsating shader animation that communicates progress without appearing frivolous. Results display condition, confidence, and severity on a single screen with expandable sections for detailed recommendations and scan history.

Authentication flows through Supabase Auth, which handles secure session management and role-based access. Patient profiles link to scan history, creating a longitudinal view of ocular health that supports monitoring and early intervention.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/iris/register.jpg" title="registration screen" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/iris/login.jpg" title="authentication flow" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/iris/profile.jpg" title="patient profile and history" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Supabase handles authentication, session management, and patient profile storage
</div>

## Diagnostic Workflow

The capture interface provides real-time feedback on image quality before submission. Users can either capture directly through the camera with positioning guides or upload existing fundus photographs from their gallery. Once submitted, the image streams to Supabase Storage while the app polls the FastAPI endpoint for processing status.

The processing screen deliberately uses animation to communicate system state—medical software often leaves users uncertain about whether their request succeeded. The shader-based orb effect provides continuous visual feedback without requiring additional network calls or battery-intensive operations.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/iris/home_and_camera.jpg" title="capture interface with guides" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/iris/processing_screen.jpg" title="inference processing state" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/iris/scan_result.jpg" title="diagnostic results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The complete diagnostic loop: capture, process, and display results with clinical recommendations
</div>

Results include the predicted condition, model confidence as a percentage, severity grading, and evidence-based next steps. Tapping into detailed diagnosis reveals additional context about the detected condition, risk factors, and recommended follow-up intervals.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/iris/detailed_diagnosis.jpg" title="expanded diagnosis view with recommendations" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Detailed diagnostic information with clinical context and follow-up guidance
</div>

## Implementation Notes

The FastAPI backend uses async handlers to prevent request blocking during inference. The TorchScript model loads once at startup and persists in memory, eliminating serialization overhead on each request. Image preprocessing normalizes pixel values and resizes inputs to the expected 224×224 resolution before feeding them to the encoder.

Supabase Row Level Security policies ensure users only access their own scans and profile data. Storage buckets apply similar access controls, with pre-signed URLs generated server-side to prevent unauthorized downloads.

The Flutter app maintains offline capability for viewing scan history, syncing new results when connectivity returns. State management uses Provider for reactive updates across the UI without prop drilling.

## Stack Summary

**Mobile**: Flutter 3.0+, Dart, Provider for state management  
**Backend**: Python, FastAPI, TorchScript model serving  
**Database**: Supabase (PostgreSQL, Auth, Storage)  
**Infrastructure**: AWS EC2, Docker  
**ML Framework**: PyTorch, DenseNet121, Prototypical Networks

The complete source code, model training notebooks, and deployment configurations are available in the [GitHub repository](https://github.com/aywhoosh/IRIS).
