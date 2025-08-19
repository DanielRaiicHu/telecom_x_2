# Proyecto: Telecom X - Parte 2

Este proyecto corresponde al **segundo desafío** de la serie **Telecom X**, una empresa ficticia de telecomunicaciones que enfrenta un problema crítico: la **evasión de clientes (churn)**.  
Mientras que en la **Parte 1** se trabajó principalmente en la **extracción, limpieza, transformación y análisis exploratorio de datos (EDA)**, en esta segunda fase avanzamos hacia la **construcción, validación e interpretación de modelos predictivos**, con el objetivo de anticipar qué clientes presentan mayor riesgo de abandonar el servicio.

---

##  Objetivo

El propósito de este proyecto es **construir un modelo de predicción de evasión de clientes** capaz de identificar patrones clave y anticipar la decisión de los usuarios. Con esto, la empresa puede diseñar **estrategias de retención más efectivas**, disminuyendo pérdidas económicas y mejorando la sostenibilidad del negocio.

---

##  Acceso al Proyecto

-  Repositorio completo en GitHub:  
   [Proyecto Telecom X - Parte 2](https://github.com/DanielRaiicHu/telecom_x_2/tree/main)

-  Notebook del proyecto (ejecutable en Google Colab o Jupyter):  
   [Notebook: telecom_x_2.ipynb](https://github.com/DanielRaiicHu/telecom_x_2/blob/main/telecom_x_2.ipynb)

-  Base de datos tratada (dataset utilizado en el análisis y modelado):  
   [datos_tratados.csv](https://raw.githubusercontent.com/DanielRaiicHu/telecom_x_2/main/datos_tratados.csv)

-  Modelo final entrenado (Champion Model, exportado en formato `.pkl`):  
   [modelo_champion.pkl](https://github.com/DanielRaiicHu/telecom_x_2/blob/main/modelo_champion.pkl)

-  Gráficos exportados del proyecto:  
   [Carpeta de gráficos](https://github.com/DanielRaiicHu/telecom_x_2/tree/main/graficos_del_proyecto)

-  Notebook del proyecto — Desafío 1 (base inicial de preparación de datos):  
   [Notebook: TelecomX.ipynb](https://github.com/DanielRaiicHu/TelecomX/blob/main/TelecomX.ipynb)

---

##  Ejecución del Proyecto

Este proyecto puede ser ejecutado en **Google Colab** (recomendado) o en un entorno local con **Jupyter Notebook**.  

1. **Abrir el Notebook en Google Colab**  
   - Accede al archivo principal desde [aquí](https://github.com/DanielRaiicHu/telecom_x_2/blob/main/telecom_x_2.ipynb).  
   - Haz clic en el botón `Open in Colab` (o copia el código en un nuevo notebook en Colab).  

2. **Cargar los datos tratados**  
   - El dataset `datos_tratados.csv` ya está disponible en el repositorio.  
   - Al ejecutar las celdas iniciales del notebook, se cargará automáticamente.  

3. **Ejecutar el análisis paso a paso**  
   - Cada celda del notebook contiene explicaciones, visualizaciones y resultados.  
   - No se requieren conocimientos avanzados de programación: basta con ejecutar las celdas en orden.  

4. **Explorar el modelo entrenado**  
   - El modelo final (Champion) se encuentra guardado en `modelo_champion.pkl`.  
   - En el notebook se muestra cómo cargarlo, realizar predicciones y analizar resultados.  

---

##  Estructura del Proyecto

El análisis está organizado en **módulos progresivos**, cada uno con objetivos específicos:

### 1. Preparación de los datos
- Importación de librerías y definición de paleta de colores.  
- Extracción de `datos_tratados.csv` (dataset trabajado en el Desafío 1).  
- Eliminación de columnas irrelevantes y tratamiento de variables binarias.  
- Codificación de variables categóricas con `OneHotEncoder`.  

### 2. Análisis exploratorio (EDA)
- Verificación de la proporción de la variable respuesta (**Evasión**).  
- Análisis de variables categóricas y numéricas con gráficos comparativos.  
- Mapas de calor de correlación entre variables, incluyendo la relación con evasión bajo distintos **umbrales**.  
- Estudio de multicolinealidad y comportamiento de la **antigüedad (12 meses)**.  

### 3. Entrenamiento de modelos
- Separación de variables explicativas y de respuesta en conjuntos de **entrenamiento, validación y prueba**.  
- Normalización de datos.  
- Entrenamiento con distintos algoritmos de clasificación.  
- Evaluación mediante:  
  - Matriz de confusión.  
  - Métricas (precisión, recall, accuracy, F1-score).  
  - Curvas ROC y PRC, métricas AUC y AP.  

### 4. Validación y confianza del modelo
- Uso de **validación cruzada con K-Fold y StratifiedKFold**.  
- Intervalos de confianza para métricas, en especial **recall**, evaluando diferentes **umbrales (0.3, 0.4, 0.5)**.  

### 5. Selección del Modelo Champion
- Optimización de hiperparámetros con **GridSearchCV**.  
- Comparación del rendimiento bajo distintos umbrales.  
- Selección del modelo final con **umbral = 0.3**, priorizando recall (detección de clientes en riesgo).  

### 6. Pruebas con nuevos registros
- Predicción sobre 5 registros reales del dataset original.  
- Simulación de registros inventados en el límite de evasión/permanencia para verificar la robustez del modelo.  
- Interpretación de resultados en escenarios prácticos.  

### 7. Interpretabilidad del modelo
- Análisis de **importancia de características (Feature Importance)**.  
- Identificación de las variables que más influyen en la evasión, como:  
  - Tipo de contrato (mensual vs largo plazo).  
  - Antigüedad.  
  - Servicios de Internet (Fibra óptica).  
  - Cargos totales y mensuales.  

---

##  Estructura de los Datos

El archivo `datos_tratados.csv` es la **base ya preprocesada** en el Desafío 1, lista para entrenar modelos.  
Las columnas principales incluyen:

- **Demográficas y contractuales**:  
  - `Genero` (Masculino/Femenino)  
  - `AdultoMayor` (Sí/No)  
  - `TienePareja`, `Dependientes`  
  - `TipoContrato` (Mensual, Un año, Dos años)  
  - `MetodoPago` (Cheque, Tarjeta, Débito automático, etc.)  

- **Servicios contratados**:  
  - `ServicioTelefonico`, `LineasMultiples`, `ServicioInternet` (DSL, Fibra óptica, Ninguno)  
  - Servicios adicionales: `SeguridadEnLinea`, `RespaldoEnLinea`, `ProteccionDispositivo`, `SoporteTecnico`, `StreamingTV`, `StreamingPeliculas`  

- **Variables numéricas**:  
  - `MesesAntiguedad` (tiempo como cliente)  
  - `CargoMensual`  
  - `CargoTotal`  
  - `CuentasDiarias` (nueva variable creada en el preprocesamiento)  

- **Variable de respuesta**:  
  - `Evasion` (Sí/No)  

 Este dataset ya está limpio, codificado y traducido al español, lo que facilita tanto el análisis exploratorio como la construcción de modelos predictivos.

---

##  Conclusión

Este **Desafío 2** consolida el trabajo iniciado en la primera parte del proyecto, pasando de un **EDA descriptivo** a un **modelo predictivo funcional**.  

- La empresa ahora cuenta con una **herramienta de predicción** que no solo explica patrones históricos de evasión, sino que **anticipa clientes en riesgo**.  
- El modelo seleccionado (Random Forest con umbral 0.3) logra un buen **balance entre recall y precisión**, favoreciendo la detección de casos de abandono aunque implique ciertos falsos positivos.  
- A través de las pruebas con nuevos registros, se validó la **aplicabilidad práctica** del modelo.  
- El análisis de importancia de variables permite comprender qué factores son determinantes en la decisión de los clientes, aportando un insumo estratégico para diseñar campañas de retención.  

En conjunto, este proyecto no solo es un ejercicio académico, sino un **caso práctico aplicable a empresas reales**, demostrando cómo los datos y la inteligencia artificial pueden convertirse en aliados clave para la toma de decisiones.  

---

##  Agradecimientos

Este proyecto fue desarrollado en el marco del programa **ONE - Oracle Next Education (Alura Latam)**.  

Un especial agradecimiento a todos quienes hacen posible este proceso de aprendizaje:  

- Profesores e instructores:  
  **Álvaro Camacho, Wilfredo Rojas, Ingrid Silva, Leti Farias, Christian Velasco, Leonardo Castillo, Alejandro Gamarra, João Henrique Gonçalves, Erika Bellido, Alia Garrudo**.  

- Profesores de emprendimiento:  
  **Gabriela Aguiar, Priscila Stuani**.  

- A **Luri**, que me ayudó y sacó de apuros en más de una ocasión.  

- A la comunidad de **Discord ONE G8 LAD Data Science**, por el apoyo y colaboración constante.  

- Y a todos quienes contribuyen día a día para hacer de este programa una oportunidad transformadora.  

---

##  Autor

**Daniel Aranzáez A.**  
Proyecto Final - Telecom X Parte 2  
2025
