# AI Act biometric-risk report

- Target: `FaceDetect`
- Generated: `2026-04-30T00:50:37+00:00`
- Status: `possible_trigger_found`
- Files with signals: `3`
- Signal lines: `24`

## Suspected triggers

- biometric identification or categorisation review

## Required documents

- AI system inventory entry
- EU AI Act biometric-risk classification assessment
- Fundamental rights impact assessment or documented rationale for why one is not required
- Technical documentation for model purpose, inputs, outputs, and risk controls
- Human oversight, logging, monitoring, and incident-response notes

## Classification context

EU AI Act context for this POC:
- Article 3 defines biometric identification as automated recognition of human features to establish identity by comparing biometric data to stored biometric data.
- Article 3 defines biometric verification as one-to-one identity confirmation against previously provided biometric data.
- Article 3 defines emotion recognition as identifying or inferring emotions or intentions on the basis of biometric data.
- Article 3 defines biometric categorisation as assigning natural persons to categories on the basis of biometric data.
- Annex III lists remote biometric identification, sensitive/protected biometric categorisation, and emotion recognition as high-risk biometric AI areas where permitted by law.
- Article 5 prohibits some biometric uses, including untargeted scraping to build facial recognition databases, workplace/education emotion inference except medical or safety uses, and biometric categorisation to infer listed sensitive traits.
- Article 50 requires deployers of emotion recognition or biometric categorisation systems to inform exposed persons.

Source references:
- Article 3 definitions: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-3
- Annex III high-risk biometric areas: https://ai-act-service-desk.ec.europa.eu/en/ai-act/annex-3
- Article 5 prohibited AI practices: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-5
- Article 50 transparency obligations: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-50

Positive examples for this POC:
- webcam/video/image/audio/voice input used to infer emotion, stress, mood, intent, or affect;
- face embeddings, face_recognition, face-api, Rekognition, Azure Face, DeepFace, dlib, OpenCV face detection, or facial landmark code used for matching or identification;
- fingerprint, iris, retina, voiceprint, gait, liveness, or other biometric-template matching;
- age, sex, ethnicity, race, disability, health, political, religious, sexual orientation, or similar categories inferred from face, voice, gait, or other biometric data.

Negative examples that should not trigger biometric AI Act remediation by themselves:
- text-only sentiment analysis of chats, emails, support tickets, or relationship messages;
- product copy that says emotional, emotion, face a consequence, interface, or user-facing;
- one-to-one biometric login verification where the sole purpose is confirming the claimed user identity, unless other biometric categorisation or identification signals appear.


## Evidence

### `face_detect.py`

- Line 1 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `import cv2`
- Line 9 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `faceCascade = cv2.CascadeClassifier(cascPath)`
- Line 12 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `image = cv2.imread(imagePath)`
- Line 13 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)`
- Line 16 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `faces = faceCascade.detectMultiScale(`
- Line 21 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `flags = cv2.cv.CV_HAAR_SCALE_IMAGE`
- Line 28 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `cv2.rectangle(image, (x, y), (x+w, y+h), (0, 255, 0), 2)`
- Line 30 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `cv2.imshow("Faces found", image)`

### `face_detect_cv3.py`

- Line 1 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `import cv2`
- Line 9 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `faceCascade = cv2.CascadeClassifier(cascPath)`
- Line 12 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `image = cv2.imread(imagePath)`
- Line 13 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)`
- Line 16 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `faces = faceCascade.detectMultiScale(`
- Line 21 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `#flags = cv2.CV_HAAR_SCALE_IMAGE`
- Line 28 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `cv2.rectangle(image, (x, y), (x+w, y+h), (0, 255, 0), 2)`
- Line 30 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `cv2.imshow("Faces found", image)`

### `live.py`

- Line 4 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `import cv2`
- Line 6 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `cap = cv2.VideoCapture(0)`
- Line 9 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `faceCascade = cv2.CascadeClassifier("haarcascade_frontalface_default.xml")`
- Line 16 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)`
- Line 19 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `faces = faceCascade.detectMultiScale(`
- Line 24 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `#flags = cv2.CV_HAAR_SCALE_IMAGE`
- Line 31 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)`
- Line 35 `OpenCV` (possible biometric image processing; direct biometric-data processing signal): `cv2.imshow('frame', frame)`

## Review note

This POC reports possible compliance triggers from source-code signals. It is not a legal conclusion and requires review by qualified counsel or a DPO.
