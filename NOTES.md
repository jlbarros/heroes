## [0.0.4] 29-ENE-2019: 18:26

----

### Crear Componente Maestro/Detalle
Nuestro componente `HeroesComponent` viola una regla básica de la OOP: 

*Una clase debe hacer una y sólo una cosa*.

O, dicho de mejor manera:

*Una clase debe tener una única razón para cambiar*

Nuestro componente presenta la lista de héroes, pero también presenta el detalle de cada héroe. Debemos separar esta funcionalidad para evitar que al crecer la aplicación su mantenibilidad se haga más difícil.

El componente `HeroesComponent`sólo presentará la lista de héroes.

Crearemos otro componente llamado `HeroDetailComponent` para presentar el detalle de un héroe.

En la terminal, tecleamos la siguiente orden para generar el nuevo componente:

`ng generate component hero-detail`

----
#### Modificar la vista del componente
Cortamos el código de la vista del componente `HeroesComponent` que corresponde a la presentación del detalle de un héroe y lo pegamos en la vista del componente `HeroDetailComponent`.

#### Adicionamos una propiedad @Input() hero al componente
En el código del componente es necesario que importemos nuestro objeto `Hero` para poder utilizarlo creando la propiedad `hero`.

Pero además, como deseamos que el usuario pueda modificar la propiedad modificamos el `import` por defecto para incluir la opción `Input` y poder asignarle esta capacidad a `hero`.

Igualmente, modificamos la vista del componente `HeroesComponent` para que ahora llame a el componente `HeroesDetailComponent`.

### ¿Qué cambió?
Al refactorizar el código en dos componentes se obtienen beneficios:

* Se redujo la complejidad de `HeroesComponent` reduciendo sus responsabilidades.
* El componente `HeroDetailComponent` puede evolucionar a un rico editor sin tocar el código de `HeroesComponent`.
* Igualmente, se puede tocar el código de `HeroesComponent` sin tocar el componente de detalles.
* Los componentes se pueden reutilizar en algún otro contexto.

### Resumen
* Se creó un componente reutilizable `HeroeDetailComponent`.
* Usamos una propiedad enlazada que le da al padre `HeroesComponent` control sobre su hijo `HeroDetailComponent`.
* Usamos un decorador `@Input` para permitir que la propiedad `hero` quede disponible para el componente externo `HeroesComponent`.

