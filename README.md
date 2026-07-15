# telecom-analysis
Análisis integral y segmentación de clientes para ConnectaTel con Python. Este proyecto abarca la auditoría y calidad de datos (tratamiento de nulos y centinelas), EDA con Seaborn, detección de outliers mediante IQR y segmentación de usuarios por edad y nivel de consumo, derivando en recomendaciones comerciales para el negocio.
Este repositorio contiene el desarrollo del proyecto de análisis de datos y segmentación de clientes para la empresa de telecomunicaciones ConnectaTel. A través de un enfoque estructurado de ciencia de datos, se auditaron los registros, se trataron inconsistencias estadísticas y se segmentó a la base de usuarios para proponer estrategias comerciales de alto impacto.

---

## Objetivo del Proyecto
El principal objetivo de este proyecto es realizar un análisis de datos de extremo a extremo (End-to-End) para:
1. **Auditar y corregir** problemas de calidad de datos en la base de usuarios y su consumo mensual.
2. **Identificar y caracterizar** los perfiles de comportamiento de los clientes según variables demográficas (edad) y transaccionales (mensajes, llamadas y minutos).
3. **Proponer recomendaciones comerciales accionables** orientadas a la optimización de planes (Upselling) y fidelización de nichos de alto valor.

---

## Datasets Utilizados
El análisis integra y cruza datos de dos fuentes principales:

1. **`user_profile` (Perfil del Cliente):**
   * Contiene datos demográficos y de suscripción de los usuarios.
   * *Columnas clave:* `user_id` (identificador único), `age` (edad), `plan` (tipo de plan contratado: Básico o Premium).
2. **`usage` (Historial de Consumo):**
   * Contiene el detalle transaccional de las interacciones realizadas.
   * *Columnas clave:* `user_id`, `type` (tipo de interacción: *call* o *text*), `duration` (duración en minutos de las llamadas), `length` (longitud en caracteres de los mensajes de texto).

---

## Etapas del Análisis Realizadas

### 1. Auditoría y Calidad de Datos (Data Cleansing)
* **Tratamiento de Valores Centinela:** Identificación del valor atípico `-999` en la variable `age` (2.0% de la muestra) e imputación controlada utilizando la mediana de la edad para preservar la distribución original de la base.
* **Análisis de Datos Faltantes (MAR):** Diagnóstico de registros nulos en las variables de consumo, demostrando que corresponden al tipo *Missing At Random (MAR)* según la lógica del negocio (un SMS no tiene duración en minutos y una llamada de voz no acumula caracteres). Se decidió mantener estos nulos legítimos para no sesgar las distribuciones.

### 2. Análisis Exploratorio de Datos (EDA)
* Generación de histogramas y curvas de densidad (KDE) para analizar el comportamiento y distribución de las variables clave: edad, cantidad de mensajes, cantidad de llamadas y minutos consumidos de forma segmentada por plan.

### 3. Detección Cuantitativa de Outliers
* Implementación de diagramas de caja (Boxplots) para la identificación visual de anomalías.
* Aplicación del **Método del Rango Intercuartílico (IQR)** para calcular límites superiores de consumo e identificar el volumen de "súper usuarios" (*heavy users*). Se justificó estadísticamente la decisión de mantener estos registros.

### 5. Segmentación Estratégica de Clientes
* **Segmentación por Uso:** Clasificación de usuarios en *Bajo uso*, *Uso medio* y *Alto uso* mediante lógica condicional basada en llamadas y mensajes.
* **Segmentación por Edad:** Creación de rangos generacionales (*Joven*, *Adulto* y *Adulto Mayor*) para evaluar el comportamiento demográfico de consumo mediante el uso de NumPy.

### 6. Propuesta de Insights y Recomendaciones
* Traducción de hallazgos en conclusiones accionables para el negocio (e.g. rediseño de planes, planes orientados a nichos específicos).
* ## Cómo Ejecutar el Notebook (en Google Colab)

**Para ejecutar este proyecto de forma interactiva en la nube sin instalar dependencias locales, puedes utilizar Google Colab:**

1. Descarga el archivo del notebook con extensión `.ipynb` de este repositorio.
2. Ve a Google Colab e inicia sesión con tu cuenta de Google.
3. Selecciona la pestaña **Subir** y arrastra el archivo `.ipynb`.
4. Descarga los archivos de datos correspondientes (los CSV de `user_profile` y `usage`) y súbelos al entorno temporal de Colab haciendo clic en el icono de carpeta de la barra lateral izquierda y seleccionando "Subir al almacenamiento de sesión".
5. Ejecuta las celdas de forma secuencial presionando `Shift + Enter` en cada bloque de código.
