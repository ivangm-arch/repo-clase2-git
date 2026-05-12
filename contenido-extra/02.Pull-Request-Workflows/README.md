# 02. Workflows para Pull Requests

## Objetivo

Ejecutar validaciones automáticamente antes de fusionar cambios en `main`.

---

## Concepto clave

En proyectos reales, muchos workflows se ejecutan sobre Pull Requests para bloquear cambios defectuosos antes de que lleguen a la rama principal.

---

## Workflow recomendado

Crea el fichero:

```text
.github/workflows/extra-02-pr-validation.yml
```

```yaml
name: Extra 02 - PR Validation

on:
  pull_request:
    branches:
      - main

permissions:
  contents: read

jobs:
  validate:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Mostrar contexto
        run: |
          echo "Evento: ${{ github.event_name }}"
          echo "Rama origen: ${{ github.head_ref }}"
          echo "Rama destino: ${{ github.base_ref }}"

      - name: Validación simple
        run: |
          test -f README.md
```

---

## Ejercicio

1. Crea una rama nueva.
2. Modifica el README.
3. Abre una Pull Request contra `main`.
4. Revisa la pestaña `Checks`.
5. Borra temporalmente `README.md` en tu rama y observa el fallo.

---

## Preguntas

- ¿Por qué es mejor validar una PR antes de hacer merge?
- ¿Qué diferencia hay entre `push` y `pull_request`?
- ¿Qué información aportan `github.head_ref` y `github.base_ref`?
