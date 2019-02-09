## [0.0.5]

----

### Servicios
La aplicación actualmente despliega datos falsos.

En este commit el `HeroesComponent` se simplifica buscan que se enfoque sólo en entregar información a la vista. Para ello crearemos un servicio simulado. Esto también facilitará las pruenas unitarias.

#### ¿Por qué servicios?
Los componentes no deben obtener o guardar datos directamente y, ciertamente, no deben presentar datos falsos a sabiendas. Deben centrarse en presentar datos y delegar el acceso de datos a un servicio.

Este commit, crea un `HeroService` que todas las clases de la aplicación podrán usar para obtener héroes.

En lugar de crear instancias de ese servicio con la palabra reservada `new`, usa la inyección de dependencia de Angular para inyectarlo en el constructor `HeroesComponent`.

Los servicios son una excelente manera de compartir información entre clases que no se conocen entre sí.

----

#### Crear el servicio
El servicio se genera así:

`> ng generate service hero`

Esto generará la clase `HeroService` en `src/app/hero.service.ts`.

El nuevo servicio importa el símbolo `Injectable` y anota la clase con el decorador `@Injectable`. Esto marca a la clase como una clase que participa en el *sistema de de inyección de dependencia*. `HeroService`va a proveer un servicio inyectable y puede también tener sus propias dependencias inyectadas.

----

#### Obtener los datos de héroes
`HeroService` podría obtener datos de héroes desde cualquier lugar: un servicio web, almacenamiento local o una fuente de datos simulada.

Eliminar de los componentes el acceso a los datos significa que podemos cambiar de opinión de la implementación en cualquier momento, sin tocar ningún componente. Ellos no saben cómo funciona el servicio.

La implementación en este tutorial continuará entregando héroes simulados.

Así que importamos la clase `Hero` y el mock de héroes en `HeroService`.

----

#### Proveer el servicio HeroService
Debemos lograr que nuestro servicio esté para que Angular pueda inyectarlo en `HeroesComponent`. Para ello registramos un proveedor. Un proveedor es algo que puede crear o entregar un servicio; en este caso, crea una instancia de la clase `HeroService` para proporcionar el servicio.

De manera predeterminada, Angular registra un proveedor con el *inyector root* para su servicio al incluir metadatos del proveedor en el decorador `@Injectable`.

Si observa la instrucción `@Injectable()` justo antes de la definición de la clase `HeroService`, puede ver que el valor de metadatos provisto es `"root"`.

Cuando proporciona el servicio en el nivel `root`, Angular crea una única instancia compartida de `HeroService` y la inyecta en cualquier clase que lo solicite. El registro del proveedor en los metadatos de @`Injectable` también permite que Angular optimice una aplicación eliminando el servicio si resulta que no se utiliza después de todo.

----

#### Actualizar HeroesComponent
Eliminamos el `import` de `HEROES`, porque ya no es necesario. Lo cambiamos por un `import` de `HeroService`.

Cambiamos la definición de heroes:

`heroes: Hero[]`

##### Inyectar el servicio HeroService

En el constructor adicionamos un parámetro de tipo `HeroService`.

Este parámetro define simultáneamente una propiedad privada `heroService` y la establece como una inyección de `HeroService`.

Cuando Angula crea una instancia de `HeroesComponent` el sistema de inyección de dependencias crea una instancia singleton de `HeroService`.

##### Adicionar getHeroes()
Creamos la función que retorna la lista de héroes.

##### Llamamos getHeroes desde ngOnInit()
Podríamos llamar a `getHeroes()` desde el constructor pero no es una buena práctica.

Reserve el constructor para una inicialización simple, como asignar  parámetros del constructor a las propiedades. El constructor no debe hacer nada; menos aún, llamar a una función que realiza solicitudes HTTP a un servidor remoto como lo haría un servicio de datos real.

----
`> ng serve --open`