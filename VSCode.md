# VSCode

## Navigation

- `ctrl+p`: command palette
- `ctrl+shift+o`: go to symbol
- `ctrl+g`: go to line
- `ctrl+x`: cut entire line
- `alt+up/down`: move line up or down
- `shift+alt+up/down`: copy line up or down
- `ctrl+d`: adds to your cursor selection the next match

## Extensions

- Docker
- Python
  - Ruff
- GitLens
- Code Spell Checker
- markdownlint
- Javascript
  - eslint
  - prettier
- Even Better TOML
- Copilot
- Better Comments
- Github Actions
- Postman
- Dev containers

## `settings.json`

`>Preferences: Open User Settings (JSON)`

```json
{
  "editor.formatOnSave": true,
  "[python]": {
    "editor.codeActionsOnSave": {
      "source.fixAll": "explicit",
      "source.organizeImports": "explicit"
    },
    "editor.defaultFormatter": "charliermarsh.ruff"
  },
  "python.analysis.typeCheckingMode": "basic",
  "explorer.confirmDragAndDrop": false,
  "editor.acceptSuggestionOnEnter": "off",
  "python.analysis.autoImportCompletions": true,
  "ruff.importStrategy": "useBundled"
}
```
