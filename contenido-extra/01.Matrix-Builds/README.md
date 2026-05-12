# 01. Matrix Builds

## Objetivo

Ejecutar el mismo pipeline en varias versiones de Python para comprobar compatibilidad.

---

## Concepto clave

Una matrix permite ejecutar el mismo job varias veces cambiando una o varias variables.

Ejemplo real:

```text
Python 3.10
Python 3.11
Python 3.12
```

GitHub creará un job por cada versión.

---

## Workflow recomendado

Crea el fichero:

```text
.github/workflows/extra-01-matrix.yml
```

con este contenido:

```yaml
name: Extra 01 - Matrix Tests

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

permissions:
  contents: read

jobs:
  test:
    name: Test Python ${{ matrix.python-version }}
    runs-on: ubuntu-latest

    strategy:
      fail-fast: false
      matrix:
        python-version: ['3.10', '3.11', '3.12']

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Configurar Python
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
          cache: pip

      - name: Instalar dependencias
        run: |
          python -m pip install --upgrade pip
          pip install pytest

      - name: Ejecutar tests
        run: pytest
```

---

## Ejercicio

1. Crea el workflow.
2. Haz push a `main` o abre una Pull Request.
3. Observa cuántos jobs se ejecutan.
4. Cambia una versión de Python por una inexistente y observa el fallo.
5. Restaura el workflow correcto.

---

## Preguntas

- ¿Cuántos jobs se han creado?
- ¿Qué hace `fail-fast: false`?
- ¿Por qué una matrix es útil en proyectos reales?
