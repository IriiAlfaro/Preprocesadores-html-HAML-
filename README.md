# Preprocesadores-html-HAML
HAML (HTML abstraction markup language) se basa en que el código sea bonito, simple y que acelere y simplifique la creación de código.
Haml es un markup lenguage que se utiliza para escribir el código HTML de cualquier documento web sin el uso de código en línea. Haml funciona como un reemplazo para sistemas de plantillas de página en línea tales como PHP, ASP y ERB, el lenguaje de plantillas utilizado en mayoría Ruby on Rails. Sin embargo, Haml evita la necesidad de forma explícita la codificación HTML en la plantilla, porque él es sí mismo una descripción del HTML, con un código para generar contenido dinámico.

### Principios básicos

Haml se basa en varios principios fundamentales para lograr lo que quieren.  Estos son:

* El markup debe ser hermoso
No debe utilizarse como una herramienta simple para navegadores para representar una página cómo el desarrollador quiere        que se vea. La representación no es lo único que la gente tiene que ver; tienen que ver, modificar y comprender como es el markup.

* El markup debe estar bien indentado 
Haml automáticamente cierra y pone las etiquetas como se debe

* La estructura del HTML debe ser claro
XML y HTML son formatos basados en la idea de un documento estructurado. Esa estructura se refleja en su markup y asimismo debe ser reflejada en meta-marcado como lógica de Haml porque Haml se basa en la de elementos secundarios (child elements), esta estructura se conserva naturalmente, haciendo el documento mucho más fácil, más lógico y más simples de leer para el usuario.

Acá hay un tutorial de como empezar con HAML y como pasar de ERB a HAML: http://haml.info/tutorial.html

### Características

* Whitespace activo
* Markup bien formateado
* Sigue las convenciones CSS
* Integra código Ruby
* Implementa Rails templates con la extención .haml

### Usar Haml:

1. Como una herramienta de lineas de comando
2. Como un plugin de Ruby on Rails
3. Como un módulo independiente Rubí.

### Ruby Module
Haml tambien puede usarse separado de Rails y ActionView. Para hacer eso, debemos de instalar la gema de Ruby:
    <pre>gem install haml</pre>
Tambien se puede usar poniendo una gema de “haml” en el cogido de Ruby y usando Haml::Engine:
    
    <pre>
    engine = Haml::Engine.new("%p Haml code!")
    engine.render #=> "<p>Haml code!</p>\n
    </pre>

### Texto sin formato
Una parte importante de cualquier documento HTML es su contenido, que es texto sin formato. Cualquier línea de Haml que es interpretado como algo más, es tomado como texto sin formato, y pasan sin modificarse. Por ejemplo:
    <pre>
    %gee
    %whiz
    Wow this is cool!
    </pre>
Es completado como:
    <pre>
    <gee>
    <whiz>
    Wow this is cool!
    </whiz>
    </gee>
    </pre>
Si uno no quiere que lo uno escriba se convierta en formato Haml uno debe de hacer, por ejemplo:
    <pre>
    %p
    <div id="blah">Blah!</div>
    </pre>
Se vería como:
    <pre>
    <p>
    <div id="blah">Blah!</div>
    </p>
    </pre>

### Elementos HTML
Nombre de un elemento: %
El símbolo de porcentaje debe ponerse al inicio de la línea y es seguido inmediatamente por el nombre del elemento y se generara el tag de cierre de una vez. Por ejemplo:
    <pre>
    %one
    %two
    %three Hey there
    </pre>
Esto se vería como:
    <pre>
    <one>
    <two>
    <three>Hey there</three>
    </two>
    </one>
    </pre>
Cualquier valor que se ponga después del signo de porcentaje será tomado como nombre del elemento.

### Atributos:
