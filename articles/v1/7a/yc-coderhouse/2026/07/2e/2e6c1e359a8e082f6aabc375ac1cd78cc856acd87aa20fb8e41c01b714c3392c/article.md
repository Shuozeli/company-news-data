---
schema_version: "1.0.0"
document_id: "2e6c1e359a8e082f6aabc375ac1cd78cc856acd87aa20fb8e41c01b714c3392c"
company_key: "yc-coderhouse"
company: "Coderhouse"
source_id: "yc-coderhouse-news-import-7a925063f664"
canonical_url: "https://www.coderhouse.com/coderlibrary/sql-analistas-marketing-consultas-medir-campanas"
published_at: "2026-07-24T00:00:00+00:00"
first_seen_at: "2026-07-25T02:42:10.739604+00:00"
fetched_at: "2026-07-28T20:24:14.254979+00:00"
content_hash: "sha256:e4f35fa8fba09ce7e7cecbea41ef406fe731b39288ce1683434cb03b5168bd06"
---

# SQL para analistas de marketing: guía | Coderhouse

Francisco Rhaiel


AI Growth Engineer


Data


## SQL para analistas de marketing: consultas esenciales para medir campañas y tomar decisiones


Publicado el


24 de julio de 2026


Saber SQL le da a un analista de marketing autonomía total sobre sus datos: en lugar de esperar reportes ajenos, consultás directamente la base y respondés tus propias preguntas. Esta guía práctica reúne las consultas esenciales para medir campañas (cohortes, atribución, segmentación y ROI) con ejemplos listos para copiar y adaptar a tu caso.


El marketing moderno vive de datos, pero la mayoría de los analistas dependen de terceros para obtenerlos. SQL rompe esa dependencia. Con unas pocas consultas bien entendidas podés medir el rendimiento real de cada campaña, entender el comportamiento de tus cohortes y calcular el retorno de la inversión sin salir de la base de datos. No hace falta ser desarrollador: SQL fue diseñado para hacer preguntas a los datos en un lenguaje casi natural.


## Lo mínimo de SQL que necesitás


Antes de las consultas avanzadas, conviene dominar la estructura base: **SELECT** para elegir columnas, **FROM** para indicar la tabla, **WHERE** para filtrar, **GROUP BY** para agrupar y **ORDER BY** para ordenar. Con eso ya podés responder la mayoría de las preguntas de marketing. La documentación oficial de[PostgreSQL](https://www.postgresql.org/docs/current/tutorial-sql.html) es una referencia gratuita y confiable para consolidar estos fundamentos.


## Segmentación de audiencias


La segmentación es el pan de cada día del marketing. Un ejemplo para contar usuarios activos por país en el último mes:


-


**SELECT** pais, **COUNT** (DISTINCT usuario_id) AS usuarios


-


**FROM** eventos


-


**WHERE** fecha >= (fecha actual menos 30 días)


-


**GROUP BY** pais **ORDER BY** usuarios DESC


Cambiando la columna de agrupación (canal, dispositivo, fuente) obtenés al instante distintas vistas de tu audiencia.


## Análisis de cohortes


Una cohorte agrupa usuarios según cuándo empezaron (por ejemplo, el mes de su primera compra) para ver cómo evoluciona su comportamiento en el tiempo. Es la herramienta clave para medir retención: en lugar de un número global, ves si los usuarios que sumaste en enero siguen activos meses después. Se arma agrupando por la fecha de primera interacción y midiendo la actividad en períodos posteriores.


## Atribución de conversiones


Atribuir una conversión al canal correcto es uno de los grandes desafíos del marketing. Con SQL podés reconstruir el recorrido del usuario uniendo las tablas de sesiones y conversiones, y aplicar un modelo de atribución simple (primer contacto, último contacto) para entender qué canales realmente traen resultados. Esto te permite dejar de repartir presupuesto a ciegas.


## ROI de campañas


El indicador que más le importa a la dirección. Uniendo la tabla de costos de campaña con la de ingresos atribuidos, calculás el retorno como (ingresos menos costos) sobre costos. Una consulta que cruza ambas tablas por identificador de campaña te da, en una sola vista, qué campañas generan ganancia y cuáles queman presupuesto. Para complementar el análisis con benchmarks y buenas prácticas de medición, recursos como[Think with Google](https://www.thinkwithgoogle.com/) ofrecen marcos actualizados de atribución y performance.


Si todavía no manejás SQL y querés resultados rápidos mientras aprendés, las herramientas de IA integradas a la planilla son un buen puente: la guía sobre cómo usar[Copilot en Excel para analizar datos](https://www.coderhouse.com/coderlibrary/copilot-excel-analizar-datos-sin-ser-analista-argentina) muestra cómo empezar a analizar sin escribir código todavía.


## Consejos para consultas de marketing efectivas


-


**Empezá simple** y sumá complejidad de a poco: primero contá, después agrupá, después uní tablas.


-


**Nombrá tus columnas calculadas** con alias claros para que el reporte se lea solo.


-


**Validá los totales** contra una fuente conocida antes de confiar en una consulta nueva.


-


**Guardá tus consultas útiles** como plantillas reutilizables del equipo.


Estas habilidades se vuelven aún más valiosas en contextos de crecimiento con presupuesto ajustado, donde medir bien es sobrevivir, un enfoque que se desarrolla en el artículo sobre[growth marketing para startups con bajo presupuesto](https://www.coderhouse.com/coderlibrary/growth-marketing-startups-bajo-presupuesto-2026) .


## Cursos recomendados de Coderhouse


Para dominar SQL y el análisis aplicado a marketing, estos programas cubren distintos niveles:


-


**Fundamento técnico:** el[Curso de SQL](https://www.coderhouse.com/cursos/sql) te enseña a consultar bases de datos desde cero, con foco práctico.


-


**Análisis completo:** el[Curso de Data Analytics](https://www.coderhouse.com/cursos/data-analytics) suma limpieza, visualización e interpretación de datos.


-


**Marketing con IA:** la[Carrera de AI Marketing](https://www.coderhouse.com/carreras/carrera-ai-marketing) integra datos e inteligencia artificial aplicados al marketing de punta a punta.


**Elegí una consulta de esta guía y probala hoy con los datos de tu última campaña: es la mejor forma de aprender SQL.**


## Preguntas frecuentes


### ¿Es difícil aprender SQL para alguien de marketing?


Es uno de los lenguajes más accesibles. Su sintaxis se parece al inglés y en pocas semanas ya podés escribir consultas útiles. La curva inicial es mucho más suave que la de un lenguaje de programación general.


### ¿Qué base de datos conviene usar para practicar?


PostgreSQL y MySQL son gratuitas y muy usadas en la industria. Para marketing, muchas veces vas a consultar el data warehouse de la empresa, pero cualquiera de estas sirve perfecto para aprender.


### ¿SQL reemplaza a herramientas como Google Analytics?


No, las complementa. Las herramientas visuales son cómodas para lo estándar; SQL te da flexibilidad total para preguntas específicas que ninguna interfaz predefinida responde.


### ¿Puedo combinar SQL con inteligencia artificial?


Sí, y es una tendencia en alza. Hoy existen asistentes que generan consultas SQL a partir de preguntas en lenguaje natural, pero entender SQL sigue siendo clave para validar y ajustar lo que la IA propone.


Sobre el autor


### Francisco Rhaiel


Soy Francisco Rhaiel, AI Growth Engineer en Coderhouse. Mi día a día consiste en automatizar y optimizar procesos aplicando lo último en inteligencia artificial, incluyendo Agentic AI y Gen AI. Soy graduado de la Universidad Torcuato Di Tella (UTDT) en Tecnología Digital, y mi recorrido me llevó a especializarme en la intersección entre tecnología, datos y negocio. Me mueve aprender, construir y aplicar tecnologías innovadoras para resolver problemas reales. Para profundizar en mi trayectoria, te espero en mi perfil de LinkedIn.
