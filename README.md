![](https://runelite.net/img/logo.png)
# plugin-hub [![Discord](https://img.shields.io/discord/301497432909414422.svg)](https://discord.gg/mePCs8U)

Este repositorio contiene marcadores para [RuneLite](https://github.com/runelite/runelite)
complementos que no son compatibles con los desarrolladores de RuneLite. Los complementos son
Se proporciona "tal cual"; no ofrecemos garantías sobre ningún complemento en este repositorio.

## Setting up the development environment

Nosotros recomendamos [IntelliJ Idea Community Edition](https://www.jetbrains.com/idea/download/) Puedes tener así como Java 11.
IntelliJ install Java (selecciona `Eclipse Temurin`) o descárgalo desde https://adoptium.net/temurin/releases/. También debes tener una cuenta de GitHub.

## Contribute to existing plugins

Recomendamos contribuir a los complementos existentes si los autores aceptan contribuciones y la función que desea agregar se adapta bien al complemento, para evitar la fragmentación del ecosistema de complementos. Reducir la fragmentación de los complementos ayuda a los usuarios a descubrir funciones más fácilmente y nos ayuda a revisar los cambios de manera más oportuna.

Puede contribuir a los complementos existentes seleccionando el complemento desde https://runelite.net/plugin-hub, navegando al repositorio de GitHub del complemento siguiendo el enlace "Informar un problema" y luego siguiendo la sección "Crear nuevos complementos" a continuación desde el paso 3.

## Creating new plugins
 1. Genera tu propio repositorio desde el [plugin template](https://github.com/runelite/example-plugin/generate) enlace (primero debes iniciar sesión en GitHub).
    Alternativamente, puede utilizar el script `create_new_plugin.py` provisto en este repositorio para generar un nuevo proyecto de complemento.

2. Ponle un nombre apropiado a tu repositorio. En mi caso, lo llamaré `helmet-check` con la descripción `Siempre debes usar un casco`. **Asegúrate de que tu repositorio esté configurado como público**.

3. En la parte superior derecha, verás un botón *Clonar o descargar*. Haz clic en él y copia el enlace.

4. Abre IntelliJ y elige *Obtener del control de versiones*. Pega el enlace que acabas de copiar en el campo URL y donde quieras guardarlo en el segundo campo.

5. Para asegurarte de que todo funciona correctamente, intenta iniciar el cliente con tu complemento externo habilitado ejecutando la prueba proporcionada. Si aún no tienes una configuración de ejecución para la prueba, intenta ejecutarla haciendo clic en `Run test`. Esto creará una configuración de ejecución y no se ejecutará debido a que las afirmaciones están deshabilitadas. Agregue `-ea`
   a las opciones de su VM en la configuración de ejecución para habilitar las aserciones, que se pueden encontrar en `Run/Debug Configurations` en `Modify options`, `Add VM options` y luego agregue `-ea` en el campo de entrada que aparece.

 The client should now launch with your plugin enabled. If you have a Jagex account, you will be unable to login without first following [this guide](https://github.com/runelite/runelite/wiki/Using-Jagex-Accounts).

 ![run-test](https://i.imgur.com/tKSQH5e.png)

6. Utilice la herramienta de refactorización para cambiar el nombre del paquete por el que desea que sea el complemento. Haga clic derecho en el paquete en la barra lateral y elija *Refactor > Rename*. Elegí cambiarle el nombre a `com.helmetcheck`.

7. Utilice la misma herramienta, *Refactor > Rename*, para cambiar el nombre de `ExamplePlugin`, `ExampleConfig` y `ExamplePluginTest` por `HelmetCheckPlugin`, etc.

8. Vaya al archivo del complemento y establezca su nombre en `PluginDescriptor`, que puede tener espacios.

9. Abra el archivo `runelite-plugin.properties` y agregue información a cada fila.
 ```
 displayName=Comprobación del casco
 author=pared de la cubierta
 description=Te avisa cuando no tienes nada equipado en la ranura de tu cabeza.
 tags=hint,gear,head
 plugins=com.helmetcheck.HelmetCheckPlugin
 ```
`tags` hará que sea más fácil encontrar su complemento cuando busque palabras relacionadas. Si desea agregar varios archivos de complemento, el campo `plugins` permite valores separados por comas, pero esto no suele ser necesario.

10. Opcionalmente, puede agregar un ícono para que se muestre junto con su complemento. Coloque un archivo con el nombre `icon.png` que no sea más grande que 48x72 px en la raíz del repositorio.

11. Escriba un README agradable para que sus usuarios puedan ver las características de su complemento.

12. Cuando tenga su complemento funcionando, confirme los cambios y envíelos a su repositorio.

### Licensing your repository
1. Vaya a su repositorio en GitHub y seleccione *Agregar archivo* (junto al botón verde *Código*) y elija *Crear nuevo archivo* en el menú desplegable.
2. En el campo de nombre de archivo, escriba *LICENCIA* y haga clic en el botón *Elegir una plantilla de licencia* que aparecerá.
3. Seleccione `Licencia BSD de 2 cláusulas "simplificada"` en la lista de la izquierda. Complete sus datos y presione *Revisar y enviar*.
4. Confirme sus cambios haciendo clic en *Confirmar cambios* en la parte inferior de la página. Asegúrese de marcar el botón para confirmar directamente en la rama maestra.

## Submitting a plugin
 1. Bifurcar el [plugin-hub repository](https://github.com/runelite/plugin-hub).
 2. Crea una nueva rama para tu complemento.
 3. Crea un nuevo archivo en el directorio `plugin-hub/plugins` con los campos:
 ```
repository=
commit=
 ```
4. Para obtener la URL del repositorio, haz clic en el botón *Clonar o descargar* y elige *Usar HTTPS*. Pega la URL en el campo `repository=`.

5. Para obtener el hash de confirmación, ve al repositorio de tu complemento en GitHub y haz clic en confirmaciones. Elige la más reciente y copia el hash completo de 40 caracteres. Se puede ver en la parte superior derecha después de seleccionar una confirmación. Pégalo en el campo `commit=` del archivo.
   Tu archivo ahora debería verse así:
 ```
repository=https://github.com/dekvall/helmet-check.git
commit=9db374fc205c5aae1f99bd5fd127266076f40ec8
 ```
6. Este es el único cambio que necesitas hacer, así que confirma tus cambios y envíalos a tu bifurcación. Luego regresa al [plugin-hub](https://github.com/runelite/plugin-hub) y haz clic en *Nueva solicitud de incorporación de cambios* en la esquina superior izquierda. Elige *Comparar entre bifurcaciones* y selecciona tu bifurcación y rama como encabezado y compara.

7. Escribe una breve descripción de lo que hace tu complemento y luego crea tu solicitud de incorporación de cambios.

8. Comprueba el resultado del flujo de trabajo de integración continua de tu solicitud de incorporación de cambios. Junto a `.github/workflows/build.yml / build (pull_request)` habrá un ✔️ o un ❌. Con un ✔️ todo está bien, sin embargo, si tiene un ❌, haz clic en `Detalles` para comprobar el registro de compilación y obtener detalles de la falla. Junto con el flujo de trabajo de compilación, también puede haber un ❌ junto a `RuneLite Plugin Hub Checks`, solo deberá preocuparse por esto si dice `View details for request changes.`, en ese caso, también debe leer los cambios solicitados. Una vez que haya leído el error de compilación y los cambios solicitados, realice los cambios necesarios y envíe otra confirmación para actualizar la solicitud de incorporación de cambios con el nuevo hash `commit=`.
   No se preocupe por la cantidad de veces que le toma resolver los errores de compilación; preferimos que todos los cambios se mantengan en una sola solicitud de incorporación de cambios para evitar enviar notificaciones con más solicitudes de incorporación de cambios recién abiertas.

9. Sea paciente y espere a que se revise y fusione su complemento.

## Actualización de un complemento
Para actualizar un complemento, simplemente actualice el manifiesto con el hash de confirmación más reciente.

## Reviewing
We will review your plugin to ensure it isn't malicious, doesn't [break Jagex's rules](https://secure.runescape.com/m=news/third-party-client-guidelines?oldschool=1), 
or isn't one of our previously [Rejected/Rolledback features](https://github.com/runelite/runelite/wiki/Rejected-or-Rolled-Back-Features).  
__If it is difficult for us to ensure the plugin isn't against the rules we will not merge it__. 

## Plugin resources
Resources may be included with plugins, which are non-code and are bundled and distributed with the plugin, such as images and sounds. You may do this by placing them in `src/main/resources`. Plugins on the pluginhub are distributed in .jar form and the jars placed into the classpath. The plugin is not unpacked on disk, and you can not assume that it is. This means that using https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getResource-java.lang.String- will return a jar-URL when the plugin is deployed to the pluginhub, but in your IDE will be a file-URL. This almost certainly makes it behave differently from how you expect it to, and isn't what you want.
Instead, prefer using https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getResourceAsStream-java.lang.String-. 

## Third party dependencies
We require any dependencies that are not a transitive dependency of runelite-client to
be have their cryptographic hash verified during the build to prevent [supply chain attacks](https://en.wikipedia.org/wiki/Supply_chain_attack) and ensure build reproducability.
To do this we rely on [Gradle's dependency verification](https://docs.gradle.org/nightly/userguide/dependency_verification.html).
To add a new dependency, add it to the `thirdParty` configuration in [`package/verification-template/build.gradle`](https://github.com/runelite/plugin-hub/blob/master/package/verification-template/build.gradle),
then run `../gradlew --write-verification-metadata sha256` to update the metadata file. A maintainer must then verify
the dependencies manually before your pull request will be merged.

## My client version is outdated
If your client version is outdated or your plugin suddenly stopped working after RuneLite has been updated, make sure that your `runeLiteVersion` is set to `'latest.release'` in `build.gradle`. If this is set correctly, refresh the Gradle dependencies by doing the following:
1. Open the Gradle tool window.
2. Right-click on the project's name. This will contain the Gradle icon (elephant).
3. Choose `Refresh Gradle Dependencies`.
If your issue is not resolved, try reloading all Gradle projects. This option is located in the toolbar in the Gradle tool window. Additionally, try invalidating caches.
