## [0.0.3] 29-ENE-2019: 14:24

### Maestro/Detalle
Cuando el usuario hace clic en la lista maestra, el componente debe desplegar el detalle del héroe seleccionado en la parte de abajo de la página.

#### Adicionar un link de evento click
En la vista `heroes.component.html` se agrega al elemento `<li>` el link al evento click:

`<li *ngFor="let hero of heroes" (click)="onSelect(hero)">`

El paréntesis alrededor de `click` le dice a Angular que escuche el evento `click` en los elemetos `<li>`. Cuando el usuario hace click en un elemento `<li>`, Angular ejecuta la expresión `onSelect(hero)`.

`onSelect(hero)` es un método de `HeroesComponent` que tienes que escribir. Angular llama a este método con el objeto `hero`, el mismo `hero` definido previamente en la expresión del `*ngFor`.

#### Adicionar un manejador del evento click

Debemos crear una propiedad que mantenga en el componente el héroe seleccionado y además un método para seleccionar un héroe.

#### Actualizar la vista para presentar los detalles
Debajo de la lista de héroes ya presentada se deben presentar los detalles del héroe seleccionado.

Para ello, agregamos a la plantilla, el código HTML necesario.

Sin embargo, una vez actualizada la plantilla, si refrescamos el explorador, vemos que la lista no se ve adecuadamente. Si buscamos en la consola descubriremos que se genera un error; `Cannot read property 'name' of undefined`.

Si hacemos click en la lista, la aplicación vuelve a funcionar correctamente.

Lo que ocurre es `selectedHero` no está aún establecido cuando inicia la aplicación.

La aplicación sólo debería presentar los detalles de un héroe cuando dicho héroe haya sido seleccionado.

Debemos encerrar el código HTML dentro de un `<div>` condicionado. Para ello utilizaremos la directiva `*ngIf` que nos permite ocultar lo que está dentro del `<div>` de acuerdo a una condición.

Con este ajuste, la aplicación ya queda funcionando correctamente.

#### Dando un estilo al héroe seleccionado
No queda claro en la lista de héroes, cuál es el héroe seleccionado. El héroe seleccionado debería tener un color o algo distintivo.

El estilo que necesitamos ya lo tenemos en la hoja de estilo del componente. Sólo debemos usarlo en nuestra vista. Para ello, usaremos la capacidad que tiene Angular de alternar el uso de una clase CSS de acuerdo a una condición dada, en este caso, que el elemento `<li>` sea el del héroe seleccionado.

----

### Resumen
* La aplicación ahora despliega una lista de héroes y un maestro/detalle del héroe seleccionado.
* El usuario puede seleccionar un héroe y ver sus detalles.
* Usamos `*ngFor` para desplegar una lista.
* Usamos `*ngIf`para incluir o excluir un bloque HTML según una condición dada.
* Podemos alternar la aplicación de una clase de estilo CSS de acuerdo con una condición dada.

----
