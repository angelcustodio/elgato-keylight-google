# Elgato Key Light con Google Assistant
Esto es una guía para poder vincular tu Elgato Key Light con Google Home y así poder controlarlo desde la app o mediante rutinas de Google Assistant. Esta guía no es más que una adaptación de la original de [sirdarckcat](https://github.com/sirdarckcat/sirdarckcat.github.io/tree/master/fakeauth) en inglés.

**Nota**: Para poder realizar todos los pasos con éxito, primero debes de ingresar en el [Programa de Avance de Google](https://support.google.com/chromecast/answer/6343937#zippy=%2Chow-do-i-join-the-preview-program)

## Paso 1
- Acceder a las [Actions on Google](https://console.actions.google.com/) y crear un nuevo proyecto
- Acepta los Términos y Condiciones
- Elige el país dónde resides ahora mismo
- Las 2 últimas opciones de sí/no puedes dejarlas en **no**, son para recibir updates en tu mail
- Aceptar y continuar

## Paso 2
- Elige un nombre para tu proyecto (improtante; esto determinará el ID del mismo)
  - Puede contener espacios, mayús/minús... Recomendable algo tipo: `Elgato Key Light`
- Elige el idioma con el que sueles utilizar Google Assistant
- Elige, de nuevo, el país donde resides ahora mismo
- Acepta

## Paso 3
- Haz click en la opción **`Smart Home`** para marcarla
- Haz click en el botón azul de arriba a la derecha de **`Start Building`**
  - Ten paciencia, a veces parece que no hace nada pero va cargando poco a poco

## Paso 4
- Una vez la página haya cargado, estarás en el **`Overview`** (lo verás en las pestañas superiores)
- Ve a la sección **`Develop`**
- En el menú lateral, elige **`Invocation`**
  - Escribe el nombre de lo que verás como dispositivo en Google Home, tipo `Elgato Key Light`
- Ahora ve, en el menú lateral, a **`Actions`**
  - En **Fulfillment URL** escribe `https://europe-west6-worldpeace-186e0.cloudfunctions.net/function-2` ([source code](https://github.com/angelcustodio/elgato-keylight-google/blob/main/files/cloudfunction.js)]
  - En **Log Level** lo puedes dejar en `Error`
  - En **Enter your testing URL for Chrome** escribe `https://raw.githubusercontent.com/angelcustodio/elgato-keylight-google/main/files/index.html` ([source code](https://github.com/angelcustodio/elgato-keylight-google/blob/main/files/index.html)]
  - En **Enter your testing URL for Node** escribe `https://raw.githubusercontent.com/angelcustodio/elgato-keylight-google/main/files/bundle.js` ([source code](https://github.com/angelcustodio/elgato-keylight-google/blob/main/files/bundle.js)]
  - En **Upload Javascript files** no tienes que tocar nada
  - En **Add capabilities** tienes que marcar la opción ☑️ **Support local query**

## Paso 5
- En **Add device scan configuration** viene la parte importante:
  - Haz click 3 veces en el botón **`+ New scan config`**
  - Verás que han salido 3 selectores con el nombre **`Select a discovery protocol`**
  - En los 3 selectores, elige la misma opción: `MDNS`
  - En cada bloque, verás que también hay un enlace de **`Add field`**
    - En los 3 bloques, haz click en ese enlace, te saldrá un selector donde elegir el tipo `Name`
  - Ahora deberías de tener 3 bloques iguales:
    - **MDNS** con 2 campos, **MDNS service name** y **Name**
  - Por orden, los bloques deben ser:
    - Bloque 1:
      - MDNS service name: `_elg._tcp.local`
      - Name: `elgato.*`
    - Bloque 2:
      - MDNS service name: `_elg._tcp`
      - Name: `elgato.*`
    - Bloque 3:
      - MDNS service name: `_elg._tcp.local.`
      - Name: `elgato.*`
- Al tenerlo todo en orde, guarda los cambios mediante el botón de arriba a la derecha

## Paso 6
- En el menú lateral, elige **`Account linking`**
- En el campo **`Client ID issued by your Actions to Google`** escribe `placeholder`
- En el campo **`Client secret`** escribe `placeholder`
- En el campo **`Authorization URL`** escribe esta URL:
  - `https://oauth-redirect.googleusercontent.com/r/CODIGO_DE_PROYECTO?code=1`
  - **Importante**: El código de proyecto lo encontrarás en la URL de tu proyecto, tendrás algo tipo `https://console.actions.google.com/u/0/project/test-12345`
  - En definitiva, tu código, en ese caso, sería `test-12345`
- En el campo **`Token URL`** escribe `https://europe-west6-worldpeace-186e0.cloudfunctions.net/function-2`
- Las 2 últimas opciones son innecesarias, simplemente guarda mediante el botón **`Save`** de abajo a la derecha

## Paso 7
Con los 6 pasos anteriores, ya estaría todo configurado para que puedas añadir el dispositivo a Google Home. Es recomendable que esperes un rato a que todos los cambios y código se propaguen por la red de Google, si pruebas lo siguiente de inmediato lo más normal es que te falle. Ten paciencia.

- Abre la app de Google Home en tu móvil
- Añade un dispositivo nuevo
- Elige la opción de **`Works with Google`**
- Pasa de la lista de servicios y ve a la búsqueda mediante el icono de la lupa
- En el buscador, escribe el nombre del proyecto o simplemente `test`
  - Si tu proyecto se llamaba `Elgato Key Light` lo podrás encontrar como `[test] Elgato Key Light`
  - Una vez te salga, selecciónalo y se agregará a tus dispositivos de Google Home
    - Repito; esto puede fallar, simplemente dale tiempo entre prueba y prueba
- Una vez tengas el dispositivo disponible, es posible que siga sin funcionar; tienes que añadirlo a una habitación
- Y tras esto, debería de funcionar a la perfección, pudiendo encender y apagar, subir y bajar intensidad y también modificar la temperatura

:)
