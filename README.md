# **Proyecto de Titulación MBD**
## **Maestría en Inteligencia de Negocios y Ciencia de Datos**
## **Universidad de las Américas**
## **Autor:** Andrés Esteban Ulloa Jaramillo

# Modelo Predictivo de la Demanda para la Optimización de Inventarios

Este repositorio contiene el código y el análisis para un modelo de predicción de demanda que busca optimizar los niveles de inventario en una empresa minorista. Utilizando datos de ventas unitarias diarias de tiendas Walmart, este proyecto implementa y compara tres modelos de pronóstico — ARIMA, SARIMA y Light Gradient Boosting Machine (LGBM) — para mejorar la planificación y gestión de inventarios.

### Problema a resolver:
La gestión de inventarios es un desafío crítico en la industria minorista, caracterizada por la volatilidad e incertidumbre de la demanda. Los modelos predictivos pueden ayudar a mitigar estos problemas al anticipar la demanda futura y evitar tanto el exceso de inventario como el desabastecimiento.

### Modelos seleccionados:
1. **ARIMA**: Un modelo de series temporales tradicional que utiliza componentes autorregresivos, de diferenciación y de promedio móvil para prever la demanda.
2. **SARIMA**: Una extensión de ARIMA que incorpora estacionalidad para capturar patrones periódicos en los datos.
3. **LGBM**: Un algoritmo de gradient boosting que incorpora variables explicativas y puede modelar relaciones no lineales, lo que le permite manejar conjuntos de datos complejos.

### Base de datos:
La base de datos empleada para el presente proyecto es pública y se puede encontrar en el siguiente enlace: [M5 Forecasting Accuracy Dataset en Kaggle](https://www.kaggle.com/c/m5-forecasting-accuracy/data)

Este proyecto utiliza el conjunto de datos M5, que proporciona datos de ventas diarias de productos de Walmart, para crear y validar modelos de predicción de demanda a nivel de categoría y de ítem. El objetivo principal es identificar el modelo más efectivo para predecir la demanda en un entorno minorista complejo e integrar las predicciones en los sistemas de gestión de inventarios.

## Metodología

El proceso de preparación de datos incluye la unión de múltiples tablas, el filtrado por tienda y rango de tiempo, y el manejo de valores faltantes. Además, se aplicaron técnicas de ingeniería de características para mejorar el rendimiento de LGBM, añadiendo datos de ventas retrasadas, promedios móviles e indicadores temporales categóricos.

## Datos

El conjunto de datos, M5, está disponible públicamente en Kaggle y contiene datos de ventas unitarias diarias de Walmart en tres estados de EE.UU.: California, Texas y Wisconsin. Los productos están clasificados por departamento e ítem, lo que permite realizar pronósticos a diferentes niveles de granularidad.

### Pasos de Procesamiento de Datos:
- **Consolidación**: Unión de tablas de historial de ventas, precios y fechas.
- **Filtrado**: Selección de datos de una tienda en California y reducción a los últimos tres años.
- **Imputación**: Relleno de valores faltantes en precios e indicadores binarios de eventos.
- **Ingeniería de Características**: Creación de variables de rezago, promedios móviles, ventas acumuladas e interacciones para los modelos LGBM.

## Selección y Evaluación de Modelos

Cada modelo fue evaluado con dos métricas:
- **Error Absoluto Medio (MAE)**: Promedio de las diferencias absolutas entre los valores predichos y reales.
- **Error Cuadrático Medio (RMSE)**: Raíz cuadrada del promedio de las diferencias al cuadrado, dando mayor peso a errores grandes.

Resumen de Resultados:
- **ARIMA y SARIMA**: Adecuados para captar patrones generales, pero con dificultades para manejar la alta variabilidad en los datos.
- **LGBM**: Proporcionó la mayor precisión y fue capaz de ajustarse a patrones de demanda irregulares con la inclusión de características adicionales.

### Mejores Parámetros

| Modelo | Nivel        | MAE    | RMSE  |
|--------|--------------|--------|-------|
| ARIMA (5,0,5)  | Categoría   | 517.47 | 666.80 |
| SARIMA (0,0,1)(1,0,2)[7] | Categoría | 296.82 | 404.99 |
| LGBM (Optimizado) | Categoría | **135.25** | **176.01** |
| ARIMA (7,1,1)  | Ítem       | 5.72   | 7.18  |
| SARIMA (3,0,1)(1,0,1)[7] | Ítem | 5.55 | 6.99 |
| LGBM (Optimizado) | Ítem     | **3.21** | **4.13** |

## Resultados e Insights

- **LGBM Supera a los Modelos Tradicionales**: Debido a su capacidad para capturar relaciones no lineales y manejar alta variabilidad, LGBM alcanzó consistentemente las tasas de error más bajas.
- **Patrones Estacionales y Temporales**: Se observó un aumento en las ventas durante los fines de semana y en ciertos meses, como agosto, mientras que enero y febrero mostraron niveles de demanda más bajos.
- **Integración en la Gestión de Inventarios**: Las predicciones del modelo pueden integrarse con un sistema de gestión de inventarios para establecer niveles óptimos de stock, con recomendaciones para ajustar el inventario basado en fluctuaciones predichas.

### Cómo usar el Notebook para replicar los resultados:
1. Clona el repositorio:
   ```bash
   git clone https://github.com/usuario/modelo-prediccion-demanda-optimizacion-inventarios.git
   cd modelo-prediccion-demanda-optimizacion-inventarios
   ```

2. Instala las dependencias:
   ```bash
   pip install -r requirements.txt
   ```

3. Ejecuta el Jupyter Notebook:
   Abre `4_prediccion_demanda_final.ipynb` para ver y ejecutar el código de preprocesamiento de datos, entrenamiento de modelos y evaluación.

## Trabajo Futuro

- **Ajustes Automatizados de Inventario**: Incorporar un sistema dinámico para actualizar los umbrales de inventario basados en predicciones de demanda en tiempo real.
- **Integración de Datos Externos**: Incluir variables externas (como indicadores económicos) para mejorar la precisión de las predicciones.
- **Escalabilidad**: Adaptar el modelo para su uso en múltiples tiendas y categorías de productos.

## Contribuciones

¡Las contribuciones son bienvenidas! Haz un fork del repositorio y envía un pull request para cualquier cambio o mejora propuesta.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT.

---

Este repositorio apoya la tesis: "MODELO PREDICTIVO DE LA DEMANDA UTILIZANDO ARIMA, SARIMA Y LGBM PARA OPTIMIZAR LOS NIVELES DE INVENTARIO EN UNA EMPRESA MINORISTA," de Andrés Esteban Ulloa Jaramillo.
