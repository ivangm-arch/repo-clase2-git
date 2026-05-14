# 🧪 Ejercicio 02: Variables y secretos

Este ejercicio te ayudará a crear y ejecutar tu primer workflow

---

## 🎯 Objetivo

- Crear un workflow basico
- Ejecutar tu workflow
- Visualizacion de logs

---

## Pasos
### 1.  Utiliza el repositorio creado en el Ejercicio 1

### 2.  Crear un secreto en GitHub `(Settings → Secrets and variables → Actions → New repository secret)` llamado `MI_SECRETO`. Añade el valor que desees.

### 3. Crea el `workflow` llamado `02_variables_secretos.yml` con el contenido:
```yaml copy
name: Uso de Variables y Secretos
on:
  push:
    branches: [ "main" ]
jobs:
  print-secrets-token:
    runs-on: ubuntu-latest
    steps:
      - name: Mostrar variable de entorno
        env:
          MI_VARIABLE: "ValorDeEjemplo"
        run: |
         echo "Variable de entorno: ${{ env.MI_VARIABLE }}"
      - name: Visualizacion de Secretos
        shell: bash
        env:
         SUPER_SECRET: ${{ secrets.MI_SECRETO }}
        run: |
         echo "Tu Mayor secreto es: $SUPER_SECRET, vaya no puede conocerse..."
      - name: Visualizacion de variables y comandos
        shell: bash
        env:
         SUPER_SECRET: ${{ secrets.MI_SECRETO }}
        run: |
         echo "Primeras 3 letras del secreto: "$(cut -c 1-3 <<< $SUPER_SECRET)", es correcto?"
```
### 4. Haz `commit` y `Push` (sin olvidar `add`). **Nota: los secretos nunca se imprimen en los logs**

### 5. Revisa la ejecucion en `Actions` y visualiza el log de la ejecucion de los 3 runners.







