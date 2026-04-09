# ArchiMate Editor - User Guide

Web-based editor for creating and managing architectural models according to the ArchiMate 3.2 standard with extensions for Architecture Decision Records (ADR), notes, and tasks management.

## Online Version and Download

- **Online version:** https://egdilna.github.io/nastroje/archimate
- **GitHub:** https://github.com/egdilna/nastroje

On GitHub you will find:
- Editor for download as a single HTML file
- DokuWiki plugin for wiki system integration
- Application documentation in Czech and English
- JSON Schema for AJX format validation (`ajx-schema.json`)

---

## Table of Contents

1. [Introduction](#introduction)
2. [AJX Format](#ajx-format)
3. [Editor Interface](#editor-interface)
4. [Model Management](#model-management)
5. [Working with Elements](#working-with-elements)
6. [Working with Relationships](#working-with-relationships)
7. [Diagrams](#diagrams)
8. [Tasks](#tasks)
9. [Notes](#notes)
10. [Architecture Decision Records (ADR)](#architecture-decision-records-adr)
11. [Text Generator](#text-generator)
12. [Import and Export](#import-and-export)
13. [Model Merging](#model-merging)
14. [Bulk Tag Operations](#bulk-tag-operations)
15. [GitHub Integration](#github-integration)
16. [DokuWiki Plugin](#dokuwiki-plugin)
17. [Tips and Tricks](#tips-and-tricks)
18. [Keyboard Shortcuts](#keyboard-shortcuts)
19. [ArchiMate Reference Guide](#archimate-reference-guide)

---

## Introduction

ArchiMate Editor is a complete tool for enterprise architecture modeling according to the ArchiMate 3.2 specification by The Open Group. The editor runs directly in the browser without installation and stores data locally in the browser.

### Main Features

- **ArchiMate 3.2** - support for all 60 element types and 11 relationship types with validity checking
- **Multilingual interface** - Czech and English
- **Auto-save** - data is saved to the browser
- **Import/export** - AJX (JSON) and ArchiMate Open Exchange XML formats
- **Model merging** - import selected parts from another model
- **Tasks** - tracking and management of architecture development tasks
- **Notes** - Markdown notes with versioning
- **ADR (Architecture Decision Records)** - architecture decision management
- **Text generator** - documentation creation from model using templates
- **Diagrams** - visual editor with drag & drop and SVG/PNG export
- **Bulk operations** - working with tags
- **Accessibility** - fully accessible interface for screen readers
- **DokuWiki integration** - plugin for team collaboration

---

## AJX Format

**AJX (ArchiMate JSON eXchange)** is a standard format for ArchiMate model exchange based on JSON. Files have the `.ajx` extension.

### AJX File Structure

```json
{
  "exportDate": "2025-01-15T10:30:00.000Z",
  "archimateVersion": "3.2",
  "model": {
    "id": "id-model-001",
    "name": "Model Name",
    "version": "1.0",
    "documentation": "Model description",
    "dublinCore": { ... },
    "properties": []
  },
  "elements": [...],
  "relationships": [...],
  "diagrams": [...],
  "adr": [...],
  "notes": [...],
  "tasks": [...]
}
```

### AJX Format Extensions

The editor uses the standard AJX format for ArchiMate models and adds three extensions:

- **adr** - Architecture Decision Records
- **notes** - Notes with Markdown support and versioning
- **tasks** - Tasks for architecture development management

Detailed specification of all fields is in the `ajx-schema.json` file (JSON Schema).

### AJX Format Benefits

- Human and machine readable
- Easy to version in Git
- Simple integration with other tools
- Validatable using JSON Schema
- More compact than XML

---

## Editor Interface

### Header

In the header you will find:
- **Model name** - click to go to the Model tab
- **Model version** - displays the current version
- **Statistics** - number of elements, relationships, diagrams, and layers
- **Language switcher** - CZ/EN

### Tabs

The editor is divided into nine main tabs:

1. **Model** - metadata and model settings
2. **Elements** - architectural elements management
3. **Relationships** - relationship management between elements
4. **Diagrams** - view creation and management
5. **Tasks** - task tracking and management
6. **Notes** - text notes with Markdown
7. **ADR** - architecture decisions
8. **Tools** - text generator and bulk operations
9. **Export/Import** - data exchange with other systems
10. **Reference** - ArchiMate specification overview

---

## Model Management

### Basic Information

- **Model ID** - unique identifier (auto-generated)
- **Model name** - displayed in the header
- **Version** - model versioning
- **Documentation** - detailed model description (supports Markdown)

### Dublin Core Metadata

Standardized metadata according to ISO 15836:

| Field | Description |
|-------|-------------|
| Creator | Author or responsible person |
| Publisher | Organization responsible for publication |
| Date | Creation or publication date |
| Language | Content language (cs, en, de...) |
| Rights | License information |
| Subject | Topic or keywords |
| Description | Brief content description |

### Custom Properties

You can add any number of custom properties in key-value format. Use the **Add Property** button and fill in the name and value.

---

## Working with Elements

### Creating a New Element

1. Select **layer** (Strategy, Business, Application...)
2. Select **element type** - the list is filtered by layer
3. Fill in the element **name**
4. Optionally add:
   - **Stereotype** - type extension (e.g., "microservice")
   - **Defines** - reference to law, standard, or governing document
   - **Tags** - comma-separated tags for categorization
   - **Description** - detailed documentation (supports Markdown)
5. Click **Save Element**

### Automatic ID Generation

Element ID is automatically generated from type and name:
- `BusinessProcess` + "Order Processing" → `bp-order-processing`

### Element Operations

| Icon | Action | Description |
|------|--------|-------------|
| ✏️ | Edit | Opens element for editing |
| 📋 | Duplicate | Creates a copy with new ID |
| 🗑️ | Delete | Deletes element and its relationships |

### Filtering Elements

Above the table are filters:
- **Layer** - filter by layer
- **Type** - filter by element type
- **Stereotype** - filter by stereotype
- **Tags** - filter by tags (including "no tags")
- **Diagram** - filter by diagram membership
- **Search** - full-text search

The **Clear Filters** button clears all filters.

### Sorting and Columns

- **Sorting** - click on column header
- **Column hiding** - "Columns" button to select visible columns

---

## Working with Relationships

### Cascading Selection

The relationship form uses intelligent cascading selection:

1. **Source layer** → filters source element types
2. **Source type** → filters specific source elements
3. **Source element** → select specific element
4. **Target layer** → filters target element types
5. **Target type** → filters specific target elements
6. **Target element** → select specific element
7. **Relationship type** → shows only allowed types per specification

### Relationship Validity Check

The editor automatically checks if the relationship is allowed according to ArchiMate 3.2. Invalid combinations are not in the menu.

### Statement Preview

After selecting source, target, and relationship type, a preview is displayed as a sentence:
> "Source element **serves** Target element"

### Filtering Relationships

- **Source element** - filter by source
- **Target element** - filter by target
- **Relationship type** - filter by type
- **Tags** - filter by tags
- **Diagram** - filter by diagram membership
- **Search** - full-text search

### Quick Filter from Elements Table

In the elements table, you can click on the relationship count to go to a filtered list of relationships for that element.

---

## Diagrams

Diagrams (views) allow organizing elements into logical groups and visualizing their relationships.

### Creating a Diagram

1. Enter **diagram name**
2. Optionally add **description**
3. Click **Create Diagram**

### Diagram Editor

After clicking **Open**, the editor displays three sub-tabs:

#### Diagram Elements

- Adding elements using cascading selection (layer → type → element)
- List of elements in the diagram with removal option
- Elements can be added or removed

#### Diagram Relationships

- Automatically displays relationships between elements in the diagram
- Read-only - relationships are managed in the Relationships tab

#### Preview

Visual diagram preview:
- Elements are displayed as rectangles colored by layer
- Relationships are displayed as lines with appropriate markers
- Automatic layout by layers (layered) or grid

### Visual Diagram Editor

The editor includes an advanced visual editor for interactive diagram editing.

#### Opening the Visual Editor

- In the diagrams table, click the **✏️ Visually** button
- In the diagram preview, click **✏️ Edit Visually**

#### Visual Editor Interface

The editor opens in a fullscreen modal window with these parts:

- **Left panel (Palette)** - list of available elements grouped by layer
- **Center (Canvas)** - workspace with grid for editing
- **Right panel (Properties)** - properties of selected element or relationship

#### Working with Elements

- **Adding element** - drag element from palette to canvas or double-click
- **Moving** - click and drag element to new position
- **Resizing** - use corner handles of selected element
- **Removing** - select element and click "Remove from diagram" in properties panel

#### Working with Relationships

- Relationships are automatically created between elements that have a relationship in the model
- **Hiding relationship** - in the properties panel you can hide a relationship
- Relationships are redrawn automatically when elements are moved

#### Canvas Controls

- **Zoom** - +/- buttons in toolbar or mouse wheel
- **Zoom 1:1** - resets zoom to 100%
- **Fit Content** - adjusts zoom to show entire diagram
- **Panning** - middle mouse button or drag on empty canvas

#### Saving

- Click **Save** to save element positions and styles
- Element positions and sizes are saved to the diagram

### Diagram Export

In the diagram preview, export buttons are available:

| Button | Description |
|--------|-------------|
| **Download SVG** | Export diagram as vector SVG file |
| **Download PNG** | Export diagram as raster PNG image (2x resolution) |

---

## Tasks

Tasks are used for tracking and managing architecture work.

### Creating a Task

1. Enter task **name**
2. Select **priority** (Low, Medium, High, Critical)
3. Enter **assignee** and **reporter**
4. Set **due date**
5. Add **description** (supports Markdown)
6. Optionally link to model **elements** or **relationships**

### Task States

| State | Icon | Description |
|-------|------|-------------|
| New | ⚪ | Newly created task |
| Open | 🔵 | Task is in progress |
| On Hold | ⏸️ | Task is on hold |
| Done | 🟢 | Task is completed |
| Cancelled | 🔴 | Task was cancelled |

### Current State

You can add notes about current state to each task (supports Markdown).

---

## Notes

Notes are used for recording information related to architecture.

### Creating a Note

1. Enter note **title**
2. Enter **author**
3. Write **content** (supports Markdown)
4. Optionally add **tags** and link to elements/relationships

### Versioning

Notes have automatic versioning:
- Each change creates a new version
- Version history is available in note detail
- Previous versions can be viewed and restored

---

## Architecture Decision Records (ADR)

ADR (Architecture Decision Records) document important architecture decisions.

### ADR Structure

- **Number** - automatically generated sequence number
- **Title** - brief decision description
- **Status** - current decision state
- **Author** and **Approver**
- **Context** - situation leading to decision
- **Decision** - what was decided
- **Consequences** - decision impacts

### ADR States

| State | Icon | Description |
|-------|------|-------------|
| Draft | ⚪ | Decision in draft |
| Discussed | 💬 | Under discussion |
| Approved | 🟢 | Approved decision |
| Rejected | 🔴 | Rejected decision |
| Updated | 🔄 | Decision was updated |
| Implemented | 🟣 | Decision is implemented |
| Tracked | 👁️ | Decision is being tracked |
| Deprecated | 🟠 | Decision is deprecated |
| Superseded | ⚫ | Superseded by another ADR |
| Closed | 🔒 | Closed decision |

### Alternatives and Selection

- Add alternatives with title and description
- Select the chosen alternative from dropdown
- Describe the reason for selection

### Status History

Every status change is automatically recorded including date and author.

### ADR Export

- **📄 Save as Markdown** - downloads individual ADR
- **📋 Copy Markdown** - copies to clipboard
- **📦 Export All ADR** - downloads all ADR as one file

---

## Text Generator

The generator creates text outputs from the model using templates with placeholders.

### Data Sources

The generator can create text from:
- **Elements** - current elements list (respects filters)
- **Relationships** - current relationships list (respects filters)
- **Tasks** - all tasks
- **Notes** - all notes
- **ADR** - all architecture decision records

### Templates

Enter a template with placeholders in curly brackets:
```
{Name} is a {Type} in the {Layer} layer.
```

### Available Placeholders

#### For Elements
- `{ID}`, `{Název}`, `{Typ}`, `{Vrstva}`
- `{Stereotyp}`, `{Určuje}`, `{Příznaky}`, `{Popis}`

#### For Relationships
- `{ID}`, `{Typ}`, `{Název}`, `{Popis}`, `{Příznaky}`, `{Statement}`
- Source: `{Zdroj}`, `{ZdrojID}`, `{ZdrojVrstva}`, `{ZdrojTyp}`, `{ZdrojStereotyp}`, `{ZdrojUrčuje}`, `{ZdrojPříznaky}`, `{ZdrojPopis}`
- Target: `{Cíl}`, `{CílID}`, `{CílVrstva}`, `{CílTyp}`, `{CílStereotyp}`, `{CílUrčuje}`, `{CílPříznaky}`, `{CílPopis}`

#### For Tasks
- `{ID}`, `{Číslo}`, `{Název}`, `{Stav}`, `{Priorita}`
- `{Řešitel}`, `{Zadavatel}`, `{Termín}`, `{Příznaky}`
- `{Popis}`, `{AktuálníStav}`, `{Vytvořeno}`, `{Aktualizováno}`

#### For Notes
- `{ID}`, `{Název}`, `{Autor}`, `{Příznaky}`
- `{Obsah}`, `{Vytvořeno}`, `{Aktualizováno}`, `{PočetVerzí}`

#### For ADR
- `{ID}`, `{Číslo}`, `{Název}`, `{Stav}`
- `{Autor}`, `{Schvalovatel}`, `{Datum}`, `{Příznaky}`
- `{Kontext}`, `{Rozhodnutí}`, `{Důsledky}`
- `{PočetAlternativ}`, `{VybranáAlternativa}`

### Options

- **Skip empty** - omits items where placeholder would be empty

---

## Import and Export

### Export

| Format | Description |
|--------|-------------|
| **Export AJX** | Download model in AJX (JSON) format |
| **Copy AJX** | Copies AJX data to clipboard |
| **Export XML** | ArchiMate Open Exchange format (including visual data) |
| **Export CSV** | Elements and relationships as CSV files |

### XML Export with Visual Data

When exporting to ArchiMate Open Exchange XML, visual information from diagrams is also saved:
- Element positions (x, y)
- Element sizes (width, height)
- Fill and border colors
- Relationship bendpoints

This information is compatible with Archi tool and other tools supporting ArchiMate Open Exchange format.

### Import

Supported formats:
- **AJX** - ArchiMate JSON eXchange (.ajx)
- **XML** - ArchiMate Open Exchange (.xml)

When importing XML, visual diagram data is also loaded if present in the file.

#### Import Options

1. **From file** - "Select File" button
2. **By pasting** - paste data into text field
3. **From clipboard** - "Paste from Clipboard" button
4. **Drag & Drop** - drag file onto the page

---

## Model Merging

Merging allows importing selected parts from another model.

### Merge Strategies

| Strategy | Description |
|----------|-------------|
| Keep existing | On ID conflict, keeps original |
| Overwrite with new | On ID conflict, replaces with new |
| Manual selection | Allows selecting specific items |

### Manual Selection

When choosing "Manual selection":
1. Load the file to merge
2. Switch between **Elements**, **Relationships**, and **Diagrams** tabs
3. Check items to import
4. Click **Merge Models**

### Imported Items Marking

Imported items automatically get the tag `Import from: [source model name]`.

---

## Bulk Tag Operations

### Available Operations

| Operation | Description |
|-----------|-------------|
| Add tag | Adds tag to all selected items |
| Remove tag | Removes tag from selected items |
| Replace tag | Replaces one tag with another |

### Item Selection

- Check items for operation
- **Select All** / **Deselect All**
- **Select Currently Filtered** - selects items matching active filters

---

## GitHub Integration

The editor allows saving and loading models directly from a GitHub repository. Each save creates a commit with history.

### Setup

1. Create a **Personal Access Token** at https://github.com/settings/tokens?type=beta
   - Select the repository where you want to save
   - Permissions: Contents → Read and write
2. In the **Export/Import** tab, find the **GitHub Integration** section
3. Paste the token and click **Save token**
4. Enter the file path in format `owner/repo/path/file.ajx`

### Usage

| Button | Description |
|--------|-------------|
| **📥 Load from GitHub** | Loads model from the specified path |
| **📤 Save to GitHub** | Saves model to the specified path (creates commit) |
| **🔗 Copy link** | Copies direct link to the model |

### Direct Links

The file path is encoded in the URL parameter `?gh=...`, so you can share a direct link to a specific model. When opening the link, the model is automatically loaded from GitHub.

### Security

- Token is stored only in browser localStorage
- Token is never saved to the data file or URL
- For public repositories, token is only needed for writing
- For private repositories, token is needed for reading too

---

## DokuWiki Plugin

The editor can be integrated with DokuWiki using the included plugin.

### Installation

1. Extract `archimateeditor.zip` to `lib/plugins/`
2. Plugin activates automatically

### Usage

Insert into wiki page:
```
<archimate instance="instance-name">
</archimate>
```

### Features

- Editor opens in popup window
- **Save to Wiki** button saves directly to wiki page
- Data is transferred via postMessage API
- Support for multiple instances on one page

---

## Tips and Tricks

### Auto-save

Model is automatically saved to browser after each change.

### Suggestions

- **Stereotypes** - offers previously used stereotypes
- **Tags** - offers existing tags from entire model (including ADR, notes, and tasks)
- **Relationship names** - offers previously used names

### Linking Items

Tasks, notes, and ADR can be linked to model elements and relationships. Linked items are clickable in previews.

### Shared Tags

Tags are shared between elements, relationships, tasks, notes, and ADR. This enables easy linking of related items.

### Markdown Support

Markdown is supported in:
- Model documentation
- Element and relationship descriptions
- ADR (context, decision, consequences, alternatives)
- Notes
- Task description and state

### Backup

Regularly export the model to an AJX file. Browser data may be deleted when clearing history.

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Tab | Move between form fields |
| Enter | Confirm form |
| Escape | Close modal window |
| Ctrl+S | Save to Wiki (in DokuWiki mode) |

---

## ArchiMate Reference Guide

### Layers

| Layer | Color | Description |
|-------|-------|-------------|
| Strategy | Brown | Strategic elements - resources, capabilities |
| Business | Gold | Business elements - actors, processes, services |
| Application | Blue | Application elements - components, services, data |
| Technology | Green | Technology elements - nodes, devices |
| Physical | Dark Green | Physical elements - equipment, facilities |
| Implementation | Purple | Implementation elements - packages, deliverables |
| Motivation | Red | Motivation elements - stakeholders, goals |
| Composite | Gray | Composite elements - locations, groupings |

### Relationship Types

| Type | Category | Description |
|------|----------|-------------|
| Composition | Structural | Element consists of other elements |
| Aggregation | Structural | Element groups other elements |
| Assignment | Structural | Assignment of active element to behavior |
| Realization | Structural | Element realizes another element |
| Serving | Dependency | Element provides functionality |
| Access | Dependency | Element accesses data |
| Influence | Dependency | Element influences another element |
| Triggering | Dynamic | Element triggers another element |
| Flow | Dynamic | Information or material flow |
| Specialization | Other | Element is specialization of another |
| Association | Other | Unspecified relationship |

---

## Support

The editor is an open-source tool available on GitHub.

- **Online version:** https://egdilna.github.io/nastroje/archimate
- **GitHub repository:** https://github.com/egdilna/nastroje
- **Bug reports:** https://github.com/egdilna/nastroje/issues

### System Requirements

- Modern web browser (Chrome, Firefox, Safari, Edge)
- JavaScript must be enabled
- localStorage required for saving

### Known Limitations

- Data is stored locally in the browser
- Model may be deleted when clearing browser data
- Regular backup exports recommended

---

*Documentation version: 3.0*
*ArchiMate® is a registered trademark of The Open Group.*
