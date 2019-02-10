## [0.0.6]

----

### Datos Observables
El método `HeroService.getHeroes()` tiene una firma síncrona, lo que implica que `HeroService` puede obtener héroes de forma síncrona. `HeroesComponent` consume el resultado de `getHeroes()` como si los héroes se pudieran buscar de forma sincrónica.

Esto no funcionará en una aplicación real. Te estás saliendo con la tuya ahora porque el servicio actualmente devuelve héroes simulados. Pero pronto la aplicación buscará héroes desde un servidor remoto, que es una operación inherentemente asíncrona.

`HeroService` debe esperar a que el servidor responda, `getHeroes()` no puede regresar inmediatamente con datos de héroes, y el navegador se bloqueará mientras el servicio espera.

`HeroService.getHeroes()` debe tener una *firma asíncrona* de algún tipo.

De esta manera puede tomar una devolución de llamada (Callback). O podría devolver una *Promesa*. O tambien, podría devolver un *Observable*.

En este tutorial, `HeroService.getHeroes()` devolverá un `Observable` en parte porque eventualmente usará el método Angular `HttpClient.get` para buscar a los héroes y `HttpClient.get()` devuelve un `Observable`.

#### Haciendo HeroService Observable
`Observable` es una de las clases clave en la librería `RxJS`.

En un tutorial posterior sobre HTTP, aprenderás que los métodos `HttpClient` de Angular devuelven RxJS Observables. En este tutorial, simularemos obtener datos del servidor con la función RxJS `of()`.

Abre el archivo `HeroService` y has un `import` de los símbolos `Observable` y `of` RxJS.

El método `getHeroes()` se modifica para que retorne un `of(HEROES)`, Así, devuelve un `Observable<Hero[]>` que emite un único valor, la matriz de héroes simulados.

#### Modificar HeroesComponent para utilizar un servicio Observable
El método `HeroService.getHeroes()` utilizado para devolver un `hero[]` ahora devuelve un `Observable<Hero[]>`.

Tenemos que modificar `HeroesComponent` para ajustarnos a esta diferencia.

`Observable.subscribe()` es la diferencia crítica.

La versión anterior asigna un array de héroes a la propiedad `heroes` del componente. La asignación se realiza de forma sincrónica, como si el servidor pudiera devolver héroes al instante o el navegador pudiera congelar la interfaz de usuario mientras espera la respuesta del servidor.

Eso no funcionará cuando `HeroService` en realidad esté haciendo solicitudes a un servidor remoto.

La nueva versión espera a que el `Observable` emita un array de héroes, lo que podría suceder ahora o dentro de unos minutos. Luego, la suscripción pasa el array emitido a la devolución de llamada, que establece la propiedad `heroes` del componente.

Este enfoque asíncrono funcionará cuando `HeroService` solicite héroes del servidor.

----

### Mostrar mensajes
En esta sección aprenderemos a:

* Adicionar un `MessageComponent` que despliega mensajes de la aplicación en la parte inferior de la pantalla.

* Crea un `MessageService` inyectable y para enviar los mensajes que serán desplegados.

* Inyectar `MessageService` en `HeroService`.

* Mostrar un mensaje cuando `HeroService` obtiene héroes con éxito.

#### Crear MessageComponent

`ng generate component messages`

Luego de generado el componente es necesario modificar la vista de `AppComponent` para que presente los mensajes.

#### Crear MessageService

`ng generate service message`

Se debe modificar `MessageService` creandole dos métodos: uno para adicionar mensajes y otro para borrar todos los mensajes.

El servicio expone su caché de mensajes y dos métodos: uno para agregar un mensaje al caché y otro para borrar el caché.

#### Inyectar MessageService en HeroService
En `HeroService` se debe importar `MessageService`.

Igualmente, se debe modificar el constructor creándole un parámetro que declare una propiedad privada de `messageService`. Angular inyectará el servicio de mensajes singleton en esa propiedad cuando cree `HeroService`.

Este es un escenario típico de "servicio en servicio": se inyecta `MessageService` en `HeroService` el cual, a su vez, se inyecta en `HeroesComponent`.

#### Enviar un mensaje desde HeroService
Modifica el método `HeroService.getHeroes()` para enviar un mensaje cuando se obtengan los héroes.

#### Modificar MessageComponent para poder mostrar mensajes
`MessagesComponent` debe mostrar todos los mensajes, incluido el mensaje enviado por `HeroService` cuando busca héroes.

Abra `MessagesComponent` e importe el `MessageService`.

Modifique el constructor con un parámetro que declare una propiedad `public messageService`. Angular inyectará el servicio de mensajes singleton en esa propiedad cuando cree el `MessagesComponent`.

La propiedad messageService debe ser pública porque está a punto de enlazarla en la plantilla. Angular sólo enlaza a propiedades públicas de los componentes.

#### Modificar la vista de MessageService para poder mostrar mensajes
Esta plantilla se enlaza directamente al servicio de mensajes del componente.

* `*ngIf` solo muestra el área de mensajes si hay mensajes para mostrar.

* `*ngFor` presenta la lista de mensajes en elementos <div> repetidos.

* Un enlace de evento Angular vincula el evento clic del botón a `MessageService.clear()`.

Los mensajes se verán mejor cuando agregue los estilos de CSS privados a `messages.component.css` como se indica en una de las pestañas de "revisión final del código" a continuación.

El navegador se actualiza y la página muestra la lista de héroes. Desplácese hasta la parte inferior para ver el mensaje del `HeroService` en el área de mensajes. Haga clic en el botón "clear" y el área de mensaje desaparecerá.

----

### Resumen

* Se refactorizó el acceso de datos a la clase `HeroService`.
* Se registró `HeroService` como proveedor de servicio a nivel `root` para que pueda ser inyectado en cualquier parte de la aplicación.
* Se usó la inyección de dependencia de angular para inyectar el servicio en un componente.
* Se le asignó al método que obtiene los datos en `HeroService` una firma asíncrona.
* Conocimos las librerías `Observable` y `RxJS Observable`.
* Usamos RxJS `of()` para devolver un observable de héroes simulados (`Observable<Hero[]>`).
* Aprendimos que es mejor hacer llamadas desde `ngOnInit()` de un componente que desde el constructor.
* Creamos un `MessageService` para la comunicación entre clases de manera debilmente acoplada.
* El `HeroService` inyectado en un componente se crea con otro servicio inyectado, `MessageService`.
