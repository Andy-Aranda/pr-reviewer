# 🤖 PR Reviewer Automático con Claude + Notion + GitHub

Este proyecto automatiza el análisis de Pull Requests (PRs) usando un LLM (Claude Desktop) conectado mediante el protocolo [MCP (Model Context Protocol)](https://www.datacamp.com/es/tutorial/mcp-model-context-protocol). 

El sistema permite recibir el enlace de un PR, generar un resumen técnico con inteligencia artificial, y guardar automáticamente ese resumen en una página de Notion.

---

## 🧩 Arquitectura del Proyecto

```plaintext
GitHub PR → MCP Server (Python) → Claude Desktop → Análisis → Notion
```

---

## ✨ Características

- Recupera automáticamente los cambios de un PR desde la API de GitHub.
- Genera un análisis semántico del código utilizando Claude Desktop.
- Crea una entrada en Notion con el resumen generado.
- Modular y extensible: puedes añadir más herramientas al servidor MCP.

---

## 🚀 ¿Cómo funciona?

1. **Claude Desktop** detecta el servidor MCP al ejecutarse localmente.
2. El usuario le pasa un enlace de PR a Claude.
3. Claude llama al servidor MCP y usa:
   - `fetch_pr` → obtiene metadatos y diffs del PR desde GitHub.
   - `create_notion_page` → guarda el análisis como una nueva página de Notion.
4. Todo el proceso se dispara desde la interfaz de Claude Desktop sin intervención manual.

---

## 🔧 Requisitos

- Python 3.10+
- [Claude Desktop](https://claude.ai/)
- Cuenta y API key de:
  - [GitHub](https://github.com/settings/tokens)
  - [Notion](https://www.notion.so/my-integrations)

---

## ⚙️ Instalación

1. Instalar `uv` (gestor de entornos Python rápido):
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. Inicializar proyecto:
   ```bash
   uv init pr_reviewer
   cd pr_reviewer
   uv venv
   source .venv/bin/activate
   ```

3. Instalar dependencias:
   ```bash
   uv add "mcp[cli]" requests python-dotenv notion-client
   ```

4. Crear archivo `.env` con tus claves:
   ```env
   GITHUB_TOKEN=ghp_***************
   NOTION_API_KEY=secret_**************
   NOTION_PAGE_ID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
   ```

5. Configura Claude Desktop con el archivo `claude_desktop_config.json`, por ejemplo:
   ```json
   {
     "mcpServers": {
       "pr-reviewer": {
         "command": "/ruta/a/python",
         "args": ["/ruta/a/pr_anayzer.py"],
         "cwd": "/ruta/a/proyecto"
       }
     }
   }
   ```

---

## 🧪 Uso

1. Ejecuta el servidor MCP:
   ```bash
   python pr_anayzer.py
   ```

2. Abre Claude Desktop y pasa un link a un PR:
   ```
   https://github.com/tu_usuario/tu_repo/pull/1
   ```

3. Claude analizará el PR y te preguntará si quieres guardar el resultado en Notion.

---

## 🧠 Créditos e inspiración

Basado en el [tutorial oficial de DataCamp sobre MCP](https://www.datacamp.com/es/tutorial/mcp-model-context-protocol).

---

## 📌 Posibles mejoras

- Automatización completa con `n8n` o GitHub Actions.
- Validación de PRs con reglas personalizadas.
- Integración con otras herramientas como Slack o ClickUp.

---

## 🧑‍💻 Autor

Andrea Aranda – [@Andy-Aranda](https://github.com/Andy-Aranda)