# 10. GitHub Models desde Actions

## Objetivo

Conocer cómo se podría invocar un modelo de IA desde GitHub Actions usando GitHub Models.

---

## Concepto clave

GitHub Models permite ejecutar modelos de IA usando credenciales de GitHub. En un contexto de CI/CD puede usarse para tareas como:

- resumir issues,
- resumir Pull Requests,
- crear borradores de release notes,
- clasificar cambios,
- generar documentación auxiliar.

---

## Importante antes de ejecutar

Este ejercicio puede depender de la disponibilidad de GitHub Models en tu cuenta u organización.

Si no está habilitado, úsalo como ejercicio conceptual.

---

## Workflow conceptual

Crea el fichero:

```text
.github/workflows/extra-10-github-models.yml
```

```yaml
name: Extra 10 - GitHub Models Demo

on:
  workflow_dispatch:
    inputs:
      texto:
        description: 'Texto a resumir'
        required: true
        default: 'GitHub Actions permite automatizar flujos de CI/CD.'

permissions:
  contents: read
  models: read

jobs:
  summarize:
    runs-on: ubuntu-latest

    steps:
      - name: Preparar payload
        run: |
          cat > payload.json <<'JSON'
          {
            "model": "openai/gpt-4o-mini",
            "messages": [
              {
                "role": "system",
                "content": "Resume el texto en una frase clara y breve."
              },
              {
                "role": "user",
                "content": "${{ inputs.texto }}"
              }
            ]
          }
          JSON

      - name: Invocar GitHub Models
        env:
          GH_TOKEN: ${{ github.token }}
        run: |
          curl --fail-with-body \
            -H "Accept: application/vnd.github+json" \
            -H "Authorization: Bearer ${GH_TOKEN}" \
            -H "X-GitHub-Api-Version: 2022-11-28" \
            https://models.github.ai/inference/chat/completions \
            -d @payload.json
```

---

## Ejercicio

1. Ejecuta el workflow manualmente.
2. Cambia el input `texto`.
3. Revisa la respuesta del modelo en los logs.
4. Discute qué riesgos tendría usar esta salida automáticamente.

---

## Buenas prácticas

- No envíes secretos ni datos sensibles a un modelo.
- Revisa siempre la salida antes de publicarla.
- No uses IA para aprobar cambios automáticamente.
- Mantén permisos mínimos.
