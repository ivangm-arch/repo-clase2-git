# 11. Dependabot

## Objetivo

Automatizar la actualización de dependencias.

---

## Concepto clave

Dependabot revisa dependencias y puede abrir Pull Requests automáticamente cuando hay nuevas versiones o actualizaciones de seguridad.

---

## Archivo recomendado

Crea el fichero:

```text
.github/dependabot.yml
```

```yaml
version: 2

updates:
  - package-ecosystem: pip
    directory: /
    schedule:
      interval: weekly
```

---

## Ejercicio
0. [Documentación de uso Dependabot](https://docs.github.com/es/code-security/how-tos/secure-your-supply-chain/secure-your-dependencies/configuring-dependabot-security-updates)
1. Crea el fichero `.github/dependabot.yml`.
2. Añade un fichero `requirements.txt` con una dependencia.
3. Haz push.
4. Revisa si GitHub detecta la configuración de Dependabot.

---

## Buenas prácticas

- Revisa cada Pull Request de Dependabot.
- Ejecuta tests antes de fusionar.
- No aceptes actualizaciones mayores sin revisar cambios incompatibles.
  
