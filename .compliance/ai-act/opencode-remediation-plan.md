## EU AI Act Biometric Remediation Plan — FaceDetect Repository

### Overall Scope Assessment

**Likely out of scope for high-risk biometric AI areas under Annex III and Article 5.**

### Why

All three files (`face_detect.py`, `face_detect_cv3.py`, `live.py`) perform Haar Cascade **face detection** only — they locate faces in static images or webcam frames and draw bounding boxes. None of the scripts:

- Compare facial data to stored biometric templates → **not biometric identification** (Art. 3)
- Confirm a claimed identity against previously provided biometric data → **not biometric verification** (Art. 3)
- Infer emotions, stress, mood, intent, or affect from facial features → **not emotion recognition** (Art. 3)
- Assign people to categories (age, sex, ethnicity, health, etc.) on the basis of biometric data → **not biometric categorisation** (Art. 3)
- Store, persist, or transmit biometric templates or face embeddings → **not targeted scraping for facial recognition databases** (Art. 5)
- Run in a workplace or education setting to infer emotions → **not prohibited workplace/education emotion inference** (Art. 5)

Detection is a lower-level computer vision operation. It answers *where* a face is, not *whose* face it is. The EU AI Act regulates the *purpose* of biometric processing (identification, categorisation, emotion inference), not the underlying image-processing primitives.

The scanner flags are correct as "possible biometric image processing" signals — the code does process facial image data — but the specific AI Act high-risk thresholds are not crossed.

### Key Distinctions Confirmed

| Signal | Classification | Reasoning |
|---|---|---|
| `cv2.CascadeClassifier`, `detectMultiScale`, `cv2.VideoCapture` | **Not identification / not categorisation / not emotion recognition** | Merely detects the presence and location of faces; no identity, trait, or emotion inference |
| Webcam live capture (`live.py`) | **Not remote biometric identification** | No comparison to stored biometric templates |
| All `imshow` / `rectangle` rendering | **Local display only; no storage** | No template persistence |

These are **not** text sentiment/relationship analysis or product copy false positives — they involve real biometric image data. The distinction is that the *purpose* (bounding-box detection) falls below the AI Act's biometric risk thresholds.

---

### Remediation Actions (POC)

Given the evidence is likely out of scope, no code removal or behavioral changes are needed. Minimum POC changes:

1. **Add a `COMPLIANCE.md`** in the repository root documenting:
   - That this codebase performs face detection only (not recognition, not identification, not emotion inference, not biometric categorisation).
   - That no biometric templates, embeddings, or identifying metadata are stored, transmitted, or persisted.
   - The intended use case (e.g., tutorial/demo, local-only processing).
   - Explicit statement that the codebase does **not** fall under Annex III high-risk biometric AI or Article 5 prohibited practices.

2. **Add a comment banner** to `live.py` (the only file with live camera capture, which carries marginally higher risk) at the top of the file:
   ```python
   # COMPLIANCE NOTE: This script performs face detection only (Haar Cascade bounding-box
   # detection). It does not perform face recognition, biometric identification, emotion
   # recognition, or biometric categorisation. No biometric data is stored or transmitted.
   # Under the EU AI Act, mere detection without identity/category/emotion inference is
   # not classified as high-risk biometric AI.
   ```

3. **No functional code changes required.** The existing behavior (detect, count, draw rectangles, display) is preserved.

---

### Manual Legal/Compliance Review — Required

The following open questions must be answered by a qualified reviewer before closing this finding:

| # | Question | Relevant Files | AI Act Reference |
|---|---|---|---|
| 1 | Is this code deployed, shipped to customers, or offered as a service, or is it a research/educational artifact internal to the organization? | All | Determines whether Art. 50 transparency obligations attach |
| 2 | Does any downstream consumer of `live.py`’s webcam feed or the detection output combine it with face recognition, emotion inference, or biometric categorisation models? | `live.py` | Annex III.1, Art. 5 |
| 3 | Is the camera capture in `live.py` ever used in a workplace or educational setting? | `live.py` | Art. 5(1)(f) |
| 4 | Are the detected face regions (ROI crops) ever stored, logged, or transmitted to another system? | All | Data retention / Art. 5 scraping risk |
| 5 | Does any consuming service use face detection as a gate for biometric identification or categorisation (e.g., detect → then recognize/categorize)? | All | Annex III.1(a)-(c) |
| 6 | Is the `haarcascade_frontalface_default.xml` model known to contain or encode biometric templates? (Standard Haar cascades do not; confirm with legal.) | All | Art. 3 definitional boundary |

### Summary

The scanner correctly identified biometric image processing signals, but the concrete functionality (bounding-box face detection without identity, emotion, or category inference) places this codebase **outside the EU AI Act's high-risk biometric AI scope**. Minimal documentation changes satisfy POC requirements. The manual review items above are the real compliance gates.

## OpenCode stderr

```text
[0m
> build · deepseek-v4-pro
[0m
[0m→ [0mRead face_detect.py
[0m→ [0mRead face_detect_cv3.py
[0m→ [0mRead live.py
```
