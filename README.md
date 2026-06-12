# 🎬 CineParser — Movie Information Extractor

> *Paste a paragraph. Get a movie's soul, structured.*

---

## What Is This?

You've seen a movie description somewhere — a blog post, a review, a friend's WhatsApp message. CineParser reads that raw, unstructured text and instantly pulls out everything that matters: title, genre, cast, director, release year, rating, and a clean summary — all formatted as structured data.

No forms to fill. No dropdowns to click. Just plain English in, clean JSON out.

---

## ✨ Demo Flow

```
Input  ──▶  "Christopher Nolan's Inception (2010) stars Leonardo DiCaprio
             as a thief who steals secrets through dreams..."

Output ──▶  {
              "title": "Inception",
              "release_year": 2010,
              "genre": ["Sci-Fi", "Thriller"],
              "director": "Christopher Nolan",
              "cast": ["Leonardo DiCaprio", ...],
              "rating": null,
              "summary": "A thief who steals secrets through dreams..."
            }
```

---

## 🧠 How It Works

```
┌─────────────────────────────────────────────────────────────┐
│                        CineParser                           │
│                                                             │
│   📝 Raw Paragraph                                          │
│        │                                                    │
│        ▼                                                    │
│   🔧 LangChain Prompt Template                              │
│        │  (injects format instructions from Pydantic)       │
│        ▼                                                    │
│   🤖 Mistral AI  (mistral-small-2603)                       │
│        │  (reasons about the text, outputs JSON)            │
│        ▼                                                    │
│   🔍 Pydantic Parser                                        │
│        │  (validates & structures the output)               │
│        ▼                                                    │
│   ✅ Clean Movie Object                                      │
└─────────────────────────────────────────────────────────────┘
```

Two interfaces, same brains:

| Mode | File | Best For |
|------|------|----------|
| **Terminal** | `core.py` | Quick scripting, automation, piping into other tools |
| **Web UI** | `UICore.py` | Human-friendly, shows raw + structured output side-by-side |

---

## 🗂️ Project Structure

```
cineparser/
├── core.py          # Terminal interface — input prompt, parse, print
├── UICore.py        # Streamlit web UI — visual, interactive
├── requirement.txt  # All dependencies
└── .env             # Your API keys (never commit this)
```

---

## ⚡ Getting Started

### 1. Clone & Install

```bash
git clone https://github.com/ramya-rastogi/CineSnap.git
cd CineSnap
pip install -r requirement.txt
```

### 2. Set Up Your API Key

Create a `.env` file in the root:

```env
MISTRAL_API_KEY=your_mistral_api_key_here
```

Get your key at [console.mistral.ai](https://console.mistral.ai)

### 3. Run It

**Terminal mode:**
```bash
python core.py
```

**Web UI mode:**
```bash
streamlit run UICore.py
```

---

## 🎯 What Gets Extracted

| Field | Type | Description |
|-------|------|-------------|
| `title` | `str` | Movie title |
| `release_year` | `int?` | Year of release (if found) |
| `genre` | `List[str]` | One or more genres |
| `director` | `str?` | Director's name (if mentioned) |
| `cast` | `List[str]` | Named actors in the paragraph |
| `rating` | `float?` | Score if referenced (e.g. 8.5/10) |
| `summary` | `str` | Concise summary of the plot |

Fields marked `?` are optional — if the paragraph doesn't mention them, they come back as `null` instead of crashing.

---

## 🛠️ Tech Stack

| Layer | Tool |
|-------|------|
| LLM | [Mistral AI](https://mistral.ai) — `mistral-small-2603` |
| Orchestration | [LangChain](https://langchain.com) |
| Schema & Validation | [Pydantic v2](https://docs.pydantic.dev) |
| Web Interface | [Streamlit](https://streamlit.io) |
| Config | [python-dotenv](https://pypi.org/project/python-dotenv/) |

---

## 🔮 Ideas for What's Next

- [ ] Support multiple movies in one paragraph
- [ ] Export extracted data to CSV / Excel
- [ ] Add Google Gemini as an alternative model
- [ ] Batch mode — process a list of paragraphs from a file
- [ ] Confidence scores on extracted fields

---

## 📄 License

MIT — do whatever you want with it, attribution appreciated.

---

*Built with LangChain + Mistral AI · Structured by Pydantic · Served by Streamlit*
