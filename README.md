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
Los brackets representan un hash en Ruby que se utiliza para especificar los atributos de un elemento. Los caracteres de comillas dentro del atributo será sustituido por las secuencias de escape. El hash se coloca después de la etiqueta que se define. Por ejemplo:
    <pre><html xmlns='http://www.w3.org/1999/xhtml' xml:lang='en' lang='en'></html></pre>
Atributo hash también puede ser extendido por varias líneas para acomodar muchos atributos. Sin embargo, los saltos sólo pueden colocarse inmediatamente después comas. Por ejemplo:
    <pre>
    %script{:type => "text/javascript",
    :src  => "javascripts/script_#{2 + 7}"}
    </pre>
Sé vería como:
    <pre>
    <script src='javascripts/script_9' type='text/javascript'></script>
    </pre>
#### :class and :id Attributes
Los atributos :class y  :id pueden ser especificados como un array de Ruby y estos elementos se juntaran. Un :class array es unido con “ ” y un :id array será unido con “_”. Por ejemplo:  
    <pre>
    %div{:id => [@item.type, @item.number], :class => [@item.type, @item.urgency]}
    </pre>
Esto equivale a:
    <pre>
    %div{:id => "#{@item.type}_#{@item.number}", :class => "#{@item.type} #{@item.urgency}"}
    </pre>
Primero se acoplarán al array y se eliminarán todos los elementos que no prueben como verdaderos. Los elementos restantes se convertirán en strings. Por ejemplo:
    <pre>
    %div{:class => [@item.type, @item == @sortcol && [:sort, @sortdir]] }
    </pre>
El contenido podría representar como:
    <pre>
    <div class="numeric sort ascending">Contents</div>
    <div class="numeric">Contents</div>
    <div class="sort descending">Contents</div>
    <div>Contents</div>
    </pre>
#### Atributos de estilo de HTML: ()
Haml también apoya una sintaxis de atributo más concisa, menos la syntaxis de Ruby que esta basada en los atributos de HTML. Éstos son usados con paréntesis en vez de corchetes, como se muestra a continuación:
    <pre>
    %html(xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en")
    </pre>
Las variables de Ruby pueden utilizarse omitiendo las comillas. Pueden utilizar variables locales o las variables de instancia. Por ejemplo:
    <pre>
    %a(title=@title href=href) Stuff
    </pre>
Esto es igual a:
    <pre>
    %a{:title => @title, :href => href} Stuff
    </pre>
Porque no hay comas separando los atributos, sin embargo, las expresiones más complicadas no están permitidas. Para los que tendrás que utilizar la sintaxis {}. Sin embargo, puede utilizar juntos dos sintaxis:
    <pre>
    %a(title=@title){:href => @link.href} Stuff
    </pre>
Tambien se puede usar #{} para insertar expresiones complicadas en un atributo de estilo HTML:
    <pre>
    %span(class="widget_#{@widget.number}")
    </pre>
Atributos de estilo HTML se pueden poner a través de varias líneas como atributos de hash-estilo:
    <pre>
    %script(type="text/javascript"
        src="javascripts/script_#{2 + 7}")
        </pre>
#### Métodos de Atributo
Un Ruby método llama a que se retorne un hash que puede ser sustituido por el hash del contenido. Por ejemplo, Haml::Helpers define el siguiente método:
    <pre>
    def html_attrs(lang = 'en-US')
    {:xmlns => "http://www.w3.org/1999/xhtml", 'xml:lang' => lang, :lang => lang}
    </pre>
Esto puede usarse en Haml, como:
    <pre>
    %html{html_attrs('fr-fr')}
    </pre>
Se mostrará como:
    <pre>
    <html lang='fr-fr' xml:lang='fr-fr' xmlns='http://www.w3.org/1999/xhtml'>
    </html>
    </pre>
Puede utilizar tantos métodos de atributo tales como quiera separandolos con comas, como una lista de argumentos de Ruby. Todos los algoritmos hash se van a fusionar, de izquierda a derecha. Por ejemplo, si se ha definido
    <pre>
    def hash1
    {:bread => 'white', :filling => 'peanut butter and jelly'}
    def hash2
    {:bread => 'whole wheat'}
    Despues:
    %sandwich{hash1, hash2, :delicious => 'true'}/
    </pre>
Se mostrará como:
    <pre>
    <sandwich bread='whole wheat' delicious='true' filling='peanut butter and jelly' />
    </pre>
Se debe tener en cuenta que la lista de atributos Haml tiene la misma sintaxis que una llamada al método Ruby. Esto significa que cualquier método de atributo deben venir antes el hash literal. Los métodos de atributo no son compatibles para los atributos de estilo HTML.

#### Class and ID: . and #
El signo de punto y el numeral son representativos de CSS. Se utilizan como métodos abreviados para especificar los atributos class e id de un elemento, respectivamente. Varios nombres de clases pueden especificarse en forma similar al CSS, encadenando los nombres de clase con puntos. Se colocan inmediatamente después de la etiqueta y antes un hash de atributos. Por ejemplo:
    <pre>
    %div#things
    %span#rice Chicken Fried
    %p.beans{ :food => 'true' } The magical fruit
    %h1.class.otherclass#id La La La
    </pre>
se compila:
    <pre>
    <div id='things'>
    <span id='rice'>Chicken Fried</span>
    <p class='beans' food='true'>The magical fruit</p>
    <h1 class='class otherclass' id='id'>La La La</h1>
    </div>
    Y,
    %div#content
    %div.articles
    %div.article.title Doogie Howser Comes Out
    %div.article.date 2006-11-05
    %div.article.entry
    Neil Patrick Harris would like to dispel any rumors that he is straight
    </pre>
se compila:
    <pre>
    <div id='content'>
    <div class='articles'>
    <div class='article title'>Doogie Howser Comes Out</div>
    <div class='article date'>2006-11-05</div>
    <div class='article entry'>
      Neil Patrick Harris would like to dispel any rumors that he is straight
    </div>
    </div>
    </div>
    </pre>
Estos métodos abreviados pueden combinarse como una larga cadena de atributos; los dos valores serán fusionados como si todos se colocaron en un array. Por ejemplo:
    <pre>
    %div#Article.article.entry{:id => @article.number, :class => @article.visibility}
    </pre>
Esto es igual a:
    <pre>
    %div{:id => ['Article', @article.number], :class => ['article', 'entry', @article.visibility]} Gabba Hey
    </pre>
Se podría compilar como:
    <pre>
    <div class="article entry visible" id="Article_27">Gabba Hey</div>
    </pre>
#### Implicit Div Elements
Porque los divs se utilizan tan seguido, son los elementos predeterminados. Si sólo define una clase y/o id mediante . o #, un div se utiliza de forma automática. Por ejemplo:
    <pre>
    #collection
    .item
    .description What a cool item!
    </pre>
Esto es igual a:
    <pre>
    %div#collection
    %div.item
    %div.description What a cool item!
    </pre>
se podría compilar como:
    <pre>
    <div id='collection'>
    <div class='item'>
    <div class='description'>What a cool item!</div>
    </div>
    </div>
    </pre>
#### Empty (void) Tags: /
El carácter de barra diagonal, cuando se coloca al final de una definición de etiqueta, causa Haml a tratarlo como un elemento vacío. Dependiendo del formato, la etiqueta se procesan sin una etiqueta de cierre (: html4 o: html5), o como una etiqueta de cierre automático (: xhtml). Por ejemplo:
    <pre>
    %br/
    %meta{'http-equiv' => 'Content-Type', :content => 'text/html'}/
    </pre>
se compila como:
    <pre>
    <br>
    <meta content='text/html' http-equiv='Content-Type'>
    cuando el formato es :html4 y :html5, y así
    <br />
    <meta content='text/html' http-equiv='Content-Type' />
    </pre>
cuando el formato es :xhtml.    
