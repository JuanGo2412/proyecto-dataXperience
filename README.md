# 📊 DataXperience KINNUX
### Análisis de ventas y comportamiento comercial mediante Ciencia de Datos

Proyecto final del curso **Ciencia de Datos: Aplicando lo aprendido**. Analizamos registros comerciales reales (anonimizados) de **KINNUX S.A.S.** aplicando las tres etapas del curso: preparación de datos, estadística descriptiva y modelado con storytelling.

## 👥 Integrantes
- Juan Sebastian Gomez Clavijo
- [Nombre completo 2] —

## 🎥 Video de presentación
**Enlace:** [PEGAR AQUÍ EL ENLACE PÚBLICO AL VIDEO]  (duración: 2–5 min)

## 🎯 Contexto y objetivo
KINNUX S.A.S. registra sus movimientos comerciales (ventas y obsequios) con información incompleta en varios campos. El objetivo es **limpiar esos datos, entender cómo se comportan las ventas y estimar el valor de un pedido a partir de la cantidad**, para apoyar decisiones de inventario, cobro y registro.

Los datos son registros reales anonimizados (`CLI_xxx`, `ASE_xx`). Existe además una base ampliada con datos sintéticos, usada solo con fines académicos.

## 📁 Estructura del repositorio
```
proyecto-dataXperience/
├── README.md
├── datos/            ← Data Frame.xlsx (181 registros, 13 variables) y versión limpia
├── notebook/         ← DataXperience_KINNUX.ipynb (Google Colab)
├── presentacion/     ← DataXperience_KINNUX_presentacion (PPTX y PDF)
└── video/            ← enlace y guion del video
```

## 🔎 Resumen por etapas

### Etapa 1 · Fundamentos y preparación de datos
- 181 registros × 13 variables; 0 filas duplicadas.
- Valores faltantes: `Producto` (2), `Tipo` (11), `Valor_Total_COP` (50), `Cliente_ID` (2) y `Cantidad` (2).
- Decisiones: categoría `NO_REGISTRADO` cuando no hay información suficiente, `$0` solo para obsequios, y nulos conservados en `Cantidad` (2) y `Valor_Total_COP` (46) para **no inventar datos**.
- Los 11 registros sin `Tipo` pertenecen al pedido `PED_R0099`: un fallo puntual, no generalizado.

### Etapa 2 · Estadística descriptiva
| Métrica | Valor total (COP) | Cantidad |
|---|---:|---:|
| Media | 381.841 | 9,39 |
| Mediana | 174.000 | 2 |
| Moda | 0 | 1 |
| Desv. estándar | 688.182 | 30,42 |
| Rango | 0 – 4.000.000 | 1 – 300 |

- Distribución sesgada a la derecha; los outliers (> $728.250) parecen pedidos mayoristas.
- Correlación cantidad–valor ≈ 0,35. Hipótesis: existen perfiles de cliente detal y mayorista.

### Etapa 3 · Modelado y storytelling
- **NGYPLUS** concentra ≈ 63 % del recaudo pagado ($24,86 M de $39,55 M); **septiembre** fue el mejor mes ($22,25 M); no hay datos de agosto.
- Cartera pendiente: $11,99 M (≈ 23 % del valor registrado).
- **Regresión lineal** (cantidad → valor), 80 % entrenamiento / 20 % prueba:

| Modelo | Error promedio (MAE) | R² |
|---|---:|---:|
| General (todos los productos) | $937.865 | −29,02 |
| Solo NGYPLUS | $80.903 | 0,98 |

  Ejemplo: 10 unidades de NGYPLUS ≈ $743.657 COP. El modelo de NGYPLUS no debe usarse para otros productos y se entrenó con pocos registros.

## 💼 Aplicación profesional
Campos obligatorios (valor, producto, canal, tipo de cliente), control periódico de cartera pendiente, dashboard de ventas para planear inventario y cotizaciones asistidas por modelos por producto.

## ▶️ Cómo ejecutar
1. Abre `notebook/DataXperience_KINNUX.ipynb` en Google Colab.
2. El cuaderno lee los datos desde `datos/Data Frame.xlsx` de este repositorio (hoja `00_Base_Anonimizada`); el repositorio debe ser **público**.
3. Ejecuta todas las celdas (Entorno de ejecución → Ejecutar todo).

Librerías: `pandas`, `numpy`, `matplotlib`, `scikit-learn`.
