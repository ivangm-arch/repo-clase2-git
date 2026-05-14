# Clase 2 GitHub Actions - Automatización CI/CD

## Objetivo del repositorio

Este repositorio contiene ejercicios prácticos para aprender GitHub Actions y los conceptos básicos de integración continua y entrega continua (CI/CD).

La clase está orientada a entender cómo automatizar tareas habituales de desarrollo:

- validar código automáticamente,
- ejecutar tests,
- trabajar con secretos,
- generar artifacts,
- lanzar workflows manuales,
- integrar servicios externos,
- y conocer patrones más avanzados en la sección extra.

---

## Conceptos importantes

### Workflow

Un workflow es una automatización definida en YAML. GitHub ejecuta workflows cuando ocurre un evento, por ejemplo un `push`, una Pull Request o una ejecución manual.

### Job

Un job es un conjunto de steps que se ejecutan en un runner.

### Step

Un step es una acción concreta dentro de un job. Puede ejecutar un comando shell o usar una action reutilizable.

### Runner

Un runner es la máquina donde GitHub ejecuta el workflow. Cada job se ejecuta en un runner y no debes asumir que dos jobs comparten el mismo sistema de ficheros.

### Action

Una action es un componente reutilizable que puedes usar dentro de un step, por ejemplo `actions/checkout@v4`.

### Secret

Un secret es una variable cifrada para almacenar información sensible, como tokens, API keys o webhooks.

---

## Orden recomendado de ejercicios

- [01. Setup](ejercicios/01.Setup/README.md)
- [02. Secrets](ejercicios/02.Secrets/README.md)
- [03. Jobs y Steps](ejercicios/03.Jobs&Steps/README.md)
- [04. Tests automáticos](ejercicios/04.Test/README.md)
- [05. Automatización y artifacts](ejercicios/05.Automatizacion/README.md)
- [06. Workflow Dispatch](ejercicios/06.Dispatch/README.md)
- [07. Dispatch con inputs](ejercicios/07.Dispatch_inputs/README.md)
- [08. Discord Webhook](ejercicios/08.Discord_webhook/README.md)

---

## Contenido extra

La sección extra contiene ejercicios avanzados y contenidos profesionales:

- [Contenido extra - GitHub Actions avanzado](contenido-extra/README.md)

Incluye:

- matrix builds,
- workflows sobre Pull Requests,
- workflows programados,
- cache de dependencias,
- permisos mínimos,
- reusable workflows,
- deploy simulado,
- IA aplicada a Pull Requests y release notes,
- GitHub Models,
- Dependabot.

---

## Buenas prácticas generales

- Usa versiones recientes de actions.
- Define permisos mínimos con `permissions`.
- Nunca publiques secretos en código ni en logs.
- Usa `pull_request` para validar cambios antes de fusionarlos.
- Usa cache para acelerar pipelines.
- Revisa los logs por job y por step.
- Trabaja con workflows pequeños y fáciles de depurar.
- Trata la IA como una herramienta de apoyo, no como una sustitución de la revisión humana.
