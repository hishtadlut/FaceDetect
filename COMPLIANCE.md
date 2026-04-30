## EU AI Act Compliance Notice

### Scope

This codebase performs **face detection only** — it uses Haar Cascade classifiers to locate faces in static images or webcam frames and draws bounding boxes around them.

**This codebase does NOT perform:**
- Face recognition or biometric identification
- Biometric verification (one-to-one identity confirmation)
- Emotion recognition, stress/mood/intent inference, or affect detection
- Biometric categorisation (age, sex, ethnicity, health, etc.)

### Data Handling

No biometric templates, face embeddings, or identifying metadata are stored, transmitted, or persisted. All processing is local and in-memory only.

### Intended Use

This is a tutorial/demonstration project accompanying a Real Python blog post. It is intended for educational purposes and local-only processing.

### AI Act Classification

This codebase does **not** fall under Annex III high-risk biometric AI or Article 5 prohibited practices of the EU AI Act. Face detection (locating where a face is) is a lower-level computer vision operation distinct from biometric identification (determining whose face it is), biometric categorisation, or emotion recognition as defined in Article 3.

### Manual Review Items

A qualified reviewer should confirm:

1. Whether this code is deployed, shipped to customers, or offered as a service (determines whether Article 50 transparency obligations attach).
2. Whether any downstream consumer combines the detection output with face recognition, emotion inference, or biometric categorisation models.
3. Whether the camera capture in `live.py` is ever used in a workplace or educational setting.
4. Whether detected face regions (ROI crops) are ever stored, logged, or transmitted to another system.
5. Whether any consuming service uses face detection as a gate for biometric identification or categorisation.
6. Whether the `haarcascade_frontalface_default.xml` model is known to contain or encode biometric templates (standard Haar cascades do not).

This document is a preliminary compliance assessment, not a legal conclusion. Review by qualified counsel or a DPO is required.
