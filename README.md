# Pug
## Introduccion
Un preprocesador es una herramienta que nos permite escribir pseudocódigo de forma modular, más fácil de reusar, leer, y mantener. pseudocódigo que después será convertido a CSS o HTML estándar que el navegador entiende.

Gracias a los preprocesadores podemos extender las características de CSS y HTML al nivel de otros lenguajes de programación, permitiéndonos usar características como variables, funciones y mixins.
### Variable
Pedazo de memoria reservado para almacenar un valor, correspondiente a un tipo de dato.

Es donde se **guardan (y se recuperan) datos** que se utilizan en un programa. *Generalmente aqui guardamos los colores que va a llevar nuestra pagina para que no sean muchos y se vuelva un piñata.*
### Funcion
La variable solo te permite guardar un dato, es por eso que los prepocesores te permite jugar con funciones. 

Las fucniones tienen la posibilidad de tener parametros o argumentos, que son **variables** que modifican su comportamiento. 
### Mixin
Es una **clase** cuya finalidad es oferecer una **funcionalidad** que pueda ser reutilizada en otras clases pero que no esta pensada para usarse de forma automatica.
### Por que utilizarlos ?
+ Te salva tiempo y dinero al tener la opcion de reutilizar codigo.
+ Tener un codigo mas sencillo de mantener y editar.
+ Modularizar nuestro proyectos de una forma logica y sencilla.

## Metodologia BEM
[Metodologia BEM Oficial](http://getbem.com/)

Es una metodologia de trabajo creada por **Yandex** para proyectos web grandes o pequeños. 
El objetivo de BEM es dividir lógicamente las piezas de las que se compone una web.

BEM establece que debemos usar clases para nuestro selectores, clases que se dividen en:
+ **Bloque:** Los bloques son nuestros contenedores más grandes que a su vez contienen elementos u otros bloques.
```.bloque{}```
+ **Elementos:** Los elementos siempre forman parte de un bloque, normalmente son los botones, textos, imágenes etc.
```.bloque__elemento{}```
+ **Modificadores:** Los modificadores se usan para establecer estilos diferentes a un mismo bloque o elemento.
```.bloque--modificador{}```

![Imagen de BEM](https://miro.medium.com/max/2390/1*tBFD64u6_kmPVFNxjau17A.png)

![Ejemplo de BEM con galaeria](https://static.platzi.com/media/user_upload/Captura%20de%20Pantalla%202020-12-04%20a%20la%28s%29%2003.48.42-191394f8-cd0c-4e6e-a387-29e371948ce9.jpg)

## Guías para creación y mantenimiento de código
> "Tener un código que luzca como si una sola persona lo haya escrito" - Wilson Sánchez

+ [Shopifhy](https://polaris.shopify.com/design/design)
+ [Atlassian](https://atlassian.design/)
+ [Salesforce](https://www.lightningdesignsystem.com/)
 
# Preprocesadores para HTML
## Introduccion a Pug
Pug es un generador de templates implementado con Javascript que nos permite escribir un pseudocódigo limpio y fácil de leer que será compilado a HTML.

[Proyecto GitHub](https://github.com/daywalkerhn/platzi-games-pug-publico)
[Getting start with Pug](https://pugjs.org/api/getting-started.html)
## Interpolacion
La interpolacion es la anidacion de elementos dentro de otros elementos.
## Variables
Las variables no vienen de forma nativa en HTML pero con PUG podemos usarlas. En ellas almacenamos datos y los reutilizarlos en todo nuestro archivo HTML evitándonos tener que escribir lo mismo una y otra vez.
### Declarar variables
```
-var titulo = "Subtítulo Principal" 
-var titulos = ["Título Principal", "Subtitulo 1", "Subtitulo 2", "Subtitulo 3"]
```
### Llamar variables
```
h2= titulo
h2 #{titulos[0]} - array primer elemento
h2 #{tituos[0][1]} -  array primer elemento caracter 1 
```
## Condicionales
```
if  usuario
	a Hola #{usuario}
else
	a.boton Registro
```  
## Loop - For
```
each  titulo  in  titulos
	li= titulo
```
Esto me sirvo por si hay un menu que se repite en distintas secciones de mi pagina web.
## Mixins
Su finalidad es ofrecer una funcionalidad que pueda ser **reutilizada** en otras clases pero que no está pensada para usarse de forma autónoma. Nos permite crear bloques reusables de código que cambian su resultado dependiendo del parámetro que enviemos.

Con los mixin logramos escribir menos código, produciendo un código más claro, más expresivo y sobre todo más fácil de mantener.
### Declaracion
```
// Se puede usar sin parametros
mixin caja(imagen, titulo, contenido)
	.caja
	.caja__imagen: img(src="./img/"+imagen , alt="imagen")
	.caja__contenido
	h3=titulo
	p=contenido
	a.boton Leer Mas
```
### Empleo
```
+caja("imagen.png", titulos[1], "Lorem ipsum dolor sit amet" )
+caja("imagen.png", titulos[2], "Lorem ipsum dolor sit amet" )
+caja("imagen.png", titulos[3], "Lorem ipsum dolor sit amet" )
```
## Includes y Extends
Pug funciona como un generador de plantillas, dos de sus principales características para lograrlo son Includes y Extends. Separamos el codigo en distintos archivos.

Los  **includes**  sirven para incluir un archivo de extensión  _*.pug_  dentro de otro. Los que hace es copiar el codigo tal cual, parte que sabemos que no se le van a seguir agregando cosas y que permanecera estatica.

Para llamarlos y ruta.pug esta en un archivo diferente:
```
include ruta.pug
```
Los  **extends**  te permiten adicionar bloques de código a una página. Esto seria como una plantilla.

Forma de "declararlo":
```
html(lang="es")
include  head.pug
body
	header
	h1= titulo
	if  usuario
		a Hola #{usuario}
	else
		a.boton Registro
	block  contenidos // Importante!
```
Forma de llamarlo al archivo principal:
```
extend ruta.pug
block  contenidos // Importante! 
```
Usamos esto por el problema del cierre de las etiqueas, en el proyecto si uso include, pug lo entenderia que el resto del contendo esta dentro de header.
# Datos Sintaxis PUG
+ No hace falta poner `div.intro__img` solo tengo que poner `.intro__img` y cuando se **compile** lo interpretara como una etiqueta **div.**
+ Cuando tengo **un elemento**  para anidar, puedo hacer `.intro__img: img(src="ruta" alt="img")`
+ Cuando el texto queda es muy largo puedo hacer:
```
p

	| Lorem ipsum dolor sit amet consectetur adipisicing elit.
	| At doloremque excepturi tenetur fugit dolore, sed quia cumque
	| repellendus quisquam possimus expedita officiis nisi quidem
	| pariatur nulla voluptas molestiae quo recusandae.
```
+ Si quiero anidar un elemento en un texto largo:
```
p

	| Lorem ipsum dolor sit amet consectetur adipisicing elit.
	| At doloremque excepturi tenetur fugit dolore, sed quia cumque
	| repellendus quisquam possimus expedita officiis nisi quidem
	| pariatur nulla voluptas molestiae quo recusandae.
	span Proin se urna quis orci expedita officiis nisi quidem pariatur nulla voluptas molestiae quo recusandae.
```


