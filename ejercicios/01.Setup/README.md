# 🧪 Ejercicio 01: Setup de Github Actions, ¡Tu primer workflow!

Este ejercicio te ayudará a crear y ejecutar tu primer workflow

---

## 🎯 Objetivo

- Crear un workflow basico
- Ejecutar tu workflow
- Visualizacion de logs

---

## Pasos

### 1.  Nuevo repositorio
Crea un repositorio nuevo en GitHub

### 2.  Crea la carpeta `.github/workflows`

### 3.  Dentro, crea un archivo `01_hola_mundo.yml` con:
```yaml copy
on:
  push:
    branches:
      - main
jobs:
  saludo:
    runs-on: ubuntu-latest
    steps:
      - name: Imprimir mensaje
        run: echo "Hola mundo desde GitHub Actions"
```

### 4.  Haz commit y push a main

```bash copy
git add .github/workflows/01_hola_mundo.yml
git commit -m "Añadir workflow de Hola Mundo"
git push origin main
```

### 5.  Ve a **Actions** y observa la ejecución.

