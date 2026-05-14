# 06. Reusable Workflows

## Objetivo

Crear workflows reutilizables para evitar duplicación.

---

## Concepto clave

Un reusable workflow permite definir una lógica común una sola vez y llamarla desde otros workflows.

---

## Workflow reutilizable

Crea el fichero:

```text
.github/workflows/reusable-python-tests.yml
```

```yaml
name: Reusable Python Tests

on:
  workflow_call:
    inputs:
      python-version:
        description: 'Versión de Python'
        required: true
        type: string

permissions:
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Configurar Python
        uses: actions/setup-python@v5
        with:
          python-version: ${{ inputs.python-version }}
          cache: pip

      - name: Instalar dependencias
        run: |
          python -m pip install --upgrade pip
          pip install pytest

      - name: Ejecutar tests
        run: pytest
```

---

## Workflow llamador

Crea el fichero:

```text
.github/workflows/extra-06-call-reusable.yml
```

```yaml
name: Extra 06 - Call Reusable Workflow

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read

jobs:
  call-tests:
    uses: ./.github/workflows/reusable-python-tests.yml
    with:
      python-version: '3.12'
```

---

## Preguntas

- ¿Qué ventajas tiene reutilizar workflows?
- ¿Qué ocurre si modificas el workflow reutilizable?
- ¿Dónde tendría sentido usar esto en una empresa?
