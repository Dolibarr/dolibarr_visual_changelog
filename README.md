# Dolibarr Visual Changelog

A lightweight, multi-language, and user-friendly visual changelog viewer for Dolibarr ERP/CRM.

This project transforms raw, technical developer changelogs into clear, organized, and benefit-driven release notes for end-users and administrators. It features dynamic version file loading, multi-language support (English, French, Greek, Spanish), and screenshot preview integrations.

---

## 🚀 Purpose

Dolibarr releases often include long technical changelogs that can be difficult to read for non-technical users. This tool presents the main changes in a visual format, grouped by business category, with translated titles, descriptions, screenshots, and optional links to the full GitHub changelog or YouTube videos.

---

## 📂 Project Structure

The project is designed to keep interface configuration separate from version content.

```text
📁 dolibarr-visual-changelog/
│── 📄 index.html              # Main web interface and rendering logic
│── 📄 config.json             # Global settings, version list, UI translations, category labels
│── 📄 v23.json        # Normalized dataset for Dolibarr v23
│── 📄 v24.json        # Normalized dataset for Dolibarr v24
│── 📄 vXX.json        # Normalized dataset for a future version
└── 📁 img/                    # Root asset folder for screenshots
    └── 📁 vXX/
        ├── 📁 en/
        ├── 📁 fr/
        └── 📁 es/
```

### Files overview

- **`config.json`** stores the active versions, category labels, and static interface translations.
- **`vXX.json`** stores the release content for one version using the new normalized structure.
- **`index.html`** dynamically loads the selected version file, groups changes by category, and renders the selected language.

---

## 🧩 New version structure

Each version file is now structured around a single `changes` array. A change exists only once and contains its technical metadata, tags, translations, links, and images.

### Root structure

```json
{
  "version": "v25",
  "links": {
    "github": "https://github.com/Dolibarr/dolibarr/releases/tag/25.0.0",
    "youtube": [
      {
        "label": "Présentation générale",
        "url": "https://www.youtube.com/watch?v=xxxx"
      }
    ]
  },
  "changes": []
}
```

### Change object structure

Each item in `changes` follows this structure:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | Yes | Stable technical identifier, for example `v25-001`. |
| `order` | integer | Yes | Display order in the interface. |
| `release` | string | Yes | Version identifier, for example `v25`. |
| `tags` | array of strings | Yes | One or more functional categories, for example `ia_innovation`. |
| `links` | array | No | Optional links specific to this change. |
| `images` | object | No | Screenshot paths by language, or a shared `default` image. |
| `translations` | object | Yes | Titles and descriptions by language. |

### Translation block

```json
"translations": {
  "fr": {
    "title": "Brouillons d'emails automatisés",
    "description": "L'assistant IA peut désormais rédiger des réponses email contextuelles directement à partir des propositions commerciales."
  },
  "en": {
    "title": "Automated Email Drafts",
    "description": "The AI assistant can now write context-aware email replies directly from your commercial proposals."
  },
  "es": {
    "title": "Borradores automáticos de correos",
    "description": "El asistente de IA ahora puede redactar respuestas de correo contextualizadas directamente desde sus propuestas comerciales."
  }
}
```

### Image block

If screenshots differ by language:

```json
"images": {
  "fr": "img/v25/fr/ai_email_draft.png",
  "en": "img/v25/en/ai_email_draft.png",
  "es": "img/v25/es/ai_email_draft.png"
}
```

If the same screenshot is shared across all languages:

```json
"images": {
  "default": "img/v25/common/ai_email_draft.png"
}
```

If no screenshot is available:

```json
"images": {
  "default": null
}
```

### Change-level links

Each change may also include its own optional links.

```json
"links": [
  {
    "label": "GitHub PR",
    "url": "https://github.com/Dolibarr/dolibarr/pull/12345"
  },
  {
    "label": "Demo video",
    "url": "https://www.youtube.com/watch?v=yyyy"
  }
]
```

---

## 📋 Recommended categories

Category keys remain defined in `config.json` and reused in `tags`:

- `ia_innovation`
- `compta_facturation`
- `ventes_logistique`
- `rh_salaires`
- `ui_ergonomie`
- `regressions_alertes`

These keys are technical identifiers. Their translated labels are managed only in `config.json`.

---

## 📂 Template for a new version file

When creating a new release file such as `v25.json`, first add `v25` to `versions_available` in `config.json`, then use the template below.

```json
{
  "version": "v25",
  "links": {
    "github": null,
    "youtube": []
  },
  "changes": [
    {
      "id": "v25-001",
      "order": 1,
      "release": "v25",
      "tags": ["ia_innovation"],
      "links": [],
      "images": {
        "fr": "img/v25/fr/ai_email_draft.png",
        "en": "img/v25/en/ai_email_draft.png",
        "es": "img/v25/es/ai_email_draft.png"
      },
      "translations": {
        "fr": {
          "title": "Brouillons d'emails automatisés",
          "description": "L'assistant IA peut désormais rédiger des réponses email contextuelles directement à partir des propositions commerciales."
        },
        "en": {
          "title": "Automated Email Drafts",
          "description": "The AI assistant can now write context-aware email replies directly from your commercial proposals."
        },
        "es": {
          "title": "Borradores automáticos de correos",
          "description": "El asistente de IA ahora puede redactar respuestas de correo contextualizadas directamente desde sus propuestas commerciales."
        }
      }
    }
  ]
}
```

---

## 🖥️ Front-end behavior

The updated `index.html` works with the normalized structure and adds several new capabilities:

- Dynamic loading of `vXX.json` files.
- Fallback compatibility with the legacy `vXX.json` structure.
- Grouping of `changes` by category using `tags`.
- Rendering of translations using `translations[lang]`.
- Image fallback with `images[lang]` or `images.default`.
- Display of the technical ID for each change.
- External links to the full GitHub changelog and one or more YouTube videos.
- Optional per-change links displayed inside cards.

---

## 🔧 config.json role

`config.json` remains the central UI configuration file. It should contain:

- `versions_available`
- translated category labels
- translated interface labels

Example:

```json
{
  "versions_available": ["v24", "v23"],
  "translations": {
    "fr": {
      "categories": {
        "ia_innovation": "🤖 Intelligence Artificielle & Innovation"
      },
      "labels": {
        "title": "Nouveautés de Dolibarr",
        "version_select": "Choisir une version :",
        "lang_select": "Langue :",
        "full_changelog": "Changelog complet",
        "videos": "Vidéos",
        "watch_video": "Voir la vidéo",
        "external_links": "Liens",
        "technical_id": "ID"
      }
    }
  }
}
```

## ✅ Authoring rules

To keep the dataset consistent:

- Use one unique `id` per change.
- Keep `tags` technical and stable.
- Store all translations inside `translations`, never in separate top-level language trees.
- Keep `order` explicit to avoid accidental display changes.
- Use `null` when no screenshot exists.
- Always use relative paths for images.
- Use `target="_blank"` links only for external resources.
