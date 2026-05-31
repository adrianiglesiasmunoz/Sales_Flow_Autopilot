# Sales_Flow_Autopilot
SALES FLOW AUTOPILOT
THE n8n + POWER BI COMMAND CENTER

Un cerebro, dos resultados: Análisis visual y Reporte escrito
👋 ¡Hola! Gracias por tu compra.
Acabas de adquirir tres "empleados digitales" que trabajarán para ti 24/7 sin pedir vacaciones. Este pack consta de dos flujos de trabajo (workflows) diseñados para n8n y un Dashboard para Power BI:
🚜 DataFeeder (El Músculo): Tu flujo de trabajo en n8n encargado de la fuerza bruta. Conecta tus fuentes de datos, los limpia y los deposita en tu base de datos centralizada sin errores humanos.
🧠 FlashReport AI (El Cerebro): El workflow que procesa la información mediante IA. Analiza tus resultados del día anterior y redacta un resumen ejecutivo que te espera en tu bandeja de entrada cada mañana antes de que tomes el primer café.
📈 Sales & Activity Flow Analytics (La Mirada): Tu Dashboard de Power BI con acabado "SaaS Premium". Es la herramienta de visualización táctica que traduce los datos en decisiones, permitiéndote monitorizar la salud de tu operativa de un solo vistazo.
Este pack es "Plug & Play": importa los archivos, conecta tus cuentas y olvídate.

🛠️ REQUISITOS PREVIOS (ANTES DE EMPEZAR)
Para que estos robots funcionen, necesitas tener preparados estos ingredientes:
Una cuenta en n8n: Puedes usar la versión Cloud (tiene prueba gratuita) o la versión de escritorio. https://n8n.io/
⚠️ Nota: Si usas la versión de n8n Escritorio, tu ordenador debe estar encendido para que las automatizaciones se ejecuten. Si necesitas que funcionen 24/7 con el PC apagado, necesitarás la versión Cloud o un servidor.
Google Drive y Google Sheets: Donde vivirán tus datos.
OpenAI API Key: Necesaria solo para el FlashReport AI. (Es una clave que permite a n8n "hablar" con GPT). 
🔗 Haz clic aquí para acceder 
1. Microsoft Power BI Desktop (Gratuito) para abrir y editar el archivo .pbix, necesitas tener instalado este software en tu ordenador Windows.
🔗 Haz clic aquí para descargarlo gratis desde Microsoft
🗂️ CONTENIDO DEL PACK
Los archivos de esta descarga:
📄 Guia_Instalacion.pdf (Este documento).
📊 Dataset_CC_v02 (El cimiento). Accede desde este  enlace
⚙️ DataFeeder.json (El robot de movimiento de datos).
🧠 FlashReport_AI.json (El analista inteligente).
📈 01_Sales&Activity_Flow_Analytics.pbix (El visor táctico).

🚜 PARTE 1: INSTALANDO "DATAFEEDER" (OPCIONAL)
Su misión: Detectar archivos CSV nuevos en una carpeta, leerlos y volcarlos en tu Hoja Maestra.
PASO 1: Importar el Cerebro
Abre n8n y crea un Nuevo Workflow.
Haz clic en los tres puntos (arriba a la derecha) > Import from File.

Selecciona el archivo DataFeeder.json que has descargado.
Verás aparecer el esquema visual del flujo.
PASO 2: Configurar tus conexiones de Google con n8n 
Para que n8n pueda leer tus datos de Google Drive y Google Sheets necesitas crear una nueva credencial (en el caso de que no tengas una ya creada).
Para ello, entra en cualquiera de los nodos de Google Sheets y selecciona la opción + Create new credential del desplegable Credential to connect with:

A continuación te pedirá que proporciones dos claves: 
Client ID y Client Secret, las cuales podrás encontrar en https://console.cloud.google.com/

Una vez introducidas ambas claves, ya solo quedará hacer clic en el botón de Sign in with Google y aceptar los permisos:

Repite la misma operación para el nodo de Google Sheets.
PASO 3: Configurar tus Carpetas (CRÍTICO ⚠️)
El robot necesita saber dónde mirar. No uses mis carpetas, usa las tuyas.
En tu Google Drive, crea una carpeta en la que se alojarán los CSV con los datos brutos de actividad. En mi caso, la he llamado 01_ENTRADA_CSV, pero puedes ponerle el nombre que quieras.
En n8n, abre el nodo llamado "Radar: Entrada CSV" y selecciona, del desplegable del campo Folder > From list, la carpeta que acabas de crear.

Ahora crea una carpeta en tu Google Drive (que será a donde se vayan moviendo los CSV de actividad una vez ya se hayan volcado en la Hoja maestra). En mi caso, la he llamado 02_PROCESADOS, pero puedes ponerle el nombre que quieras.
Abre el nodo final "Limpiador: Mover a Procesados" y mapea el ID del archivo CSV. Para esto, en el campo File > By ID, copia literalmente la siguiente expresión: {{ $('Radar: Entrada CSV').item.json.id }}y en el desplegable del campo Parent Folder > From list, busca y selecciona el nombre de la carpeta que has creado en el paso anterior. 

⛔ IMPORTANTE: No cambies el nombre de los nodos (las cajitas) en n8n, o las fórmulas dejarán de funcionar.
PASO 4: Conectar la Hoja de Cálculo
Crea una copia de mi Google Sheet Dataset_CC_v02, elimina el contenido y pega el tuyo. Accede al fichero desde este enlace.
REGLA DE ORO: La primera fila debe tener EXACTAMENTE estos encabezados para que el robot sepa dónde poner cada dato: FECHA | MES-AÑO | WORKING DAY | CLIENTES LLAMADOS | CLIENTES CONTACTADOS | VENTAS | IMPORTE TOTAL
En n8n, abre el nodo "Volcado a Base de Datos".
En "Document", selecciona el nombre de tu archivo de Google Sheet.
En "Sheet Name", selecciona el nombre de la pestaña donde están los datos.

🧠 PARTE 2: INSTALANDO "FLASHREPORT AI"
Su misión: Leer tu hoja maestra, analizar tendencias con IA y enviarte un email.
PASO 1: Importar y Conectar
Crea otro workflow nuevo e importa el archivo FlashReport AI.json.
Abre el primer nodo "Fuente: Ventas Diarias".
Selecciona el mismo Google Sheet que configuraste en el paso anterior (en mi caso, Dataset_CC_v02).

PASO 2: Activar la Inteligencia Artificial
Abre el nodo "Analista IA".
En "Credential", selecciona "Create New".
Pega tu API Key de OpenAI.
Nota: Si no tienes una, ve a platform.openai.com, regístrate y crea una "Secret Key". Cuesta céntimos al mes.
No necesitas tocar el "Prompt" (las instrucciones), ya lo he programado para que actúe como un analista senior.
PASO 3: Configurar el Email de Destino
Abre el último nodo "Envío Reporte por email".
Conecta tu cuenta de Gmail (al igual que hicimos con Google Sheets y Google Drive en la página 3).

Por último, en el campo "To:" (Para), escribe la dirección de correo electrónico en la quieres que se reciba el reporte, así como el asunto del email (Subject).

📑 PARTE 3 - PREPARA TUS DATOS
El dashboard se alimenta del archivo Google Sheet llamado Dataset_CC_v02. Para que funcione con tu equipo, sigue esta regla de oro:
⚠️ ADVERTENCIA IMPORTANTE: Puedes borrar mis datos de ejemplo y pegar los tuyos, pero NUNCA cambies los nombres de los encabezados de la primera fila (FECHA, MES-AÑO, WORKING DAY, CLIENTES LLAMADOS...). Si cambias una sola letra, el sistema no reconocerá la columna.
Instrucciones:
Abre mi archivo Dataset_CC_v02 en tu Google Drive y crea una copia. Accede desde el enlace que te he dejado en las páginas 1 y 3.
Borra las filas de datos de ejemplo (de la fila 2 hacia abajo).
Pega o escribe tus datos respetando el orden de las columnas.
Selecciona el acceso al fichero como “Cualquier persona con el enlace” para que Power BI pueda leer los datos

⚙️PARTE 4 - CONECTA EL DASHBOARD
Al abrir el archivo Power BI (01_Sales&Activity_Flow_Analytics.pbix) por primera vez, es posible que veas un error o datos vacíos. Esto es normal: Power BI está buscando el Excel en mi ordenador. Vamos a decirle dónde está en el tuyo.
Sigue estos 4 pasos:
Abre el archivo Power BI.
En la barra superior, despliega la flechita del botón Transformar datos.
Haz clic en Editar parámetros.

Borra la URL de ejemplo y pega la URL de tu Google Sheet.
Haz clic en Aceptar .

Si Power BI te pide credenciales, selecciona 'Cuenta de organización' (o Google), pulsa 'Iniciar sesión', entra con tu email de Gmail y dale a 'Conectar'.
✅ Tip Pro: Una vez cerrada la ventana, verás una barra amarilla arriba que dice "Aplicar cambios". Haz clic ahí o en el botón "Actualizar" de la barra principal.
🚦 CÓMO PROBAR QUE FUNCIONA
Vamos a hacer un simulacro real:
Haz clic en el botón "Execute Workflow" (el botón de Play) en el flujo DataFeeder. Se quedará "Escuchando...".
Sube un archivo CSV de prueba a tu carpeta 01_ENTRADA_CSV de Drive.
¡Magia! ✨ Deberías ver cómo n8n detecta el archivo, lo procesa y tus datos aparecen mágicamente en tu Google Sheet.
Ahora ya deberías de verlos actualizados en el Dashboard de PBI, tras haber hecho clic en Actualizar > Esquema y Datos de la cinta de opciones.
Ahora ve al flujo FlashReport AI y dale a "Execute Workflow".
Revisa tu bandeja de entrada. Deberías tener un email con un análisis HTML profesional de los datos que acabas de subir.

🆘 SOLUCIÓN DE PROBLEMAS FRECUENTES (FAQ)
P: El DataFeeder da error al intentar leer el archivo.
R: Asegúrate de que el archivo que subes al Drive es un CSV (delimitado por comas) y que tiene encabezados. Si subes un Excel (.xlsx) directo, el nodo "Descarga Binaria" podría confundirse si no lo ajustas.
P: El FlashReport AI dice que no hay datos suficientes.
R: El filtro "Histórico (3M)" está configurado para comparar los últimos 3 meses. Si tu Excel solo tiene datos de ayer, la IA no puede calcular tendencias. Añade al menos 3 meses de datos antiguos a tu Sheet para ver todo el potencial.
P: La IA alucina o da datos raros.
R: Verifica la columna WORKING DAY en tu Excel. La IA usa esa columna para comparar "peras con peras" (ej: Día hábil 5 de Enero vs Día hábil 5 de Febrero). Si esa columna está vacía o mal calculada, el análisis fallará.
P: Me da error de "Authentication" en Google Drive. 
R: Es normal la primera vez. En n8n, dentro del nodo de Drive, haz clic en "Credentials" > "Connect Account". Se abrirá una ventana de Google pidiéndote permiso. Acepta y listo.
P: ¿Puedo cambiar el prompt de la IA? 
R: ¡Por supuesto! El nodo "Analista IA" es editable. Puedes decirle que sea "más formal", "más agresivo en ventas" o que se centre en métricas de calidad. Eres el dueño del robot.

🎓 ENTENDIENDO LA LÓGICA (CÓMO PIENSAN TUS ROBOTS)
Igual que en el Dashboard te explicamos qué es el AHT, aquí es vital que entiendas cómo "piensa" tu automatización para sacarle partido:
Normalización de Fechas: El sistema convierte cualquier formato de fecha loco que venga en el CSV (ej: 12/05/24 o 2024-05-12) a un formato estándar. Esto evita errores de lectura.
Lógica "Working Day" (Día Hábil): Para comparar si vas mejor o peor que el mes pasado, la IA no compara "día 5 vs día 5". Compara "5º día hábil vs 5º día hábil". Esto elimina el ruido de los fines de semana y festivos, dándote una comparación real de "peras con peras".
El Filtro de Seguridad: El robot solo lee los últimos 3-5 meses de datos. Esto hace que el proceso sea ultra-rápido y no consuma recursos innecesarios leyendo datos de hace dos años.
