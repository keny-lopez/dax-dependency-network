# 🔗 Red de Dependencias de Medidas DAX

**Visualizador interactivo de dependencias para modelos semánticos Power BI**

[![Demo en vivo](https://img.shields.io/badge/Demo-Live-brightgreen)](https://keny-lopez.github.io/dax-dependency-network/)
[![Licencia MIT](https://img.shields.io/badge/Licencia-MIT-blue)](LICENSE)
[![Power BI](https://img.shields.io/badge/Power%20BI-External%20Tool-F2C811)](https://powerbi.microsoft.com/)

**[▶ Ver demo en vivo](https://keny-lopez.github.io/dax-dependency-network/)**

---

## El problema

Los modelos semánticos de Power BI crecen sin control. Después de meses 
de desarrollo, nadie sabe con certeza qué medidas sostienen el modelo, 
cuáles están obsoletas, ni qué ocurre si modificas una medida base. 
Hacer ese análisis manualmente en modelos de 50+ medidas toma días 
y es propenso a errores críticos.

## La solución

Herramienta de visualización interactiva que convierte los metadatos 
exportados por **Measure Killer** en un grafo de dependencias navegable, 
filtrable y portable — un archivo HTML standalone que funciona en 
cualquier navegador sin instalaciones ni licencias.

## ¿Qué puedes detectar con ella?

- ✅ Medidas críticas que sostienen el modelo (hubs de alta conectividad)
- ✅ Medidas sin uso — deuda técnica eliminable con seguridad
- ✅ Cadenas de dependencia a 1, 2 y 3 niveles de profundidad
- ✅ Distribución del modelo por carpeta DAX y tier de criticidad
- ✅ Impacto potencial antes de modificar cualquier medida base

## Stack técnico

| Tecnología | Uso |
|---|---|
| `D3.js v7` | Grafo de fuerzas interactivo |
| `HTML / CSS / JS` | Sin frameworks, sin dependencias en runtime |
| `Python` | ETL de metadatos desde CSV de Measure Killer |
| `Measure Killer` | Extracción de metadatos del modelo semántico |

## Lectura visual del grafo

| Elemento | Significado |
|---|---|
| **Tamaño del nodo** | Número total de usos en el modelo |
| **Color del borde** | Tier de criticidad: 🔴 Crítica · 🟠 Alto · 🟡 Medio · 🟢 Bajo · ⚪ Sin uso |
| **Color de relleno** | Carpeta DAX a la que pertenece la medida |
| **Dirección de flecha** | A → B significa que A referencia a B en su fórmula DAX |

## Cómo actualizar con un nuevo modelo
```bash
# 1. Exporta el CSV desde Measure Killer con estas columnas:
#    Prefijo_Medida, Nombre_Medida, Carpeta_Visualizacion,
#    Estado, Num_Usos, Tier, TipoObj_EnElQueSeUsa, Nombre_Uso, Tipo_Dato

# 2. Ejecuta el script ETL para generar NODES y EDGES
python etl_measure_killer.py

# 3. Reemplaza los bloques de datos en index.html
# 4. Commit y push — GitHub Pages se actualiza automáticamente
```

## Funcionalidades

- 🔍 **Búsqueda** por nombre de medida en tiempo real
- 🎯 **Filtros** por tier de criticidad, carpeta y estado de uso
- 📐 **Profundidad** de dependencias configurable (1, 2 o 3 niveles)
- 🌙 **Modo oscuro / claro** con un clic
- 🗺️ **Minimapa** para navegación en modelos grandes
- 📤 **Exportación** a SVG
- ⚙️ **Física** del grafo ajustable (repulsión, longitud de enlaces, gravedad)
- 📱 **Responsive** — funciona en móvil y desktop

## Requisitos para reproducirlo

- Measure Killer instalado como External Tool en Power BI Desktop
- Python 3.x con librería `csv` (incluida en stdlib)
- Cualquier navegador moderno para visualizar el resultado

---

## Autor

**Keny López**  
Data Analyst · Microsoft Certified Power BI Data Analyst Associate  
Analista Geoespacial · Python · R · Candidato a Científico de Datos  
Tegucigalpa, Honduras

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Keny%20López-0077B5)](https://www.linkedin.com/in/kenylopez-data-analyst/)

---

*Desarrollado como herramienta de auditoría y documentación de modelos 
semánticos Power BI. Reutilizable en cualquier proyecto que use 
Measure Killer como fuente de metadatos.*
```
