# 🧪 Ejercicio 05: Automatización

Este ejercicio os ayudará a conocer como generar archivos durante un workflow y subirlos como artifacts.
Estos luego se pueden descargar desde GitHub Actions. Resulta muy util para compartir resultados de compilaciones, logs, reports o cualquier fichero generado automaticamente

---

## 🎯 Objetivo

- Gestion de artifacts

---

## Pasos
### 1.  Utiliza el repositorio creado en el Ejercicio 1

### 2. Crea un nuevo workflow llamado `05_artifact.yml` y añade el contenido:
```yaml copy
name: Subir Artifact
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Crear archivo de ejemplo
        run: echo "Contenido del artifact" > archivo.txt

      - name: Subir artifact
        uses: actions/upload-artifact@v4
        with:
          name: mi-artifact
          path: archivo.txt
```

### 3. Haz commit y push del nuevo workflow
```bash copy
git add .github/workflows/05_artifact.yml
git commit -m "Ejercicio 5: Añadir workflow de artifacts"
git push origin main
```

### 4. Ves a `Actions`-> entra en el workflow creado en este ejercicio.

### 5. En la parte inferior verás una seccion llamada `Artifacts`y verás el fichero creado `mi-artifact`.

### 6. Descarga el artifact creado y visualiza su contenido
Recuerda que el texto `Contenido del artifact` lo hemos generado en tiempo de ejecucion del workflow

