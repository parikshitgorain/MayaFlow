# MayaFlow: Product Requirements Document (PRD)
## Autonomous Retention-Engineered Content Studio

*"Maya" - Sanskrit for "Magic" and "Illusion" - the power to conjure reality from imagination*

---

## 1. Executive Summary

### The Problem: Creator Burnout

In the Creator Economy, "Burnout" is the #1 killer of content production. Creators spend 90% of their time on manual editing tasks—syncing audio, generating subtitles, finding b-roll footage, color grading, and optimizing for platform-specific requirements—leaving only 10% for creative ideation. A single 60-second video can take 10+ hours to produce.

Generic AI tools have flooded the market, but they produce "slop"—culturally-agnostic, retention-poor content that fails to connect with audiences. An AI-generated video of an "Indian village" looks like a European countryside. Voice-overs sound robotic. Videos lack the pacing and hooks needed to retain viewer attention beyond the first 3 seconds.

### The Solution: MayaFlow

**MayaFlow** is the world's first "Zero-Touch" Content Architect—a digital sorcerer that conjures complete, viral-ready videos from mere text. Like the ancient concept of Maya (illusion/magic), it transforms imagination into tangible reality. Built entirely on AWS, MayaFlow weaves together AI intelligence, cultural awareness, and viral science to create videos that don't just exist—they connect, engage, and spread.

The system embodies the essence of Maya: creating something from nothing, making the impossible effortless, and turning creative vision into visual reality with a single command.

### Unique Value Propositions

**1. The "Culture-Lock" Engine**
Unlike generic AI models, MayaFlow embeds cultural intelligence into every layer. When generating a Hindi fable about a tiger and mouse, the system understands:
- Architectural styles of Indian villages
- Traditional clothing and color palettes
- Regional storytelling pacing and narrative structures
- Language-specific voice characteristics (breath patterns, intonation)

**2. The "Retention Engine"**
MayaFlow doesn't just assemble clips—it engineers retention using viral science:
- **3-Second Rule**: No visual shot exceeds 3 seconds without a zoom, pan, or scene change
- **Audio Ducking**: Background music automatically lowers by 15dB during voice-over
- **Burned-In Captions**: High-contrast, bold subtitles positioned in the TikTok/Reels safe zone
- **Intelligent Cropping**: Amazon Rekognition centers subjects when converting horizontal to vertical

**3. The "Hybrid-Reality" Trust Model**
By blending real stock footage with AI-generated characters, MayaFlow solves the "Uncanny Valley" problem. Videos feel 50% more authentic than pure AI-generated content because fantastical elements (talking animals) are grounded in realistic environments.


### Impact Metrics

| Metric | Traditional Production | MayaFlow |
|--------|----------------------|-----------|
| Time to Publish | 10+ hours | 5-15 minutes |
| Technical Skill Required | High (editing software) | None (text input only) |
| Cost per Video | $50-500 (freelancers/tools) | ~$0.13 (AWS costs) |
| Cultural Accuracy | Manual research required | Automatic (AI-driven) |
| Retention Optimization | Manual A/B testing | Built-in (3-second rule) |

---

## 2. System Architecture

### AWS-Native Technology Stack

MayaFlow is built entirely on AWS services to maximize student credit utilization and eliminate infrastructure management overhead.

```
┌─────────────────────────────────────────────────────────────┐
│                     USER INTERFACE                          │
│              (Magic Box + Video History)                    │
│                  AWS AppSync (GraphQL)                      │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                  ORCHESTRATION LAYER                        │
│              AWS Step Functions (State Machine)             │
└─┬───────┬────────┬────────┬────────┬────────┬──────────────┘
  │       │        │        │        │        │
  ▼       ▼        ▼        ▼        ▼        ▼
┌───┐   ┌───┐    ┌───┐   ┌───┐    ┌───┐    ┌───┐
│ 1 │   │ 2 │    │ 3 │   │ 4 │    │ 5 │    │ 6 │
└───┘   └───┘    └───┘   └───┘    └───┘    └───┘

1. Intent Analysis (Amazon Bedrock - Claude 3.5 Sonnet)
2. Script Generation (Amazon Bedrock - Claude 3.5 Sonnet)
3. Visual Creation (Amazon Titan + Pexels API via Lambda)
4. Voice Synthesis (Amazon Polly Neural - Language-Specific)
5. Video Rendering (AWS Fargate - FFmpeg Docker Container)
6. Publishing (AWS Lambda - YouTube/Instagram APIs)

┌─────────────────────────────────────────────────────────────┐
│                     DATA LAYER                              │
│  Amazon S3 (Videos, Audio, Images, Music Library)          │
│  Amazon DynamoDB (User Data, Video History, OAuth Tokens)  │
└─────────────────────────────────────────────────────────────┘
```


### Service Justifications

| AWS Service | Purpose | Why This Service? |
|------------|---------|-------------------|
| **Amazon Bedrock** | AI intelligence layer for script generation, language detection, metadata optimization | Access to Claude 3.5 Sonnet for high-context cultural awareness without managing model infrastructure. Supports multi-language prompting and structured output generation. |
| **AWS Step Functions** | Workflow orchestration | Manages long-running, multi-stage pipelines (5-15 min) with built-in error handling, retries, and visual monitoring. Lambda's 15-min timeout is insufficient for video rendering. |
| **Amazon Polly (Neural)** | Voice synthesis | Neural voices (Aditi/Kajal for Hindi) produce breath-aware, emotionally expressive speech that retains attention 3x better than standard TTS. Supports 29 languages. |
| **AWS Fargate** | Video rendering compute | Runs heavy FFmpeg jobs requiring 4-8 GB RAM and 10+ minutes. Fargate provides right-sized compute with automatic scaling without managing EC2 instances. |
| **Amazon S3** | Asset storage | Durable storage for videos, audio, images, and music library. Lifecycle policies auto-archive old content to Glacier. Event notifications trigger processing steps. |
| **Amazon DynamoDB** | User data and state | Single-digit millisecond latency for video history queries. On-demand pricing scales with usage. DynamoDB Streams enable real-time UI updates via AppSync. |
| **AWS AppSync** | Real-time UI updates | GraphQL subscriptions push live progress updates without managing WebSocket infrastructure. Automatic connection scaling and authentication. |
| **Amazon Rekognition** | Intelligent cropping (optional) | Detects and centers primary subjects when cropping horizontal footage to vertical format, ensuring important visual elements remain in frame. |
| **Amazon Titan** | AI image generation | Creates culturally-aware, style-consistent visuals for animated content that stock footage cannot provide. Supports detailed prompts for regional aesthetics. |
| **AWS Lambda** | Event-driven glue code | Handles lightweight operations (API validation, OAuth management, triggering workflows). Pay-per-invocation model eliminates idle costs. |
| **Amazon Cognito** | User authentication | Manages user sign-up, sign-in, and OAuth token storage with built-in security. Integrates seamlessly with AppSync for authenticated GraphQL access. |

---

## 3. Data Contract Specification

### Video Project JSON Schema

The `Script_Generator` (Amazon Bedrock) outputs a structured JSON document that controls the entire video production pipeline. This contract ensures deterministic rendering and enables precise control over timing, visuals, and effects.

```json
{
  "project_id": "vid_a1b2c3d4",
  "user_id": "user_12345",
  "created_at": "2026-02-15T10:30:00Z",
  "language": "hi",
  "genre": "fable",
  "aspect_ratio": "9:16",
  "target_platform": "instagram_reels",
  "metadata": {
    "title": "बाघ और चूहे की दोस्ती | Tiger & Mouse Friendship",
    "description": "एक प्राचीन भारतीय कहानी जो सिखाती है कि छोटे दोस्त भी बड़ी मुश्किलों में काम आते हैं। #HindiStories #Fables #Friendship",
    "tags": ["hindi", "fable", "kids", "moral_story", "indian_folklore"],
    "thumbnail_prompt": "Cartoon tiger and mouse shaking hands in Indian village, vibrant colors, 3D style"
  },
  "audio": {
    "voice_id": "Aditi",
    "voice_engine": "neural",
    "background_music": "ambient_fable_01.mp3",
    "music_volume_db": -20,
    "ducking_reduction_db": -15
  },
  "scenes": [
    {
      "sequence": 1,
      "narration_text": "एक बार की बात है, एक घने जंगल में एक बड़ा बाघ रहता था।",
      "narration_audio_s3": "s3://MayaFlow-audio/vid_a1b2c3d4/scene_01.mp3",
      "duration_ms": 4200,
      "visual_type": "ai_generated",
      "visual_prompt": "Majestic tiger in dense Indian jungle, 3D cartoon style, vibrant green foliage, traditional Indian art aesthetic",
      "visual_s3": "s3://MayaFlow-visuals/vid_a1b2c3d4/scene_01.png",
      "retention_effect": "zoom_in",
      "effect_start_ms": 2000,
      "subtitle_text": "एक बार की बात है, एक घने जंगल में एक बड़ा बाघ रहता था।",
      "subtitle_timing": [
        {"start_ms": 0, "end_ms": 1500, "text": "एक बार की बात है,"},
        {"start_ms": 1500, "end_ms": 3000, "text": "एक घने जंगल में"},
        {"start_ms": 3000, "end_ms": 4200, "text": "एक बड़ा बाघ रहता था।"}
      ]
    },
    {
      "sequence": 2,
      "narration_text": "एक दिन, एक छोटा चूहा बाघ के पंजे में फंस गया।",
      "narration_audio_s3": "s3://MayaFlow-audio/vid_a1b2c3d4/scene_02.mp3",
      "duration_ms": 3800,
      "visual_type": "ai_generated",
      "visual_prompt": "Small mouse trapped under tiger's paw, worried expression, 3D cartoon style, Indian jungle background",
      "visual_s3": "s3://MayaFlow-visuals/vid_a1b2c3d4/scene_02.png",
      "retention_effect": "pan_right",
      "effect_start_ms": 1800,
      "subtitle_text": "एक दिन, एक छोटा चूहा बाघ के पंजे में फंस गया।",
      "subtitle_timing": [
        {"start_ms": 0, "end_ms": 1200, "text": "एक दिन,"},
        {"start_ms": 1200, "end_ms": 2500, "text": "एक छोटा चूहा"},
        {"start_ms": 2500, "end_ms": 3800, "text": "बाघ के पंजे में फंस गया।"}
      ]
    },
    {
      "sequence": 3,
      "narration_text": "चूहे ने बाघ से माफी मांगी और वादा किया कि वह एक दिन उसकी मदद करेगा।",
      "narration_audio_s3": "s3://MayaFlow-audio/vid_a1b2c3d4/scene_03.mp3",
      "duration_ms": 5100,
      "visual_type": "ai_generated",
      "visual_prompt": "Mouse pleading to tiger, hands folded in namaste gesture, emotional scene, 3D cartoon style",
      "visual_s3": "s3://MayaFlow-visuals/vid_a1b2c3d4/scene_03.png",
      "retention_effect": "zoom_in",
      "effect_start_ms": 2500,
      "subtitle_text": "चूहे ने बाघ से माफी मांगी और वादा किया कि वह एक दिन उसकी मदद करेगा।",
      "subtitle_timing": [
        {"start_ms": 0, "end_ms": 1800, "text": "चूहे ने बाघ से माफी मांगी"},
        {"start_ms": 1800, "end_ms": 3500, "text": "और वादा किया कि"},
        {"start_ms": 3500, "end_ms": 5100, "text": "वह एक दिन उसकी मदद करेगा।"}
      ]
    }
  ],
  "rendering_config": {
    "resolution": "1080p",
    "fps": 30,
    "codec": "h264",
    "format": "mp4",
    "subtitle_font": "Montserrat-Bold",
    "subtitle_size": 48,
    "subtitle_color": "#FFFF00",
    "subtitle_outline_color": "#000000",
    "subtitle_outline_width": 3,
    "subtitle_position": "center_bottom",
    "subtitle_safe_zone_margin": 120
  }
}
```


### Data Contract Field Definitions

| Field | Type | Description | Constraints |
|-------|------|-------------|-------------|
| `project_id` | string | Unique identifier for the video project | UUID format |
| `language` | string | ISO 639-1 language code | Supported: en, hi, es, fr, de, ja |
| `genre` | string | Content genre for music/style selection | fable, news, tutorial, entertainment |
| `aspect_ratio` | string | Video dimensions | "9:16" (vertical) or "16:9" (horizontal) |
| `target_platform` | string | Publishing destination | youtube_shorts, instagram_reels, facebook |
| `scenes[].duration_ms` | integer | Scene duration in milliseconds | Must be ≤ 6000 (6 seconds) |
| `scenes[].visual_type` | string | Visual source | "ai_generated" or "stock_footage" |
| `scenes[].retention_effect` | string | Engagement effect | "zoom_in", "zoom_out", "pan_left", "pan_right", "none" |
| `scenes[].effect_start_ms` | integer | When to trigger effect | Must be < duration_ms |
| `subtitle_timing[].start_ms` | integer | Subtitle appearance time | Relative to scene start |
| `subtitle_timing[].end_ms` | integer | Subtitle disappearance time | Must be ≤ scene duration |

---

## 4. Functional Requirements

### REQ-FMT-01: Shorts Compliance Engine

**Requirement:** The system SHALL enforce strict platform compliance rules for short-form vertical video to ensure content is not rejected or improperly displayed on YouTube Shorts, Instagram Reels, and TikTok.

**Rationale:** Social media platforms have strict technical requirements for Shorts/Reels. Videos that violate these requirements are rejected, cropped, or deprioritized by algorithms. Enforcing compliance at the generation stage ensures 100% acceptance rate.

**Acceptance Criteria:**
1. IF video format is "Short (Vertical)", THEN THE System SHALL strictly cap total duration at 59.0 seconds maximum
2. IF the generated script exceeds 59 seconds, THEN THE Script_Generator SHALL cut content to fit the time limit (NOT speed up audio)
3. Vertical videos SHALL be rendered at exactly 1080x1920 pixels (9:16 aspect ratio) with no letterboxing or pillarboxing
4. THE Video_Editor SHALL position all text, subtitles, and overlays within the "Social Safe Zone" defined as:
   - Horizontal: Center 80% of width (108px margin on each side)
   - Vertical: Middle 60% of height (384px margin top, 384px margin bottom)
5. THE System SHALL validate final video dimensions and duration before publishing
6. IF validation fails, THEN THE System SHALL reject the video and log specific compliance violations

**Technical Implementation:**
- Duration enforcement: Script_Generator truncates content at 55 seconds (4-second buffer)
- Resolution validation: FFmpeg output verification
- Safe zone calculation: Automated margin application in subtitle rendering

**Safe Zone Diagram:**
```
┌─────────────────────────┐
│   Top UI (384px)        │ ← TikTok/Reels buttons
├─────────────────────────┤
│ ┌─────────────────────┐ │
│ │                     │ │
│ │   SAFE ZONE         │ │ ← Text/Subtitles here
│ │   (Content Area)    │ │
│ │                     │ │
│ └─────────────────────┘ │
├─────────────────────────┤
│   Bottom UI (384px)     │ ← Like/Share buttons
└─────────────────────────┘
```

---

### REQ-UI-01: Magic Box Interface

**Requirement:** The system SHALL provide a simplified user interface called the "Magic Box" with minimal input fields.

**Acceptance Criteria:**
- Single text area with prompt: "What is your video idea?"
- Format toggle: "Short (Vertical)" vs "Long (Horizontal)"
- "Auto-Pilot" checkbox: "Auto-Post to YouTube/Instagram when complete"
- Single action button: "Generate & Publish"
- Video history list displaying past videos with status (Processing / Waiting for Approval / Published URL)

**Technical Implementation:**
- Frontend: React with AWS Amplify for hosting
- Backend: AWS AppSync GraphQL API
- Real-time updates: GraphQL subscriptions for live progress tracking

---

### REQ-AI-04: Viral Pacing for Shorts

**Requirement:** For vertical short-form videos, the system SHALL use a "Fast-Paced" script structure optimized for maximum viewer retention on Shorts/Reels platforms.

**Rationale:** Short-form video algorithms prioritize content that maintains viewer attention. The first 0.5 seconds determine whether a viewer scrolls away. Fast cuts and looping structures increase watch time and algorithmic promotion.

**Acceptance Criteria:**
1. WHEN generating scripts for "Short (Vertical)" format, THE Script_Generator SHALL implement a "Fast-Paced" structure with three components:
   - **The Hook**: Visual change or attention-grabbing element within the first 0.5 seconds
   - **The Cuts**: No individual scene longer than 2.0 seconds (stricter than the general 3-second rule)
   - **The Loop**: Final sentence that creates curiosity or loops back to the beginning
2. THE Script_Generator SHALL front-load the most engaging content in the first 3 seconds
3. Each scene SHALL have a clear visual transition (cut, zoom, pan) to maintain pacing
4. THE Script SHALL end with a call-to-action or loop statement (e.g., "And that's why...", "Want to see more?", "This proves that...")
5. FOR horizontal "Long" format videos, THE System SHALL use standard pacing (3-second rule, slower narrative structure)

**Technical Implementation:**
- Script templates: Separate prompt templates for Short vs Long format
- Pacing validation: Automated scene duration analysis
- Hook generation: Bedrock prompt engineering for attention-grabbing openings

**Example Short Script Structure:**
```
Scene 1 (0-2s): HOOK - "You won't believe what happened next..."
Scene 2 (2-4s): Setup - "A tiger met a mouse in the jungle"
Scene 3 (4-6s): Conflict - "The mouse was trapped!"
Scene 4 (6-8s): Twist - "But the mouse made a promise..."
...
Scene N (57-59s): Loop - "And that's why small friends matter most!"
```

---

### REQ-AI-01: Intent Analysis and Language Detection

**Requirement:** The system SHALL automatically detect the target language and content genre from the user's text input.

**Acceptance Criteria:**
- Detect language with 95%+ accuracy for supported languages (English, Hindi, Spanish, French, German, Japanese)
- Classify genre (fable, news, tutorial, entertainment) based on content analysis
- Configure downstream services (voice, visuals, music) based on detected attributes
- Complete analysis within 2 seconds

**Technical Implementation:**
- Service: Amazon Bedrock (Claude 3.5 Sonnet)
- Prompt engineering for multi-language classification
- Output: Structured JSON with language code and genre classification

**Example Prompt:**
```
Analyze this video idea and return JSON:
Input: "A story about a tiger and mouse in Hindi"
Output: {"language": "hi", "genre": "fable", "target_audience": "children"}
```

---

### REQ-AI-02: Script Generation with Cultural Awareness

**Requirement:** The system SHALL generate a complete video script in the detected language with culturally-appropriate content and pacing.

**Acceptance Criteria:**
- Generate scripts in the detected language (not translated from English)
- Include scene descriptions with cultural context (e.g., "Indian village" not "generic village")
- Structure content with clear narration timing and visual cues
- Adapt script length based on video format (30-45 seconds for vertical, 60-90 seconds for horizontal)
- Include specific visual prompts for each scene that respect cultural aesthetics

**Technical Implementation:**
- Service: Amazon Bedrock (Claude 3.5 Sonnet)
- Custom prompt templates for each supported language and genre
- Output: Complete video project JSON (see Data Contract section)

**Culture-Lock Logic:**
```
IF language == "hi" AND genre == "fable":
  - Use traditional Indian storytelling structure (moral at end)
  - Visual style: Vibrant colors, traditional art influences
  - Character designs: Culturally appropriate clothing and settings
  - Pacing: Slower, emphasis on moral lessons
```

---

### REQ-AI-03: Viral Metadata Generation

**Requirement:** The system SHALL automatically generate SEO-optimized, platform-specific metadata designed to maximize discoverability and click-through rate.

**Acceptance Criteria:**
- Generate clickbait-style title (40-60 characters) optimized for views
- Create compelling description (150-200 characters) that encourages engagement
- Generate 5-10 trending hashtags relevant to content
- Ensure all metadata is in the detected language
- Follow platform-specific best practices (YouTube vs Instagram formatting)

**Technical Implementation:**
- Service: Amazon Bedrock (Claude 3.5 Sonnet)
- Analyze trending content patterns for the genre
- Output: Metadata object in video project JSON

**Example Output:**
```json
{
  "title": "बाघ और चूहे की दोस्ती | Tiger & Mouse Friendship 🐯🐭",
  "description": "एक प्राचीन भारतीय कहानी जो सिखाती है कि छोटे दोस्त भी बड़ी मुश्किलों में काम आते हैं। #HindiStories",
  "tags": ["hindi", "fable", "kids", "moral_story", "indian_folklore", "tiger", "mouse", "friendship"]
}
```

---

### REQ-VIS-01: Intelligent Visual Generation

**Requirement:** The system SHALL automatically create or retrieve appropriate visuals for each scene based on genre and cultural context.

**Acceptance Criteria:**
- For animated/fictional content: Use Amazon Titan Image Generator with culturally-aware prompts
- For realistic content: Search Pexels API with genre-appropriate keywords
- Apply correct orientation parameter ("portrait" for vertical, "landscape" for horizontal)
- Ensure visual style consistency across all scenes
- Generate visuals at appropriate resolution (1080x1920 for vertical, 1920x1080 for horizontal)

**Technical Implementation:**
- AI Generation: Amazon Titan Image Generator via Bedrock
- Stock Footage: Pexels API via AWS Lambda
- Storage: Amazon S3 with organized folder structure

**Visual Selection Logic:**
```python
if scene.visual_type == "ai_generated":
    # Use Amazon Titan
    prompt = f"{scene.visual_prompt}, {cultural_style}, {art_style}"
    image = bedrock.invoke_titan_image(prompt, aspect_ratio)
elif scene.visual_type == "stock_footage":
    # Use Pexels API
    orientation = "portrait" if aspect_ratio == "9:16" else "landscape"
    videos = pexels.search(scene.keywords, orientation=orientation)
    video = select_best_match(videos, scene.duration_ms)
```

---

### REQ-VIS-02: Custom Thumbnail Generation

**Requirement:** The system SHALL generate a custom thumbnail image optimized for click-through rate on the target platform.

**Acceptance Criteria:**
- Generate thumbnail at platform-specific resolution (1280x720 for YouTube, 1080x1920 for Instagram)
- Feature high-contrast imagery related to video topic
- Overlay clickbait title text using bold, readable font (Montserrat-Bold or Impact)
- Use attention-grabbing colors (yellow text with black outline)
- Position text to avoid platform UI overlays

**Technical Implementation:**
- Base image: Amazon Titan Image Generator
- Text overlay: FFmpeg with custom filter
- Storage: Amazon S3 alongside video file

---

### REQ-AUDIO-01: Language-Specific Voice Synthesis

**Requirement:** The system SHALL generate natural-sounding voice-over in the detected language using appropriate voice characteristics for the genre.

**Acceptance Criteria:**
- Use Amazon Polly Neural voices for all supported languages
- For Hindi: Use Aditi (female) or Kajal (female) neural voices
- Select voice characteristics (pitch, speed, tone) based on genre
- Generate audio with natural pacing, emphasis, and intonation
- Produce high-quality audio at 24kHz sample rate, 128 kbps bitrate

**Technical Implementation:**
- Service: Amazon Polly (Neural Engine)
- Voice selection logic based on language and genre
- SSML markup for emphasis and pacing control

**Voice Selection Matrix:**
| Language | Genre | Voice ID | Speaking Rate | Pitch |
|----------|-------|----------|---------------|-------|
| Hindi | Fable | Aditi | medium | +0% |
| Hindi | News | Kajal | fast | +5% |
| English | Tutorial | Joanna | medium | +0% |
| English | Entertainment | Matthew | medium | -5% |


---

### REQ-VID-01: The 3-Second Rule (Retention Engineering)

**Requirement:** The system SHALL strictly enforce that no visual shot lasts longer than 3.0 seconds without a retention-boosting effect.

**Rationale:** Viewer attention drops significantly after 3 seconds of static visuals. By inserting zoom, pan, or scene change effects, we reset the attention clock and maintain engagement.

**Acceptance Criteria:**
- Analyze each scene's duration from the video project JSON
- IF scene duration > 3000ms, THEN apply a retention effect (zoom_in, zoom_out, pan_left, pan_right)
- Effect must start at the 2-second mark (2000ms) to preemptively reset attention
- Effect duration: 1-2 seconds with smooth easing
- Log warning if scene exceeds 6 seconds (hard limit)

**Technical Implementation:**
- Service: AWS Fargate (FFmpeg)
- FFmpeg filters: `zoompan`, `crop`, `scale`

**FFmpeg Command Example:**
```bash
# Zoom-in effect starting at 2 seconds
ffmpeg -i input.mp4 \
  -filter_complex "[0:v]zoompan=z='if(between(t,2,4),1+0.5*(t-2)/2,1)':d=1:s=1080x1920" \
  -c:a copy output.mp4
```

---

### REQ-VID-02: Burned-In Captions (Hardsubs)

**Requirement:** The system SHALL generate hardcoded subtitles directly onto video frames using high-readability styling optimized for mobile viewing.

**Acceptance Criteria:**
- Font: Montserrat-Bold or Roboto-Bold (minimum 48pt for vertical, 36pt for horizontal)
- Color: Yellow (#FFFF00) text with black (#000000) outline (3px width)
- Position: Center-bottom with 120px margin from bottom edge (safe zone for TikTok/Reels UI)
- Timing: Synchronized to voice-over with word-level precision
- Language: Rendered in the detected language with proper Unicode support

**Technical Implementation:**
- Service: AWS Fargate (FFmpeg)
- FFmpeg `subtitles` filter with ASS/SSA styling

**FFmpeg Subtitle Style:**
```
[V4+ Styles]
Format: Name, Fontname, Fontsize, PrimaryColour, OutlineColour, Outline, Alignment
Style: Default,Montserrat-Bold,48,&H00FFFF,&H000000,3,2

[Events]
Format: Start, End, Style, Text
Dialogue: 0:00:00.00,0:00:01.50,Default,एक बार की बात है,
Dialogue: 0:00:01.50,0:00:03.00,Default,एक घने जंगल में
```

---

### REQ-VID-03: Audio Ducking

**Requirement:** The system SHALL automatically lower background music volume when voice-over is active to ensure narration clarity.

**Acceptance Criteria:**
- Background music base volume: -20dB
- When voice-over is active: Reduce music by additional -15dB (total: -35dB)
- When voice-over pauses: Return music to -20dB
- Transition smoothing: 200ms fade in/out to avoid abrupt changes
- Apply ducking to all scenes with narration

**Technical Implementation:**
- Service: AWS Fargate (FFmpeg)
- FFmpeg `sidechaincompress` filter

**FFmpeg Command Example:**
```bash
ffmpeg -i voiceover.mp3 -i background_music.mp3 \
  -filter_complex \
  "[1:a]volume=-20dB[music]; \
   [music][0:a]sidechaincompress=threshold=0.1:ratio=4:attack=200:release=200[out]" \
  -map "[out]" output.mp3
```

---

### REQ-VID-04: Intelligent Cropping for Vertical Format

**Requirement:** WHERE Amazon Rekognition is available, the system SHALL use AI-powered subject detection to intelligently crop horizontal stock footage for vertical format.

**Acceptance Criteria:**
- Detect primary subject (person, animal, object) in horizontal footage
- Calculate crop window that centers the subject in 9:16 frame
- Maintain subject visibility throughout the clip
- Fallback to center-crop if Rekognition is unavailable or subject detection fails
- Apply smooth tracking if subject moves within frame

**Technical Implementation:**
- Service: Amazon Rekognition (Label Detection + Object Tracking)
- Processing: AWS Lambda for coordinate calculation
- Rendering: AWS Fargate (FFmpeg crop filter)

**Rekognition Integration:**
```python
# Detect subject in frame
response = rekognition.detect_labels(
    Image={'S3Object': {'Bucket': bucket, 'Name': key}},
    MaxLabels=10,
    MinConfidence=80
)

# Find primary subject bounding box
subject = response['Labels'][0]['Instances'][0]['BoundingBox']

# Calculate crop coordinates for 9:16
crop_x = subject['Left'] * width - (target_width / 2)
crop_y = 0  # Keep full height
crop_width = target_width
crop_height = height

# Apply crop in FFmpeg
ffmpeg -i input.mp4 -vf "crop={crop_width}:{crop_height}:{crop_x}:{crop_y}" output.mp4
```

---

### REQ-VID-05: Video Assembly and Rendering

**Requirement:** The system SHALL assemble all components (visuals, voice-over, background music, subtitles, effects) into a final video file meeting platform-specific technical requirements.

**Acceptance Criteria:**
- Resolution: 1080p minimum (1080x1920 for vertical, 1920x1080 for horizontal)
- Frame rate: 30 fps
- Codec: H.264 (x264)
- Format: MP4 (container)
- Audio: AAC codec, 128 kbps, 44.1kHz
- Duration: 30-60 seconds (enforced by platform requirements)
- File size: < 100MB for Instagram, < 256MB for YouTube
- Render time: < 10 minutes for 60-second video

**Technical Implementation:**
- Service: AWS Fargate (4 vCPU, 8GB RAM)
- Container: Custom Docker image with FFmpeg 6.0+
- Orchestration: AWS Step Functions (Wait state during rendering)

**Rendering Pipeline:**
```
1. Download all assets from S3 (visuals, audio, music)
2. Generate subtitle file (ASS format) from JSON timing data
3. Apply retention effects (zoom/pan) to visuals
4. Mix voice-over with background music (with ducking)
5. Burn subtitles onto video frames
6. Encode final video (H.264, 1080p, 30fps)
7. Upload to S3
8. Trigger next Step Functions state
```

---

### REQ-PUB-01: Conditional Publishing (Auto-Pilot Logic)

**Requirement:** The system SHALL provide binary publishing logic based on the "Auto-Pilot" checkbox state.

**Acceptance Criteria:**
- IF Auto-Pilot is enabled: Skip review, publish immediately after rendering
- IF Auto-Pilot is disabled: Set status to "Waiting for Approval", require manual approval
- Videos in "Waiting for Approval" state SHALL NOT auto-publish
- Provide "Approve" and "Delete" buttons for waiting videos
- When user clicks "Approve": Trigger publishing immediately

**Technical Implementation:**
- State management: DynamoDB (video status field)
- UI: React with conditional rendering based on status
- Publishing trigger: AWS Lambda invoked by user action or Step Functions

**State Machine Logic:**
```
IF auto_pilot == true:
    → Render Complete → Publish → Update Status: "Published"
ELSE:
    → Render Complete → Update Status: "Waiting for Approval" → Wait for User Action
    → User Clicks "Approve" → Publish → Update Status: "Published"
```

---

### REQ-PUB-02: Platform-Specific Publishing

**Requirement:** The system SHALL upload videos to YouTube Shorts or Instagram Reels with platform-specific metadata and technical requirements.

**Acceptance Criteria:**
- YouTube Shorts: Duration < 60 seconds, MP4/H.264, vertical or square aspect ratio
- Instagram Reels: Duration < 60 seconds, MP4/H.264, 9:16 aspect ratio
- Upload video file and custom thumbnail
- Set title, description, tags from generated metadata
- Use user's OAuth 2.0 tokens for authenticated upload
- Return published video URL on success
- Retry up to 3 times on transient failures (network errors, rate limits)

**Technical Implementation:**
- Service: AWS Lambda (Node.js or Python)
- APIs: YouTube Data API v3, Instagram Graph API
- Authentication: OAuth 2.0 tokens stored in DynamoDB (encrypted at rest)

**YouTube Upload Example:**
```python
from googleapiclient.discovery import build
from googleapiclient.http import MediaFileUpload

youtube = build('youtube', 'v3', credentials=oauth_credentials)

request = youtube.videos().insert(
    part="snippet,status",
    body={
        "snippet": {
            "title": metadata['title'],
            "description": metadata['description'],
            "tags": metadata['tags'],
            "categoryId": "22"  # People & Blogs
        },
        "status": {
            "privacyStatus": "public",
            "selfDeclaredMadeForKids": False
        }
    },
    media_body=MediaFileUpload(video_file, chunksize=-1, resumable=True)
)

response = request.execute()
video_url = f"https://youtube.com/shorts/{response['id']}"
```

---

### REQ-PUB-03: Platform API Compliance

**Requirement:** The system SHALL configure platform-specific API parameters to ensure videos are properly categorized and displayed as Shorts/Reels.

**Rationale:** Simply uploading a vertical video is insufficient. Platforms require specific API parameters to categorize content as "Shorts" or "Reels" for proper algorithmic distribution and UI presentation.

**Acceptance Criteria:**
1. WHEN publishing to YouTube Shorts, THE Auto_Publisher SHALL:
   - Set `privacyStatus: "public"` in the API request
   - Add "#Shorts" hashtag to both title and description
   - Set video category to "22" (People & Blogs) or user-specified category
   - Ensure aspect ratio is 9:16 or 1:1 (square)
   - Verify duration is ≤ 60 seconds
2. WHEN publishing to Instagram Reels, THE Auto_Publisher SHALL:
   - Set `media_type: "REELS"` in the Graph API request
   - Select cover image from the first frame of the video
   - Include location tag if available
   - Add relevant hashtags to caption (max 30)
   - Ensure aspect ratio is exactly 9:16
3. IF platform API returns validation errors, THEN THE System SHALL log the specific error and retry with corrected parameters
4. THE System SHALL verify successful upload by checking for a valid video URL in the API response

**Technical Implementation:**
- YouTube API: `youtube.videos().insert()` with Shorts-specific parameters
- Instagram API: `instagram_business_account.media_publish()` with Reels type
- Error handling: Parse API error responses and apply corrections

**YouTube Shorts API Example:**
```python
request = youtube.videos().insert(
    part="snippet,status",
    body={
        "snippet": {
            "title": f"{metadata['title']} #Shorts",
            "description": f"{metadata['description']}\n\n#Shorts {' '.join(['#' + tag for tag in metadata['tags']])}",
            "categoryId": "22",
            "tags": metadata['tags'] + ["Shorts"]
        },
        "status": {
            "privacyStatus": "public",
            "selfDeclaredMadeForKids": False,
            "madeForKids": False
        }
    },
    media_body=MediaFileUpload(video_file)
)
```

**Instagram Reels API Example:**
```python
# Step 1: Create media container
container = graph.post(
    f"/{instagram_account_id}/media",
    data={
        "media_type": "REELS",
        "video_url": video_s3_url,
        "caption": f"{metadata['title']}\n\n{metadata['description']}\n\n{' '.join(['#' + tag for tag in metadata['tags']])}",
        "cover_url": thumbnail_s3_url
    }
)

# Step 2: Publish
result = graph.post(
    f"/{instagram_account_id}/media_publish",
    data={"creation_id": container['id']}
)
```

---

### REQ-EDIT-01: Conversational Remix Engine

**Requirement:** The system SHALL allow users to modify a generated video by inputting natural language commands, enabling iterative refinement without manual timeline editing.

**User Story:** As a user, I want to type "Make the ending more dramatic" and have the system automatically update the script, music, and visuals, so that I can refine my video through conversation rather than complex editing tools.

**Rationale:** Traditional video editing requires technical skills and time. A conversational interface democratizes video refinement by allowing users to describe desired changes in natural language. The system intelligently maps these requests to specific JSON fields and regenerates only the affected components, making iteration fast and cost-effective.

**Acceptance Criteria:**
1. The Video Preview page SHALL display a text chat input labeled: "Suggest changes (e.g., 'Change music to rock', 'Re-write scene 2', 'Make voice more energetic')"
2. WHEN a user submits a change request, THE Intent_Analyzer SHALL parse the natural language command and map it to specific fields in the Video Project JSON:
   - "Change voice to male" → Updates `audio.voice_id` to a male voice
   - "Make it shorter" → Updates `target_duration` and intelligently trims `scenes` array
   - "Change scene 3 to a beach" → Updates `scenes[2].visual_prompt` and marks scene for regeneration
   - "Make the music more upbeat" → Updates `audio.background_music` to a higher BPM track
   - "Add more dramatic pauses" → Updates `scenes[].subtitle_timing` with longer gaps
3. THE System SHALL implement smart re-rendering that ONLY regenerates the assets that changed:
   - IF only music changed, DO NOT regenerate images or voice-over
   - IF only one scene's visual changed, DO NOT regenerate other scenes
   - IF only voice characteristics changed, DO NOT regenerate visuals
   - Result: Remixing is 5x faster and 80% cheaper than generating from scratch
4. THE System SHALL save the previous version as "Version N" before applying changes, enabling undo functionality
5. Users SHALL be able to view version history and revert to any previous version
6. THE System SHALL support up to 5 remix iterations per video before requiring a full regeneration

**Technical Implementation:**
- Input: User text prompt + Current Video Project JSON
- Processing: Amazon Bedrock Agent receives prompt → Analyzes changes → Modifies JSON → Returns updated JSON with change markers
- Execution: AWS Step Functions re-runs only the affected steps (e.g., Voice Generation OR Image Generation) and then re-runs Video Assembly
- Version control: DynamoDB stores all JSON versions with timestamps

**Change Mapping Logic:**
```python
# Bedrock Agent Prompt
"""
Analyze this change request and update the Video Project JSON:

User request: "Change the voice to male and make scene 2 more colorful"
Current JSON: {video_project_json}

Return:
1. Updated JSON with changes
2. List of affected components: ["voice", "scene_2_visual"]
3. Regeneration plan: ["synthesize_voice", "generate_scene_2_image", "reassemble_video"]
"""

# Example Response
{
  "updated_json": {...},
  "affected_components": ["audio.voice_id", "scenes[1].visual_prompt"],
  "regeneration_steps": [
    "synthesize_voice_with_new_id",
    "generate_image_for_scene_2",
    "reassemble_video"
  ],
  "estimated_cost": "$0.05",
  "estimated_time": "2 minutes"
}
```

**Supported Change Types:**
| User Command | JSON Field Updated | Regeneration Required |
|--------------|-------------------|----------------------|
| "Change voice to [male/female/specific name]" | `audio.voice_id` | Voice synthesis only |
| "Make it [shorter/longer]" | `target_duration`, `scenes[]` | Script + all assets |
| "Change scene N to [description]" | `scenes[N].visual_prompt` | Single scene visual |
| "Make music [faster/slower/genre]" | `audio.background_music` | Audio mixing only |
| "Re-write the ending" | `scenes[-3:].narration_text` | Last 3 scenes + voice |
| "Add more pauses" | `scenes[].subtitle_timing` | Subtitle rendering only |
| "Make it more [emotion]" | `genre`, `audio.voice_tone` | Voice + music |

**Version Control Schema:**
```json
{
  "project_id": "vid_123",
  "versions": [
    {
      "version_number": 1,
      "created_at": "2026-02-15T10:00:00Z",
      "json_snapshot": {...},
      "video_s3_url": "s3://MayaFlow-videos/vid_123_v1.mp4",
      "change_description": "Original generation"
    },
    {
      "version_number": 2,
      "created_at": "2026-02-15T10:05:00Z",
      "json_snapshot": {...},
      "video_s3_url": "s3://MayaFlow-videos/vid_123_v2.mp4",
      "change_description": "Changed voice to male, made scene 2 more colorful",
      "parent_version": 1
    }
  ],
  "current_version": 2
}
```

**Cost Optimization:**
- Full regeneration: $0.13
- Voice-only remix: $0.02 (85% savings)
- Single scene visual remix: $0.03 (77% savings)
- Music-only remix: $0.01 (92% savings)

**User Experience Flow:**
```
1. User generates video → Version 1 created
2. User watches video, types: "Make the voice more energetic"
3. System analyzes → Updates voice_tone parameter → Regenerates voice only
4. System reassembles video with new voice → Version 2 created (2 min)
5. User watches, types: "Perfect! But change scene 3 to a sunset"
6. System regenerates scene 3 visual only → Version 3 created (1 min)
7. User approves → Publishes Version 3
```

---

### REQ-ORCH-01: Workflow Orchestration

**Requirement:** The system SHALL use AWS Step Functions to orchestrate the complete video creation pipeline with error handling and state persistence.

**Acceptance Criteria:**
- Define state machine with sequential steps: Intent Analysis → Script Generation → Visual Creation → Voice Synthesis → Video Rendering → Publishing
- Include wait states for long-running operations (rendering can take 5-15 minutes)
- Implement retry logic with exponential backoff for transient failures
- Catch and handle errors at each step with appropriate fallback actions
- Persist workflow state to enable resume after failures
- Provide visual workflow monitoring in AWS Console

**Technical Implementation:**
- Service: AWS Step Functions (Standard Workflows)
- State types: Task, Wait, Choice, Parallel, Fail, Succeed
- Integration: Direct SDK integrations with Bedrock, Lambda, Fargate

**State Machine Definition (Simplified):**
```json
{
  "StartAt": "IntentAnalysis",
  "States": {
    "IntentAnalysis": {
      "Type": "Task",
      "Resource": "arn:aws:states:::bedrock:invokeModel",
      "Parameters": {
        "ModelId": "anthropic.claude-3-5-sonnet-20241022-v2:0",
        "Body": {
          "prompt": "Analyze this video idea: ${input.video_idea}"
        }
      },
      "Next": "ScriptGeneration",
      "Retry": [{"ErrorEquals": ["States.ALL"], "MaxAttempts": 3}]
    },
    "ScriptGeneration": {
      "Type": "Task",
      "Resource": "arn:aws:states:::bedrock:invokeModel",
      "Next": "ParallelAssetCreation"
    },
    "ParallelAssetCreation": {
      "Type": "Parallel",
      "Branches": [
        {"StartAt": "GenerateVisuals", "States": {...}},
        {"StartAt": "SynthesizeVoice", "States": {...}}
      ],
      "Next": "VideoRendering"
    },
    "VideoRendering": {
      "Type": "Task",
      "Resource": "arn:aws:states:::ecs:runTask.sync",
      "Parameters": {
        "LaunchType": "FARGATE",
        "TaskDefinition": "MayaFlow-renderer"
      },
      "Next": "CheckAutoPilot"
    },
    "CheckAutoPilot": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.auto_pilot",
          "BooleanEquals": true,
          "Next": "PublishVideo"
        }
      ],
      "Default": "WaitForApproval"
    },
    "PublishVideo": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:PublishToSocial",
      "End": true
    },
    "WaitForApproval": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke.waitForTaskToken",
      "End": true
    }
  }
}
```


---

### REQ-RT-01: Real-Time Progress Tracking

**Requirement:** The system SHALL provide live progress updates to the user interface using AWS AppSync GraphQL subscriptions.

**Acceptance Criteria:**
- Push status updates after each major workflow step completion
- Display progress bar showing percentage completion (0-100%)
- Show descriptive status messages: "Writing Script...", "Generating Visuals...", "Synthesizing Voice...", "Rendering Video...", "Publishing..."
- Maintain WebSocket connection throughout entire workflow (5-15 minutes)
- Handle connection drops gracefully with automatic reconnection

**Technical Implementation:**
- Service: AWS AppSync (GraphQL API with subscriptions)
- Client: Apollo Client or AWS Amplify (React)
- Updates triggered by: Step Functions state transitions via EventBridge

**GraphQL Schema:**
```graphql
type VideoProject {
  id: ID!
  status: VideoStatus!
  progress: Int!
  currentStep: String!
  createdAt: AWSDateTime!
  videoUrl: String
}

enum VideoStatus {
  QUEUED
  PROCESSING
  WAITING_FOR_APPROVAL
  PUBLISHING
  PUBLISHED
  FAILED
}

type Mutation {
  updateVideoProgress(id: ID!, progress: Int!, currentStep: String!): VideoProject
}

type Subscription {
  onVideoProgressUpdate(id: ID!): VideoProject
    @aws_subscribe(mutations: ["updateVideoProgress"])
}
```

**Client Subscription:**
```javascript
const subscription = API.graphql(
  graphqlOperation(onVideoProgressUpdate, { id: videoId })
).subscribe({
  next: ({ value }) => {
    setProgress(value.data.onVideoProgressUpdate.progress);
    setStatus(value.data.onVideoProgressUpdate.currentStep);
  }
});
```

---

### REQ-SEC-01: Authentication and Authorization

**Requirement:** The system SHALL use Amazon Cognito for user authentication and secure OAuth token management.

**Acceptance Criteria:**
- Support email/password sign-up and sign-in
- Implement OAuth 2.0 flow for YouTube and Instagram authorization
- Store OAuth tokens encrypted at rest in DynamoDB
- Automatically refresh expired tokens
- Allow users to revoke social media permissions
- Enforce authenticated access to all API operations

**Technical Implementation:**
- Service: Amazon Cognito User Pools
- OAuth: Cognito Hosted UI with custom identity providers
- Token storage: DynamoDB with encryption at rest (AWS KMS)

---

### REQ-SEC-02: Hackathon "Guest Mode" Configuration

**Requirement:** The system SHALL support a configurable "Guest Mode" to allow Judges and Demo Users to access the platform without creating an account.

**Rationale:** During hackathon judging or demo sessions, requiring full account creation with email verification creates friction that prevents judges from experiencing the product. Guest Mode provides instant access while maintaining security boundaries.

**Acceptance Criteria:**
1. The frontend SHALL respect an environment variable `NEXT_PUBLIC_HACKATHON_MODE=true` to enable Guest Mode
2. WHEN `HACKATHON_MODE` is true, the Login Screen SHALL display a prominent "Start Testing (Judge Access)" button
3. WHEN a user clicks the Guest Mode button, THE System SHALL authenticate the user as a "Guest" with a temporary Cognito Identity ID
4. Guest users SHALL receive pre-loaded demo credits ($10.00 value, ~77 videos) for testing purposes
5. Guest users SHALL have full access to the Magic Box and video generation features
6. Guest users SHALL NOT be able to change passwords, view other users' history, or access OAuth settings
7. Guest sessions SHALL expire after 24 hours of inactivity
8. WHEN `HACKATHON_MODE` is false (production), the Guest Mode button SHALL NOT be displayed

**Technical Implementation:**
- Environment variable: `NEXT_PUBLIC_HACKATHON_MODE` (boolean)
- Guest authentication: Cognito Identity Pools with unauthenticated access
- Credit allocation: DynamoDB entry with guest user ID and $10.00 balance
- Session management: 24-hour TTL on guest user records

**Security Considerations:**
- Guest users cannot access other users' data (enforced by IAM policies)
- Guest-generated videos are stored in isolated S3 prefix
- Rate limiting prevents abuse (max 10 videos per guest session)
- Guest mode is disabled in production environments

---

### REQ-DATA-01: Data Storage and Lifecycle

**Requirement:** The system SHALL efficiently store and manage video assets, user data, and workflow state with cost-optimized lifecycle policies.

**Acceptance Criteria:**
- Store video files, audio, images in Amazon S3 with organized folder structure
- Store user data, video history, OAuth tokens in DynamoDB
- Implement S3 lifecycle policy: Archive to Glacier after 90 days, delete after 365 days
- Organize S3 objects by user ID and project ID for efficient retrieval
- Enable S3 versioning for critical assets (final videos)
- Use DynamoDB on-demand pricing for unpredictable usage patterns

**Technical Implementation:**
- S3 bucket structure: `s3://MayaFlow-assets/{user_id}/{project_id}/{asset_type}/`
- DynamoDB tables: `Users`, `VideoProjects`, `OAuthTokens`
- S3 lifecycle policy: Transition to Glacier after 90 days, expire after 365 days

---

### REQ-ERR-01: Error Handling and Recovery

**Requirement:** The system SHALL handle errors gracefully with automatic retries, detailed logging, and user-friendly error messages.

**Acceptance Criteria:**
- Retry transient errors (network failures, rate limits) up to 3 times with exponential backoff
- Log all errors to Amazon CloudWatch with contextual information (user ID, project ID, step name)
- Display user-friendly error messages in the UI (avoid technical jargon)
- Preserve partial progress to avoid redundant regeneration
- Provide "Retry" button for failed videos in Video History
- Send error notifications via email for critical failures

**Technical Implementation:**
- Logging: Amazon CloudWatch Logs
- Monitoring: CloudWatch Alarms for error rate thresholds
- Retry logic: Built into Step Functions state machine
- Notifications: Amazon SNS for email alerts

**Error Categories:**
| Error Type | Retry Strategy | User Message |
|------------|----------------|--------------|
| Network timeout | 3 retries, exponential backoff | "Connection issue. Retrying..." |
| API rate limit | 3 retries, 60s delay | "Service busy. Retrying shortly..." |
| Invalid input | No retry | "Please check your video idea and try again." |
| Rendering failure | 1 retry | "Video rendering failed. Retrying..." |
| Publishing failure | 3 retries | "Upload failed. Retrying..." |

---

## 5. Business Viability

### Cost Analysis (Per Video)

MayaFlow is designed to operate within AWS student credit limits ($100-200 total). Below is the estimated cost breakdown for a single 60-second video:

| Service | Operation | Unit Cost | Usage | Cost per Video |
|---------|-----------|-----------|-------|----------------|
| **Amazon Bedrock** | Claude 3.5 Sonnet | $0.003/1K input tokens, $0.015/1K output tokens | ~5K input, ~3K output | $0.060 |
| **Amazon Polly** | Neural voice synthesis | $0.016/1M characters | ~500 characters | $0.008 |
| **Amazon Titan** | Image generation | $0.008/image | 5 images | $0.040 |
| **AWS Fargate** | Video rendering (4 vCPU, 8GB) | $0.04048/vCPU-hour, $0.004445/GB-hour | 10 min | $0.014 |
| **Amazon S3** | Storage + data transfer | $0.023/GB storage, $0.09/GB transfer | 50MB | $0.005 |
| **AWS Step Functions** | State transitions | $0.025/1K transitions | 10 transitions | $0.0003 |
| **AWS Lambda** | API operations | $0.20/1M requests | 5 invocations | $0.000001 |
| **Amazon DynamoDB** | Read/write operations | $1.25/million writes | 10 writes | $0.000013 |
| **AWS AppSync** | GraphQL operations | $4.00/million operations | 20 operations | $0.00008 |
| **Amazon Rekognition** | Label detection (optional) | $0.001/image | 5 images | $0.005 |
| **TOTAL** | | | | **~$0.13** |

**Scalability with Student Credits:**
- $100 credits = ~770 videos
- $200 credits = ~1,540 videos

**Cost Optimization Strategies:**
1. Cache generated visuals in S3 for reuse in similar videos
2. Use Fargate Spot instances (70% cost reduction) when available
3. Implement request throttling to prevent excessive Bedrock API calls
4. Archive old videos to Glacier after 90 days (90% storage cost reduction)
5. Use DynamoDB on-demand pricing to avoid paying for idle capacity

---

### Launch Strategy and Monetization

**Phase 1: Free Tier (Day 1-30)**
- **Offering**: 3 videos per day, unlimited users
- **Goal**: Build user base, gather feedback, validate product-market fit
- **Limitations**: No auto-publishing (manual download only), watermark on videos
- **Target**: 1,000 users, 10,000 videos generated

**Phase 2: Pro Tier (Day 30+)**
- **Pricing**: $9/month or $90/year (save 17%)
- **Features**:
  - Unlimited video generation
  - Auto-publishing to YouTube Shorts and Instagram Reels
  - No watermarks
  - Priority rendering (faster queue)
  - Advanced analytics dashboard
  - Custom branding options
- **Target**: 10% conversion rate (100 paying users by Month 3)

**Revenue Projections (Month 3):**
- Free users: 900 users × $0 = $0
- Pro users: 100 users × $9 = $900/month
- AWS costs: 100 users × 30 videos/month × $0.13 = $390/month
- **Net profit**: $510/month (57% margin)

**Growth Strategy:**
1. **Viral Loop**: Every published video includes subtle "Made with MayaFlow" branding
2. **Referral Program**: Give 1 month free Pro for every 3 referrals
3. **Creator Partnerships**: Partner with micro-influencers for testimonials
4. **Regional Expansion**: Launch Hindi, Spanish, French versions simultaneously
5. **Platform Integrations**: Add TikTok, Facebook Reels support in Month 6

**Break-Even Analysis:**
- Development costs (AWS credits): $200 (covered by student credits)
- Monthly operating costs: $50 (domain, monitoring, support tools)
- Break-even: 6 paying users ($54/month revenue)
- Expected break-even: Week 6

---

### Target Market and Use Cases

**Primary Users:**
1. **Content Creators** - Reduce editing time from 10 hours to 5 minutes
2. **Educators** - Create engaging educational videos in regional languages
3. **Small Businesses** - Produce marketing content without hiring agencies
4. **Cultural Preservationists** - Animate folklore and traditional stories
5. **Social Media Managers** - Generate daily content at scale

**Use Case Examples:**
- **Hindi Fables**: Preserve traditional stories with culturally-accurate animation
- **Product Tutorials**: Create how-to videos in multiple languages
- **News Summaries**: Convert text articles into engaging video format
- **Recipe Videos**: Transform written recipes into step-by-step visual guides
- **Motivational Quotes**: Generate shareable short-form content

---

### Competitive Landscape

| Feature | MayaFlow | Generic AI Tools | Traditional Editing |
|---------|-----------|------------------|---------------------|
| **Time to Publish** | 5-15 minutes | 30-60 minutes | 10+ hours |
| **Cultural Awareness** | ✅ Built-in | ❌ Generic output | ✅ Manual research |
| **Retention Optimization** | ✅ 3-second rule | ❌ No optimization | ✅ Manual A/B testing |
| **Multi-Language Support** | ✅ 6+ languages | ⚠️ Translation only | ✅ Manual voiceover |
| **Cost per Video** | $0.13 | $5-50 | $50-500 |
| **Technical Skill Required** | None | Low | High |
| **Auto-Publishing** | ✅ Yes | ❌ No | ❌ No |

---

### Success Metrics

**Technical Metrics:**
- Video generation success rate: > 95%
- Average rendering time: < 10 minutes
- API error rate: < 2%
- User authentication success rate: > 99%

**Business Metrics:**
- User retention (30-day): > 40%
- Videos published per user per month: > 5
- Average video view count: > 1,000 views
- User satisfaction score: > 4.5/5

**Impact Metrics:**
- Regional language content created: > 50% of total
- Cultural stories preserved: > 100 unique narratives
- Creator time saved: > 10,000 hours collectively
- Cost savings vs traditional production: > $100,000 collectively

---

## 6. Extensibility & Future-Proofing

### REQ-ARCH-02: Microservices & Event-Driven Architecture

**Requirement:** The system SHALL be architected as loosely coupled microservices that communicate via event-driven patterns to enable independent scaling and component replacement.

**Rationale:** Monolithic architectures become difficult to maintain and scale as features grow. By using microservices with event-driven communication, we can swap out individual components (e.g., changing the voice AI provider from Polly to ElevenLabs) without redeploying the entire backend.

**Acceptance Criteria:**
1. THE System SHALL implement the "Lego Pattern" where each major component (Script_Generator, Voice_Engine, Video_Editor, Publisher) is a separate, independently deployable service
2. Components SHALL communicate via Amazon EventBridge events, NOT direct API calls or hard-coded integrations
3. Each service SHALL subscribe to specific event types and publish completion events for downstream consumers
4. Services SHALL be stateless and idempotent to enable horizontal scaling
5. THE System SHALL use AWS Step Functions as the orchestration layer that coordinates events across services

**Technical Implementation:**
- Event bus: Amazon EventBridge (custom event bus)
- Service deployment: AWS Lambda (lightweight services) or ECS Fargate (heavy services)
- Event schema: JSON with versioned schema registry

**Event Flow Example:**
```
User submits video idea
  ↓
EventBridge: "VideoRequestCreated" event
  ↓
Script_Generator Lambda subscribes → Generates script → Publishes "ScriptGenerated" event
  ↓
Visual_Engine Lambda subscribes → Creates visuals → Publishes "VisualsCreated" event
  ↓
Voice_Engine Lambda subscribes → Synthesizes audio → Publishes "VoiceGenerated" event
  ↓
Video_Editor Fargate subscribes → Renders video → Publishes "VideoRendered" event
  ↓
Publisher Lambda subscribes → Uploads to platform → Publishes "VideoPublished" event
```

**Benefits:**
- Replace any component without affecting others
- Scale individual services based on bottlenecks
- Add new services (e.g., AI Music Generator) by subscribing to existing events
- Test services in isolation with mock events

---

### REQ-API-01: API Versioning Strategy

**Requirement:** All API endpoints SHALL use URI versioning to ensure backward compatibility and smooth client migrations.

**Rationale:** Mobile apps and third-party integrations cannot instantly update when APIs change. Supporting multiple API versions prevents breaking existing clients while allowing new features to be added.

**Acceptance Criteria:**
1. All API endpoints SHALL use URI versioning format: `/api/v1/resource`, `/api/v2/resource`
2. THE System SHALL support at least one previous API version (N-1) for a minimum of 6 months after a new version is released
3. WHEN a new API version is released, THE System SHALL document all breaking changes in a migration guide
4. Deprecated API versions SHALL return a `Deprecation` header with sunset date
5. THE System SHALL log API version usage metrics to track migration progress

**Technical Implementation:**
- API Gateway: AWS AppSync or API Gateway with version-specific resolvers
- Version routing: Lambda function ARN aliases (v1, v2) or separate Lambda functions
- Documentation: OpenAPI/Swagger specs for each version

**Version Lifecycle:**
```
v1 Released (Month 1)
  ↓
v2 Released (Month 6) → v1 marked deprecated
  ↓
v1 Sunset announced (Month 9) → 3-month migration window
  ↓
v1 Removed (Month 12) → Only v2 supported
```

**Example Versioned Endpoints:**
```
POST /api/v1/videos/generate
  - Original schema: {video_idea, format}

POST /api/v2/videos/generate
  - Enhanced schema: {video_idea, format, language, genre, music_mood}
  - Backward compatible: v1 fields still work
```

---

### REQ-CONFIG-01: Feature Flag System

**Requirement:** The system SHALL implement a feature flag mechanism to enable dynamic feature rollout, A/B testing, and gradual releases without code deployments.

**Rationale:** Feature flags allow "dark launching" new features to specific user segments (admins, beta testers, 10% of users) before full rollout. This reduces risk and enables rapid iteration based on feedback.

**Acceptance Criteria:**
1. THE System SHALL implement a feature flag service using AWS AppConfig or DynamoDB
2. The frontend SHALL check feature flags before rendering new UI elements or enabling new functionality
3. Feature flags SHALL support targeting rules: user ID, user tier (free/pro), percentage rollout, geographic region
4. THE System SHALL cache feature flags client-side with 5-minute TTL to reduce API calls
5. Admins SHALL be able to toggle feature flags via a configuration dashboard without code deployment

**Technical Implementation:**
- Storage: DynamoDB table with flag name, enabled status, targeting rules
- Client SDK: AWS AppConfig SDK or custom GraphQL query
- Admin UI: React dashboard with real-time flag updates

**Feature Flag Schema:**
```json
{
  "flag_name": "enable_4k_rendering",
  "enabled": true,
  "targeting": {
    "user_tiers": ["pro"],
    "percentage_rollout": 25,
    "user_ids": ["admin_123", "beta_tester_456"]
  },
  "created_at": "2026-02-15T10:00:00Z",
  "updated_at": "2026-02-20T14:30:00Z"
}
```

**Use Cases:**
- **Gradual Rollout**: Enable "AI Music Generation" for 10% of users, monitor performance, increase to 50%, then 100%
- **Beta Testing**: Enable "Multi-Language Subtitles" only for beta testers
- **Emergency Kill Switch**: Disable "Auto-Publishing" if platform APIs are down
- **A/B Testing**: Show "New UI Layout" to 50% of users, measure engagement

---

### REQ-DATA-02: Schema Evolution and Backward Compatibility

**Requirement:** The Video Project JSON Schema SHALL use optional fields for all non-critical attributes to enable schema evolution without breaking existing parsers.

**Rationale:** As new features are added (e.g., AI music generation, custom fonts, advanced effects), the data contract will evolve. Using optional fields ensures that older services can still parse new JSON documents by ignoring unknown fields.

**Acceptance Criteria:**
1. All new fields added to the Video Project JSON Schema SHALL be optional (not required)
2. Services SHALL gracefully ignore unknown fields when parsing JSON documents
3. THE System SHALL maintain a schema version field in all JSON documents
4. WHEN a service encounters a schema version it doesn't support, IT SHALL log a warning but continue processing with available fields
5. THE System SHALL provide a schema migration tool to upgrade old video projects to new schema versions

**Technical Implementation:**
- Schema versioning: `"schema_version": "2.1.0"` field in all JSON documents
- Parsing strategy: Use permissive JSON parsers that ignore unknown fields
- Migration: Lambda function that reads old schema, applies transformations, writes new schema

**Schema Evolution Example:**
```json
// Version 1.0 (Original)
{
  "schema_version": "1.0.0",
  "project_id": "vid_123",
  "language": "hi",
  "scenes": [...]
}

// Version 2.0 (Added music mood)
{
  "schema_version": "2.0.0",
  "project_id": "vid_123",
  "language": "hi",
  "music_mood": "upbeat",  // NEW OPTIONAL FIELD
  "scenes": [...]
}

// Version 2.1 (Added custom fonts)
{
  "schema_version": "2.1.0",
  "project_id": "vid_123",
  "language": "hi",
  "music_mood": "upbeat",
  "subtitle_font": "Roboto-Bold",  // NEW OPTIONAL FIELD
  "scenes": [...]
}
```

**Backward Compatibility Rules:**
- Old services (v1.0) can parse v2.0 documents by ignoring `music_mood`
- New services (v2.0) can parse v1.0 documents by using default value for `music_mood`
- Never remove required fields (breaking change)
- Never change field types (breaking change)
- Always add new fields as optional

---

### REQ-PLUGIN-01: Plugin Architecture for Future Extensions

**Requirement:** The system SHALL support a plugin architecture to enable third-party integrations and custom extensions without modifying core code.

**Rationale:** As MayaFlow grows, users may want custom integrations (e.g., custom AI models, proprietary music libraries, brand-specific visual styles). A plugin system enables extensibility without bloating the core platform.

**Acceptance Criteria:**
1. THE System SHALL define plugin interfaces for: Visual Generators, Voice Synthesizers, Music Providers, Publishing Platforms
2. Plugins SHALL be registered in a plugin registry (DynamoDB table) with metadata: name, version, author, capabilities
3. Users SHALL be able to enable/disable plugins via the settings dashboard
4. THE System SHALL load plugins dynamically at runtime based on user configuration
5. Plugins SHALL run in isolated execution environments (separate Lambda functions) to prevent security issues

**Technical Implementation:**
- Plugin interface: Standardized JSON input/output contracts
- Plugin registry: DynamoDB table with plugin metadata
- Plugin execution: Lambda functions invoked via EventBridge

**Plugin Interface Example:**
```python
# Visual Generator Plugin Interface
class VisualGeneratorPlugin:
    def generate(self, prompt: str, aspect_ratio: str) -> str:
        """
        Generate visual from prompt.
        Returns: S3 URL of generated image/video
        """
        pass

# Example: Custom Stable Diffusion Plugin
class StableDiffusionPlugin(VisualGeneratorPlugin):
    def generate(self, prompt: str, aspect_ratio: str) -> str:
        # Call Stable Diffusion API
        image_url = stable_diffusion_api.generate(prompt)
        # Upload to S3
        s3_url = upload_to_s3(image_url)
        return s3_url
```

**Future Plugin Examples:**
- **ElevenLabs Voice Plugin**: Alternative to Amazon Polly with more voice options
- **Suno AI Music Plugin**: Generate custom background music instead of using library
- **TikTok Publisher Plugin**: Add TikTok as a publishing platform
- **Brand Style Plugin**: Apply company-specific visual styles and fonts

---

## 7. Implementation Roadmap

### Phase 1: MVP (Weeks 1-4)
- ✅ Magic Box UI (React + Amplify)
- ✅ Amazon Bedrock integration (script generation)
- ✅ Amazon Polly integration (voice synthesis)
- ✅ Basic video assembly (FFmpeg on Fargate)
- ✅ S3 + DynamoDB setup
- ✅ Manual publishing (download video)

### Phase 2: Automation (Weeks 5-8)
- ✅ AWS Step Functions orchestration
- ✅ Amazon Titan image generation
- ✅ Pexels API integration
- ✅ Auto-publishing to YouTube
- ✅ Real-time progress tracking (AppSync)

### Phase 3: Retention Engineering (Weeks 9-12)
- ✅ 3-second rule implementation
- ✅ Burned-in captions
- ✅ Audio ducking
- ✅ Amazon Rekognition cropping
- ✅ Thumbnail generation

### Phase 4: Scale & Polish (Weeks 13-16)
- ✅ Instagram Reels support
- ✅ Multi-language expansion (6+ languages)
- ✅ Cost optimization (caching, Spot instances)
- ✅ Error handling improvements
- ✅ User analytics dashboard

---

## 8. Glossary

| Term | Definition |
|------|------------|
| **Maya** | Sanskrit for "Magic" or "Illusion," representing the system's ability to conjure video reality from simple text—transforming imagination into tangible visual content |
| **Magic Box** | Simplified user interface with minimal input fields |
| **Brain** | Intelligent backend orchestration system (Amazon Bedrock) |
| **Retention Engine** | Algorithm that enforces viral pacing (3-second rule, effects) |
| **Culture-Lock** | System that ensures culturally-appropriate content generation |
| **Hybrid-Reality** | Blending real stock footage with AI-generated elements |
| **Hardsubs** | Burned-in captions permanently embedded in video frames |
| **Audio Ducking** | Automatic volume reduction of background music during voice-over |
| **Auto-Pilot** | Mode where video publishes automatically without user review |
| **Safe Zone** | Screen area that avoids platform UI overlays (bottom 120px) |
| **Viral Science** | Data-driven techniques for maximizing viewer retention |

---

## 9. Appendix

### Supported Languages and Voices

| Language | Code | Amazon Polly Neural Voices | Cultural Considerations |
|----------|------|---------------------------|-------------------------|
| English | en | Joanna, Matthew, Salli | Neutral accent, clear pronunciation |
| Hindi | hi | Aditi, Kajal | Traditional storytelling pacing, respectful tone |
| Spanish | es | Lupe, Pedro | Regional variations (Spain vs Latin America) |
| French | fr | Léa, Rémi | Formal vs informal register |
| German | de | Vicki, Hans | Compound word handling |
| Japanese | ja | Takumi, Kazuha | Honorifics, formal speech patterns |

### Background Music Library

| Genre | Track Name | Duration | Mood | BPM |
|-------|-----------|----------|------|-----|
| Fable | ambient_fable_01.mp3 | 120s | Calm, mystical | 80 |
| News | upbeat_news_01.mp3 | 90s | Energetic, urgent | 120 |
| Tutorial | soft_tutorial_01.mp3 | 180s | Focused, helpful | 90 |
| Entertainment | fun_entertainment_01.mp3 | 120s | Playful, exciting | 128 |

### Platform-Specific Requirements

**YouTube Shorts:**
- Duration: 15-60 seconds
- Aspect ratio: 9:16 (vertical) or 1:1 (square)
- Resolution: 1080x1920 minimum
- Format: MP4 (H.264 + AAC)
- File size: < 256MB
- API: YouTube Data API v3

**Instagram Reels:**
- Duration: 15-60 seconds
- Aspect ratio: 9:16 (vertical only)
- Resolution: 1080x1920
- Format: MP4 (H.264 + AAC)
- File size: < 100MB
- API: Instagram Graph API

---

**Document Version:** 1.0  
**Last Updated:** 2026-02-15  
**Status:** Final for Hackathon Submission  
**Track:** AI for Media, Content & Digital Experiences

