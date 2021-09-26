<h1> Primeros pasos con este proyecto (Descarga materiales aqui) </h1> 

El package.json es necesario porque en él vamos a instalar las dependencias, las dependencias tienen ciertas aplicaciones de node que tienen un paquete en específico que hace que el archivo pueda actualizarse a la nueva versión para que así el trabajo tenga las mismas versiones que la que te pidieron. 

<h1> Creando un archivo de Gulp </h1> 

Gulp utiliza es un tipo de función que hace <b> más sencillo hacer lo ya aprendido en JavaScript</b>. 

Si usamos un <b>require</b> entonces vamos a <b>traer una función a la página de gulp</b>: 
```js
const { series } = require('gulp'); 
```
Con esto estamos <b>extrayendo la función de <b>series</b> de gulp</b>. 

La función <b> exports </b> sirve para exportar o hacer disponible nuestro código de manera externa, en vez de colocar el nombre de la función y un paréntesis, vamos a colocar exports.<b>nombre de la función</b> = algo; colocandolo así vamor a llamar la función: 
```js 
exports.hola = hola; 
```

Si colocamos un done entonces vamos a decirle a la terminar que hasta ahí termina esa función: 
```js 
function hola( done ) {
    console.log('Hola mundo en Gulp'); 

    done(); 
} 
```
La función de series lo que hace es que te permite que cuando ejecutes una función puedas ejecutar otra: 
```js 
exports.tareas = series( css, javascript, minificarHTML ); 
```
Para mostrar el valor en la terminal debemos colocar gulp y después el nombre del export, pero si queremos escribir menos en la terminal para poder enviar el mensaje entonces podemos modificar el export colocandole un default y después <b>en la terminal solo debemos colocarle gulp</b>: 
```js 
exports.default = series( css, javascript, minificarHTML ); 
```
Otra función es parallel, parallel lo que hace es lo mismo que series, la diferencia es que parallel te da los valores al mismo tiempo, pero finalizan primero los que tenían menos información: 
```js 
exports.default = parallel( css, javascript, minificarHTML ); 
```

<h1> Compilando SASS con Gulp </h1> 

Una diferencia es cuando importamos algo son las llaves: 
```js 
const { series, parallel } = require('gulp'); 
const sass = require('gulp-sass'); 
```
Lo que pasa es que el archivo de gulp tiene muchos archivos, pero si colocamos las llaves entonces seleccionamos solamente uno de esos valoresl, pero si el archivo que  importaremos tiene solo un archivo entonces podemos seleccionarlo sin las llaves. 

Si queremos importar una imágen en un archivo scss entonces  tenemos que colocar un return con la ubicación del archivo: 
```js 
function css(  ) { 
    return src('src/scss/app.css'); 
}
```

<h1> Escuchar por cambios con watch </h1> 

Si queremos agregar más elementos entonces tenemos que volver a ejecutar nuestra hoja de estilos, gulp sirve para automatizar tareas, en este caso una función que sirve es <b>watch</b>, whatch lo que hace es que podemos decidir que archivos queremos que cambien cada vez que le modifiquemos algo al scss: 
```js 
function watchArchivos() {
    watch( 'src/scss/app.scss', css ); 
}
```
Esto es algo parecido a Open With Live Server. 

Si queremos que pare esta función entonces en la terminal debemos colocarle un Ctrl + C, después solo debemos darle un enter y ya no estará activa esa función, pero si la vuelves a ejecutar entonces volverán a cambiarse los valores cada vez de guardes un cambio en el scss. 

<h1> Creando diferentes archivos y variables </h1> 

Una de las ventajas de SASS es que nuestros proyectos van a ser más fáciles de mantener porque una de sus características es que te permite separar dentro de diferentes archivos toda tu funcionalidad de SASS. 

Si queremos incluir un archivo scss en otro entonces en su propia carpeta tenemos que colocarle una diagonal baja y después el nombre del archivo: 
<img src="imagenesNotas/extencion scss.PNG"> 

Lo que pasa es que todo lo que pongamos en el archivo con la diagonal baja se va a incluir en el otro. Algo importante es que tenemos que tenemos que agregarle al documento original que lo queremos agregar porque o si no no va a pasar nada, lo que tenemos que colocar es un import: 
```scss
@import 'variables'; 
```
Cuando hagamos esto lo que pasará es que cuando modifiquemos el archivo con la diagonal no pasará nada, pero si sigue diferente y modificamos y guardamos el archivo original o sin la diagonal lo que pasará ees que ya va a hacerse ese cambio. Si queremos que se haga el cambio sin necesidad de  hacer todo entonces tenemos que colocar esto: 
```js 
function watchArchivos() {
    watch( 'src/scss/*.scss', css ); 
}
```
Lo que pasa es que si colocamos un asterisco en vez de un nombre, lo que le decimos a la consola es que no importa el nombre que tennga el archivo porque mientras la extensión sea scss entonces se va a hacer el cambio. Algo que pasa es que el asterisco solo busca cualquier archivo en la carpeta actual, pero si esta en otra carpeta el archivo con el que lo estamos vinculando entonces se tiene que hacer algo diferente: 
```js 
function watchArchivos() {
    watch( 'src/scss/**/*.scss', css ); 
}
```
Eso lo que hace es que buscará todos los archivos con esa extensión. 

<h1> Agregando Fuentes de Google Fonts </h1> 



<h1> Creando el Header </h1> 

Anidar es un bucle que consiste en meter ese bucle dentro de otro: 
```scss 
.header {
    background-color: $verde; 
    
    .contenido-header {
        padding: 1rem; 

    } 

    h1 {
        margin: 1rem; 
    }
}
```

<h1> Aplicando SASS al Header y Nav </h1> 

Hay una opción que se llama aperson, hay veces que estas anidando algo pero tienes que conservar algo dentro de otro objeto pero entonces  te marcaría un error, pero aperson lo que hace es que si quieres modificar algo dentro de ese mismo objeto en scss lo que paasará es que el archivo que esta dentro con el aperson lo va a poner al mismo nivel que el objeto que lo rodea: 
```scss
a {
    color: $blanco; 
    font-size: 2rem; 

    &:hover {
        color: $amarillo; 
    }
}
```

<h1> Creando Mixins en SASS </h1> 

Un Mixin es una clase que contiene métodos para otras clases. Para crear un mixin debes colocar esto: 
```scss 
@mixin nuevoMixin {  
    font-size: 3rem; 
    color: $morado; 
    text-transform: uppercase; 
}
```
Y para poner en el código de otras páginas scss tenemos que poner esto: 
```scss 
@include nuevoMixin; 
```
Hay una opción en la que puedes hacer inteligente al mixin, tenemos que colocar un paréntesis y dentro de él puedes colocarle un valor: <b> ($transform)</b>, lo que debes hacer en colocarle ese mismo valor a un transform como un text transform: 
```scss
@mixin nuevoMixin($transform) {  
    font-size: 3rem; 
    color: $morado; 
    text-transform: $transform; 
}
```
Luego para ponerle valores entonces debes colocarle un paréntesis y ahí dentro le vas a colocar el valor que tendrá esa etiqueta dentro del transform: 
```scss
@include nuevoMixin(uppercase); 
```
Una de las cosas que se pueden hacer es crear objetos y luego meterlos en su mixin:
```scss 
        @include telefono {
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
        }
```
El problema es que no pueden ser demasiado grandes, para solucionar eso solamente tenemos que colocarle un @content: 
```scss
@content; 
```

La ventaja de los mixins es que fomentan la reutilización de código y evitan problemas típicos asociados con la herencia múltiple.

<h1> Vídeo en HTML5 </h1> 

Para agregar un vídeo en una página lo que se tiene que hacer es colocar una etiqueta llamada video, y si es solo un vídeo entonces lo ponemos con un src, pero si son muchos entonces los colocas dentro de las etiquetas de apertura y cierre de video: 
```html
<video src="video/concierto.mp4">  </video> 
```
Una cosa es que cuando coloques el vídeo va a aparecer estático, para poder controlar el vídeo debes agregarle algo llamado controls, lo que te va a permitir es ponerle en pausa, avanzar, etc. 

Otra opción es muted, muted sirve para que el vídeo no se escuche.

Loop es una función que si la colocas entonces te va a reproducir el vídeo automáticamente cada vez que termine el vídeo. 

Hay una función que se llama autoplay, autoplay lo que hace es que cuando recarguemos la página se va a reproducir el vídeo automáticamente: 
```html
<video src="video/concierto.mp4" controls autoplay muted loop>  </video> 
```
Para agregar varios vídeos entonces debemos colocar una etiqueta llamada source, esta etiqueta es solo de apertura, dentro de source vamos a colocar un src con el vídeo, algo importante es que tenemos que poner el tipo de vídeo, puede ser mp4, ogg o webm, una cosa importante es que a veces un vídeo no agarra en distintas plataformas, por eso se utiliza source, para poner varias opciónes: 
```html 
<video controls autoplay muted loop> 
    <source src="video/concierto.mp4" type="video/mp4"> 
    <source src="video/concierto.ogg" type="video/ogg"> 
    <source src="video/concierto.webm" type="video/webm"> 
</video> 
```

<h1> Añadiendo un efecto sobre el vídeo </h1> 

Una etiqueta con posición absoluta no podrá salirse de la etiqueta padré si es que tiene la posición relativa, lo que pasará es que la etiqueta con posición absoluta podrá moverse donde sea pero no podrá salirse de la etiqueta con la posición relativa: 
```scss
.video {
    position: relative; 

    .overlay {
        position: absolute; 
        width: 10rem; 
        height: 10rem; 
        background-color: $rosa;  
    } 
} 
```
Para sacarlo de la posición relativa entonces debemos usar un número negativo. 

En la parte hasta abajo de el vídeo hay una pequeña línea que no esta cubierta o no esta el margen negro del vídeo, eso pasa porque los vídeos por default tienen un inline, y para quitar eso debemos colocarle un display block: 

Un overflow especifica si quieres recortar el contenido, dibujar barras de desplazamiento o mostrar el contenido excedente en un elemento a nivel de bloque. 

<h1> Creando un Degradado en CSS3 </h1> 

Si queremos colocar un degradado entonces debemos colocar un background, y seguido de él un <b>linear-gradient</b> con esto ahora solo debes colocarle sus valores que quieres: 
```scss
.overlay {
        background: linear-gradient( to top, $rosa, $amarillo); 
    } 
```
Esto lo que hará será hacer un degradado hacia arriba comenzando por el color rosa y terminará con el color amarillo. Algo que podemos hacer es colocarle un porcentaje para que el color este hasta un punto y después de ese punto se va a aplicar el otro color. Si queremos que los colores vayan en diagonal entonces al comienzo del código debes colocarle un deg: 
```scss
.overlay {
        background: linear-gradient( 45deg, $rosa, $amarillo); 
    } 
```

<h1> Finalizando el Contenido sobre el vídeo </h1> 

El z-index sirve para poder colocar algo detras de el objeto o fondo, también puede colocarlo delante de algún objeto: 
```scss
    .contenido-video {
        position: relative; 
        z-index: 1; 
    }
```

<h1> Creando la sección de información sobre el festival </h1> 

Cuando colocamos un line-height entonces no se le coloca que es pixeles o rem, te lo pone en automatico. 

Cuando usamos un flex direction column entonces los valores justify content y align items, cambian de dirección. 

<h1> Gulp para minificar imágenes </h1> 

Si queremos crear una funcion con la cual podamos seleccionar todas las imagenes para poder inificarlas entonces solo debemos colocar esto: 
```js 
function imagenes() {
    return src('src/img/**/*') 
}
```

<h1> Notificando imágenes comprimidas </h1> 



<h1> Utilizar Gulp para automatizar imagenes Webp </h1> 



<h1> Primeros pasos con Line Up </h1> 

La diferencia entre un ol y un ul es que el ol te lo pone en forma de lista, en cambio el ul te pone todo ordenado por puntos: 
```html
<ul> 
    <li> hola </li>  
    <li> hola </li>  
</ul> 

<ol> 
    <li> hola </li>  
    <li> hola </li>  
</ol> 
```

<h1> Primeros pasos con el SASS para el Line Up </h1> 

Los :after siempre tienen que tener un content porque entonces no funciona, puede estar vacío incluso: 
```scss
&:after {
    content: ''; 
}
```
