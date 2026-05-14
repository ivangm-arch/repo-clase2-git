# 04. Cache de dependencias

## Objetivo

Reducir el tiempo de ejecución reutilizando dependencias instaladas anteriormente.

---

## Concepto clave

La cache evita descargar o construir de nuevo dependencias que no han cambiado.

En Python, `actions/setup-python@v5` puede cachear dependencias de `pip`.

---

## Workflow recomendado

Crea el fichero:

```text
.github/workflows/extra-04-cache.yml
```

```yaml
name: Extra 04 - Cache Dependencies

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read

jobs:
  test-with-cache:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Configurar Python con cache
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'
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

1. Ejecuta el workflow una primera vez.
2. Revisa los logs de instalación.
3. Ejecuta el workflow de nuevo.
4. Compara tiempos y mensajes relacionados con cache.

---

## Preguntas

- ¿Cuándo se reutiliza la cache?
- ¿Qué cambios podrían invalidarla?
