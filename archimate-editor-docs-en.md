# ArchiMate Editor - User Guide

A web-based editor for creating and managing architectural models according to the ArchiMate 3.2 standard.

## Online Version and Download

- **Online version:** https://mrt.site44.com/archimate-editor.html
- **GitHub:** https://github.com/michalradacz/archimate-editor

On GitHub you will find:
- Editor available for download as a single HTML file
- Application documentation
- JSON Schema for AJX format validation

## Table of Contents

1. [Introduction](#introduction)
2. [AJX Format](#ajx-format)
3. [Editor Interface](#editor-interface)
4. [Model Management](#model-management)
5. [Working with Elements](#working-with-elements)
6. [Working with Relationships](#working-with-relationships)
7. [Diagrams](#diagrams)
8. [Text Generator](#text-generator)
9. [Import and Export](#import-and-export)
10. [Merging Models](#merging-models)
11. [Bulk Tag Operations](#bulk-tag-operations)
12. [Tips and Tricks](#tips-and-tricks)
13. [Keyboard Shortcuts](#keyboard-shortcuts)
14. [ArchiMate Reference](#archimate-reference)

---

## Introduction

ArchiMate Editor is a complete tool for enterprise architecture modeling according to The Open Group's ArchiMate 3.2 specification. The editor runs directly in the browser without installation and stores data locally in the browser.

### Key Features

- Support for all 60 ArchiMate 3.2 element types
- All 11 relationship types with validity checking per specification
- Multilingual interface (Czech, English)
- Automatic saving to browser storage
- Import/export in AJX and ArchiMate Open Exchange XML formats
- Model merging with manual selection option
- Text description generator from model
- Bulk tag operations
- Visual diagram preview with SVG export
- Fully accessible interface for screen readers

---

## AJX Format

**AJX (ArchiMate JSON eXchange)** is a standard format for exchanging ArchiMate models based on JSON. Files use the `.ajx` extension.

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
    "dublinCore": {
      "creator": "Author",
      "publisher": "Publisher",
      "date": "2025-01-15",
      "language": "en",
      "rights": "License",
      "subject": "Subject",
      "description": "Description"
    },
    "properties": []
  },
  "elements": [...],
  "relationships": [...],
  "diagrams": [...]
}
```

### Benefits of AJX Format

- Human and machine readable
- Easy to version control with Git
- Simple integration with other tools
- Validatable using JSON Schema
- More compact than XML

---

## Editor Interface

### Header

The header contains:
- **Model name** - click to navigate to Model tab
- **Statistics** - count of elements, relationships, and diagrams
- **Language switcher** - CZ/EN

### Tabs

The editor is divided into six main tabs:

1. **Model** - metadata and model settings
2. **Elements** - architectural element management
3. **Relationships** - relationship management between elements
4. **Diagrams** - view creation and management
5. **Generator** - text output generation
6. **Export/Import** - data exchange with other systems

---

## Model Management

### Basic Information

- **Model ID** - unique identifier (automatically generated)
- **Model name** - displayed in the header
- **Version** - model versioning
- **Documentation** - detailed model description

### Dublin Core Metadata

Standardized metadata according to ISO 15836:

- **Creator** - author or responsible person
- **Publisher** - organization responsible for publication
- **Date** - creation or publication date
- **Language** - content language (cs, en, de...)
- **Rights** - licensing information
- **Subject** - topic or keywords
- **Description** - brief content description

### Custom Properties

You can add any number of custom properties in key-value format. Use the **Add property** button and fill in the name and value.

### Buttons

- **Save metadata** - saves changes
- **Reset** - restores default values

---

## Working with Elements

### Creating a New Element

1. Select the **layer** (Strategy, Business, Application...)
2. Select the **element type** - list is filtered by layer
3. Enter the element **name**
4. Optionally add:
   - **Stereotype** - type extension (e.g., "microservice" for ApplicationComponent)
   - **Determines** - reference to law, standard, or governing document
   - **Tags** - comma-separated tags for categorization
   - **Description** - detailed documentation
5. Click **Save element**

### Automatic ID Generation

Element ID is automatically generated from type and name:
- `BusinessProcess` + "Order Processing" → `bp-order-processing`

### Editing an Element

- Click the **pencil** icon in the table
- Form is pre-filled with element values
- After modifications, click **Save element**

### Duplicating an Element

- Click the **copy** icon in the table
- A copy is created with a new ID (suffix `-copy` is added)
- The copy opens for editing

### Deleting an Element

- Click the **trash** icon in the table
- Confirm deletion
- **Warning:** All relationships connected to the element will also be deleted

### Filtering Elements

Above the table are filters:
- **Layer** - filter by layer
- **Type** - filter by element type
- **Stereotype** - filter by stereotype
- **Tags** - filter by tags
- **Search** - full-text search

The **Clear filters** button clears all filters.

### Table Sorting

Click on a column header to sort the table:
- First click: ascending (A→Z)
- Second click: descending (Z→A)

### Hiding Columns

Click on **Columns** and select which columns to display. Settings are saved.

### Type Hints

After selecting an element type, a brief description according to the ArchiMate specification is displayed.

---

## Working with Relationships

### Cascade Selection

The relationship form uses intelligent cascade selection:

1. **Source layer** → filters source element types
2. **Source type** → filters specific source elements
3. **Source element** → select specific element
4. **Target layer** → filters target element types
5. **Target type** → filters specific target elements
6. **Target element** → select specific element
7. **Relationship type** → shows only allowed types per specification

### Relationship Validity Check

The editor automatically checks if a relationship is allowed according to ArchiMate 3.2:
- Allowed relationships are displayed in green
- Invalid combinations are not in the list

### Statement Preview

After selecting source, target, and relationship type, a preview is shown as a sentence:
> "Source element **serves** Target element"

### Automatic Relationship ID

Relationship ID is automatically generated as a combination of source and target IDs.

### Optional Attributes

- **Relationship name** - optional relationship description
- **Description** - detailed documentation
- **Tags** - tags for categorization

### Filtering Relationships

- **Source element** - filter by source
- **Target element** - filter by target
- **Relationship type** - filter by type
- **Name** - filter by name
- **Search** - full-text search

### Quick Filter from Elements Table

In the elements table, you can click on the relationship count to navigate to a filtered relationship list for that element.

---

## Diagrams

Diagrams (views) allow you to organize elements into logical groups and visualize their relationships.

### Creating a Diagram

1. Enter the **diagram name**
2. Optionally add a **description**
3. Click **Create diagram**

### Diagram Editor

After clicking **Open**, the editor displays with three sub-tabs:

#### Diagram Elements

- Add elements using cascade selection (layer → type → element)
- List of elements in the diagram with removal option
- Elements can be added and removed

#### Diagram Relationships

- Automatically displays relationships between elements in the diagram
- Read-only - relationships are managed in the Relationships tab

#### Preview

Visual diagram preview:
- Elements are displayed as rectangles colored by layer
- Relationships are displayed as lines with appropriate markers
- **Download SVG** button exports the preview as a vector image

### Diagram Management

- **Edit description** - change diagram documentation
- **Delete** - remove diagram (elements remain)

---

## Text Generator

The generator creates text outputs from the model using templates with placeholders.

### Templates

Enter a template with placeholders in square brackets:
```
[name] is a [type] in the [layer] layer.
```

### Available Placeholders

#### For Elements
- `[id]` - element identifier
- `[name]` - element name
- `[type]` - element type
- `[layer]` - element layer
- `[stereotype]` - stereotype
- `[determines]` - determining document
- `[tags]` - tags
- `[description]` - documentation

#### For Relationships
- `[id]` - relationship identifier
- `[type]` - relationship type
- `[source]` - source element name
- `[target]` - target element name
- `[name]` - relationship name
- `[description]` - relationship documentation
- `[tags]` - relationship tags
- `[verb]` - relationship verb (serves, realizes...)

### Filters

You can limit generation to:
- Selected **layer**
- Selected **element/relationship type**
- Selected **stereotype**
- Selected **tags**

### Options

- **Skip empty** - omits items where a placeholder would be empty
- **Generate for elements/relationships** - data source switch

### Output

- Generated text can be copied to clipboard
- **Clear** button clears the output

---

## Import and Export

### Export AJX

Click **Export AJX** to download the model in AJX (JSON) format. The file will be named after the model with `.ajx` extension.

### Copy AJX

Copies AJX data to clipboard for pasting elsewhere.

### Export XML

Exports the model in **ArchiMate Open Exchange** format (standard XML format for exchange between tools).

### Export CSV

Exports elements and relationships as CSV files for import into spreadsheet applications.

### Import

Supported formats:
- **AJX** - ArchiMate JSON eXchange (.ajx)
- **XML** - ArchiMate Open Exchange (.xml)

#### Import from File

1. Click **Select file**
2. Choose a .ajx or .xml file
3. Click **Import**

#### Import by Pasting

1. Paste AJX or XML data into the text field
2. Click **Import**

#### Paste from Clipboard

The **Paste from clipboard** button automatically pastes clipboard content. On mobile devices or when the Clipboard API is unavailable, a modal window appears for manual pasting.

### Delete All

The **Delete all** button clears the entire model including all elements, relationships, and diagrams.

---

## Merging Models

Merging allows you to import selected parts from another model into the current one.

### Merge Strategies

- **Keep existing** - on ID collision, keeps the original element
- **Overwrite with new** - on ID collision, replaces with new element
- **Manual selection** - allows selecting specific elements and relationships

### Manual Selection

When choosing "Manual selection":

1. Load the file to merge
2. Switch between **Elements** and **Relationships** tabs
3. Use **search** for quick finding
4. Check items to import
5. **Select all** / **Deselect all** buttons work with visible items

#### Selection by Relationships

1. Switch to the **Relationships** tab
2. All elements are automatically unchecked
3. Check desired relationships
4. Source and target elements are automatically selected
5. Click **Merge Models**

#### Selection by Elements

1. Stay on the **Elements** tab
2. Uncheck elements you don't want
3. Relationships between selected elements are imported automatically
4. Click **Merge Models**

### Imported Item Marking

Imported elements and relationships automatically receive a tag with the source model name, e.g., `Import from: Source model`.

### Statistics

After merging, statistics are displayed:
- Number of added/overwritten elements
- Number of added/overwritten relationships
- Number of added/overwritten diagrams

---

## Bulk Tag Operations

### Opening the Modal Window

Click the **Bulk operations** button in the filters section.

### Scope Selection

- **Elements** - operations on element tags
- **Relationships** - operations on relationship tags

### Item Selection

- Check items for the operation
- **Select all** / **Deselect all** - bulk selection
- **Select currently filtered** - selects items matching active filters

### Available Operations

#### Add Tag
Adds the specified tag to all selected items (if they don't already have it).

#### Remove Tag
Removes the specified tag from all selected items.

#### Replace Tag
Replaces one tag with another in all selected items.

---

## Tips and Tricks

### Automatic Saving

The model is automatically saved to the browser after each change. When reopening, the last state is loaded.

### Quick Navigation from Relationships

In the elements table, the "Relationships" column shows the relationship count. Clicking the number navigates to a filtered relationship list for that element.

### Autocomplete Suggestions

- **Stereotypes** - suggests previously used stereotypes
- **Tags** - suggests existing tags from the model
- **Relationship names** - suggests previously used names

### Relationship Validation

The editor automatically validates relationships according to the ArchiMate 3.2 specification. Invalid combinations are not offered.

### Drag & Drop

Files can be imported by dragging them onto the page.

### Dublin Core

Fill in Dublin Core metadata for better interoperability with other tools and for model documentation.

### Model Version

Use the Version field to track model changes over time.

### Backup

Regularly export the model to an AJX file as backup. Browser data may be deleted when clearing history.

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Tab | Move between form fields |
| Enter | Submit form (in some contexts) |
| Escape | Close modal window |

---

## ArchiMate Reference

### Layers

| Layer | Color | Description |
|-------|-------|-------------|
| Strategy | Brown | Strategic elements - resources, capabilities, value streams |
| Business | Gold | Business elements - actors, processes, services |
| Application | Blue | Application elements - components, services, data |
| Technology | Green | Technology elements - nodes, devices, artifacts |
| Physical | Dark Green | Physical elements - equipment, facilities, materials |
| Implementation | Purple | Implementation elements - work packages, deliverables |
| Motivation | Red | Motivation elements - stakeholders, goals, requirements |
| Composite | Gray | Composite elements - locations, groupings |

### Relationship Types

| Type | Category | Description |
|------|----------|-------------|
| Composition | Structural | Element is composed of other elements |
| Aggregation | Structural | Element aggregates other elements |
| Assignment | Structural | Assignment of active element to behavior |
| Realization | Structural | Element realizes another element |
| Serving | Dependency | Element provides functionality to another |
| Access | Dependency | Element accesses data |
| Influence | Dependency | Element influences another element |
| Triggering | Dynamic | Element triggers another element |
| Flow | Dynamic | Flow of information or material |
| Specialization | Other | Element is a specialization of another |
| Association | Other | Unspecified relationship |

---

## Support

The editor is an open-source tool available on GitHub.

- **Online version:** https://mrt.site44.com/archimate-editor.html
- **GitHub repository:** https://github.com/michalradacz/archimate-editor
- **Bug reports:** https://github.com/michalradacz/archimate-editor/issues

On GitHub you will find:
- Editor available for download as a standalone HTML file
- This documentation in Czech and English
- JSON Schema (`ajx-schema.json`) for AJX file validation

### System Requirements

- Modern web browser (Chrome, Firefox, Safari, Edge)
- JavaScript must be enabled
- localStorage required for saving

### Known Limitations

- Data is stored locally in the browser
- Clearing browser data will delete the model
- Regular export backups are recommended

---

*Documentation version: 1.0*
*ArchiMate® is a registered trademark of The Open Group.*
