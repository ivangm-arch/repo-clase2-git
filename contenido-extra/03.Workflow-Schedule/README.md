# 03. Workflows programados

## Objetivo

Ejecutar workflows automáticamente con una planificación tipo cron.

---

## Concepto clave

`schedule` permite ejecutar tareas periódicas:

- limpieza,
- generación de informes,
- comprobaciones nocturnas,
- validaciones de seguridad.

---

## Workflow recomendado

Crea el fichero:

```text
.github/workflows/extra-03-schedule.yml
```

```yaml
name: Extra 03 - Scheduled Check

on:
  schedule:
    - cron: '0 8 * * 1'
  workflow_dispatch:

permissions:
  contents: read

jobs:
  scheduled-check:
    runs-on: ubuntu-latest

    steps:
      - name: Mostrar fecha
        run: date -u

      - name: Ejecutar comprobación
        run: echo "Comprobación programada ejecutada correctamente"
```

---

## Ejercicio

1. Crea el workflow.
2. Ejecútalo manualmente desde GitHub con `workflow_dispatch`.
3. Cambia el cron para que represente otra planificación.

---

## Nota importante

GitHub interpreta los cron en UTC.
