# 🧪 Ejercicio 07: Dispatch Avanzado (Tipos de Inputs y Desplegables)

En este ejercicio aprenderemos a utilizar los diferentes tipos de parámetros (`inputs`) que ofrece `workflow_dispatch`, incluyendo listas desplegables (`choice`), casillas de verificación (`boolean`), selectores de entorno (`environment`) y texto libre (`string`).
Esto es especialmente útil para parametrizar despliegues controlados evitando errores de escritura manual.

---

## 🎯 Objetivo

- Configurar inputs tipados en `workflow_dispatch` (`choice`, `boolean`, `environment`, `string`)
- Utilizar listas desplegables y valores por defecto en la interfaz de GitHub Actions
- Evaluar condicionales simples con los parámetros recibidos

---

## Pasos
### 1. Utiliza el repositorio creado en el Ejercicio 1

### 2. Crea un nuevo workflow llamado `07_dispatch_inputs.yml` e incluye este contenido:
```yaml copy
name: Workflow Manual Avanzado
on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Version a desplegar (ej. 1.0.0)'
        required: true
        type: string
        default: '1.0.0'
      navegador:
        description: 'Selecciona el motor para los tests'
        required: true
        type: choice
        options: ['chrome', 'firefox', 'safari']
        default: 'chrome'
      ejecutar_tests:
        description: 'Ejecutar suite de pruebas antes de continuar'
        required: false
        type: boolean
        default: true
      entorno:
        description: 'Entorno de destino'
        required: true
        type: choice
        options: ['development', 'staging', 'production']
        default: 'development'
jobs:
  despliegue-parametrizado:
    runs-on: ubuntu-26.04
    steps:
      - name: Mostrar resumen de parametros
        run: |
          echo "Iniciando ejecucion manual..."
          echo "Version: ${{ inputs.version }}"
          echo "Navegador: ${{ inputs.navegador }}"
          echo "Ejecutar tests: ${{ inputs.ejecutar_tests }}"
          echo "Entorno: ${{ inputs.entorno }}"

      - name: Ejecucion condicional de tests
        if: ${{ inputs.ejecutar_tests == true }}
        run: echo "Ejecutando tests E2E en ${{ inputs.navegador }}..."
```

### 3. Haz commit y push del nuevo workflow
```bash copy
git add .github/workflows/07_dispatch_inputs.yml
git commit -m "Ejercicio 7: Workflow manual con tipos de inputs y desplegables"
git push origin main
```

### 4. Ejecuta manualmente el workflow
- Ve a `Actions` → Selecciona el workflow creado a la izquierda: `Workflow Manual Avanzado`.
- Haz clic en **Run workflow**.
- Prueba los distintos controles generados en el formulario: escribe la versión, selecciona un navegador del desplegable, marca o desmarca el checkbox de tests y elige un entorno (si no tienes entornos creados en el repositorio, puedes cambiar `type: environment` por `type: choice` en el código).
- Haz clic en el botón verde **Run workflow**.

### 5. Observa los logs de la ejecución y comprueba cómo se imprimen las variables seleccionadas y cómo se comporta el paso condicional según marques o desmarques el checkbox