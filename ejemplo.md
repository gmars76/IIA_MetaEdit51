## Ejemplo de Uso


### Metamodelo Objetivo: ER Básico
Para realizar el ejemplo vamos a definir un metamodelo sencillo basado y por todos conocido: Un diagrama ER básico con relaciones 1 a 1 y 1 a N. El objetivo final será poder desarrollar un modelo como el de la figura 3.1 y generar el código java básico de las entidades.

![Figura 3-1: Modelo Objetivo](http://i.imgur.com/LhOEWep.png)

En el ejemplo se definirá el metamodelo de diagrama ER, en el que se presentan 2 objetos (según la nomenclatura GOPPPRR usada por MetaEdit+): Entidades y Atributos. 

Las relaciones entre las Entidades serán siempre binarias y podrán ser de dos tipos: 1 a 1 (herencia) o 1 a N.

### GOPPRR

En MetaEdit+ los metamodelos estan definidos mediante el lenguaje de metamodelado GOPPRR (Graph, Object, Property, Port, Relationship and Role). Los metatipos definidos por GOPPRR están representados en la figura 3.2.

![Figura 3-2: Estructura GOPPRR](http://i.imgur.com/aC68f39.png)

* Un *Graph* es un modelo individual (representado como un diagrama).
* Los *Objects* son los principales elementos del *Graph*.
* Las *Relationship* conecta los objetos (como la relación 1 a N une entidades en el ejemplo).
* Un *Role* conecta un objeto a la relación (discrimina el modo en que la entidad se conecta a la relación).
* Un *Port* añade matices de significado a como un Role se conecta a un *Object*.
* Una *Property* es un atributo de un *Object*.

Utilizando éstos metatipos podemos definir la estructura básica de nuestro *ER Básico*:

![Figura 3-3: Metamodelo ER Basico](http://i.imgur.com/LQCEpkR.png)

El modelo anterior se puede leer como sigue: Las Entidades están compuestas por una colección Atributos y se relacionan binariamente entre ellas de dos maneras: mediante relaciones 1 a 1 (herencia) o mediante relaciones 1 a N (1 a muchos).

Ya que tenemos el metamodelo definido vamos a pasar a implementarlo en MetaEdit+.

### Implementando el Metamodelo

#### Login
MetaEdit+ es una aplicación basada en repositorio y por tanto debe establecerse una conexión con la Base de Datos interna. En el arranque de la herramienta MetaEdit+ muestra los Repositorios disponibles y todos los proyectos abiertos en cada uno. 
Para empezar bastará con seleccionar el repositorio "Demo" marcando "User" como Repository User. Seleccionamos FamilyTree como proyecto y pulsamos "Login". Si es la primera ejecución de la herramienta y tenemos la edición de evaluación solicitará el código de licencia de evaluación que previamente hemos recibido por correo.

![Figura 3-4: Login](http://i.imgur.com/ZQxIusN.png)

Inmediatamente después se nos presentará el MetaEdit+ Launcher

![Figura 3-5: MetaEdit+ Launcher](http://i.imgur.com/UTqSg40.png)

Ahora crearemos un nuevo proyecto desde el menu "Repository/New Project..." y le damos el nombre de "ER". 

![Figura 3-6: Proyecto vacio](http://i.imgur.com/YOfW7XJ.png)

#### Creación del Metamodelo

A continuación empezamos a crear el metamodelo siguiendo una estrategia top-down, desde el *Graph* (diagrama) inicial y continuando con los *Objects*, *Relationships* y *Roles*.

Seleccionamos del Menú "Metamodel | Graph Tool" que nos abrirá la herramienta de definición del metamodelo:

![Figura 3-7: Graph Tool Inicial](http://i.imgur.com/xy2gTud.png)

Ahora vamos a crear dos propiedades globales al diagrama "Nombre" y "Versión".

En la pestaña "Basics" pasamos a introducir el nombre de nuestro metalenguaje "ER" y en el apartado de propiedades pulsamos con el botón derecho "Add Property..." y seleccionamos "New Property Type" 

![Figura 3-8: New Property Type](http://i.imgur.com/s6w0pmJ.png)

Le damos nombre "Nombre" y tipo "Editable List" y pulsamos en "Save and close" para que se guarde. Añadimos otra propiedad "Version" de tipo "String" de modo que quede como en la figura 3-9.

*Es importante hacer notar que la propiedad que tenga el prefijo "*" será la que se establezca como identificador del elemento (Graph u Object), pudiéndose cambiar pulsando en otra propiedad y pulsando "set as identifier".

![Figura 3-9: Basics relleno](http://i.imgur.com/VSrcw6b.png)

El siguiente paso es definir los principales elementos del metalenguaje (Objects, Relationships y Roles) y sus propiedades. Para ello seleccionamos la pestaña "Types" del Graph Tool e iremos creando cada uno de los elementos requeridos en nuestro lenguaje.

![Figura 3-10: Types vacio](http://i.imgur.com/2RXSluA.png)

La forma de proceder es similar para todos los elementos: Seleccionando con el botón derecho la opción "Add new..." sobre una columna determinada crearemos el elemento que corresponda a la columna, pudiendo añadir propiedades de la misma forma que hemos efectuado con el elemento Graph en la pestaña "Basics".

##### Creación de los Objects

En nuestro metamodelo necesitamos crear dos "Objects": Entidad y Atributo

Primero procedemos a crear el Objeto "Atributo" al cual le asignaremos dos propiedades tipo string: "Nombre" (identificador) y "Tipo".

![Figura 3-11: Object Atributo](http://i.imgur.com/mwalYvP.png)

A continuación creamos el Objeto "Entidad" al cual le asignaremos la propiedad tipo string "Nombre" y una propiedad especial denominada "Atributos". 
Ésta propiedad será una colección de Object de tipo "Atributo" (previamente definido). Para ello, tras añadir la nueva propiedad y darle el nombre "Atributos" seleccionamos el datatype "Collection" y en item type seleccionamos el "Object" correspondiente, tal y como muestra la figura 3-12.

![Figura 3-12: Property Tool Atributos](http://i.imgur.com/8ymA4U5.png)

Una vez realizado, el Objeto "Entidad" debería reflejarse como lo hace la figura 3-13:

![Figura 3-13: Object Entidad](http://i.imgur.com/5dtGIZZ.png)

Una vez finalizado podemos pulsar en "Save" o "Save and close" para grabar el progreso de nuesto metamodelo.

##### Creación de los Relationships

De forma similar a la creación de los "Object", creamos en la columna "Relationships" los dos tipos de relación requeridos en nuestro metamodelo, "1a1" y "1aN", añadiéndoles a cada una la propiedad "Nombre" de tipo String.

![Figura 3-14: Relación 1a1](http://i.imgur.com/Zh18FPi.png)

![Figura 3-15: Relación 1aN](http://i.imgur.com/WvmBDcn.png)

##### Creación de los Roles

A continuación y de la misma manera que en los elementos anteriores creamos los Roles necesarios. Los Roles definen el comportamiento de un Object en la relación y para simplificar nuestro metamodelo necesitaremos 3: "Origen", "Destino" y "DestinoN".

Ninguno de los mismos tiene propiedades asignadas, con lo que bastará con establecer sus nombres.

![Figura 3-16: Types Relleno](http://i.imgur.com/HayICPW.png)

##### Creación de los Simbolos

Desde la pestaña "Types" podemos modificar los símbolos de cada uno de los elementos del metamodelo pulsando con el botón derecho del ratón y seleccionando "Edit Symbol" que nos abrirá el "Symbol Editor", donde tenemos a nuestra disposición un editor con las herramientas gráficas básicas para realizar la representación gráfica del elemento. 

![Figura 3-17: Symbol Editor](http://i.imgur.com/9NNKEma.png)

* Símbolo de 'Atributo':
Para crear la representación gráfica del Objeto "Atributo" crearemos un texto vacio. Una vez creado lo seleccionamos con el botón derecho y pulsamos en la opción "Format..." (o hacemos doble-clic sobre él). 

![Figura 3-18: Format Atributo](http://i.imgur.com/5EPBsCC.png)

En la pestaña Context seleccionamos la opción "Generator" e introducimos el texto ":Nombre '  (' :Tipo ')'" con lo que estamos generando dinámicamente el contenido del campo, componiendolo con las propiedades del Object que representa. 

![Figura 3-19: Symbol Atributo](http://i.imgur.com/ZZdKQZk.png)

Al salvar el resultado vemos que aparece un recuadro rojo con un punto de mira en el centro, éste elemento es el que representa el contorno del objeto gráfico resultante.

* Símbolo de 'Entidad':

Para definir la representación de "Entidad" empezaremos creando un rectángulo de fondo, estableciendo un color de fondo mediante la opción "Format..." del mismo.

A continuación creamos el campo principal de la entidad, añadiendo un campo tipo texto y estableciendo mediante la opción de "Format..." que el contenido refleje la propiedad "Nombre" de forma dinámica.

![Figura 3-20: Format Entidad.Nombre](http://i.imgur.com/5jVRQaT.png)

Después necesitamos representar la colección de atributos de la entidad para lo que incluimos un elemento de tipo "Template", pulsando en un punto del interior y haciendo doble clic en un punto un poco mas abajo. Con ésto aparecen una serie de recuadros respresentando los elementos de la colección a mostrar. 

Si seleccionamos del menú contextual la opción "Edit Layout" podremos minimizar la separación entre los elementos y el ancho de los mismos de forma que ocupen el cuadro de fondo.

Solo nos queda establecer los elementos que se representan para lo que mediante la opción "Format..." del template seleccionamos la pestaña "Subobjects" y establecemos la fuente como "Collection Propery" y marcamos "Atributos".

![Figura 3-21: Format Entidad.Template](http://i.imgur.com/u4TzF5g.png)

![Figura 3-22: Symbol Entidad](http://i.imgur.com/IIu4VVl.png)

* Símbolo de 'DestinoN'

Para finalizar estableceremos la representación para la relación 1aN, modificando el símbolo del Role "DestinoN".

Bastará con dibujar una línea horizontal con un circulo en el extremo derecho:

![Figura 3-23: Symbol DestinoN](http://i.imgur.com/SI2mP7L.png)

##### Salvando el Repositorio

Para grabar el progreso de nuestro modelo es importante realizar "Commit" en el repositorio desde el MetaEdit+ launcher: 

![Figura 3-24: Commit-Abandon](http://i.imgur.com/ZbfnQO0.png)


##### Estableciendo las Relaciones (Bindings)

Para finalizar la definición del metamodelo solo resta establecer como los elementos se relacionan entre sí, estableciendo el comportamiento real de las Relationships definidas en el mismo, para ello MetaEdit+ establece los llamados "Bindings" entre los elementos de nuestro metamodelo.

Desde la ventana Graph Tool seleccionamos la pestaña "Bindings"

![Figura 3-25: Bindings vacio](http://i.imgur.com/IVJAqMK.png)

* Relación 1a1:

En la columna "Relationships" pulsamos "Add..." y añadimos la Relación "1a1". Con ella seleccionada Añadimos el Role "Origen" y el Object "Entidad". Con la misma Relationships "1a1" seleccionada, añadimos otro Role "Destino" y marcamos el Object "Entidad" de nuevo. 

De ésta forma estamos indicando que la relación 1a1 une dos objetos "Entidad", el primero con el Role "Origen" y el segundo con el Role "Destino"

![Figura 3-26: Bindings 1a1](http://i.imgur.com/ADta5he.png)

* Relación 1aN:

En la columna "Relationships" pulsamos "Add..." y añadimos la Relación "1aN". Con ella seleccionada Añadimos el Role "Origen" y el Object "Entidad". Con la misma Relationships "1a1" seleccionada, añadimos otro Role "DestinoN" y marcamos el Object "Entidad" de nuevo. 

De ésta forma estamos indicando que la relación 1aN une dos objetos "Entidad", el primero con el Role "Origen" y el segundo con el Role "DestinoN"

![Figura 3-27: Bindings 1aN](http://i.imgur.com/erscUSb.png)

*Es posible establecer la cardinalidad de una relación desde la columna Role, seleccionando "Cardinality..."

##### Grabar el progreso

Podemos pulsar en "Save and close" en la Graph Tool y realizamos el Commit en el MetaEdit+ Launcher para grabar el avance.

#### Desarrollando el Modelo

Para crear un modelo que siga nuestro metamodelo pulsamos en el botón "Create Graph" y a continuación seleccionamos el metamodelo a seguir, en éste caso "ER"

![Figura 3-28: Create Graph](http://i.imgur.com/Ivv97gU.png)

A continuación establecemos las propiedades globales del diagrama:

![Figura 3-29: ER Graph: Atributos globales](http://i.imgur.com/4UgKHoD.png)

Una vez establecidas las propiedades globales se nos presenta la herramienta de definición de modelos, con la barra de acciones representando los elementos disponibles de nuestro modelo "Entidad", "Atributo" y las relaciones correspondientes. 

![Figura 3-30: ER Graph: Editor vacio](http://i.imgur.com/Ng96W6L.png)


Su funcionamiento es suficientemente intuitivo y nos permite crear fácilmente un modelo de nuestro dominio a semejanza del objetivo final del ejemplo, seleccionando los elementos definidos en nuestro metamodelo de la barra de acciones en la parte superior y rellenando las propiedades en la parte inferior izquierda.

![Figura 3-1: Modelo Objetivo](http://i.imgur.com/LhOEWep.png)

#### Transformaciones M2T

Como se ha indicado anteriormente MetaEdit+ utiliza el lenguaje propio *MERL* para la transformación M2T, y por su complejidad queda fuera del alcance del presente análisis, pero indicaremos de forma ágil como conseguir el objetivo final del metamodelo: su transformación a un lenguaje de programación (java).

Para generar código a partir de un diagrama se abre el mismo y desde el menú "Graph" se selecciona "Generate" indicando una de las transformaciones genéricas suministradas automáticamente por MetaEdit+.

![Figura 3-31: ER Graph: Seleccionar Transformación](http://i.imgur.com/DjZ1kCI.png)

Por ejemplo, si generamos la transformación "Export Graph to HTML" podemos observar la definición de nuestro modelo en una página html, mostrando todos los objetos y sus relaciones.

![Figura 3-32: ER Graph: Resultado Transformación HTML](http://i.imgur.com/Q1eoiaA.png)

Si lo que queremos es definir una transformación propia, el menú "Graph" seleccionamos "Edit Generators..." y en el menú pinchamos en "Generator | New..." estableciendo el nombre deseado para nuestro Generador.

Para lograr nuestro objetivo básico, introducimos el siguiente contenido en el Generador.

```
Report 'java_Entidades'

subreport 'java_translators' run

foreach .() 
{ 
	@ent = :Nombre 
	'public class ' :Nombre 
	
	/* Relaciones 1 a 1: HERENCIA */ 
	do >1a1 {
		@asociacion_nombre =:Nombre
		do ~Origen {
			do .() {
				if not (:Nombre = @ent) then
					' extends ' :Nombre
/*					if @asociacion_nombre then '		// ' @asociacion_nombre endif   */
				endif
			}
		}
	}
	
	' {' newline
	
	/* Propiedades */
	do :Atributos {
		'	private ' :Tipo ' ' :Nombre ';' newline
	}
	
	/* Relaciones 1 a N */ 
	newline
	do >1aN {
		
		@asociacion_nombre =:Nombre
		do ~Origen {
			do .() {
				if not (:Nombre = @ent) then 
					@instancia = :Nombre%lower
					'	private ' :Nombre ' ' @instancia ';'
					if @asociacion_nombre then '		// ' @asociacion_nombre endif
				
				endif
			}
		}
		do ~DestinoN {
			do .() {
				if not (:Nombre = @ent) then
					@instancia = :Nombre%lower
					'	private List<' :Nombre '> ' @instancia 's;'
					if @asociacion_nombre then '		// ' @asociacion_nombre endif
				endif
			}
		}
		newline
	}
	'}' newline newline
}	

endreport	
```

endreport

![Figura 3-33: ER Graph: Generador ](http://i.imgur.com/iM2XhmO.png)

* Como se observa el lenguaje MERL resulta algo engorroso aunque cumple con los objetivos deseados.

Una vez creado, Podemos ejecutarlos desde el menú "Graph" con la acción "Generate" y seleccionando el generador recién desarrollado.

![Figura 3-34: ER Graph: Resultado Java ](http://i.imgur.com/zqkXFsq.png)



