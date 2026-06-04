# Dolibarr Visual Changelog

A lightweight, multi-language, and user-friendly visual changelog viewer for Dolibarr ERP/CRM. 

This project transforms raw, technical developer changelogs into clear, organized, and benefit-driven release notes for end-users and administrators. It features dynamic version file loading, multi-language support (English, French, Spanish), and screenshot preview integrations.

---

## 🚀 Purpose

Dolibarr releases come with comprehensive but raw text changelogs that can be overwhelming for non-technical users. This tool reads a modular structured dataset to display key features sorted by business categories (Accounting, HR, Sales, AI, etc.) with explicit descriptions and visual previews, helping teams understand **what actually changes** in their daily software usage.

---

## 📂 Project Structure & Architecture

To ensure scalable collaboration and avoid giant, unmaintainable JSON files, the data layer is completely decoupled. 

* **`config.json`** acts as the core configuration file, handling the list of active versions and localized interface/category titles.
* **`vXX.json`** files are standalone, independent datasets containing the actual release notes for that specific version. They are loaded dynamically by the browser only when selected.

```text
📁 dolibarr-visual-changelog/
│── 📄 index.html          # Main web interface & dynamic rendering script logic
│── 📄 config.json         # Global settings, list of active versions, and UI translations
│── 📄 v23.json            # Standalone feature datasets specific to version 23
│── 📄 v24.json            # Standalone feature datasets specific to version 24
└── 📁 img/                 # Root asset folder for feature screenshots
    └── 📁 v24/             # Subfolder specific to Dolibarr version 24
        ├── 📁 en/          # English interface screenshots
        ├── 📁 fr/          # French interface screenshots
        └── 📁 es/          # Spanish interface screenshots
