# 05. Seguridad y permissions

## Objetivo

Aplicar el principio de mínimo privilegio en GitHub Actions.

---

## Concepto clave

Por defecto, un workflow puede recibir un `GITHUB_TOKEN`. Debes limitar sus permisos a lo estrictamente necesario.

---

## Workflow recomendado

Crea el fichero:

```text
.github/workflows/extra-05-permissions.yml
```

```yaml
name: Extra 05 - Minimal Permissions

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read

jobs:
  security-check:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Comprobar permisos mínimos
        run: |
          echo "Este workflow solo necesita leer contenido del repositorio"
```

---

## Buenas prácticas

- No uses permisos de escritura si no son necesarios.
- No imprimas secretos en logs.
- Evita ejecutar código no confiable con tokens con permisos elevados.
- Revisa especialmente workflows que se ejecutan desde Pull Requests.

---

## Ejercicio

1. Añade `permissions: contents: read` a un workflow existente.
2. Comprueba que sigue funcionando.
3. Discute qué workflows necesitarían `contents: write` y por qué.
