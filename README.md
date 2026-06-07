# webpage-factory

A self-contained Sesi project for programmatically compiling responsive HTML pages, layouts, visual charts, and data reports.

---

## 📂 Project Structure

* **`exports/`** - Core modules for generating webpages, charts, data, and databases:
  * `site-builder.sesi` - Renders HTML components (grid layouts, navigation bars, accordions, modals, forms).
  * `markdown-compiler.sesi` - Parses markdown documents into semantic HTML.
  * `visual-charts.sesi` - Renders pure HTML/CSS/SVG visual charts (bar, line, scatter, radar, donut, candlestick, treemap) with zero client-side JavaScript.
  * `data-analyzer.sesi` - Dynamic CSV parser and statistics aggregator.
  * `db-helper.sesi` - Flat-file JSON database engine for persistent storage.
* **`bin/`** - Sesi interpreter CLI executable (`sesi.js`), compiler linter (`lint.sesi`), and test runner (`test-runner.sesi`).
* **`chatbot/`** - Contains the built-in Sesi Co-Pilot script (`sesi_db_chatbot.sesi`).
* **`demo/`** - Contains the dashboard page demo scripts and assets.
* **`main.sesi`** - Entry point Sesi script.
* **`index.html`** - Generated webpage output from `main.sesi` (created after running).

---

## 🚀 Commands

Install dependencies:
```bash
npm install
```

To execute your main Sesi program:
```bash
npm start
```

To compile the dashboard page demo:
```bash
npm run demo
```

To run inline Sesi code evaluations:

```bash
npm run eval "print 'Hello from eval'"
```

To run the linter on your whole workspace:

```bash
npm run lint
```

You can also run lint on individual files:

```bash
npm run lint <filename>
```

Get tips & tricks from the built-in Sesi Co-Pilot:

```bash
npm run support
```
```bash
npm run support <topic>
```

To encrypt a file:

```bash
npm run encrypt <filename>
```

To decrypt a file:

```bash
npm run decrypt <filename>
```

---

## 📦 Module API Reference

### `site-builder` — HTML Component Compiler

Import with: `import {fn_name} from "site-builder"`

| Function | Description |
| :--- | :--- |
| `generate_page(title, content)` | Generates a full HTML document with preset stylesheets. |
| `save_page(filename, title, content)` | Compiles and writes a styled HTML page to disk. |
| `embed_media(path, type)` | Embeds an `<img>` or `<video>` element. |
| `compile_nav_bar(brand, links)` | Generates a styled header navigation bar. |
| `compile_hero_banner(title, subtitle, ctaText, ctaUrl)` | Compiles a full-width hero section. |
| `compile_bento_grid(items)` | Generates a responsive CSS grid layout. |
| `compile_accordion(items)` | Compiles a `<details>`-based collapsible accordion. |
| `compile_tabs(tabs)` | Compiles a radio-toggled tab view. |
| `compile_modal(id, triggerText, modalTitle, modalBody)` | Renders a CSS-only modal dialog. |
| `compile_form_block(actionUrl, fields, submitText)` | Generates a standard input form. |
| `compile_footer_block(copyright, links)` | Renders a site footer with copyright and links. |
| `compile_carousel(items)` | Compiles a CSS scroll-snap media carousel. |
| `compile_data_table(headers, rows, caption)` | Generates a semantic `<table>`. |
| `compile_sticky_sidebar(mainContent, sideContent, sidePosition)` | Wraps content in a sticky two-column layout. |
| `compile_breadcrumb(crumbs)` | Generates a semantic breadcrumb navigation trail. |
| `compile_search_bar(targetClass, placeholder)` | Injects a self-contained JS-powered search filter. |
| `compile_progress_bar(label, percent)` | Renders an accessible progress indicator. |
| `compile_code_block(language, code, collapsed)` | Collapsible code block with a copy-to-clipboard button. |
| `compile_timeline(events)` | Renders a vertical `<ol>` timeline. |
| `generate_seo_metadata(meta)` | Generates `<meta>` SEO and Open Graph tags. |
| `generate_sitemap_xml(topics, baseUrl)` | Compiles a `sitemap.xml`-format string. |
| `concurrent_build(topics, outputDir)` | Builds multiple pages in parallel using `spawn`. |

---

### `markdown-compiler` — Markdown → HTML Parser

Import with: `import {fn_name} from "markdown-compiler"`

| Function | Description |
| :--- | :--- |
| `parse_markdown_full(mdText)` | Parses headers, lists, task lists, tables, blockquotes, code blocks, footnotes, and inline formatting into HTML. |
| `compile_markdown_file(mdPath, htmlPath, title)` | Reads a local `.md` file and saves it as a standalone webpage. |
| `parse_bold(line)` | Processes `**bold**` inline spans. |
| `parse_italic(line)` | Processes `*italic*` and `_italic_` inline spans. |
| `parse_links(line)` | Processes `[label](url)` anchor tags. |
| `parse_images(line)` | Processes `![alt](url)` image tags. |
| `parse_inline_code(line)` | Processes `` `code` `` spans. |
| `compile_table(tableLines)` | Converts a collected set of pipe-table lines into an HTML `<table>`. |
| `collect_footnotes(lines)` | Scans for `[^key]: text` definitions and renders a `<footer>` footnote block. |

---

### `visual-charts` — SVG/HTML Chart Engine

Import with: `import {fn_name} from "visual-charts"`

All chart functions return raw HTML strings. No client-side JavaScript required.

| Function | Description |
| :--- | :--- |
| `compile_bar_chart(data, chartTitle)` | Horizontal bar chart from `[{label, value}]`. |
| `compile_sparkline(values, chartTitle)` | SVG polyline sparkline from an array of numbers. |
| `compile_gauge_indicator(value, minVal, maxVal, label)` | Linear gauge bar with dynamic color thresholds. |
| `compile_pie_chart(data, chartTitle)` | SVG pie chart with percentage labels and legend. |
| `compile_donut_chart(data, chartTitle, centerLabel)` | SVG donut chart with center label and legend. |
| `compile_heatmap(rows, cols, chartTitle)` | CSS grid heatmap with green-to-red intensity coloring. |
| `compile_scatter_plot(points, xLabel, yLabel, chartTitle)` | SVG scatter plot with labeled axes. |
| `compile_radar_chart(axes, chartTitle, maxVal)` | SVG radar/spider chart from N-axis `{label, value}` data. |
| `compile_funnel_chart(stages, chartTitle)` | SVG funnel chart with tapered trapezoid stages. |
| `compile_candlestick_chart(data, chartTitle)` | Brutalist SVG candlestick chart from OHLC data points. |
| `compile_treemap_chart(data, chartTitle)` | SVG treemap chart using aspect-ratio aware slice-and-dice partitioning. |

---

### `data-analyzer` — CSV & Collection Processing

Import with: `import {fn_name} from "data-analyzer"`

| Function | Description |
| :--- | :--- |
| `parse_csv(csvText)` | Parses a CSV string into an array of mapped record objects. |
| `export_to_csv(records, fieldsList)` | Serializes records back to CSV string format. |
| `compute_average(records, key)` | Returns the mean of a numeric field across all records. |
| `compute_max(records, key)` | Returns the maximum value of a numeric field. |
| `compute_min(records, key)` | Returns the minimum value of a numeric field. |
| `sort_records(records, key, ascending)` | Bubble-sorts records by a specified field. |
| `filter_records(records, key, filterVal)` | Returns records matching a key-value pair. |
| `export_to_json(records)` | Serializes records into a valid JSON string. |
| `export_to_excel_xml(records, fieldsList)` | Serializes records to Microsoft Office Excel XML (SpreadsheetML) format. |
| `export_to_word_xml(records, fieldsList)` | Serializes records to Microsoft Office Word XML (WordprocessingML) format. |
| `compute_sum(records, key)` | Calculates the cumulative sum of a numeric field. |
| `compute_median(records, key)` | Calculates the median of a numeric field. |
| `compute_mode(records, key)` | Calculates the mode (most common value) of a numeric field. |
| `compute_std_dev(records, key)` | Calculates the population standard deviation of a numeric field. |
| `group_by(records, key)` | Groups records into an object dictionary partitioned by key values. |
| `validate_records(records, requiredFields)` | Validates that all records contain specified required schema keys. |
| `validate_numeric_field(records, key)` | Identifies record indices with malformed non-numeric values. |

---

### `db-helper` — Flat-File JSON Database

Import with: `import {fn_name} from "db-helper"`

| Function | Description |
| :--- | :--- |
| `init_db(dbPath)` | Initializes an empty database file if one doesn't exist. |
| `read_db(dbPath)` | Reads and parses the database file into an object. |
| `write_db(dbPath, dbObject)` | Serializes and writes the database object to disk. |
| `insert_record(dbPath, collection, record)` | Inserts a record with a unique auto-generated ID. |
| `find_records(dbPath, collection, filterKey, filterVal)` | Queries all records matching a key-value filter. |
| `find_records_paginated(dbPath, collection, filterKey, filterVal, limit, offset)` | Paginated record queries. |
| `count_records(dbPath, collection)` | Returns the total count of records in a collection. |
| `update_record(dbPath, collection, id, updatedFields)` | Merges updated fields into a record by ID. |
| `delete_record(dbPath, collection, id)` | Removes a record from a collection by ID. |
| `find_records_multi(dbPath, collection, filterQuery)` | Returns all records matching a structured key-value filter query. |
| `sort_records_by(dbPath, collection, key)` | Queries and returns all records sorted numerically or alphabetically by a key. |
| `list_collections(dbPath)` | Returns a list of all active collection names in the database. |
| `backup_db(dbPath)` | Creates a timestamped replica of the flat-file database on disk. |
