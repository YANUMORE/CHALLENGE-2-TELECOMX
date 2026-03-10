**#CHALLENGE 2 TELECOM X:**

**##Análisis de Evasión de Clientes (Churn)**

**SOBRE EL PROYECTO:**

Telecom X es una empresa de que ofrece y presta servicios de telefonia e internet y tiene un porcentaje de Evasión de clientes (churn) que impacta directamente sus ingresos


**PROYECTO:** Challenge 2 de Data Science del programa ONE (Oracle Next Education) en alianza con Alura Latam. 

Como analista de datos, El objetivo de este proyecto para Telecom X es realizar un diagnóstico integral y estratégico de la evasión de clientes (Churn) para transformar los datos en acciones que protejan los ingresos de la empresa.


**PROBLEMA del Negocio:**
¿Por qué los clientes evaden(abandonan) Telecom X?
     
     1. Tipo de contrato 
     2. Tiempo de permanencia (Tenure)
     3. Método de pago utilizado
     4. Cargos mensuales

**Metodología ETL**
El proyecto sigue una arquitectura ETL dividida en 3 fases:
1. Fase 1: Extracción de la data
Carga del dataset desde la API pública del challenge mediante requests y normalización de la estructura JSON anidada con pd.json_normalize().
url = "https://raw.githubusercontent.com/ingridcristh/challenge2-data-science-LATAM/main/TelecomX_Data.json"
df_expanded = pd.json_normalize(data)

2. Fase 2: Transformación
   En esta fase se manipula la data cruda y se pasa a tener información inteligente lista para los análisis.
   1. Limpieza y Exploración:
Antes de analizar, hay que asegurar que los datos sean confiables.
     a. Manejo de Nulos: Identificar si faltan datos.
     b. Corrección de Tipos: Asegurar que los números sean tratados como números (float/int) y no como texto-
     c. Eliminación de Duplicados: Borrar registros repetidos que puedan inflar falsamente el resultado.

     2. Estandarización y Formateo
     Preparar los datos para que las herramientas de visualización (como Seaborn o Matplotlib) los entiendan.

     3. Consistencia de Categorías: Asegurar que en la columna Churn, todos los "Yes" y "No" estén escritos igual (evitar errores de mayúsculas/minúsculas).
   
     4. Ingeniería de Características (Feature Engineering: Se creó la columna account_charges_daily = account_charges_monthly / 30.
     a. Es la parte más estratégica. Aquí es donde creas "nuevas métricas" a partir de las existentes:
     b. Codificación Binaria: Convertir el "Yes/No" de Churn en 1 y 0 para poder calcular promedios y correlaciones.

     5. Preparación para el Modelo (Encoding)
     Si vas a usar Machine Learning, en esta fase transformas las categorías de texto en números:
     Conversión de Churn Yes/No → binario 1/0
3. Fase 3: Carga y Análisis de datos:
   La carga es el proceso de almacenar los datos ya limpios y transformados en un destino final donde puedan ser consultados de forma segura y eficiente.
   El análisis de datos de la empresa Telecom X es el proceso de "hacer hablar a los números"
     Consiste en cuatro niveles estratégicos que se fueron construyendo a lo largo del proyecto:
   
**Resultados del Análisis**

1. Análisis Descriptivo (¿Qué está pasando?)
Es el nivel básico donde se resume la realidad actual de la empresa. Obtuve La Tasa de Churn (26.54%): Esto nos dice la magnitud del problema. Sin este análisis, no sabríamos si la empresa está en crisis o no.
Promedios y Totales: Saber cuánto paga un cliente en promedio y cuánto tiempo se queda (Tenure).

2. Análisis Exploratorio (¿Por qué pasa?)
Aquí es donde realice el cruce de las variables para encontrar a los "culpables". Es la parte más importante del proyecto:
Contrato vs. Churn: Arrojo que el contrato "Mes a Mes" es el principal motor de la fuga.
Método de Pago vs. Churn: Se identificó que el "Electronic Check" es un síntoma de desvío.
Antigüedad (Tenure) vs. Churn: Confirmó que los primeros 18 meses son los más peligrosos.

3. Análisis Visual (¿Cómo lo comunicamos?)
Consiste en convertir esos cruces de variables en gráficos que cualquier gerente pueda entender de un vistazo:
Boxplots: Lo usé para ver la dispersión del dinero (TotalCharges) y el tiempo (Tenure). Si la "caja" de los que se van es baja, el problema es de clientes nuevos.
Gráficos de Barras: Lo usé para comparar el volumen de personas vs. el porcentaje de riesgo.

4. Análisis de Diagnóstico (Hallazgos de Negocio)
Es la fase final donde se conectan los datos con la estrategia. En este caso, el diagnóstico fue:
Segmentación de Riesgo: No todos los clientes son iguales. El análisis te permitió crear el perfil del "Cliente en Alerta Máxima" (Mes a mes + Cheque electrónico + Menos de 1 año).
Costo de Oportunidad: Entender que perder a un cliente con altos TotalCharges (los outliers que vimos) es mucho más grave que perder a uno nuevo.

**Conclusiones e Insights**

El análisis integral de los 7,043 registros de Telecom X revela una crisis de retención prematura que afecta al 26.54% de la base de clientes. El problema no es la falta de ventas, sino la incapacidad de estabilizar al cliente nuevo.

     **Insights**

La Ventana de Vulnerabilidad: La fuga no es aleatoria; ocurre principalmente en los primeros 18 meses de vida del cliente. Si un usuario supera los 2 años, su probabilidad de evasión cae drásticamente.

El "Facilitador" de la Fuga: El contrato Mes a Mes es el mayor predictor de riesgo. Casi la mitad de estos clientes terminan cancelando, lo que genera una "puerta giratoria" que quema presupuesto de marketing.

Fricción en el Pago: El uso de Cheque Electrónico (pago manual) duplica la tasa de evasión en comparación con los métodos automáticos. La falta de domiciliación bancaria permite que el cliente evada(abandone) por un impulso ante cualquier insatisfacción.

Conclusiones Estratégicas
Rentabilidad Comprometida: Telecom X está perdiendo clientes antes de recuperar el Costo de Adquisición (CAC). Esto significa que muchos de los clientes que se van en el "Yes" del Churn representaron una pérdida neta de dinero.

Segmentación del Esfuerzo: La estrategia de retención no debe ser masiva. El foco debe estar en el perfil de Alto Riesgo: Cliente nuevo + Contrato mensual + Pago manual.

Fidelización Silenciosa: Los clientes con contratos de 1 y 2 años son el ancla de estabilidad de la empresa. Protegerlos de la obsolescencia técnica es vital para mantener el flujo de caja a largo plazo.

**Recomendaciones Estratégicas**

**Estrategia**	          **Segmento Objetivo**	               **Meta de Retención**

1. Contrato Anual	     Clientes Mes a Mes	                    Reducir churn del segmento en un 15%.
2. Pago Automático	     Usuarios de Cheque Electrónico	     Disminuir la mora y la cancelación impulsiva.
3. Onboarding	          Clientes nuevos (0-12 meses)	          Cruzar la "barrera de los 18 meses".
4. Upgrade VIP	          Clientes de alto valor (Outliers)	     Proteger el ingreso residuesidual histórico.

**Tecnologías Utilizadas**

Herramienta	          Uso
☁️ Google Colab	Entorno de ejecución en la nube
🐙 GitHub	          Control de versiones
🐍 Python 3.10+	Lenguaje principal
🐼 Pandas	          Manipulación y análisis de datos
📊 Matplotlib	     Visualización estática
🎨 Seaborn	     Visualización estadística avanzada
🌐 Requests	     Consumo de API REST

**USO Y EJECUCIÓN**

1. Opción — Google Colab (Recomendado)
   
   a. Abre Google Colab
   b. Ve a Archivo → Abrir cuaderno → GitHub
   c. Pega la URL de este repositorio
   c. Selecciona TelecomX_LATAM.ipynb
   d. Ejecuta las celdas en orden ▶️
   
2. Opción — Local
 
   a. Clonar el Repositorio:https://github.com/YANUMORE/CHALLENGE-2-TELECOM-X.git
      
Estructura del Repositorio **ChallengeTELECOM-X**
-README.md
-TelecomX_LATAM.ipynb

**Autor: Yanucelly Moreira. Alura Latam + Oracle Next Education**
https://www.linkedin.com/in/yanucelly-moreira/

yanu.moreira@gmail.com 



