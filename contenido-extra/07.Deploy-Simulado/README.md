# 07. Deploy simulado

## Objetivo

Simular un despliegue usando GitHub Actions y environments.

---

## Concepto clave

GitHub permite asociar jobs a environments como `development`, `staging` o `production`.

En repositorios reales, los environments pueden requerir aprobaciones antes de desplegar.

---

## Workflow recomendado

Crea el fichero:

```text
.github/workflows/extra-07-deploy.yml
```

```yaml
name: Extra 07 - Simulated Deploy

on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Entorno de despliegue'
        required: true
        type: choice
        options:
          - development
          - staging
          - production

permissions:
  contents: read

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: ${{ inputs.environment }}

    steps:
      - name: Simular build
        run: echo "Build completado"

      - name: Simular deploy
        run: echo "Deploy realizado en ${{ inputs.environment }}"
```

---

## Ejercicio

1. Ejecuta el workflow manualmente.
2. Selecciona distintos entornos.
3. Revisa cómo aparece el environment en la ejecución.
4. Opcional: configura aprobación manual para `production` en GitHub.
