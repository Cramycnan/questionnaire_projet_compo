# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-page HTML application providing a comprehensive client questionnaire for music composers working on film, TV, video games, and other media projects. The form is in French and helps composers gather all essential information before starting a composition project.

**Tech Stack**: Pure HTML with embedded CSS and vanilla JavaScript - no build tools, frameworks, or dependencies.
**External Library**: XLSX.js (v0.18.5) loaded via CDN for Excel export functionality.

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
- Auto-save functionality with debouncing (500ms delay)
- Progress calculation (dynamic based on mode)
- Mode toggle (Essential vs Complete)
- Export to Excel (9 tabs)
- Export to text file
- Import/Export JSON backup
- Form reset functionality
- Keyboard shortcuts (Ctrl+S to save, Ctrl+E to export)
- Priority badges display
- Quick notes visibility
- Error handling (QuotaExceeded, SecurityError)

## Architecture

### Single-File Structure

The HTML file contains three main sections:
1. **`<style>` block (lines 10-535)**: All CSS including:
   - Base styles and responsive design
   - Mode toggle button styles
   - Priority badges and UX improvements
   - Essential mode styles
   - Print styles

2. **`<body>` block (lines 537-853)**: HTML structure with:
   - Mode toggle button (fixed top-left)
   - Save status notification (fixed top-right)
   - 8 major sections of questions
   - Priority badges on 8 essential fields
   - Quick notes on 3 critical fields
   - Dynamic music pieces section
   - Progress indicator (fixed bottom-right)

3. **`<script>` block (lines 854-1893)**: All JavaScript logic including:
   - Music pieces management (dynamic add/remove)
   - Mode toggle (Essential/Complete)
   - Progress calculation (mode-aware)
   - Auto-save with debouncing (500ms)
   - Error handling for localStorage
   - Excel export with 9 tabs
   - Text export
   - JSON import/export
   - Keyboard shortcuts

## Key Features

### 1. Data Persistence
Uses `localStorage` with key `'composerClientData'` to auto-save form data. Data is saved with **500ms debouncing** to optimize performance.

**Error Handling**:
- `QuotaExceededError`: Displays warning to export data
- `SecurityError`: Notifies user (private browsing)
- Generic errors: Safe fallback with notification
- Size monitoring: Warning at 3MB threshold

### 2. Progress Tracking
Calculates completion percentage **dynamically based on current mode**:
- **Essential Mode**: Counts only priority fields (8 essential + music pieces + project info)
- **Complete Mode**: Counts all fields
- Updates in real-time via the fixed progress indicator

### 3. Mode Toggle (Essential/Complete)
**Button**: Fixed top-left, toggles between two modes
- **Essential Mode** (🎯): Shows only priority fields, hides secondary sections
- **Complete Mode** (📋): Shows all fields

**Visual feedback**:
- Button changes color and text
- Progress indicator adapts (shows "X/Y essentiels" in Essential mode)
- Secondary sections become semi-transparent and disabled in Essential mode

### 4. Priority System
**8 Essential Fields** marked with red badge "ESSENTIEL":
1. Type de projet (project type)
2. Durée totale (project duration)
3. Synopsis
4. Budget total musique (music budget)
5. Date de livraison finale (deadline)
6. Dépôt SACEM (SACEM registration)
7. Cession de droits (rights transfer)

**Visual markers**:
- Red badge "ESSENTIEL" on top-right of field
- Subtle red border on field container
- Enhanced red border on focus

### 5. Export Capabilities

#### Excel Export (NEW)
Creates a professional `.xlsx` file with **9 themed tabs**:
1. **📊 Dashboard**: Overview with key info and progress
2. **📋 Projet**: General project information
3. **💰 Budget & Planning**: Financial and timeline details
4. **🎼 Morceaux**: Music pieces table (8 columns)
5. **🎵 Besoins Musicaux**: Global musical requirements
6. **⚖️ Droits**: Legal aspects
7. **🎧 Technique**: Technical specifications
8. **🤝 Collaboration**: Workflow and communication
9. **➕ Compléments**: Additional information

**Dashboard includes**:
- Client and project info
- 6 essential fields with status (filled or ⚠️ NON RENSEIGNÉ)
- Progress indicator (X/6 essential fields)

#### Text Export
Creates a formatted `.txt` file with all filled responses, organized by sections.

#### JSON Import/Export
- **Export**: Via browser console with `window.exportJSON()`
- **Import**: Via file picker (📥 Importer button)
- **Format**: Backward compatible with previous versions

### 6. Form Sections

**Main Sections** (with secondary designation where applicable):
1. **Informations générales** - Project type, duration, synopsis (3 priority fields)
2. **Aspects financiers** (important section) - Budget, payment (1 priority field)
3. **Besoins musicaux** - Global music needs + dynamic pieces section
4. **Planning et deadlines** - Timeline, milestones (1 priority field)
5. **Aspects techniques** (secondary section) - Formats, mixing, sync
6. **Droits et aspects juridiques** (important section) - SACEM, rights (2 priority fields)
7. **Modalités de collaboration** (secondary section) - Validation, communication
8. **Éléments complémentaires** (secondary section) - Temp track, constraints, billing

### 7. Dynamic Music Pieces System
- **Add pieces**: Button "➕ Ajouter un morceau"
- **Collapsible**: Click header to expand/collapse each piece
- **Removable**: Delete button on each piece (except first one created)
- **10 fields per piece**: Title, duration, type, genre, instrumentation, mood, constraints, variations, references, notes
- **Auto-save**: Each piece is included in localStorage and exports

### 8. UX Improvements
- **Larger input fields**: 1.05em font, 12-15px padding, 70px min-height
- **Better spacing**: 30px between sections
- **Quick notes**: Yellow background on 3 critical fields (budget, deadline, SACEM)
- **Enhanced focus**: Elevation effect (translateY -2px) with colored shadow
- **Auto-resize textareas**: Expand as user types
- **Notification system**: Success (green), Warning (orange), Error (red)

## JavaScript Functions

### Core Functions
- `updateProgress()`: Recalculates completion percentage (mode-aware) and updates UI
- `toggleSimpleMode()`: Switches between Essential and Complete modes
- `showNotification(message, type)`: Displays notifications with auto-hide

### Save/Load Functions
- `debouncedAutoSave()`: Queues save with 500ms debouncing
- `autoSave()`: Saves all form data to localStorage with error handling
- `saveManually()`: Triggers autoSave with user confirmation
- `restoreData()`: Loads saved data from localStorage with error handling

### Music Pieces Functions
- `createMusicPieceHTML(id, data)`: Generates HTML for a music piece
- `addMusicPiece(data)`: Adds new music piece to DOM
- `removeMusicPiece(id)`: Removes music piece from DOM
- `toggleMusicPiece(id)`: Collapses/expands music piece
- `updateMusicPieceTitle(id, title)`: Updates title in piece header
- `getMusicPiecesData()`: Collects all music pieces data

### Export Functions
- `exportData()`: Exports form data to formatted text file
- `exportExcel()`: Creates Excel file with 9 tabs
- `getFieldValue(fieldName)`: Helper to retrieve field values
- `importData()`: Imports data from JSON file
- `resetForm()`: Clears all fields and localStorage

### Utility Functions
- `autoResize(textarea)`: Auto-adjusts textarea height to content

### Global Variables
- `musicPieceCounter`: Counter for unique piece IDs
- `isSimpleMode`: Boolean flag for current mode state
- `saveTimeout`: Timeout ID for debouncing

### Window Functions (Console Access)
- `window.exportJSON()`: Exports complete data as JSON file (accessible via browser console)
- `window.printForm()`: Triggers browser print dialog

## File Naming

Note: The current filename includes "(1)" which suggests it may be a downloaded copy. Consider renaming to `composer-client-checklist.html` or `index.html` for cleaner deployment.

## Localization

The application is entirely in French. All UI text, labels, and export formats use French language and formatting conventions (e.g., date format, currency references).

## Data Structure

### localStorage Format
```json
{
  "clientName": "string",
  "projectName": "string",
  "contactDate": "YYYY-MM-DD",
  "contactPerson": "string",
  "fields": {
    "project-type": "string",
    "project-duration": "string",
    // ... all other fields as data-field attributes
    "musicPieces": [
      {
        "id": "piece_timestamp_counter",
        "title": "string",
        "duration": "string",
        "type": "diegetic|extra-diegetic|mixed",
        "genre": "string",
        "instrumentation": "string",
        "mood": "string",
        "constraints": "string",
        "variations": "string",
        "references": "string",
        "notes": "string"
      }
    ]
  }
}
```

### Backward Compatibility
The data structure is **fully backward compatible**. Old JSON files without `musicPieces` array or priority fields will import correctly with graceful degradation.

## Styling Guidelines

### Color Palette
- **Primary**: `#667eea` (purple-blue gradient base)
- **Secondary**: `#764ba2` (purple gradient end)
- **Success**: `#48bb78` (green)
- **Warning**: `#ed8936` (orange)
- **Error**: `#e53e3e` (red)
- **Important sections**: `#fff5f5` (light red background)
- **Priority badge**: `#e53e3e` (red)
- **Quick notes**: `#fff3cd` (yellow background)

### Responsive Breakpoints
- Mobile: `max-width: 768px`
- Desktop: Default layout

### Fixed UI Elements
- **Mode toggle**: Top-left, z-index 1001
- **Save status**: Top-right, z-index 1001
- **Progress indicator**: Bottom-right, z-index 1000

## Browser Compatibility

**Tested on**:
- Chrome/Edge (modern)
- Firefox (modern)
- Safari (modern)

**Requirements**:
- localStorage support
- ES6+ JavaScript support
- CSS Grid and Flexbox support
- Blob and File APIs for exports

## Performance Considerations

1. **Debouncing**: Save operations are debounced by 500ms to avoid excessive localStorage writes
2. **Size monitoring**: Warns when localStorage data exceeds 3MB
3. **Lazy evaluation**: Progress calculation only runs when fields change
4. **Efficient DOM queries**: Uses specific selectors to minimize DOM traversal

## Security Considerations

1. **No server communication**: All data stays in browser
2. **Private browsing**: Gracefully handles localStorage restrictions
3. **XSS prevention**: No `innerHTML` usage with user data (only template literals)
4. **No external dependencies**: Except XLSX.js from trusted CDN with integrity hash

## Known Limitations

1. **localStorage size**: Browser-dependent (typically 5-10MB)
2. **Private browsing**: Auto-save disabled
3. **No cloud sync**: Data is device-specific
4. **Excel styles**: Basic Excel export without complex formatting
5. **Print layout**: Optimized but may need adjustment for specific printers

## Future Enhancement Ideas

If expanding this project, consider:
- PDF export with custom styling
- Cloud backup option
- Multi-language support
- Templates for different project types
- Client portal for reviewing questionnaires
- Integration with project management tools
- Advanced Excel styling with conditional formatting
