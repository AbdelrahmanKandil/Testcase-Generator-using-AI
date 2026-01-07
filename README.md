<div align="center">

  <h1>🧪 Kandil Testing Kit</h1>

  <h3><em>Create quality test cases faster.</em></h3>

  <p align="center">
    This is an open-source set of rules and instructions for AI-powered test case generation. It automates the routine process of creating test cases for manual testing: based on feature requirements and existing test case examples. As a result, users get test cases that completely match the style and structure of those typically written manually.
  </p>

  <p align="center">
    <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT License" /></a>
  </p>

</div>

---

## 🤖 Supported AI Tools

This kit works with multiple AI assistants:

| Tool | How to Use |
|------|------------|
| **Cursor AI** | Uses `.cursor/commands/` folder automatically. Run `/kandil.generate`, `/kandil.init`, `/kandil.clear` |
| **GitHub Copilot** | Reads `.github/instructions/Copilot.instructions.md` automatically. Just ask: `Generate test cases from: login.md` |
| **Google Gemini / AI Studio** | Copy content from `Copilot.instructions.md` and paste as context, then provide your requirements |
| **ChatGPT / Claude** | Copy the instructions file content as system prompt, then provide your requirements |

> 💡 **Tip:** For non-Cursor tools, make sure the AI can see the instructions file (`.github/instructions/Copilot.instructions.md`). You can either reference it directly or paste its content.

---

> ℹ️ **Recommendation:** For best results, use clearly structured, complete, and formalized requirements, as well as specific test case examples. The quality of input data directly affects the quality of the generated output.

---

## 🗂️ Project Structure

```text
Kandil-Testing-Kit/
├── .github/
│   └── instructions/
│       └── Copilot.instructions.md  # instructions for GitHub Copilot & other AIs
├── config/
│   ├── default-rules.md         # fallback rules (automatic)
│   └── user-rules.mdc           # personal rules (generated)
|
├── feature-requirements/        # feature/UI requirements
├── generated-test-cases/        # generation results
├── test-case-examples/          # your test case examples
├── .cursor/
│   ├── rules/
│   │   └── kandil.cursorrules.mdc # core rules for LLM
│   └── commands/
│       ├── kandil.generate.md
│       ├── clear.md
│       └── init.md
└── README.md
```

---

## 📒 Supported Formats

- 📝 `md`, `txt`
- 🖼️ `png`, `jpg` (OCR; accuracy depends on quality)
- ⛔ `docx`, `pdf` not supported — convert to md/txt or png/jpg

---

## 🔄 Converting DOCX/PDF to Markdown

If you have requirements in `.docx` or `.pdf` format, you can convert them to Markdown using **Pandoc**.

### Installing Pandoc

**Windows:**
```powershell
winget install --id JohnMacFarlane.Pandoc
```
Or download the installer from [pandoc.org/installing.html](https://pandoc.org/installing.html)

**macOS:**
```bash
brew install pandoc
```

**Linux:**
```bash
sudo apt-get install pandoc  # Debian/Ubuntu
sudo yum install pandoc      # RedHat/CentOS
```

### Converting Requirements to Markdown

**Basic conversion:**
```bash
pandoc BRD.docx -o output.md
```

**Convert with better formatting:**
```bash
pandoc BRD.docx -t markdown -o output.md
```

**Extract embedded images to media folder:**
```bash
pandoc BRD.docx --extract-media=./media -t markdown_strict -o output.md
```

**Advanced conversion (strict markdown, extract media, no wrapping):**
```bash
pandoc BRD.docx -t markdown_strict-raw_html --extract-media=./media --wrap=none -o output.md
```

**Convert PDF to Markdown:**
```bash
pandoc input.pdf -o output.md
```

> 💡 **Note:** PDF conversion quality depends on the PDF structure. For best results, use DOCX sources when available.

### Converting Generated Test Cases to Other Formats

After generating test cases, you can export them to Word or Excel:

**Convert to HTML:**
```bash
sed 's/<br[[:space:]]*\/?>/\n/g' generated-test-cases/your-test-cases.md | pandoc -f markdown-raw_html -t html -s -o output.html
```

**Convert to Word (DOCX):**
```bash
pandoc generated-test-cases/your-test-cases.md -o output.docx
```

**Convert to Excel-compatible HTML:**
```bash
pandoc generated-test-cases/your-test-cases.md -t html -o output.html
```
Then open `output.html` in Excel and save as `.xlsx`.

---

## ⚡ Quick Start

1. **Clone** the repository:
   ```
   git clone https://github.com/AbdelrahmanKandil/Testcase-Generator-using-AI.git
   cd Testcase-Generator-using-AI
   ```
2. **Add examples:** place 3–5 test case files in the `test-case-examples/` folder. Supported formats: `md`, `txt`, `png`, `jpg`.
3. **Save requirements:** place your specifications in the `feature-requirements/` folder (supports: md, txt, png, jpg).
4. **Initialize personal rules:** in Cursor chat, run
   ```
   /kandil.init Full Name
   ```
   After execution, the file `config/user-rules.mdc` will be created.
5. **Generate test cases:** run the command
   ```
   /kandil.generate feature-requirements/your-file.md
   ```
   - Using GitHub Copilot/ChatGPT: ask `Generate test cases from: feature-requirements/your-file.md`.
   - The resulting file appears in `generated-test-cases/{YYYY-MM-DD}_{name}_test-cases.md`.
6. **Reset style (if needed):** if you want to change generation rules, run
   ```
   /kandil.clear
   ```
   After that, you can initialize personal rules again with different examples.

---

## 🛠️ Commands

- `/kandil.init` — analyzes your examples, creates personal rules (user-rules), shows summary.
- `/kandil.generate` — uses active rules and requirements, generates test cases.
   - Using Copilot/ChatGPT: ask `Generate test cases from: feature-requirements/your-file.md`.
   - If the requirements file has multiple user stories, specify the one to focus on (e.g., “Generate test cases for user story: checkout flow”).
- `/kandil.clear` — resets user-rules, offers cleanup of examples/requirements/output.

---

## ⚠️ Limitations

- ⛔ No `docx/pdf` support — conversion required.
- 🖼️ OCR depends on image quality.
- 🔌 Advanced integrations (API, export, etc.) are out of current scope.

---

## License

Kandil Testing Kit is distributed under the [MIT](https://opensource.org/licenses/MIT) license. Feel free to use, modify, and develop the project under the terms of this license.

---

Thank you for supporting open source!
