# Darija & Arabic NLP Annotator

A browser-based pre-annotation tool for Arabic, Moroccan Darija, and French-Arabic code-switched text. Paste raw text, get structured annotations — then review, correct, and export.

This isn't a replacement for human annotators. It's an accelerator — it gets you 80% of the way there and flags the spots where you need to pay attention.

**[Live Demo →](#)** · **[Report a Bug](https://github.com/Jenniyaa/darija-arabic-nlp-annotator/issues)**

---

## Why This Exists

Most annotation workflows aren't built for Darija.

Arabic gets partial support. Darija almost never. Darija mixed with French in the same sentence? Nothing handles that.

But that's how Moroccans actually write online. "mzyan bzzaf had lfilm, tbarkallah 3la les acteurs" is a real sentence — Darija in Latin script, code-switching into French mid-sentence. This is the norm, not an edge case.

This tool was built out of that frustration. It takes raw text and returns structured annotations with sentiment, language detection, intent, topic tags, and quality flags — formatted for direct use in any annotation platform or NLP pipeline.

---

## Features

- **Multi-dialect support** — Arabic (MSA), Moroccan Darija, French, and mixed/code-switched text
- **Franco-Arab handling** — Correctly processes Darija written in Latin script (3, 7, 9, etc.)
- **Cautious Darija annotation** — System prompt tuned to default to lower confidence and flag slang, rather than wrongly assigning High confidence to ambiguous expressions
- **Two annotation levels** — Basic (sentiment + language) or Detailed (sentiment, intent, topics, flags, notes)
- **Batch processing** — Annotate one entry or hundreds at once, one per line
- **Export options** — Copy to clipboard, download as JSON, or download as CSV
- **No API key stored in code** — Users enter their own Groq API key in the UI
- **Zero setup** — Single HTML file, runs in any browser, no server or build step required

---

## Limitations & Honest Notes

This tool uses an LLM under the hood, and LLMs have real blind spots with Darija.

**What goes wrong:**

- Darija slang often looks neutral but carries vulgar, sarcastic, or emotionally charged meanings that differ completely from their Modern Standard Arabic roots. The model frequently misses this.
- Short informal expressions get misclassified as "Neutral, High confidence" when they're actually frustrated, sarcastic, or angry.
- Code-switched text (Darija + French) adds another layer of ambiguity the model doesn't always navigate well.

**What we did about it:**

- The system prompt is tuned to make the model generally more cautious with Darija — defaulting to Medium or Low confidence rather than High.
- Short informal Darija expressions are treated as likely emotional rather than neutral.
- Slang and ambiguity flags are triggered more aggressively.

**The bottom line:**

This is a pre-annotation tool, not a final annotator. Always review the output before using it in production datasets. The value is in the time saved, not in blind trust.

---

## Output Schema

Each annotated entry returns:

| Field | Description |
|---|---|
| `id` | Sequential integer |
| `original_text` | Exact input text |
| `clean_text` | Normalized version (typos fixed, noise removed) |
| `detected_language` | Arabic, Darija, French, English, Mixed-AR-FR, Mixed-DA-FR, etc. |
| `sentiment` | Positive, Negative, Neutral, or Mixed |
| `sentiment_confidence` | High, Medium, or Low |
| `intent` | Opinion, Question, Request, Statement, Emotion, Humour, Sarcasm |
| `topics` | Up to 3 topic tags (e.g. politics, youth, education) |
| `flags` | code-switching, offensive, ambiguous, dialect-variant, slang, etc. |
| `annotation_note` | Reviewer notes on edge cases or ambiguity |

Basic mode returns only: id, original_text, clean_text, detected_language, sentiment, sentiment_confidence.

---

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/Jenniyaa/darija-arabic-nlp-annotator.git
cd darija-arabic-nlp-annotator
```

### 2. Open in your browser

Double-click `index.html` — no server needed.

### 3. Enter your Groq API key

Paste your key into the input field at the top of the tool. Get a free key at [console.groq.com](https://console.groq.com).

Your key stays in your browser session only — it's never stored or sent anywhere except directly to Groq's API.

---

## Deployment

Single HTML file, no dependencies. Deploy anywhere:

**Vercel:**
```bash
npm i -g vercel
vercel
```

**GitHub Pages:**
Push to a repo, go to Settings → Pages → select branch.

**Netlify:**
Drag and drop the folder at [app.netlify.com/drop](https://app.netlify.com/drop).

---

## Tech Stack

- Vanilla HTML/CSS/JS — no frameworks, no build step
- [Groq API](https://groq.com) with `llama-3.3-70b-versatile` for better nuance with dialect and slang
- [DM Sans](https://fonts.google.com/specimen/DM+Sans) + [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono)

---

## Use Cases

- Pre-annotating Arabic/Darija datasets before human review
- Quick sentiment analysis on social media data (YouTube, Twitter, Facebook comments)
- Bootstrapping annotation for low-resource dialect NLP
- Linguistic research on Darija-French code-switching patterns
- Portfolio project demonstrating NLP annotation pipeline knowledge

---

## Future Improvements

- **In-UI correction** — Let users edit annotations directly in the output and export the corrected version, turning it into a full annotation workflow
- **Community Darija glossary** — A growing set of slang examples fed into the system prompt, contributed by native speakers
- **Other Arabic dialects** — Support for Tunisian, Algerian, Egyptian, and Levantine dialect patterns
- **Serverless API proxy** — Optional Vercel/Netlify function to keep the Groq key fully server-side for production use

---

## Contributing

Contributions are welcome — especially from native Darija speakers who can help improve slang handling. If you find a misannotation, open an issue with the input text and what the correct annotation should be. That directly improves the tool for everyone.

---

## Author

**Fatima Zohra Hligue**

- [LinkedIn](https://www.linkedin.com/in/fatima-zohra-hligue/)
- [GitHub](https://github.com/Jenniyaa)

---

## License

MIT
