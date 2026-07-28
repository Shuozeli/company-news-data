---
schema_version: "1.0.0"
document_id: "5c62ecece74d6f57de373c7b3860ea3bbd2de7dc0de78780744cf674d110435f"
company_key: "yc-coderhouse"
company: "Coderhouse"
source_id: "yc-coderhouse-news-import-7a925063f664"
canonical_url: "https://www.coderhouse.com/coderlibrary/bonsai-27b-modelo-ia-celular-offline"
published_at: "2026-07-27T00:00:00+00:00"
first_seen_at: "2026-07-28T07:56:38.769046+00:00"
fetched_at: "2026-07-28T07:56:35.409468+00:00"
content_hash: "sha256:27d70e00b10342facedce311d1b2dd27289fc8e369e5cedb8c8552499a47ffe5"
---

# Bonsai 27B: modelo de IA que corre en tu celular offline | Coderhouse

Francisco Rhaiel


AI Growth Engineer


Inteligencia Artificial


## Bonsai 27B: el primer modelo de 27.000 millones de parámetros que corre en tu celular sin internet


Publicado el


27 de julio de 2026


Un modelo de 27.000 millones de parámetros que corre en un teléfono, sin internet y a velocidad usable, sonaba imposible hace poco. Bonsai 27B, de PrismML, lo logró: comprimió un modelo enorme en apenas 3,9 GB usando cuantización de 1-bit y lo hizo funcionar de forma local en un smartphone. Acá te contamos cómo lo consiguieron y qué cambia para quienes construyen con IA.


El lanzamiento —bajo una licencia abierta— es relevante porque ataca uno de los mayores límites de la IA actual: la dependencia de servidores en la nube. Si un modelo potente corre en tu bolsillo, se abren usos que antes no eran viables.


## El problema que resuelve: la IA vive en la nube


La mayoría de los modelos potentes corren en centros de datos porque necesitan mucha memoria y cómputo. Eso implica conexión permanente, costos de API y que tus datos viajen a un servidor externo. Bonsai 27B propone lo contrario: **IA local, privada y sin conexión** .


## Cómo metieron 27B de parámetros en 3,9 GB


La clave es la **cuantización** : reducir la precisión con la que se guarda cada parámetro. Un modelo tradicional guarda cada peso con muchos bits; la cuantización extrema de 1-bit los reduce al mínimo, achicando el tamaño de forma drástica.


-


**Tamaño:** de decenas de GB a solo 3,9 GB, apto para un celular moderno.


-


**Velocidad:** alrededor de 11 tokens por segundo en un smartphone de gama alta, suficiente para uso interactivo.


-


**El desafío técnico:** cuantizar tan agresivamente sin destruir la calidad del modelo, el verdadero logro de ingeniería.


Para entender la idea detrás de estos parámetros y su entrenamiento, es útil repasar[qué es el machine learning y para qué sirve](https://www.coderhouse.com/coderlibrary/que-es-el-machine-learning-y-para-que-sirve) .


## Qué cambia para los developers


-


**Apps con IA offline:** asistentes que funcionan en zonas sin conexión o en modo avión.


-


**Privacidad total:** los datos nunca salen del dispositivo.


-


**Sin costos de API:** el modelo corre localmente, sin pagar por llamada.


-


**Menor latencia:** sin viaje al servidor, la respuesta es inmediata.


Los pesos de modelos como este suelen publicarse en[Hugging Face](https://huggingface.co/) , donde la comunidad los prueba y adapta. Publicaciones como[The Verge](https://www.theverge.com/ai-artificial-intelligence) vienen siguiendo la tendencia de la IA "on-device", que empuja a los fabricantes de chips a optimizar sus teléfonos para estas cargas.


## Los límites, sin sobrevender


La IA local no reemplaza todo. Los modelos cuantizados pueden perder algo de calidad frente a sus versiones completas en la nube, y las tareas más exigentes seguirán necesitando servidores. Pero para un enorme abanico de usos cotidianos, tener un modelo capaz en el bolsillo es un cambio de paradigma.


## Cursos recomendados de Coderhouse


Para construir aplicaciones que integren modelos como Bonsai, el[Curso de AI Engineering](https://www.coderhouse.com/cursos/ai-engineering) te da las bases técnicas. Si querés armar agentes y asistentes, el[Curso de AI Agents](https://www.coderhouse.com/cursos/ai-agents) es ideal. Y para entender el panorama general de la IA y hacia dónde va, empezá con el[Curso de Introducción a la Inteligencia Artificial](https://www.coderhouse.com/cursos/introduccion-inteligencia-artificial) .


## Preguntas frecuentes


### ¿Qué es la cuantización de un modelo?


Es una técnica para reducir la precisión con que se almacenan los parámetros, achicando el tamaño del modelo y su consumo de memoria. La cuantización de 1-bit es la versión más extrema.


### ¿Un modelo en el celular es tan bueno como uno en la nube?


Para muchas tareas cotidianas, sí. Para las más complejas, los modelos completos en la nube siguen teniendo ventaja. La cuantización implica un intercambio entre tamaño y calidad.


### ¿Por qué importa que la IA funcione sin internet?


Habilita privacidad total, uso en zonas sin conexión, respuestas más rápidas y cero costo de API. Es clave para apps móviles y sectores sensibles a la privacidad.


### ¿Puedo probar este tipo de modelos hoy?


Sí. Los modelos abiertos suelen publicarse en repositorios como Hugging Face, y existen apps que permiten ejecutarlos localmente en el teléfono con distintos niveles de dificultad.


Sobre el autor


### Francisco Rhaiel


Soy Francisco Rhaiel, AI Growth Engineer en Coderhouse. Mi día a día consiste en automatizar y optimizar procesos aplicando lo último en inteligencia artificial, incluyendo Agentic AI y Gen AI. Soy graduado de la Universidad Torcuato Di Tella (UTDT) en Tecnología Digital, y mi recorrido me llevó a especializarme en la intersección entre tecnología, datos y negocio. Me mueve aprender, construir y aplicar tecnologías innovadoras para resolver problemas reales. Para profundizar en mi trayectoria, te espero en mi perfil de LinkedIn.
