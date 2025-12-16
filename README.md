# Highlight AI - Chrome Extension

A powerful Chrome extension for AI-powered text highlighting, PDF analysis, and image OCR with local offline capabilities.

## Features

### 1. **AI Chat Sidebar** 🤖
- Open a persistent sidebar on any webpage
- Chat with AI powered by OpenRouter (Deepseek/Mistral models)
- Press Enter to send, Shift+Enter for new line
- Automatic context from selected text

### 2. **PDF Upload & RAG** 📄
- Upload PDF files to the sidebar
- Automatic text extraction and chunking
- Retrieval-Augmented Generation (RAG) for intelligent document Q&A
- AI answers questions using PDF content as context

### 3. **Image OCR** 🔤
- Paste screenshots directly into the sidebar
- Three-tier OCR engine:
  - **Local Tesseract** (offline, no API needed) ✅ CONFIGURED
  - **CDN Tesseract** (fallback if local fails)
  - **OCR.Space API** (optional, requires API key)
- Extract text from images
- Ask AI questions about images

### 4. **PDF Reading** 📖
- Automatic PDF extraction when on PDF pages
- No upload needed - reads directly from browser

## Installation & Setup

### Step 1: Basic Setup
1. Go to `chrome://extensions/`
2. Enable **Developer mode** (top right)
3. Click **Load unpacked**
4. Select this extension folder

### Step 2: Add OpenRouter API Key
1. Get API key from https://openrouter.ai/
2. Click extension icon → **Options**
3. Paste your OpenRouter API key
4. Click **Save Settings**

### Step 3: Enable Offline OCR (Optional)
✅ **Already configured!** Local Tesseract files are included:
- `tesseract/tesseract.min.js` - Main library
- `tesseract/worker.min.js` - Worker thread
- `tesseract/tesseract-core.wasm.js` - Core engine

No additional setup needed for offline OCR!

### Step 4: Setup OCR API Fallback (Optional)
If you want OCR to work without local Tesseract:
1. Get free API key from https://ocr.space/ocrapi
2. Click extension icon → **Options**
3. Paste your OCR.Space API key
4. Click **Save Settings**

## Usage Guide

### Opening the Sidebar
1. Navigate to any webpage or PDF
2. Click the **✨ Ask AI** button (bottom-right)
3. Sidebar appears on the right side

### Chat with AI
- Type your question
- Press **Enter** to send (Shift+Enter for multiline)
- AI responds using uploaded PDFs or page context

### Upload & Chat with PDFs
1. Click **📄 Upload PDF** button in sidebar header
2. Select a PDF file
3. Wait for extraction (shows progress)
4. Ask questions - AI will search the PDF for answers

### Extract Text from Screenshots (OCR)
1. Take a screenshot (Windows: Shift+PrintScreen)
2. Paste into sidebar (Ctrl+V)
3. Click **🔤 Extract Text (OCR)**
4. Text appears below image and in input field

### Ask AI About Images
1. Paste image into sidebar
2. Click **💬 Ask AI About Image**
3. Type your question in the prompt
4. AI responds with image analysis (includes OCR text)

### Close Sidebar
- Click **Close** button in header
- Works on regular pages and PDFs

## File Structure

```
highlight ai/
├── manifest.json          # Extension configuration
├── background.js          # Service worker (AI calls)
├── content.js            # Page injection script
├── sidebar.html          # Sidebar UI template
├── sidebar.js            # Sidebar logic
├── popup.html/js         # Popup UI
├── options.html/js       # Settings page
├── pdfReader.js          # PDF extraction
├── icon-128.png          # Extension icon
├── pdfjs/                # PDF.js library (bundled)
│   ├── pdf.mjs
│   └── pdf.worker.mjs
└── tesseract/            # OCR library (LOCAL) ✅
    ├── tesseract.min.js
    ├── worker.min.js
    └── tesseract-core.wasm.js
```

## Settings

### Extension Options Page
Access via: Extension Icon → **Options**

**Fields:**
- **Model**: Select AI model (default: OpenRouter Deepseek)
- **OpenRouter API Key**: Your API key (starts with `or-...`)
- **OCR API Key** (optional): OCR.Space API key for fallback OCR

## Troubleshooting

### Issue: "Extension context invalidated" error
**Solution:** Refresh the webpage after reloading the extension

### Issue: OCR not working
**Solutions:**
1. Check if local Tesseract files exist in `tesseract/` folder
2. Add OCR.Space API key in Options as fallback
3. Check browser console (F12) for error details

### Issue: AI not responding
**Solutions:**
1. Verify OpenRouter API key is valid
2. Check internet connection
3. Verify API key has credit/quota

### Issue: PDF upload fails
**Solutions:**
1. Use PDFs with text (not scanned images)
2. Try a smaller PDF file
3. Check browser console for errors

## Advanced Features

### RAG (Retrieval-Augmented Generation)
- Uploaded PDFs are split into 1000-character chunks
- Each question searches these chunks for relevant content
- Top 5 matching chunks included as context for AI
- Naive keyword matching (no ML models needed)

### Keyboard Shortcuts
- **Ctrl+V**: Paste images into sidebar
- **Enter**: Send message (in input field)
- **Shift+Enter**: New line (in input field)

## API Usage & Credits

- **OpenRouter**: ~$0.001 per question (check current rates)
- **OCR.Space**: Free tier includes 25,000 requests/day
- **Local Tesseract**: Completely free, offline, no limits

## Architecture

```
Webpage/PDF
    ↓
Content Script (content.js)
    ↓
Sidebar (sidebar.html + sidebar.js)
    ↓
Background Service Worker (background.js)
    ↓
OpenRouter API → AI Response
```

- **Content Script**: Injects floating button, manages sidebar injection
- **Sidebar**: Handles UI, OCR, PDF upload, chat
- **Background**: Routes AI requests, applies RAG context

## Privacy & Security

- All local processing is private (OCR via local Tesseract)
- PDFs only processed locally, never sent to servers
- API calls go only to OpenRouter (AI) and OCR.Space (if configured)
- Extension data stored in Chrome's secure storage

## Future Improvements

Potential enhancements:
- [ ] Embedding-based semantic search (instead of keyword matching)
- [ ] Multiple PDF support with document references
- [ ] Custom model selection
- [ ] Export chat history
- [ ] Highlight synchronization
- [ ] Multi-language OCR
- [ ] Batch image OCR

## Support & Feedback

For issues or suggestions:
1. Check the troubleshooting section above
2. Review console errors (F12 → Console)
3. Verify API keys and configuration

## License

Personal use only. Modify as needed for your use case.

---

**Last Updated:** November 2025
**Version:** 1.0
**Status:** Fully Functional ✅
