# LAB | Express Beers

## Introducción

A veces, nos gustaría tener una lista muy descriptiva de todas las cervezas para poder ver su tipo, color, el porcentaje de alcohol de cada cerveza o qué cerveza se combina bien con algo de comida. En este ejercicio, crearemos una aplicación web donde el usuario podrá ver una lista de cervezas, recibir sugerencias aleatorias y leer una explicación muy descriptiva de cada cerveza.

"¿Cómo obtendremos toda esta información?". Bueno, usaremos un paquete npm como fuente de datos.

Para este ejercicio, trabajaremos con el paquete npm **[PunkAPI](https://www.npmjs.com/package/punkapi-javascript-wrapper)**. En segundo plano, el paquete se comunica con una _base de datos_ remota que contiene todas las cervezas. El paquete nos permite utilizar sus métodos que pueden ayudarnos a mostrar cervezas. Cada cerveza tiene algunas propiedades, y podemos jugar con estos datos para practicar el trabajo con plantillas, `layuts` y` partials` de Handlebars.

**En este lab, también podemos practicar la lectura de documentos externos (PunkAPI) y aprender cómo obtener lo que necesitamos de la base de datos.**

## Requerimientos

- Hacer `fork` este repositorio.
- Hacer `clone` del respositorio.

## Entrega

- Una vez que termines, correr los siguientes comandos:

```shell
$ git add .
$ git commit -m "done"
$ git push origin master
```

- Crear un Pull Request para poder corregir.

## Instrucciones

### Paso 0: Setup Inicial

Para ejecutar nuestra aplicación, lo primero que tenemos que hacer es instalar todas sus dependencias. Ejecute el siguiente comando:

```shell
$ npm install
```

Para correr la aplicación:

```shell
$ node app.js

# you can also run: npm start
```

### Paso 1: Creando el layout

Nuestro código de inicio incluye la configuración básica necesaria para ejecutar nuestra aplicación. La ruta **`/`** está configurada para representar el archivo `index.hbs`. Comencemos creando un layout.

Dentro de la carpeta `views`, cree un archivo` layout.hbs`. En la iteración adicional, puede darle a su aplicación algo de estilo, pero por ahora, centrémonos en la lógica.

Recuerde agregar el `{{{body}}}` al **layout**.

Agregue una barra de navegación que incluya enlaces a 3 páginas:

- _Home_ ==> debe navegar a `/`.
- _Beers_ ==> debe navegar a `/beers`.
- _Random Beer_ ==> debe navegar a `/random-beer`.

Layout listo, pasemos a la creación de estas tres páginas.

### Paso 2 - Home _page_

- La primera página debe ser **Inicio** y debe mostrarse en **`/`**. El archivo que se renderiza es `index.hbs`.
- Este archivo debe incluir la _imagen de cerveza_, que puede encontrar en `/public/images`. Junto con la imagen,`index.hbs` debe tener dos enlaces:` Check the Beers!` Y `Check a Random Beer`. Ambos enlaces deben navegar a las rutas correspondientes (que también definimos previamente en nuestra barra de navegación). Más tarde, puede diseñar estas etiquetas `a` para que parezcan botones.

![image](https://user-images.githubusercontent.com/23629340/36723774-7d791ef2-1bb1-11e8-991b-39dbf4fd8a59.png)

### Paso 3 - Beers _page_

Lo siguiente en lo que trabajaremos es en una página donde podemos presentar todas las cervezas que recuperaremos de la base de datos. Esta página será renderizada cada vez que el usuario visite la ruta `/beers`.

Esto nos lleva a la conclusión de que en este paso, tenemos las dos áreas de enfoque principales:

- La ruta `/beers`, y
- La vista `beers.hbs`.

#### Paso 3.1 La ruta `/beers`

En este paso, tendremos un par de micropasos. :

- Cree una ruta `/beers` dentro del archivo `app.js`.
- Dentro de la ruta `/beers`, llame al método `getBeers()`(**PunkAPI** proporciona este método, y puede encontrar más sobre él [aquí](https://www.npmjs.com/package/punkapi-javascript-wrapper#getbeersoptions)). **Llamar al método `.getBeers ()` devuelve una promesa que debería resolverse con una matriz de 25 cervezas**.
- Más adelante, deberías pasar esa matriz a la vista `beers.hbs`.

El ejemplo de cómo funciona este método se muestra a continuación:

```js
punkAPI
  .getBeers()
  .then(beersFromApi => console.log('Beers from the database: ', beersFromApi))
  .catch(error => console.log(error));
```

#### Paso 3.2 La vista `beers.hbs`

- Cree un archivo `beers.hbs` para renderizar cada vez que llamemos a esta ruta.
- Este archivo debería tener acceso a las cervezas que obtenemos como respuesta de la base de datos. Recuerde, debe llamar al método `render` después de obtener la matriz _beers_. *_Pista:_ Eso significa que dentro de la función estás pasando al método `then`. :wink:*
- En la vista `beers.hbs`, recorra la **matriz de cervezas** usando un bucle`{{#each}}`. Muestra una **imagen**, **nombre**, **descripción** y **tagline**.

Ahora, cuando haga clic en el enlace "Beers" en la barra de navegación superior o en el botón "Check the beers", debería poder ver todas las cervezas. :boom:

### Paso 4 - Página random beer

Como en el paso anterior, tendremos que centrarnos en crear una ruta para mostrar una cerveza aleatoria. Cuando se recupera una cerveza al azar, tenemos que pasarla a la vista.

#### Paso 4.1 La ruta `/random-beer`

- Creemos la ruta `/random-beer`.
- Dentro de la ruta, debes llamar al método PunkAPI `getRandom()`. Devuelve una promesa que se resolverá con un objeto de cerveza diferente en cada llamada. Mire la [documentación](https://www.npmjs.com/package/punkapi-javascript-wrapper#getrandom) para comprender la estructura de los datos que se supone que debe recuperar. :+1:

El ejemplo de cómo funciona este método se muestra a continuación: 

```js
punkAPI
  .getRandom()
  .then(responseFromAPI => {
    // aqui ponemos el resto de nuestro código después
  })
  .catch(error => console.log(error));
```

- Finalmente, la cerveza recibida debe pasarse al archivo `random-beer.hbs`. Aún no tienes este archivo, así que procedamos a crearlo.

#### Paso 4.2 La vista `random-beer.hbs`

- El archivo `random-beer.hbs` debería mostrar la cerveza aleatoria que se recuperó de la base de datos. Debes mostrar una **imagen**, **nombre**, **descripción**, **tagline**, **maridaje de alimentos** y **consejos de cervecería**. La siguiente imagen muestra cómo podría verse esta página si le da un poco de estilo. Sin embargo, el estilo lo pondremos después, así que, por ahora, concéntrate en renderizar toda la información:

![image](https://user-images.githubusercontent.com/23629340/36724536-c5924892-1bb3-11e8-8f22-fd1f8ce316af.png)

Ahora, cada vez que el usuario hace clic en el enlace _Random beer_ en la barra de navegación o en el botón _Check a random beer_ en la página de inicio, debería ver esta página con una nueva cerveza aleatoria.

:::info
En cada paso, debe generar un `partial` pasando la información con respecto a la cerveza correspondiente.
:::

### Paso 5 - Beer `partial`

**Los `partial` representan componentes que pueden ser reutilizados.**

Veamos qué propiedades de la cerveza mostramos en la página `/beers` _(beers page)_ y compárelas con las propiedades que mostramos en la página` /random-beer` _(random beer)_:

| propiedades/ página  |      `/beers`      |   `/random-beer`   |
| :--------------:     | :----------------: | :----------------: |
|      imágen          | :white_check_mark: | :white_check_mark: |
|       nombre         | :white_check_mark: | :white_check_mark: |
|   descripción        | :white_check_mark: | :white_check_mark: |
|     tagline          | :white_check_mark: | :white_check_mark: |
|   maridaje de comida |        :x:         | :white_check_mark: |
|   consejos           |        :x:         | :white_check_mark: |

Como podemos ver, tenemos 4 en propiedades comunes, lo que significa que nuestro código podría ser un poco más **DRY** si lo refactorizamos usando _partials_.

Debes crear un `partial` para mostrar cada cerveza.

- Primero, necesitamos registrarnos donde se ubicarán nuestros `partials`. Por lo tanto, debe agregar el siguiente código al archivo `app.js`:

```jsx
hbs.registerPartials(path.join(__dirname, 'views/partials'));
```

- A continuación, debe crear una carpeta `partials` dentro de` views`, y un archivo `beerpartial.hbs` dentro de la carpeta` partials` (**Nota**: No incluimos guiones en los nombres parciales de `hbs` , dado que los parciales del manillar deben seguir las mismas convenciones de nomenclatura que las variables de JavaScript).
- Nuestro `beerpartial.hbs` mostrará las propiedades que comparten ambas vistas: **imagen**, **nombre**, **descripción** y **tagline** de la cerveza.
- Ahora, puede continuar y conectar este parcial en la vista `beers.hbs` dentro del bucle` each`.

Después de crear el `partial` y recorrer el `array` de cervezas, en nuestra ruta `/beers`, deberíamos tener lo siguiente:

![image](https://user-images.githubusercontent.com/23629340/36724392-61fa7336-1bb3-11e8-8468-189908167e10.png)

- También podemos utilizar en la página `random-beer.hbs`.

Nuestro código se redujo mucho solo porque logramos crear un fragmento de código reutilizable (el parcial), que ahora podemos colocar donde necesitemos usar este conjunto de propiedades.

### Paso 6 - Detalle de cada cerveza

Tenemos que hacer que se pueda hacer clic en todas las cervezas de la página de cervezas. Si los usuarios hacen clic en una cerveza específica, deberían poder ver una página con la información detallada de esa cerveza en particular. **Puede reutilizar el mismo `partial` que utilizó para el paso 5**. De hecho, debería hacerlo. Para eso son los `partials`. El truco consiste en envolver en una etiqueta `<a href></a>` el nombre de cada cerveza.

La etiqueta debe tener el `id` de la cerveza en la propiedad`href`. Algo como:

```html
<a href="/beers/beer-i3f4d34s34b"><!-- Nombre de la cerveza --></a>
```

Para comprender cómo puede obtener el `id` de la URL, lea esta sección del [la documentación de Express](http://expressjs.com/en/4x/api.html#req.params) o revise la lección de `GET Params`.

Para averiguar cómo puede obtener una cerveza individual del punkAPI usando el _beerId_, consulte el [método `.getBeer(id)` en la documentación de punkAPI](https://www.npmjs.com/package/punkapi-javascript-wrapper#getbeerid).

### Paso 7 - Agregar estilos

El diseño general debería verse así:

![image](https://user-images.githubusercontent.com/23629340/36723450-8bbcb164-1bb0-11e8-81c3-4fe939730bb9.png)

Encontrará los `colores` y las`fuentes` en el archivo `css`. Recuerda vincular el archivo `css` a tu **layout**.

¡Deja que tu lado artístico brille! :sparkles:

Happy Coding! 💙
