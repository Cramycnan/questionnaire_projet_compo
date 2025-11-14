# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-page HTML application providing a comprehensive client questionnaire for music composers working on film, TV, video games, and other media projects. The form is in French and helps composers gather all essential information before starting a composition project.

**Tech Stack**: Pure HTML with embedded CSS and vanilla JavaScript - no build tools, frameworks, or dependencies.

## Development

### Running the Application

Simply open the HTML file in any modern web browser:
```bash
# Using default browser
xdg-open "composer-client-checklist (1).html"

# Or with a specific browser
firefox "composer-client-checklist (1).html"
google-chrome "composer-client-checklist (1).html"
```

Alternatively, serve it with a local HTTP server:
```bash
python3 -m http.server 8000
# Then navigate to http://localhost:8000
```

### Development Workflow

This is a self-contained single-file application. All modifications are made directly to the HTML file - no compilation or build process required. Simply edit and refresh the browser to see changes.

### Testing Changes

After editing, open the file in a browser and manually test:
- Form input and validation
- Auto-save functionality (check browser console for localStorage)
- Progress calculation (46 total fields)
- Export to text file
- Import/Export JSON backup
- Form reset functionality
- Keyboard shortcuts (Ctrl+S to save, Ctrl+E to export)

## Architecture

### Single-File Structure

The HTML file contains three main sections:
1. **`<style>` block (lines 7-336)**: All CSS including responsive design and print styles
2. **`<body>` block (lines 338-657)**: HTML structure with 8 major sections of questions
3. **`<script>` block (lines 659-901)**: All JavaScript logic

### Key Features

**Data Persistence**: Uses `localStorage` with key `'composerClientData'` to auto-save form data. Data is saved on every input change.

**Progress Tracking**: Calculates completion percentage based on 46 total fields (4 project info fields + 42 question fields). Updates in real-time via the fixed progress indicator.

**Export/Import**:
- Text export: Creates a formatted `.txt` file with all filled responses
- JSON backup: Uses `window.exportJSON()` function (accessible via browser console) to create a structured backup
- JSON import: Restores data from previously exported JSON files

**Form Sections** (8 major areas):
1. Informations générales (General project info)
2. Aspects financiers (Budget and payment) - marked as "important"
3. Besoins musicaux (Musical requirements)
4. Planning et deadlines (Timeline)
5. Aspects techniques (Technical specifications)
6. Droits et aspects juridiques (Rights and legal) - marked as "important"
7. Modalités de collaboration (Collaboration workflow)
8. Éléments complémentaires (Additional elements)

### JavaScript Functions

- `updateProgress()`: Recalculates completion percentage and updates UI
- `autoSave()`: Saves all form data to localStorage and shows notification
- `saveManually()`: Triggers autoSave with user confirmation
- `restoreData()`: Loads saved data from localStorage on page load
- `exportData()`: Exports form data to a formatted text file
- `importData()`: Imports data from a JSON file
- `resetForm()`: Clears all fields and localStorage
- `window.exportJSON()`: Console-accessible function for JSON backup export

## File Naming

Note: The current filename includes "(1)" which suggests it may be a downloaded copy. Consider renaming to `composer-client-checklist.html` or `index.html` for cleaner deployment.

## Localization

The application is entirely in French. All UI text, labels, and export formats use French language and formatting conventions (e.g., date format, currency references).
