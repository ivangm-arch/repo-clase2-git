# Contenido extra - GitHub Actions avanzado

Esta sección contiene ejercicios adicionales para ampliar la clase principal con casos más cercanos a un entorno profesional.

## Objetivos

- Entender patrones reales de CI/CD.
- Validar Pull Requests automáticamente.
- Optimizar pipelines con cache.
- Aplicar buenas prácticas de seguridad.
- Reutilizar workflows.
- Simular despliegues.
- Introducir automatización con IA sin perder el foco en CI/CD.

---

## Ejercicios

- [01. Matrix Builds](01.Matrix-Builds/README.md)
- [02. Pull Request Workflows](02.Pull-Request-Workflows/README.md)
- [03. Workflows programados](03.Workflow-Schedule/README.md)
- [04. Cache de dependencias](04.Cache-Dependencias/README.md)
- [05. Seguridad y permissions](05.Security-Permissions/README.md)
- [06. Reusable Workflows](06.Reusable-Workflows/README.md)
- [07. Deploy simulado](07.Deploy-Simulado/README.md)
- [08. IA para Pull Requests](08.AI-PR-Summary/README.md)
- [09. IA para Release Notes](09.AI-Release-Notes/README.md)
- [10. GitHub Models desde Actions](10.GitHub-Models/README.md)
- [11. Dependabot](11.Dependabot/README.md)
- [12. Demo Java, tests unitarios y GitHub Actions con IA](#12-demo-java-tests-unitarios-y-github-actions-con-ia)

---

## 12. Demo Java, tests unitarios y GitHub Actions con IA

### Objetivo

Practicar un flujo de integración continua con Java 21 y Maven, desde la creación de un repositorio hasta la validación de cambios mediante tests y GitHub Actions. El ejercicio incluye protección de la rama principal y el uso de IA como apoyo, sin fusionar el Pull Request final.

### Prompt

Usa el siguiente prompt para preparar la demo. Completa las tareas en el orden indicado y comprueba en GitHub los resultados antes de dar el ejercicio por terminado.

```text
Quiero preparar una demo didáctica para una clase de GitHub. Crea y configura un repositorio público en mi cuenta con estos datos:

- Nombre visible: “Prueba Test java actions con IA”
- Nombre técnico del repositorio: `prueba-test-java-actions-con-ia`
- Descripción: “Demo de Java, tests unitarios y GitHub Actions”

Realiza las tareas en este orden:

1. Crea el repositorio en GitHub con `main` como rama predeterminada.
2. Inicializa un proyecto Java con Maven y Java 21. Incluye un `README.md` con instrucciones para ejecutar los tests localmente y una explicación breve del flujo de la demo.
3. Añade una clase `Calculator` con métodos para sumar y restar dos números.
4. Añade tests unitarios con JUnit para ambos métodos y ejecútalos. No continúes hasta que pasen.
5. Añade un workflow de GitHub Actions que ejecute los tests en cada `push` a `main` y en cada pull request dirigido a `main`. Usa permisos mínimos y asigna al job el nombre estable `Unit tests`.
6. Sube el proyecto base y el workflow a `main`.
7. Después de subir el proyecto base, protege `main` para que los cambios solo puedan entrar mediante pull request y exige que pase el check `Unit tests` antes de fusionar. Aplica la protección también a administradores y no configures excepciones de bypass, siempre que GitHub y los permisos de la cuenta lo permitan. No exijas aprobaciones de revisión.
8. Crea una rama de funcionalidad a partir de `main`. Añade a `Calculator` un método para multiplicar dos números y su test unitario.
9. Ejecuta los tests, sube la rama y abre un pull request dirigido a `main`.
10. Comprueba en GitHub que el workflow se ejecutó para ese pull request y que el check `Unit tests` terminó correctamente. Deja el pull request abierto; no lo fusiones.

Al terminar, proporciona los enlaces al repositorio y al pull request, indica el resultado de los tests y del workflow, y confirma qué reglas de protección quedaron efectivamente aplicadas. Si alguna tarea no se puede completar por permisos, configuración o limitaciones de GitHub, explica cuál y el motivo; no afirmes que una configuración se aplicó si no pudiste verificarla.
```
