# Masterclass Data Analytics con Python — Academia MC

Materiales de la masterclass gratuita del domingo 25 de octubre de 2026.

Los tres proyectos responden la **misma pregunta de negocio** sobre el **mismo archivo de ventas**: *¿cómo venimos y en qué mes vendimos más?* Cada uno usa una herramienta distinta.

| # | Archivo | Herramienta | Qué hace |
|---|---------|-------------|----------|
| 1 | [`notebook_pandas.ipynb`](notebook_pandas.ipynb) | Python + Pandas | Carga el CSV, convierte fechas, trata los montos faltantes y agrupa las ventas por mes con un gráfico |
| 2 | [`analisis_sql.sql`](analisis_sql.sql) | PostgreSQL | Resuelve la misma pregunta con una consulta `GROUP BY`. Los resultados coinciden con los de Pandas |
| 3 | [`mini_reporte_ia.ipynb`](mini_reporte_ia.ipynb) | Python + IA | Calcula 3 indicadores y le pide a una IA que redacte una explicación. Después la verifica contra los datos |

Los datos están en [`ventas.csv`](ventas.csv): 1850 ventas entre septiembre de 2025 y octubre de 2026. Cada fila es un ticket.

## Cómo usar los notebooks (Google Colab)

1. Abrí el notebook directamente en Colab:
   - [Abrir `notebook_pandas.ipynb` en Colab](https://colab.research.google.com/github/Academia-Mariana-Casella/masterclass-data-analytics-python/blob/main/notebook_pandas.ipynb)
   - [Abrir `mini_reporte_ia.ipynb` en Colab](https://colab.research.google.com/github/Academia-Mariana-Casella/masterclass-data-analytics-python/blob/main/mini_reporte_ia.ipynb)
2. Descargá [`ventas.csv`](https://raw.githubusercontent.com/Academia-Mariana-Casella/masterclass-data-analytics-python/main/ventas.csv) (clic derecho → *Guardar como*).
3. En Colab, abrí el ícono de carpeta de la izquierda y subí `ventas.csv`.
4. Ejecutá las celdas en orden (`Shift + Enter`).

> Cada notebook de Colab tiene su propia sesión, así que hay que subir el CSV en cada uno. Si la sesión se reinicia, también hay que volver a subirlo.

Si preferís trabajar en tu compu, necesitás Python 3 con `pandas` y `matplotlib`, y el CSV en la misma carpeta que el notebook.

## Cómo usar el archivo SQL (PostgreSQL)

Desde la carpeta donde están los archivos, corré el script completo con `psql`:

```bash
psql -d tu_base -f analisis_sql.sql
```

La primera parte crea la tabla `ventas` y la carga desde el CSV. El resto son las consultas.

- Ojo: al principio del script hay un `DROP TABLE ventas`, que borra la tabla si ya existe.
- `\COPY` es un comando de `psql`. En pgAdmin o DBeaver no funciona; ahí usá la opción de importar CSV.
- En Windows, si los acentos se ven mal, ejecutá `set PGCLIENTENCODING=UTF8` en la misma consola antes de correr el script.

## Sobre la parte de IA

En `mini_reporte_ia.ipynb`, la respuesta de la IA es **una ejecución guardada de antemano**: el notebook no llama a ninguna API. A la IA se le pasa **solo el resumen numérico**, nunca el archivo completo. La idea central es que la IA redacta y la persona analista verifica.
