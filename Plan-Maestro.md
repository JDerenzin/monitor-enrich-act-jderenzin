# Plan Maestro: Monitor → Enrich → Act

Este documento es la base del proyecto y sirve como bitácora principal para las decisiones de diseño.

## 1. Resumen del Proyecto

**Nombre:** Monitor → Enrich → Act
**Objetivo:** Capturar listings o productos desde múltiples fuentes (APIs, scrapers, CSVs, eventos), normalizar y enriquecer los registros, versionar y almacenar historial, exponer datos a un dashboard y activar acciones automáticas cuando se cumplan reglas de negocio.

## 2. Componentes Principales (Arquitectura Lógica)

1.  **Conectores / Orígenes:** APIs, scrapers, CSV uploads, webhooks.
2.  **Orquestador:** n8n para controlar triggers, rutas y llamadas a workers.
3.  **Ingesta / Workers:** Servicios Python (FastAPI) que realizan scraping, parsing y validaciones.
4.  **Enriquecimiento:** APIs externas y/o LLMs para normalización.
5.  **Almacenamiento:** Postgres (relacional + time series).
6.  **Procesamiento ETL:** Scripts para dedup, agregaciones, KPIs.
7.  **Acción / Outputs:** Dashboard (Metabase/Retool) + n8n flows → CRM / Email / Slack.
8.  **Observabilidad:** Logs centralizados, métricas, alertas.

## 3. Diseño de Datos (Esquema sugerido para Postgres)

```sql
-- Tabla principal de items
CREATE TABLE items (
    id SERIAL PRIMARY KEY,
    source_id VARCHAR(255),
    source_name VARCHAR(100),
    title TEXT,
    description TEXT,
    url TEXT,
    normalized_url TEXT,
    price DECIMAL,
    currency VARCHAR(10),
    -- ... otros campos ...
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabla para el historial de precios (Time-Series)
CREATE TABLE price_history (
    id SERIAL PRIMARY KEY,
    item_id INTEGER REFERENCES items(id),
    price DECIMAL,
    currency VARCHAR(10),
    recorded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabla para loguear las ingestiones
CREATE TABLE ingestion_log (
    id SERIAL PRIMARY KEY,
    source_name VARCHAR(100),
    status VARCHAR(50), -- 'success', 'failure'
    items_ingested INTEGER,
    error_message TEXT,
    executed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
