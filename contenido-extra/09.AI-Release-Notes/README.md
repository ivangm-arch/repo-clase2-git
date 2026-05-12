# 09. IA para Release Notes

## Objetivo

Entender cómo automatizar la generación de notas de versión.

---

## Concepto clave

Las release notes pueden generarse a partir de:

- commits,
- Pull Requests,
- issues cerradas,
- etiquetas (`tags`).

La IA puede ayudar a convertir esa información técnica en un resumen legible.

---

## Workflow sin IA externa

Este workflow genera un borrador básico a partir del historial Git.

Crea el fichero:

```text
.github/workflows/extra-09-release-notes.yml
```

```yaml
name: Extra 09 - Release Notes Draft

on:
  workflow_dispatch:

permissions:
  contents: read

jobs:
  release-notes:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Generar release notes básicas
        run: |
          echo "# Release notes" > release-notes.md
          echo "" >> release-notes.md
          git log --oneline -10 >> release-notes.md
          cat release-notes.md

      - name: Subir artifact
        uses: actions/upload-artifact@v4
        with:
          name: release-notes
          path: release-notes.md
          retention-days: 5
```

---

## Ejercicio

1. Ejecuta el workflow manualmente.
2. Descarga el artifact.
3. Reescribe las release notes en lenguaje comprensible para un usuario final.
4. Discute qué partes podría mejorar una IA.
