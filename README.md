# AngularComponentsUI

Este proyecto fue generado con: [Angular CLI](https://github.com/angular/angular-cli) version 6.0.8.

La intención es concentrar una biblioteca de componentes reutilizables Angular.

## Development server

Ejecutar `ng serve` para desplegar un servidor de desarrollo en `http://localhost:4200/`. La aplicación se recargará automaticamente con cada cambio al codigo fuente.

## Ejecutar pruebas unitarias

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Generar un nuevo componente

* Para agregar una nueva librería, dentro de `/AngularComponentsUI` ejecutar el comando `ng generate library [NombreLibreria] --prefix axy`

* Dentro de la ruta `/AngularComponentsUI/projects/` se generará una nueva carpeta con el nombre de la librería generada

* En el archivo `/AngularComponentsUI/projects/[NombreLibreria]/src/public_api.ts` agregar todos los archivos (servicios, componentes, etc) que el componente necesita para trabajar:
  ```javascript
    export * from './lib/[NombreLibreria].component';
    export * from './lib/[NombreLibreria].module';
  ```
* En el directorio `/AngularComponentsUI/projects/[NombreLibreria]/src/lib` se encuentran todos los archivos donde construiremos nuestro componente

* Para generar subcomponentes que sean parte de nuestra librería ejecutar el siguiente comando: `ng generate component [NuevoComponente] --project=[NombreLibreria]`

* Para probar el componente en un proyecto angular real, agregarlo al proyecto ubicado en `/AngularComponentsUI/src/`, no es necesario instalarlo con `npm install`, ya que automáticamente se registro la librería en el archivo: `/AngularComponentsUI/tsconfig.json` de la siguiente forma:
```javascript
"paths": {
      "[nombre-libreria]": [
        "dist/[nombre-libreria]"
      ],
      "[nombre-libreria]/*": [
        "dist/[nombre-libreria]/*"
      ]
    }
```
por lo que solo basta con registrarlo en el archivo: `/AngularComponentsUI/src/app/app.module.ts`

```typescript
import { [NombreLibreria] } from '[nombre-libreria]';
@NgModule({
  imports: [
    ...,
    [NombreLibreria]
  ],
})
export class AppModule { }
```

> [NombreLibreria] - Sustituir por el nombre de la librería a construir omitiendo los `[]`, tratar de omitir espacios y mejor utilizar PascalCase  
> Para mas información este [tutorial](https://medium.com/@tomsu/how-to-build-a-library-for-angular-apps-4f9b38b0ed11) puede ser de utilidad: 

## Consideraciónes a seguir para generar un componente reutilizable

* Evitar incluir referencias a bibliotecas externas, solo en caso de ser necesario agregarlas dentro del paquete anexando la versión con la que la librería fue creada
* En caso de generar librerias con componentes UI, manejarlos responsivos y tratar de evitar colocar medidas fijas, así como manejar el estado de disabled mediante un input boolean
* Si se generan componentes que necesiten el uso de ngModel, revisar el proyecto: `/AngularComponentsUI/projects/three-steps-selector/src/lib/three-steps-selector.component.ts` con la mejor manera de implementarlo, para mas información seguir este [tutorial](http://anasfirdousi.com/how-to-make-custom-angular-components-form-enabled-ngModel-enabled.html)

## Construir un componente

Ejecutar `ng build [NombreLibreria]` y para construir la versión final ejecutar `ng build [NombreLibreria] --prod`, esto generará la version de la librería dentro de la ruta: `/AngularComponentsUI/dist/[NombreLibreria]/`

> [NombreLibreria] - Sustituir por el nombre de la librería a construir omitiendo los `[]`, tratar de omitir espacios y mejor utilizar PascalCase

## Instalar componente en repositorio Nexus (Axity)

* Para dar de alta el repositorio Nexus de Axity ejecutar: `npm adduser --registry http://devtools.axity.com/nexus3/repository/npm-hosted/` (Ingresar credenciales Active Directory)

* Colocarse en la ruta: `/AngularComponentsUI/dist/[NombreLibreria]/`

* Para publicar la librería ejecutar: `npm publish --registry http://devtools.axity.com/nexus3/repository/npm-hosted/` el nombre lo tomara del archivo package.json de la librería

> Para no tener que colocar el registry en cada momento, basta con agregar la siguiente linea:
> ```javascript
> "publishConfig": {
>    "registry": "http://devtools.axity.com/nexus3/repository/npm-hosted/"
>  }
> ```
> En el archivo package.json de nuestra librería

## Contribuciones

Mediante pull-request se evaluan los cambios a componentes, mas información:
francisco.rodriguez@axity.com 

## Componentes registrados
* [Selector de tres pasos](/bitbucket/projects/AXITY/repos/angularcomponentsui/browse/projects/three-steps-selector/) 

## Axity
![Axity logo](./assets/axity.png "Axity")
# Angular-base
