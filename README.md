# Dolibarr Visual Changelog

A lightweight, multi-language, and user-friendly visual changelog viewer for Dolibarr ERP/CRM. 

This project transforms raw, technical developer changelogs into clear, organized, and benefit-driven release notes for end-users and administrators. It features dynamic version file loading, multi-language support (English, French, Greek, Spanish), and screenshot preview integrations.

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
│── 📄 vXX.json            # Standalone feature datasets specific to version XX
└── 📁 img/                 # Root asset folder for feature screenshots
    └── 📁 vXX/             # Subfolder specific to Dolibarr version XX
        ├── 📁 en/          # English interface screenshots
        ├── 📁 fr/          # French interface screenshots
        └── 📁 es/          # Spanish interface screenshots
```
---

## 🧩 Version Data File Structure (vXX.json)

To add a new version or contribute to an existing one, you need to follow a strict JSON schema. These files are split by language codes and then sub-divided by functional business categories.

📋 Data Fields Schema

Every object added inside a category array must contain these three fields :
Key | Type | Description

- [Required] text           | string |          The commercial title of the feature. Avoid technical jargon or issue numbers (e.g., do not use #12345).

- [Required] description    | string |          A clear description of what the feature does and how it benefits the end user.

- [Required] image          | string / null |   The relative path to the screenshot (img/vXX/lang/filename.png). Must be set to null if no image is available.

## 📂 Blank Template Blueprint

When creating a new version file (e.g., v25.json), open config.json to append your new version tag to the "versions_disponibles" index, then copy and paste this empty template to start coding:

```text
{
  "en": {
    "ia_innovation": [],
    "compta_facturation": [],
    "ventes_logistique": [],
    "rh_salaires": [],
    "ui_ergonomie": [],
    "regressions_alertes": []
  },
  "fr": {
    "ia_innovation": [],
    "compta_facturation": [],
    "ventes_logistique": [],
    "rh_salaires": [],
    "ui_ergonomie": [],
    "regressions_alertes": []
  },
  "es": {
    "ia_innovation": [],
    "compta_facturation": [],
    "ventes_logistique": [],
    "rh_salaires": [],
    "ui_ergonomie": [],
    "regressions_alertes": []
  }
}
```

Example:
```Example 
{
  "en": {
    "ia_innovation": [
      {
        "text": "Automated Email Drafts",
        "description": "The AI assistant can now write context-aware email replies directly from your commercial proposals.",
        "image": "img/v25/en/ai_email_draft.png"
      }
    ],
    "compta_facturation": [
      {
        "text": "Multi-Currency Stripe Integration",
        "description": "Customers can now pay their invoices online using their local currency with real-time conversion rates.",
        "image": null
      }
    ],
    "ventes_logistique": [],
    "rh_salaires": [],
    "ui_ergonomie": [],
    "regressions_alertes": [
      {
        "text": "Deprecating Old PDF Engine",
        "description": "The legacy PDF generation system has been removed. Ensure your custom modules use the new system.",
        "image": null
      }
    ]
  },
  "fr": {
    "ia_innovation": [
      {
        "text": "Brouillons d'emails automatisés",
        "description": "L'assistant IA peut désormais rédiger des propositions de réponses à vos emails directement depuis vos devis.",
        "image": "img/v25/fr/ai_email_draft.png"
      }
    ],
    "compta_facturation": [
      {
        "text": "Intégration Stripe Multi-Devises",
        "description": "Vos clients peuvent désormais régler leurs factures en ligne dans leur devise locale avec un taux de conversion en temps réel.",
        "image": null
      }
    ],
    "ventes_logistique": [],
    "rh_salaires": [],
    "ui_ergonomie": [],
    "regressions_alertes": [
      {
        "text": "Suppression de l'ancien moteur PDF",
        "description": "L'ancien système de génération PDF a été retiré. Vérifiez que vos modules personnalisés utilisent le nouveau moteur.",
        "image": null
      }
    ]
  },
  "es": {
    "ia_innovation": [
      {
        "text": "Borradores de Email Automatizados",
        "description": "El asistente de IA ahora puede redactar respuestas de correo electrónico basadas en el contexto directamente desde sus presupuestos.",
        "image": "img/v25/es/ai_email_draft.png"
      }
    ],
    "compta_facturation": [],
    "ventes_logistique": [],
    "rh_salaires": [],
    "ui_ergonomie": [],
    "regressions_alertes": []
  }
}
```
