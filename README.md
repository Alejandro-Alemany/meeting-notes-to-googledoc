# Meeting Notes to Google Doc Converter

A Python script that automatically converts markdown-formatted meeting notes into a beautifully formatted Google Document. Built for Google Colab with complete authentication handling and rich formatting support.

## 🎯 Overview

This tool takes structured markdown meeting notes and converts them into a professional Google Doc with:
- Proper heading hierarchy (H1, H2, H3)
- Nested bullet point lists with correct indentation
- Interactive checkboxes for action items
- Styled @mentions (bold and colored)
- Formatted footer information

## ✨ Features

- **Google Docs API Integration**: Direct creation and formatting of Google Docs
- **Markdown Parsing**: Intelligent parsing of markdown syntax
- **Hierarchical Formatting**: Maintains document structure with proper heading styles
- **Nested Lists**: Preserves bullet point hierarchy with appropriate indentation
- **Interactive Checkboxes**: Converts markdown `- [ ]` into actual Google Docs checkboxes
- **Mention Styling**: @mentions are highlighted in bold blue
- **Footer Formatting**: Meeting metadata styled distinctly in italic gray
- **Error Handling**: Comprehensive error handling with informative messages
- **Colab Authentication**: Seamless authentication in Google Colab environment

## 📋 Requirements

- Python 3.7+
- Google Colab environment (or local Jupyter with modifications)
- Google account with access to Google Docs API
- Required Python packages:
  - `google-api-python-client`
  - `google-auth-httplib2`
  - `google-auth-oauthlib`

## 🚀 Quick Start

### Option 1: Run in Google Colab (Recommended)

1. **Open the notebook in Google Colab**:
   - Upload `meeting_notes_to_googledoc.ipynb` to your Google Drive
   - Open it with Google Colab
   - Or click this link: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/meeting-notes-to-googledoc/blob/main/meeting_notes_to_googledoc.ipynb)

2. **Run the cells in order**:
   - Execute each cell sequentially by pressing `Shift + Enter`
   - Or select `Runtime > Run all` from the menu

3. **Authenticate when prompted**:
   - You'll be asked to authenticate with your Google account
   - Click the authentication link and follow the prompts
   - Grant the necessary permissions

4. **Get your document**:
   - The script will create a new Google Doc
   - A clickable link will be displayed
   - The document will be accessible in your Google Drive

### Option 2: Run Locally (Advanced)

If you want to run this outside of Colab:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/meeting-notes-to-googledoc.git
   cd meeting-notes-to-googledoc
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up Google Cloud credentials**:
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project or select an existing one
   - Enable the Google Docs API
   - Create OAuth 2.0 credentials
   - Download the credentials file as `credentials.json`
   - Place it in the project directory

4. **Modify authentication** (in the notebook):
   Replace the Colab authentication code with:
   ```python
   from google.oauth2 import service_account
   from google_auth_oauthlib.flow import InstalledAppFlow
   
   SCOPES = ['https://www.googleapis.com/auth/documents']
   flow = InstalledAppFlow.from_client_secrets_file('credentials.json', SCOPES)
   creds = flow.run_local_server(port=0)
   ```

5. **Run the notebook**:
   ```bash
   jupyter notebook meeting_notes_to_googledoc.ipynb
   ```

## 📖 Usage

### Basic Usage

The notebook is pre-configured with example meeting notes. Simply run all cells to see it in action.

### Custom Meeting Notes

To convert your own markdown meeting notes:

1. **Prepare your markdown file**:
   - Create a `.md` file with your meeting notes
   - Follow the markdown format (see Format Guide below)

2. **Update the notebook**:
   - Replace the `MEETING_NOTES` variable content with your markdown text
   - Or modify the code to read from a file:
   ```python
   with open('your_notes.md', 'r') as f:
       MEETING_NOTES = f.read()
   ```

3. **Run the conversion**:
   - Execute the final cell to create the Google Doc

### Format Guide

The converter supports the following markdown syntax:

#### Headings
```markdown
# Main Title (H1)
## Section Header (H2)
### Sub-section Header (H3)
```

#### Bullet Points
```markdown
* First level bullet
  * Second level bullet
    * Third level bullet
```

#### Checkboxes (Action Items)
```markdown
- [ ] Task description
- [ ] @person: Task with mention
```

#### Mentions
```markdown
@username will be styled in bold blue
```

#### Footer (after horizontal rule)
```markdown
---
Meeting recorded by: Name
Duration: 45 minutes
```

## 🏗️ Project Structure

```
meeting-notes-to-googledoc/
│
├── meeting_notes_to_googledoc.ipynb  # Main Colab notebook
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── .gitignore                         # Git ignore rules
└── LICENSE                            # License file (optional)
```

## 🔧 How It Works

### Architecture

The converter follows a clear pipeline:

1. **Markdown Parsing** (`MarkdownParser` class):
   - Reads markdown text line by line
   - Identifies element types (headings, bullets, checkboxes, etc.)
   - Extracts metadata (indent levels, mentions)
   - Returns structured data

2. **Document Creation** (`GoogleDocsFormatter` class):
   - Creates a new Google Doc via API
   - Converts parsed elements into Google Docs API requests
   - Handles text insertion and formatting
   - Applies styles (headings, bullets, colors, fonts)

3. **Formatting Application**:
   - Batches all formatting requests
   - Applies them to the document in one API call
   - Returns the document URL

### Key Components

- **MarkdownParser**: Parses markdown into structured elements
- **GoogleDocsFormatter**: Converts elements to Google Docs API requests
- **convert_markdown_to_google_doc()**: Main orchestration function

## 🎨 Formatting Details

| Element | Google Docs Style |
|---------|------------------|
| `# Heading` | Heading 1 (built-in style) |
| `## Heading` | Heading 2 (built-in style) |
| `### Heading` | Heading 3 (built-in style) |
| `* Bullet` | Disc/Circle/Square bullets |
| `- [ ] Checkbox` | Interactive checkbox bullets |
| `@mention` | Bold, blue (#0066CC) |
| Footer text | Italic, gray (#666666) |

## 🚨 Troubleshooting

### Authentication Issues

**Problem**: Authentication fails or credentials are rejected

**Solution**:
- Ensure you're running in Google Colab
- Re-run the authentication cell
- Clear browser cookies and try again
- Check that Google Docs API is enabled in your Google Cloud project

### API Errors

**Problem**: HTTP errors when creating/formatting document

**Solution**:
- Verify your Google account has access to Google Docs
- Check your internet connection
- Ensure you've granted all required permissions
- Try reducing the size of your markdown file

### Formatting Issues

**Problem**: Document formatting doesn't look right

**Solution**:
- Check your markdown syntax
- Ensure proper indentation (2 spaces per level)
- Verify checkbox syntax: `- [ ]` (spaces between brackets)
- Make sure mentions start with `@` without spaces

## 📝 Example Output

Given this markdown:
```markdown
# Product Team Sync

## Attendees
- Sarah Chen
- Mike Johnson

## Action Items
- [ ] @sarah: Review the proposal
```

Creates a Google Doc with:
- "Product Team Sync" as Heading 1
- "Attendees" as Heading 2
- Bulleted list with names
- "Action Items" as Heading 2
- Interactive checkbox with **@sarah** in bold blue

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👤 Author

Created as part of a software engineering assessment.

## 🙏 Acknowledgments

- Google Docs API Documentation
- Google Colab for providing an excellent development environment
- The markdown specification for formatting guidelines

## 📞 Support

If you encounter any issues or have questions:
1. Check the [Troubleshooting](#-troubleshooting) section
2. Review the [Google Docs API documentation](https://developers.google.com/docs/api)
3. Open an issue on GitHub

---

**Note**: This tool requires a Google account and internet connection. All documents are created in your Google Drive.

