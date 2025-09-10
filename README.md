# Monitor → Enrich → Act Pipeline

Un pipeline de datos robusto para capturar, enriquecer, almacenar y actuar sobre listings o productos de múltiples fuentes.

## 🎯 Objetivo

Construir un sistema unificado que:
1.  **Monitorice:** Capture datos de diversas fuentes (APIs, scraping, CSVs, webhooks).
2.  **Enriquezca:** Normalice, limpie y enriquezca los registros usando lógica de negocio y APIs externas.
3.  **Actúe:** Almacene un historial versionado, exponga los datos en un dashboard y active acciones automáticas (CRM, email, Slack) basadas en reglas.

## 🛠 Stack Tecnológico Previsto

*   **Lenguaje:** Python (FastAPI, Pandas, Requests, BeautifulSoup)
*   **Orquestación:** n8n
*   **Base de Datos:** PostgreSQL
*   **Dashboard:** Metabase / Retool / Streamlit
*   **Infraestructura:** Docker, Docker Compose

## 📋 Estado del Proyecto

**Fase: Diseño e Investigación**
- [x] Definición de arquitectura y objetivos
- [ ] Configuración del entorno de desarrollo
- [ ] Implementación del esquema de base de datos
- [ ] Desarrollo del worker básico (FastAPI)
- [ ] Creación de flujos de n8n para ingesta

## 🗺 Bitácora de Aprendizaje

Las decisiones técnicas, problemas resueltos y lecciones aprendidas se documentan en la [Wiki](https://github.com/tu-usuario/tu-repo/wiki) de este repositorio.

---

*Este es un proyecto de aprendizaje en activo desarrollo.*
