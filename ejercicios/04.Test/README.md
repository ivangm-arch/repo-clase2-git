# 🧪 Ejercicio 04: Pruebas Automaticas

Este ejercicio aprenderemos a integrar test automaticos en un workflow.
Cada vez que se haga un push a la rama principal, se ejecutaran pruebas para verificar el codigo.

La Integración Continua (CI) permite detectar errores antes de que los cambios se fusionen a la rama principal.
Se ejecutan scripts de prueba automáticamente en un entorno limpio (runner) provisto por GitHub.
Usaremos Python y pytest como ejemplo, pero el mismo principio aplica para cualquier lenguaje o framework de testing.
Esto garantiza que cada commit cumple los requisitos de calidad antes de continuar con otros procesos como despliegue.

---

## 🎯 Objetivo

- Integracion de test en workflows

---

## Pasos
### 1.  Utiliza el repositorio creado en el Ejercicio 1

### 2.  Dentro del repositorio, crea un directorio para el proyecto
```bash copy
mkdir proyecto
cd proyecto
```
### 3. Crea un entorno virtual en Python

Mac/unix:
```bash copy
python -m venv venv
source venv/bin/activate
```

Windows:
```bash copy
python -m venv venv
source venv/Scripts/activate
```
Nota:  Si os da un error del tipo: `bash: venv/bin/activate: No such file or directory`, podeis aseguraros de la ruta necesaria a incluir en `source` haciendo un `ls` del directorio `venv`

###4. Instala `pytest` y crea un archivo `requirements.txt`
```bash copy
pip install pytest
pip freeze > requirements.txt
```

### 5. Crea un test de ejemplo en proyecto/test_demo.py y este contenido:
```python copy
def test_suma():
    assert 2 + 2 == 4

def test_resta():
    assert 5 - 3 == 2
```

### 6. Crea un nuevo workflow llamado `04_tests.yml`. Añade el siguiente contenido:
```yaml copy
name: Pruebas Python
on:
  push:
    branches:
      - main
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Configurar Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.x'
      
      - name: Instalar dependencias
        run: pip install -r proyecto/requirements.txt
      
      - name: Ejecutar tests
        run: pytest proyecto/test_demo.py
```

### 7. Haz commit y push de los cambios realizados
```bash copy
git add .
git commit -m "Ejercicio 4: Añadir workflow de tests automáticos"
git push origin main
```

### 8. Haz commit y push de los cambios realizados

### 9. Observa las ejecuciones de los jobs en ´Actions´. Revisa que los 2 test se han ejecutado correctamente

### 10. Sal del entorno virtual de `Python`
```bash copy
deactivate
```

