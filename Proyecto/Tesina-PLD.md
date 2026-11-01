# PLD-Agent — Decisiones y estado del proyecto

Tesis de la Maestría en Ciencia de Datos, UANL. Documento de trabajo con lo afirmado y decidido hasta el 1 de noviembre de 2026.

## Contenido

1. [Visión general](#1-visión-general)
2. [Alcance](#2-alcance)
3. [Datos](#3-datos)
4. [Diseño del sistema](#4-diseño-del-sistema)
5. [Evaluación](#5-evaluación)
6. [Objetivos adoptados (capítulo 4)](#6-objetivos-adoptados-capítulo-4)
7. [Cómo se escribe la tesis](#7-cómo-se-escribe-la-tesis)
8. [Reglas de formato y entrega](#8-reglas-de-formato-y-entrega)
9. [Fuentes y referencias](#9-fuentes-y-referencias)
10. [Repositorio y entorno](#10-repositorio-y-entorno)
11. [Pendientes](#11-pendientes)
12. [Lo que no se ha definido todavía](#12-lo-que-no-se-ha-definido-todavía)

---

## 1. Visión general

- **Nombre del proyecto:** PLD-Agent (antes "SentinelPLD"; en adelante se llama PLD-Agent). Antes se había adoptado "CreditSentry" (riesgo crediticio) y se cambió por este tema.
- **Qué es:** un sistema multiagente de IA (con modelos de lenguaje) que **vigila un modelo de detección de lavado de dinero (PLD/AML)**, detecta cuándo pierde eficacia y diagnostica la causa.
- **Idea central:** un modelo de detección de lavado se degrada en producción sin que nadie lo note. El monitoreo tradicional (reglas y umbrales fijos) detecta tarde y no explica la causa. El proyecto evalúa si un sistema de agentes lo hace mejor.
- **Programa:** Maestría en Ciencia de Datos, UANL. Es para los tetramestres 5 y 6 (Anteproyecto de Tesis, Proyecto de Consultoría y Producto Integrador).
- **Director de tesis:** Dr. José de Jesús Rocha Salazar. Ya se tomaron con él Deep Learning y Business Intelligence.
- **Clase del anteproyecto:** Dra. Azucena Yoloxóchitl Ríos Mercado.
- **Meta de publicación:** ACM CAIS 2027, o un congreso equivalente de sistemas de IA y MLOps.

## 2. Alcance

**Sí incluye:** detección de la pérdida de eficacia y diagnóstico de su causa, en un entorno de producción simulado, comparado con el monitoreo tradicional.

**No incluye:**
- Financiamiento al terrorismo.
- Modificación automática del modelo.
- Reporte a la autoridad.

## 3. Datos

| Conjunto | Uso |
|---|---|
| **HI-Small** | Desarrollo. Todo se construye y depura aquí y luego se **congela**. |
| **HI-Large** | Evaluación principal. |
| **LI-Large** | Replicación. |

- **Fuente:** IBM AMLworld, un conjunto **sintético** (Altman et ál., 2023). Se dice con honestidad que es sintético.
- **Partición cronológica 60/20/20.** Se ordena por fecha, sin mezclar.
- **Ventaja que se usa:** los datos traen "verdad conocida", es decir, se sabe qué operaciones son lavado.
- **Dónde se describe:** en Metodología, no en la justificación.
- Se descargaron también las versiones Medium y LI-Small, pero **no están en el plan**.
- **Orden de trabajo:** primero se elige el dataset y después se delimita el problema (porque el Dr. de Consultoría dijo que ya se debía tener el dataset).

## 4. Diseño del sistema

> **Arquitectura pendiente.** Hay ideas nuevas que se van a aterrizar primero y después se presentarán. Lo que sigue es la versión anterior y puede cambiar.

**Reparto de trabajo (versión anterior):** las herramientas en **PySpark** calculan las métricas, y los **agentes LLM razonan**. La orquestación es código normal, sin IA.

**Agentes:** detección, diagnóstico, reporte y juez.

**Modelo base: por definir.** El Dr. recomendó usar **autoencoders**. Ya no se da por decidido el gradient boosting, porque no hay convicción de usarlo.

**Escenarios de drift:** se inyectan a propósito, con una taxonomía **causa × forma temporal × magnitud**, de tipos típicos en lavado de dinero. Como se provocan, se conoce la causa real y se puede verificar si el sistema acierta.

**Las cinco configuraciones a comparar:**

| # | Configuración |
|---|---|
| 1 | Umbrales fijos (monitoreo tradicional) |
| 2 | Pipeline determinista, sin LLM |
| 3 | Agente único |
| 4 | Multiagente completo |
| 5 | Multiagente sin juez |

**Dos modos:** sin etiquetas, y con etiquetas retrasadas.

## 5. Evaluación

- Se desarrolla en HI-Small y se congela.
- Después se evalúa en HI-Large y se replica en LI-Large.
- Corridas repetidas, intervalos de confianza y pruebas no paramétricas.

## 6. Objetivos adoptados (capítulo 4)

**General:** *Evaluar en qué medida un sistema de agentes de inteligencia artificial detecta a tiempo y explica la pérdida de eficacia de un modelo de detección de lavado de dinero, en comparación con el monitoreo tradicional basado en reglas y umbrales fijos, en un entorno de producción simulado, para aportar evidencia sobre su utilidad en la vigilancia de estos modelos.*

**Específicos:**
1. Establecer escenarios simulados en los que un modelo de detección de lavado de dinero pierde eficacia por causas conocidas, para contar con referencias contra las cuales verificar la detección y el diagnóstico.
2. Determinar el tiempo con que el sistema de agentes detecta la pérdida de eficacia y la proporción de causas que identifica correctamente, para medir su oportunidad y exactitud.
3. Contrastar el desempeño del sistema de agentes con el del monitoreo tradicional en esos mismos escenarios, para identificar en qué condiciones ofrece una ventaja.

La Dra. observó que al objetivo general le faltaba la finalidad (el "para qué"), y ya se agregó.

## 7. Cómo se escribe la tesis

- **Capítulo 2 (Planteamiento):** sin subsecciones, párrafos continuos. P1 contexto, P2 respuesta global (GAFI), P3 México, P4 delimitación sin tecnicismos ni "drift", P5 solo la pregunta de investigación.
- **Capítulo 3 (Justificación, 1-2 cuartillas), 4 párrafos:** (1) relevancia con cifras nuevas, (2) beneficiarios, (3) aporte científico y vigencia de los agentes, (4) factibilidad. Sin "cómo".
- **Cifras de sanciones:** del exporte del portal de la CNBV (2022-2025). Se descartaron la prensa y JAAK como fuentes.
- **Capítulo 5 (Marco Teórico), por método de índices:**
  - 5.1 Lavado de dinero y detección de operaciones sospechosas (5.1.1-5.1.3)
  - 5.2 Modelos de aprendizaje automático para la detección (5.2.1-5.2.3)
  - 5.3 Pérdida de eficacia de los modelos en producción (5.3.1-5.3.4)
  - 5.4 Agentes de inteligencia artificial (5.4.1-5.4.3)
  - 5.5 Trabajos relacionados, con tabla comparativa

## 8. Reglas de formato y entrega

- Plantilla institucional, formato APA 7, sin alterar el formato de la plantilla.
- Títulos en Title Case. Nivel 1 a 1 tab y nivel 2 a 2 tabs (1.25 cm y 2.50 cm).
- Entrega en Word y PDF, con el mismo nombre: "ANTEPROYECTO AV4 + nombre completo".

## 9. Fuentes y referencias

- **Criterio de fuentes:** primero artículos revisados por pares (sin blogs). Páginas oficiales vigentes solo si es necesario. Enlaces aparte, sin links en la bibliografía.
- **Aprobadas:** Altman, Jensen y Iosifidis, Mohamed, Pirmorad (preprint), Sethi, Wang, Dal Pozzolo, Gama, Lu, Rabanser, Rocha-Salazar, FATF, UIF, CNBV, Núñez Camacho, Blanco Cordero, Albanese, UNODC, Zhang y Trubey (solo "como se citó en").
- **No citar:** Bhuiyan (2026).

## 10. Repositorio y entorno

- Repositorio solo para el proyecto, en la carpeta `PLD-Agent`, trabajado en VS Code sobre Windows. Privado.
- Gestión de dependencias con **uv** y `pyproject.toml`. **pandas fijado a menos de 3** por compatibilidad con PySpark.
- Paquete de Python: **`pld_agent`** (con guion bajo, porque el guion impide importarlo). Subcarpetas: `data`, `model`, `drift`, `monitoring`, `agents`, `experiments`, `evaluation`.
- Otras carpetas: `configs`, `tests`, `scripts`, `docs`, `notebooks`.
- **Secretos:** `.env` ignorado, `.env.example` versionado, y **pre-commit con gitleaks** para bloquear llaves.
- **Datos:** viven en `data/` en la raíz del repo. Git ignora su contenido, **salvo el README** de esa carpeta, que sí se versiona.
- **Local primero** (HI-Small con Spark) y **nube (GCP) para HI-Large y LI-Large**.
- Java 17 y Spark 4.1.1 ya funcionan en la máquina.
- **Snowflake:** se quiere trabajar con él durante el proyecto. Todavía no se sabe en qué parte; está **en veremos**.
- Dónde va cada cosa: `scripts/` para revisiones puntuales, `notebooks/` para exploración, `src/pld_agent/` para código reutilizable.

## 11. Pendientes

**Del repositorio y del código**
- Cargador de datos y partición 60/20/20. Falta pegar las 3 primeras líneas de `data\HI-Small_Trans.csv`.
- Definir la **arquitectura** (pendiente de aterrizar las ideas y presentarlas).
- Decidir el **modelo base** (autoencoders recomendados por el Dr. frente a gradient boosting).
- Decidir **dónde entra Snowflake**.
- Después: modelo base, escenarios de drift, herramientas de métricas, agentes.
- Alerta de presupuesto en GCP antes de gastar.

**Del anteproyecto**
- **Auditoría de referencias** (recordatorio pedido): fichas de Sethi, Wang, Pirmorad, Altman, Jensen y Iosifidis, Rocha-Salazar, Albanese, Blanco Cordero y CNBV; formato de "Recuperado el"; orden alfabético; cifras de segunda mano (98% y 34 de 6,113).
- **Correcciones del AV4:** "eficiencia" por "eficacia" en el objetivo específico 2 y en los títulos 5.3 y 5.3.4 del cuerpo.

**De la literatura**
- Búsqueda cerrada hasta que se reabra (novedad en Scopus/IEEE/ACM, consulta al Dr. Rocha, fuentes para 5.2.1, 5.2.2, 5.4.1 y 5.4.3).

## 12. Lo que no se ha definido todavía

Estos puntos no aparecen decididos, así que no se dan por hechos:

- Qué modelo de lenguaje se usará para los agentes (proveedor y versión).
- Qué modelo base se usará (autoencoders o gradient boosting) y con qué librería.
- La arquitectura final del sistema.
- En qué parte del proyecto se usará Snowflake.
- La lista concreta de escenarios de drift (qué causas, formas y magnitudes).
- Las métricas exactas, el número de repeticiones y qué pruebas no paramétricas.
- Cuánto costará la nube y qué presupuesto se pondrá.
- La novedad del trabajo, que sigue sin confirmarse con una búsqueda formal.