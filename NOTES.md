## [0.0.1] 28-ENE-2019: 16:02

### Crear un mock de heroes
Eventualmente, los datos se obtienen desde un servidor remoto. Por ahora, crearemos un mock de heroes, y pretenderemos que vienen de un servidor.

Crear un archivo `mock-heroes.ts` en `src/app/`.

En dicho archivo se crea una constante HEROES que contiene un array con los heroes que usaremos. Para usarlos debemos exportarlos.

### Desplegar los heroes
#### Modificar el componente heroes
En el archivo `src/app/heroes/heroes.component.ts` se importa HEROES.

Igualmente, en dicho archivo se modifica la clase HeroesComponent 
para que ahora use nuestro mock de heroes.

#### Modificar la plantilla del componente heroes
Se modifica el archivo `heroes.component.html` para presentar una lista de heroes de nuestro mock.

Para ello se hace uso de la directiva `ngFor` la cual es un repetidor. Es decir, repite el elemento huesped por cada elemento en una lista.

En este caso:
* `<li>` es el elemento huesped
* `heroes` es la lista
* `hero` es el actual objeto por cada iteración a través de la lista.

En este punto, es un buen momento para apreciar nuestro trabajo:

`> ng server --open`

#### Dando estilo a los heroes
Se puede adicionar más estilos a `style.css` haciendo crecer todo lo que desees este archivo a medida que creas más componentes. 

Pero es mejor definir estilos privados para un componente y mantener todo lo que el componente necesita (el código, HTML y CSS) junto en un solo lugar.

Este enfoque hace que sea más fácil reutilizar el componente en otro lugar y entregar el aspecto deseado del componente incluso si los estilos globales son diferentes.

Cuando se CLI generó el `HeroesComponent`, creó un `heroes.component.css` para dicho componente y apuntó `styleUrls` a dicho archivo.

Entonces, sólo necesitamos entrar al archivo `heroes.component.css` y pegar allí los estilos que usaremos para este componente.

`> ng server --open`