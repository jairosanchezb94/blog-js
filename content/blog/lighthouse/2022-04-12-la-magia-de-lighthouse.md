---
layout: blog
title: La magia de Lighthouse
date: 2022-04-12T15:36:19.280Z
thumbnail: /src/images/images.jpg
---
<!--StartFragment-->

Un sitio web no es algo físico, como un libro o un periódico. Para poder acceder a sus contenidos, estos tienen que descargarse a través de la red, procesarse y renderizarse en un navegador web. Esto implica un coste en tiempo y dinero, cosas que los usuarios tienen en muy alta estima y no están dispuestos a derrochar.

Al igual que la sociedad moderna, también la web (moderna también) tiene un problema de obesidad. Se ha escrito mucho y creado multitud de recursos para combatirlo, aunque a veces, especialmente navegando desde el móvil, nos pueda dar la impresión de que estos no se estén aplicando de forma efectiva. Esto es especialmente cierto desde que **HTML5 y Javascript** han empezado a dominar el entorno: estas tecnologías han transformado el ecosistema [web](https://www.divisadero.es/lexicograma?web), permitiendo crear aplicaciones muy potentes y bonitas, pero a costa de añadir peso y complejidad y, por tanto, aumentando la carga de trabajo del navegador web.

Tradicionalmente, las métricas importantes a la hora de diseñar una página web eran muy básicas (como, por ejemplo, el tiempo de carga de página, o el de carga del DOM), pero esto no siempre tiene una relación directa con la experiencia de usuario. En los últimos años se han desarrollado nuevos conceptos que ponen al usuario en el foco central, como el [Speed Index](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index), las variedades de [First Paint](https://developers.google.com/web/fundamentals/performance/user-centric-performance-metrics#first_paint_and_first_contentful_paint) y muchas otras, algunas más específicas, como el [Time to First Tweet](https://blog.alexmaccaw.com/time-to-first-tweet).

Y en torno a ello, también han surgido multitud de herramientas para detectar y remediar problemas. Es un tema amplio y que puede parecer complicado si uno no tiene antecedentes en este ámbito, pero son conceptos que conviene entender y tener en cuenta si se gestiona un sitio web o, en general, cualquier activo digital. A continuación, se describe una herramienta en concreto seleccionada por ser muy adecuada como primer toma de contacto:

**Lighthouse**

Aunque la mayor parte del tiempo los navegadores sólo se usan para navegar la web, han ido evolucionando para convertirse en herramientas muy versátiles. En concreto, tienen funcionalidad muy potente para analizar el rendimiento de sitios web. En Chrome, una de las herramientas a nuestra disposición es **Lighthouse**.

Lighthouse es una herramienta de código abierto integrada en Google Chrome a partir de su versión 60, que hace posible realizar un auditado automatizado de un sitio web con sólo el clic de botón. Este auditado no sólo analiza aspectos de rendimiento, sino también SEO, accesibilidad y experiencia de usuario, atendiendo a unos criterios y buenas prácticas definidas de antemano.

**Uso**

Para lanzar la herramienta, no hay más que acceder al sitio web que queramos analizar, abrir el panel de herramientas de desarrollador de Chrome (si estás leyendo esto desde Chrome, puedes hacerlo ahora mismo, pulsando F12) y acceder a la pestaña *Audits*.

<!--EndFragment-->

![ejemplo: ](/src/images/pic1.png)

<!--StartFragment-->

Panel de bienvenida de Lighthouse. Se destaca la pestaña *Audits* (1), y dentro de ella los controles para configurar el tipo de emulación (movil/escritorio) (2) y velocidad de red (3)

Tras pulsar en *Perform an audit…*, podemos elegir entre las categorías que nos interesen:

<!--EndFragment-->

![ejemplo: ](/src/images/pic2.png)

Tipos de análisis que ofrece Lighthouse en Chrome 67.0

Después, la herramienta recargará la página varias veces bajo distintas condiciones (al mismo tiempo que muestra mensajes con estadísticas muy interesantes acerca de las consecuencias de un buen diseño web de cara a los objetivos de conversión) y presentará los resultados. Arriba se muestra un resumen, con una puntuación asignada para cada categoría.

<!--EndFragment-->

<!--StartFragment-->

Resumen de resultados para un post de este blog

Por suerte, este blog de analítica web puntúa alto en las categorías más importantes, pero hay que notar que en este caso sólo se lanzó el auditado una vez. Para un análisis más completo y fiable convendría hacerlo varias veces con distintas configuraciones y comparar los distintos resultados.

**Análisis de resultados**

Estas calificaciones pueden ser una aproximación interesante, pero lo realmente útil está en el desglose de cada categoría. Hay muchos detalles que analizar y explicar, en este post mencionaremos algunos de ellos centrándonos en la categoría de Rendimiento.

En esta categoría, las métricas en las que se basa el análisis son muy orientadas a la experiencia de usuario, y se muestra de manera muy visual, como se percibe la página a medida que ésta carga, con capturas de pantalla a medida que fue cargando la web:

<!--EndFragment-->

![ejemplo: ](/src/images/pic4.png)

<!--StartFragment-->

Este blog tarda poco más de medio segundo en llegar al First Meaningful Paint (instante en el que se muestra el contenido principal de la web al usuario), lo cual no es una mala puntuación. No obstante, esta simulación era con las mejores condiciones posibles de red. Si se activa emulación de dispositivo móvil con de red lenta (2G o 3G), los resultados no serían tan bonitos.

Más abajo, en la interfaz, también se ofrecen consejos generales de qué mejoras podrían hacerse en la web y en cuánto podría mejorar el tiempo de carga. Es muy recomendable pararse a leerlos en detalle, ya que se explican cosas muy interesantes. Por ejemplo, en la siguiente imagen se delata que se espera a cargar el documento entero para mostrárselo al usuario, cuando en su lugar se podrían cargar las imágenes *offscreen* mientras el usuario lee el título y primer párrafo, en la vista principal (*lazy-loading*).

<!--EndFragment-->

![ejemplo: ](/src/images/pic5.png)

Según la imagen, podrían ahorrarse hasta 340 milisegundos en tiempo de carga aparente de cara al usuario, lo que significaría cortarlo casi por la mitad.

Lighthouse destaca porque permite obtener unas conclusiones bastante útiles acerca de un sitio web, sobre todo teniendo en cuenta lo fácil e instructivo que resulta usarlo. Pero esta es sólo una de las pestañas en el panel de desarrolladores de Chrome, en realidad es posible hacer [muchas](https://www.analiticaweb.es/nueva-actualizacion-devtools-google-chrome/) otras [cosas](https://www.analiticaweb.es/valida-app-herramientas-desarrolladores-chrome/) desde esta interfaz. En concreto, en un post futuro merecerá la pena describir la pestaña *Performance*, que, aunque no es tan intuitiva, permite hacer un análisis mucho más profundo (al igual que su equivalente en Firefox, también muy potente) del rendimiento.

**Conclusiones**

Todo esto está muy bien, pero conviene no dejarse llevar por el enfoque simplista de entretener al usuario con contenido tan pronto como sea posible. Minimizar el tiempo que sólo se muestra una pantalla en blanco (o peor aún, un mensaje de *loading*) está bien, pero todos hemos encontrado aplicaciones o páginas web que parecían ligeras y rápidas, a las que se les ve el plumero en cuanto hacemos *scroll* y vemos que el resto de la web aún no se muestra correctamente.

No sólo esto, otros factores también son importantes. Navegar por la web debería ser algo simple, y más con tecnología que está continuamente mejorando; cosas como que el móvil no queme al tacto, que el usuario no tenga que recargar la batería del móvil cada 8 horas o no se le obligue a gastar hasta el [80% de los datos de su tarifa en anuncios](https://www.techdirt.com/articles/20160317/09274333934/why-are-people-using-ad-blockers-ads-can-eat-up-to-79-mobile-data-allotments.shtml), no parecen mucho pedir.

Y no es sólo que todo esto sea interesante, es que tiene repercusiones. Parece inevitable que la web que no tenga en cuenta el rendimiento, perderá usuarios a favor de la que sí lo haga, y la que abuse del uso de anuncios, perderá sus beneficios a favor del uso de *adblockers*.

<!--EndFragment-->

Más información en su web oficial: 

https://developers.google.com/web