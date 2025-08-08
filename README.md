## 🧩 Project: **COLLEGE PPT**

An AI-powered web tool for students and educators to generate beautiful presentations automatically — just by giving a topic and basic info. Slides are generated via Gemini/ChatGPT in JSON format and can be edited, enriched with images, and downloaded as PPT or PDF.

---

## 🔥 Feature Overview

| #  | Module                    | Description                                                          |
| -- | ------------------------- | -------------------------------------------------------------------- |
| 1  | 🧾 Input Form             | Topic + front slide info                                             |
| 2  | ⚙️ Prompt Builder         | Generates universal AI prompt with JSON schema                       |
| 3  | 📡 API Request (Node.js)  | Sends prompt to Gemini/ChatGPT backend                               |
| 4  | 🔍 AI Response Parser     | Parses AI’s JSON output: slides, bullets, image topics               |
| 5  | 🧱 IndexedDB Storage      | Saves JSON data, front slide info, images locally                    |
| 6  | 🧊 Slide Preview Renderer | Renders all slides beautifully with title, bullets, and image area   |
| 7  | 🖼️ Image Suggestion/Slot | Displays image topic → links to Google Images → drag-drop image slot |
| 8  | 💾 Save/Load Presentation | Load previous work using IndexedDB                                   |
| 9  | 📤 Export Module          | Export to .pptx or .pdf                                              |
| 10 | 🌐 Offline-First          | Fully works without internet after generation                        |

---

## 🧾 🧍 Input Fields (Front Slide Details)

| Field            | Input Placeholder                            |
| ---------------- | -------------------------------------------- |
| Topic Name       | “AI in Agriculture”                          |
| Name             | “Sabir Ali Mondal”                           |
| Roll             | “34900123032”                                |
| Department       | “Computer Science Engineering”               |
| College Name     | “Cooch Behar Government Engineering College” |
| University Name  | “MAKAUT”                                     |
| Number of Slides | “7” (excluding front slide)                  |

---

## 🪄 AI Prompt Structure

```plaintext
You are a professional PowerPoint creator.

Your task is to return a JSON object containing slide-by-slide breakdown of a presentation.

Input Details:
- Topic: {{TOPIC}}
- Student Name: {{NAME}}
- Roll: {{ROLL}}
- Department: {{DEPT}}
- College: {{COLLEGE}}
- University: {{UNIVERSITY}}
- Date: (Current Date)
- Number of content slides (excluding front slide): {{SLIDE_COUNT}}

Output JSON Format:

{
  "frontSlide": {
    "topic": "...",
    "name": "...",
    "roll": "...",
    "department": "...",
    "college": "...",
    "university": "...",
    "date": "..."
  },
  "slides": [
    {
      "title": "Slide Title",
      "bullets": ["Point 1", "Point 2"],
      "imageSearch": "Image keyword"
    },
    ...
  ]
}

Rules:
- Do not include commentary or markdown
- Max 4 bullets per slide
- Include one imageSearch string per slide based on topic
```

---

## 🖥️ UI/UX Design

### 📄 Left Panel (Form)

* Fields for Topic, Name, Roll, etc.
* “Generate PPT” button
* On success → stores full JSON in IndexedDB
* On error → shows fallback or retry message

### 🎞️ Main Workspace (Slides)

* Displays each slide preview
* Includes:

  * Slide Title
  * Bullet Points
  * 🔍 Suggested Image Tag (clickable)
  * 🖼️ Drag-drop zone to upload or place image

---

## 💾 IndexedDB Schema

| Store Name     | Key               | Value                      |
| -------------- | ----------------- | -------------------------- |
| `meta_info`    | `topic-1`         | `{topic, name, roll, ...}` |
| `slides_data`  | `topic-1`         | JSON object with slides    |
| `slide_images` | `topic-1-slide-3` | Image as blob or base64    |
| `last_opened`  | `last`            | `topic-1`                  |

---

## 📤 Export Options

### 🟪 Export to PPTX

* Uses `PptxGenJS`
* Each slide:

  * Title (H1 or 36px)
  * Bullets (20px)
  * Optional image if uploaded

### 🟥 Export to PDF

* Uses `html2pdf.js` or `jsPDF`
* Renders HTML slide previews into downloadable PDF

---

## 🔗 Image Suggestion → Google Images

```js
const searchQuery = encodeURIComponent(slide.imageSearch);
const url = `https://www.google.com/search?tbm=isch&q=${searchQuery}`;
```

* Add a “Search Image 🔍” button beside drag-drop
* Opens Google Images
* User drags image from browser → drops into slot → auto-saved to IndexedDB

---

## ✅ Final Flow (Summary)

1. User fills form and clicks **Generate Slides**
2. Prompt is built → sent to **Node.js backend**
3. Gemini/ChatGPT returns JSON with slides
4. JSON stored in IndexedDB
5. Slides rendered with title, bullets, image suggestion
6. User manually adds images via drag-drop
7. All data persists locally (offline-first)
8. Final export as **PPTX or PDF**

---

## 🧩 College PPT Templates (User Can Choose)

```
1. Academic Presentation Template
2. Minimalist Thesis Defense
3. Cool College Presentation
4. Geometric College Presentation
```

Download from SlidesGo or host on Drive/public repo. Allow selection via dropdown or preview tiles.
