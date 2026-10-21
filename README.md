<div align="center">

# 🛡️ PromptGuard

### AI Privacy Sanitizer

**Strip emails, phone numbers, IP addresses, API keys and your own sensitive keywords from text *before* you paste it into ChatGPT, Claude, Gemini or any other AI tool.**

100% client-side · Zero dependencies to install · One single HTML file

[**🚀 Live Demo**](https://xiaoyulei317-droid.github.io/PromptGuard---AI-Privacy-Sanitizer/) · [Report a Bug](https://github.com/xiaoyulei317-droid/PromptGuard---AI-Privacy-Sanitizer/issues) · [Request a Feature](https://github.com/xiaoyulei317-droid/PromptGuard---AI-Privacy-Sanitizer/issues)

![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)
![No Backend](https://img.shields.io/badge/backend-none-blue.svg)
![Single File](https://img.shields.io/badge/build-none%20%C2%B7%20single%20HTML-8b5cf6.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

</div>

---

## 📖 About

PromptGuard is a lightweight, open-source web tool that removes personal and confidential information from any text in real time. Paste a log file, an email thread, a config file or a bug report on the left, and get a clean, AI-ready version on the right, with every sensitive item replaced by a clear placeholder tag such as `[EMAIL_REDACTED]` or `[API_KEY_REDACTED]`.

Everything runs **locally in your browser**. Your text is never uploaded, stored or logged, and there is no server at all.

## 🔗 Live Demo

👉 **https://xiaoyulei317-droid.github.io/PromptGuard---AI-Privacy-Sanitizer/**

> Click **Load Sample Text** to see every detection rule in action.

## 🤔 Why PromptGuard?

AI assistants have become part of everyday work, and so has the habit of pasting raw text into them. That text often contains more than you realize:

- 📧 **Customer emails and phone numbers** in support tickets and CRM exports
- 🌐 **Internal IP addresses** in server logs and stack traces
- 🔑 **API keys and tokens** in `.env` files, `curl` commands and config snippets
- 🏢 **Client names, project code names and colleagues' names** in meeting notes

Once that data is sent to a third-party AI service, you no longer control it. It may be stored, reviewed or used for training, depending on the provider and your plan. A single leaked API key can cost real money within minutes, and sharing customer data can break GDPR, CCPA or your company's policies.

**PromptGuard adds a 2-second safety step between your clipboard and the AI.** You still get useful answers from the AI, because the structure and meaning of your text stay intact. Only the sensitive values are removed.

## ✨ Features

### 🔍 Smart detection

| Rule | Replaced with | What it catches |
| --- | --- | --- |
| **Email** | `[EMAIL_REDACTED]` | Standard addresses, including `+tags` and multi-level domains |
| **Phone Number** | `[PHONE_REDACTED]` | International (`+1`, `+44`, `+886`, …), area codes in parentheses, dashed, dotted and spaced formats, common mobile numbers |
| **IP Address** | `[IP_REDACTED]` | IPv4 with octet validation, plus full and compressed IPv6 (`::1`, `fe80::1`, …) |
| **API Key / Token** | `[API_KEY_REDACTED]` | `sk-…` keys (OpenAI, Anthropic, OpenRouter, DeepSeek), AWS, Google, GitHub, GitLab, Slack, Stripe, Hugging Face, Groq, xAI, JWTs, `Bearer` tokens and `SECRET_KEY=…` style secrets |
| **Custom Keywords** | `[KEYWORD_REDACTED]` | Any word or phrase you add: names, companies, project code names, internal hostnames |

### 🎯 Low false positives

The detectors are tuned so that ordinary text is left alone. These are **not** redacted:

- Dates and times: `2026-10-21`, `14:30`, `2026-10-21T14:30:00Z`
- Version numbers and decimals: `3.14.2`, `3.14159`
- Money, ranges and IDs: `$12,500`, `5000-8000`, `#48213`
- UUIDs, credit-card-length numbers and tables of numbers
- Code such as `std::io`, `Add::new` and Python slices like `a[1::2]`

When two rules overlap, the stronger one wins. For example, a keyword inside an email address never leaves part of the address visible.

### ⚡ Real-time workflow

- **Live preview:** the output updates as you type or paste
- **Color-coded highlighting:** each type of redaction has its own color, so you can review the result at a glance
- **One-click copy** of the clean text (with a fallback for older browsers)
- **Load Sample Text** button for a quick demo
- **Drag and drop** a `.txt` file straight into the input box

### 📊 Live statistics

- Number of items redacted, broken down by type
- Character and word count (input vs. output)
- Estimated token count, so you know how much of the model's context window you will use

### 🎨 Polished UI

- Clean, modern design built with Tailwind CSS
- 🌗 **Dark / light mode** that follows your system setting and remembers your choice
- Fully responsive, from phones to wide screens
- Keyboard accessible, with ARIA switches and visible focus rings

### 🔒 Privacy by design

- **No backend, no analytics, no cookies, no tracking**
- No web fonts or third-party requests, apart from the Tailwind CSS CDN
- Only your rule toggles and theme preference are saved, in `localStorage`. **Your text and keyword list are never stored.**
- Works offline once Tailwind has loaded. Add a prebuilt CSS file for fully offline use.

## 🚀 Quick Start

PromptGuard is a single `index.html` file. There is no build step and nothing to install.

**Option 1: open it locally**

```bash
git clone https://github.com/xiaoyulei317-droid/PromptGuard---AI-Privacy-Sanitizer.git
cd PromptGuard---AI-Privacy-Sanitizer
```

Then double-click `index.html` to open it in your browser.

**Option 2: serve it locally**

```bash
npx serve .
```

**Option 3: deploy to GitHub Pages (free)**

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Source**, choose **Deploy from a branch**, select `main` and `/ (root)`, then click **Save**.
4. After about a minute, your tool is live at `https://xiaoyulei317-droid.github.io/PromptGuard---AI-Privacy-Sanitizer/`.

It also works as-is on Netlify, Vercel, Cloudflare Pages or any static host.

## 🧪 Example

**Input**

```text
Reporter: Jane Doe <jane.doe@example.com>
Phone: +1 (555) 123-4567
Affected host: 192.168.1.42
OPENAI_API_KEY=sk-proj-••••••••••••••••••••••••
This belongs to Project Phoenix. Deployed on 2026-10-21.
```

**Output** (with the custom keywords `Jane Doe` and `Project Phoenix`)

```text
Reporter: [KEYWORD_REDACTED] <[EMAIL_REDACTED]>
Phone: [PHONE_REDACTED]
Affected host: [IP_REDACTED]
OPENAI_API_KEY=[API_KEY_REDACTED]
This belongs to [KEYWORD_REDACTED]. Deployed on 2026-10-21.
```

## 🛠️ How It Works

All logic lives in two `<script>` blocks inside `index.html`:

1. **Sanitizer engine** (`PromptGuard`, pure JavaScript with no DOM access). Each rule runs its own regular expressions on the original text, in priority order: API Key → Email → IP → Phone → Keyword. Candidate matches pass through validation functions (for example `isLikelyPhone()` and `isLikelyIPv6()`) that filter out look-alikes. Matched character ranges are reserved, so overlapping matches can never split one another. The text is then rebuilt with placeholder tags.
2. **UI layer**. Handles input events, toggles, keyword chips, theme, clipboard and statistics.

Matching runs in linear time on typical input. A 1 MB document is processed in about 50 ms.

### Token estimation

Token counts are a heuristic: about **4 characters per token** for Latin-script text and about **1 token per Chinese, Japanese or Korean character**. Real counts vary by model and tokenizer.

## 🧩 Customization

Want to detect a new kind of secret? Add a pattern to the `API_KEY_PATTERNS` array in `index.html`:

```js
// Example: detect "acme_live_..." internal tokens
{ re: /(?<![\w-])acme_live_[A-Za-z0-9]{24,}/g },
```

Want different placeholder text? Edit the `tag` values in the `RULES` object:

```js
email: { label: 'Email', tag: '<EMAIL>' },
```

## ⚠️ Limitations

PromptGuard is a **safety net, not a guarantee**. Detection is pattern-based, so:

- It does **not** recognize arbitrary names, addresses or other free-form personal data. Add those as **Custom Keywords**.
- Short local phone numbers without an area code (such as `555-1234`) are intentionally skipped, because they look the same as number ranges.
- New or unusual API key formats may not be recognized yet. PRs are welcome.

**Always review the output before sharing it.**

## 🗺️ Roadmap

- [ ] Numbered, consistent tags (`[EMAIL_1]`, `[EMAIL_2]`) so the AI can tell entities apart
- [ ] Restore original values in the AI's reply (reversible mapping)
- [ ] More detectors: credit cards (Luhn-validated), IBANs, national ID numbers, street addresses
- [ ] Browser extension
- [ ] Optional encrypted saving of keyword lists

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/new-detector`
3. Commit your changes: `git commit -m "Add detector for XYZ tokens"`
4. Push the branch and open a Pull Request.

When you add or change a detector, please include examples of text it **should** catch and text it **should not** catch.

## 📄 License

Released under the [MIT License](LICENSE). Free to use, modify and distribute.

---

<div align="center">

If PromptGuard helps keep your data safe, please consider giving it a ⭐ on GitHub!

</div>
