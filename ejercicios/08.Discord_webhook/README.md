# 🧪 Ejercicio 07: Integración con Discord

Este ejercicio nos va a permitir comprender que, un workflow de GitHub puede ejecutar practicamente cualquier comando o programa en diferentes lenguajes y Sistemas Operativos.

En este caso vamos a realizar una integración con la herramienta `Discord`, haciendo uso de los `Webhooks`.
Para ello vamos a crear un nuevo servidor en `Discord`, crear un `Webhook`, guardar la información en `Secrets` y realizar un llamada `HTTP` usando el comando `curl` de Linux.
---

## 🎯 Objetivo

- Comprension del potencial de los workflows de GitHub.
- Integración con Discord para notificaciones

---

## Pasos
### 1.  Utiliza el repositorio creado en el Ejercicio 1

### 2. Accede a Discord utilizando tu cuenta y crea un nuevo servidor. Para ello pula el icono `+` en la izquierda para añadir un nuevo servidor.
* Sigue el asistente de creación en Discord. `Crear mi plantilla` -> `Para mis amigos y yo` -> Darle el nombre al servidor, Ejemplo `GitHub Actions`
* Una vez creado en la parte izquierda os aparecerá un nuevo Servidor con un canal de texto por defecto llamado `#general`.

## 3. Crear un webhook en Discord
* Una vez dentro del servidor `GitHub Actions` Creado, entramos en los ajustes del canal de texto `#general` haciendo click en el icono `⚙`
* Entramos en la seccion `Integraciones` -> `Crear un Webhook`. Nos creará un WebHook al cual podemos cambiarle el nombre y la apariencia.
* Hacemos click en el boton `Copiar URL de Webhook`. La url proporcionada será similar a esto: `https://discord.com/api/webhooks/1410577503663292467/XzAG0aJ8QH5_idQ4R3O7aa46_6n9tFFKgAcfluIfJaa4mIQYu7AnqSopGIrOvfQlXXXX`

## 4. Guardamos la URL en un secreto de repositorio con el nombre `DISCORD_WEBHOOK`

## 5. Creamos un workflow llamado `07_discord.yml` e inclumos el siguiente contenido:
```yaml copy
name: Notificar Discord
on:
  push:
    branches:
      - main
jobs:
  notify-discord:
    runs-on: ubuntu-latest
    steps:
      - name: Enviar mensaje a Discord
        env:
          WEBHOOK_URL: ${{ secrets.DISCORD_WEBHOOK }}
          COMMIT_AUTHOR: ${{ github.actor }}
          COMMIT_MESSAGE: ${{ github.event.head_commit.message }}
          COMMIT_URL: ${{ github.event.head_commit.url }}
          COMMIT_DATE: ${{ github.event.head_commit.timestamp }}
        run: |
          # Construir JSON usando jq para que sea válido
          JSON=$(jq -n \
            --arg author "$COMMIT_AUTHOR" \
            --arg message "$COMMIT_MESSAGE" \
            --arg url "$COMMIT_URL" \
            --arg date "$COMMIT_DATE" \
            '{content: "**Nuevo push por \($author)**\n**Mensaje:** \($message)\n**Fecha y hora del commit:** \($date)\n**Commit URL:** \($url)"}'
          )

          curl -H "Content-Type: application/json" \
               -X POST \
               -d "$JSON" \
               $WEBHOOK_URL
```

## 6. Hacemos commit y push del nuevo workflow
```bash copy
git add .github/workflows/07_discord.yml
git commit -m "Ejercicio 7: Mi nueva integración con Discord"
git push origin main
```

## 7. Revisamos el log de la ejecucion de la `Action` y revisamos el mensaje del bot en `Discord`

