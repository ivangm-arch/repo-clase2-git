# 🧪 Ejercicio 03: Jobs y Steps

Este ejercicio te ayudará a crear y ejecutar tu primer workflow
* Cada job se ejecuta en un runner separado.
* Por defecto, los jobs se ejecutan en paralelo.
* Para que un job espere a que otro termine antes de ejecutarse, usamos la propiedad `needs`.

---

## 🎯 Objetivo

- Ejecucion de jobs en paralelo
- Ejecucion de jobs en secuencial
- Dependencias entre jobs

---

## Pasos
### 1.  Utiliza el repositorio creado en el Ejercicio 1

### 2.  Crea un workflow llamado `03_jobs_paralelos.yml`

### 3. Añade este contenido al fichero:
```yaml copy
name: Jobs en Paralelo
on:
  push:
    branches:
      - main
jobs:
  python:
    runs-on: ubuntu-latest
    steps:
      - name: Comprobar Python
        run: python3 --version

  node:
    runs-on: ubuntu-latest
    steps:
      - name: Comprobar Node.js
        run: node --version
```
### 4. Haz commit y push
``` bash copy
git add .github/workflows/03_jobs_paralelos.yml
git commit -m "Ejercicio 3: Jobs en paralelo"
git push origin main
```

### 5. Observa las ejecuciones de los jobs en ´Actions´

### 6.  Crea otro workflow llamado `03_jobs_secuencial.yml`

### 7. Añade el contenido:
```yaml copy
name: Jobs Secuenciales
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Construir proyecto
        run: echo "Construyendo proyecto..."

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Ejecutar tests
        run: echo "Ejecutando tests..."
```

### 8. Haz commit y push
``` bash copy
git add .github/workflows/03_jobs_secuencial.yml
git commit -m "Ejercicio 3: Jobs en secuencial"
git push origin main
```

### 9. Observa las ejecuciones de los jobs en `Actions`




