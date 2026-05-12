# 🧪 Ejercicio 06: Dispatch

En este ejercicio aprenderemos como ejecutar manualmente un workflow utilizando `workflow_dispatch`.
Esto es especialmente util cuando queremos controlar cuando se ejecuta un workflow, por ejemplo: despliegues puntuales, pruebas unitarias...

---

## 🎯 Objetivo

- Ejecucion manual de workflows
- Definir inputs a las ejecuciones

---

## Pasos
### 1.  Utiliza el repositorio creado en el Ejercicio 1

### 2. Crea un nuevo workflow llamado `06_dispatch.yml` e incluye este contenido:
```yaml copy
name: Workflow Manual
on:
  workflow_dispatch:
    inputs:
      nombre:
        description: 'Tu nombre'
        required: true
        default: 'Alumno'
jobs:
  saludo:
    runs-on: ubuntu-latest
    steps:
      - name: Saludo personalizado
        run: echo "Hola, ${{ github.event.inputs.nombre }}!"
```

### 3. Haz commit y push del nuevo workflow
```bash copy
git add .github/workflows/06_dispatch.yml
git commit -m "Ejercicio 6: Workflow manual básico"
git push origin main
```

### 4. Ejecuta manualmente el workflow
* Ve a `Actions` → Selecciona el workflow creado a la izquierda: `Workflow Manual`
* Haz clic en Run workflow
* Introduce tu nombre en el input y ejecuta.
  
* ### 5. Observa los logs de la ejecucion y comprueba que ha sustituido correctamente la variable
