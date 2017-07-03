**"Application service provider para Itris Software"**
Es una interfaz para obtener datos de una base de datos usando la arquitectura nativa de Itris Software. 
Las siguientes funcionalidades son utilizadas por la aplicación "com.pedidositrisv2.app" ver la ficha del producto.
https://play.google.com/store/apps/details?id=com.pedidositrisv2.app&hl=es
Todas las respuestas darán por resultado texto en formato JSON.


----------

**CONEXIÓN**
Con este servicio verificamos si la URL del WebService de la aplicación está on line o no.  Recibe una sola variable.
Esta URL se ejecuta cuando en la app se presiona el botón (Configuración->Conexión).
![enter image description here](http://pos.itris.com.ar/bak-02-17/img/botonesdered.png)

> Ingresa en tu navegador con la variable y valor deseado: 
> http://itris.no-ip.com:85/app/pos/itstestws.php
> 
> Definición de variable 
> **ws** = {url respetando el formato [http] y el [www]}
> 
> Modo de uso: (usamos como ejemplo el dominio de Itris Software)
> http://itris.no-ip.com:85/app/pos/itstestws.php?ws=http://www.itris.com.ar

**MODE DEBUG**

> Si lo que queremos hacer es un prueba rápida podemos activar el modo debug ingresando la siguiente ruta:
> http://itris.no-ip.com:85/app/pos/itstestws.php?debug=true

El atributo [debug] debe tener el siguiente valor: True.
El sistema realizará un test usando la página (http://www.itris.com.ar).

**RESULTADO**
> {"valor":1,"Status":"200","url":"http:\/\/iserver.itris.com.ar:3000\/ITSWS\/ItsCliSvrWS.asmx?WSDL"}

----------
**LOGIN**
Con este servicio la app prueba los datos de login al WebService de Itris Software.
Ingresa en tu navegador y la variable y valor deseado: 
![enter image description here](http://pos.itris.com.ar/bak-02-17/img/botonesdered.png)

> http://itris.no-ip.com:85/app/pos/itslogin.php

Definición de variables:
 
> **ws** = '*Ruta absoluta del WebService de Itris Software.*';

> **base** = '*Nombre de la base de datos de Itris Software.*';

> **user** = 'Usuario de la aplicación Itris';

> **pass** = 'Password de la aplicación Itris';


Ejemplo de testing de conexión de ingreso manual:
> http://itris.no-ip.com:85/app/pos/itslogin.php?ws=http://itris.no-ip.com:85/ItsWs/ItsCliSvrWS.asmx?WSDL&base=LM_10_09_14&user=administrador&pass=12348

Resultado

> {"ItsLoginResult":"1","motivo":"La base de datos no existe, verifique la existencia de la misma"}

**Resultados y definiciones:**
*ItsLoginResult*: Puede devolver 0 (cero) o 1 (uno). Cero cuando es ejecución exitoso y Uno es ejecución con errores.

*motivo*: Indica el motivo de ejecución.

Para este ejemplo vemos que el resultado contiene código 1 (uno) lo que refiere a un error y además tenemos el motivo del error. Para poder probar el login con tus webservice, tenés que reemplazar los valores de las variables por los datos que correspondan a tu conexión.

**MODE DEBUG**
Podemos probar la ruta en modo debug ingresando la siguiente dirección pasando como variable **debug = true** esto significa que la el ItsLogin será ejecutado con datos predefinidos.

> http://itris.no-ip.com:85/app/pos/itslogin.php?debug=true

El resultado será el siguiente:

> {"ItsLoginResult":"0","session":"{F5D4CDEE-D0D9-4629-8EE9-7276F07F76EF}"}

**Resultados y definiciones:**
*ItsLoginResult*: Puede devolver **0** (cero) o **1** (uno). **Cero** cuando es ejecución exitoso y **Uno** es ejecución con errores.

*session*: Es un string de sesión que devuelve el WebService para luego poder utilizar todos los métodos.


----------

**DESCARGAR CLIENTES**
Con esta funcionalidad la aplicación obtiene los clientes de la base de datos pasada por parámetros. Recibe cuatro variable.
![enter image description here](http://pos.itris.com.ar/bak-02-17/img/downclientes.png)

> http://itris.no-ip.com:85/app/pos/downloadclient.php

Definición de variables:
 
> **ws** = '*Ruta absoluta del WebService de Itris Software.*';

> **base** = '*Nombre de la base de datos de Itris Software.*';

> **user** = 'Usuario de la aplicación Itris';

> **pass** = 'Password de la aplicación Itris';

Ejemplo de testing de conexión de ingreso manual:
> http://itris.no-ip.com:85/app/pos/itslogin.php?ws=http://iserver.itris.com.ar:3000/ItsWs/ItsCliSvrWS.asmx?WSDL&base=LM_10_09_14&user=administrador&pass=12348

Para probar con los datos reales de tu WebService solo se tiene que reemplazar los valores de las variables (WS, BD, USER, PASS).

El resultado será un JSON con el siguiente formato:

> {"ItsLoginResult":"0",
> "ItsGetDate":"2016\/10\/08 14:17:06",
> "Cantidad":2,
> "Data":
> [{
> "ID":" 14931538",
> "DESCRIPCION":"Martin Coste",
> "TE":"15-5133 4525",
> "NUM_DOC":"14.931.538",
> "FK_ERP_LIS_PRECIO":"1",
> "SALDO":13212.12},
> 
> {"ID":"00000000",
> "DESCRIPCION":"%",
> "TE":"15-4960-0422",
> "NUM_DOC":"00.000.000",
> "FK_ERP_LIS_PRECIO":"2",
> "SALDO":0}
> ]}

**Resultados y definiciones:**
***ItsLoginResult***: Puede devolver **0** (cero) o **1** (uno). **Cero** cuando es ejecución exitoso y **Uno** es ejecución con errores.

***ItsGetDate***: Contiene la fecha y hora de la última vez que se le solicitó los datos al webservice de Itris.

***Cantidad***: Indica la cantidad de registros obtenidos.

***ID***: Corresponde al campo *código* de la empresa de la tabla *ERP_EMPRESAS*.

***DESCRIPCION***: Corresponde al campo *Descripción* de la empresa de la tabla *ERP_EMPRESAS*.

***TE***: Corresponde al campo *Teléfono* de la empresa de la tabla *ERP_EMPRESAS*.

***NUM_DOC***: Corresponde al campo *Número de documento* de la empresa de la tabla *ERP_EMPRESAS*.

***FK_ERP_LIS_PRECIOS***: Indica el *ID* de la lista de precios asociada a la empresa en la tabla *ERP_EMPRESAS*.

***SALDO***: Corresponde al saldo de cuenta corriente del cliente. El dato se indica en el campo *Saldo* en la tabla *ERP_EMPRESAS*.

**MODE DEBUG**
Si lo que queremos hacer es un prueba rápida podemos activar el modo debug ingresando la siguiente ruta:
> http://itris.no-ip.com:85/app/pos/downloadclient.php?debug=true

El resultado será el siguiente:

> {"ItsLoginResult":"0","ItsGetDate":"2016\/10\/08 14:35:51","Cantidad":2,"Data":[{"ID":" 14931538","DESCRIPCION":"Martin Coste","TE":"15-5133-4525","NUM_DOC":"14.931.538","FK_ERP_LIS_PRECIO":"1","SALDO":13212.12},{"ID":"00000000","DESCRIPCION":"%","TE":"15-4960-0422","NUM_DOC":"00.000.000","FK_ERP_LIS_PRECIO":"2","SALDO":0}]}


----------

**PRECIOS DE VENTAS Y STOCK**
Este proceso permite recuperar los precios y stock.
![enter image description here](http://pos.itris.com.ar/bak-02-17/img/downprecios.png)
> http://itris.no-ip.com:85/app/pos/erp_pre_ven.php

Definición de variables:
 
> **ws** = '*Ruta absoluta del WebService de Itris Software.*';

> **base** = '*Nombre de la base de datos de Itris Software.*';

> **user** = 'Usuario de la aplicación Itris';

> **pass** = 'Password de la aplicación Itris';

Ejemplo de testing de conexión de ingreso manual:
> http://itris.no-ip.com:85/app/pos/erp_pre_ven.php?ws=http://iserver.itris.com.ar:3000/ItsWs/ItsCliSvrWS.asmx?WSDL&base=LM_10_09_14&user=administrador&pass=12348

Para probar con los datos reales de tu WebService solo se tiene que reemplazar los valores de las variables (WS, BD, USER, PASS).

El resultado será un JSON con el siguiente formato:

> {"ItsLoginResult":"0",
>  "ItsGetDate":"2016\/10\/08 18:47:31",
>  "Cantidad":40,
>  "Data[{
>  "ID":"11",
>  "FK_ERP_ARTICULOS":"SC436X8",
>  "DES_ART":"Horno Electrico 6 Funciones",
>  "FK_ERP_LIS_PRECIO":"2",
>  "SAL_DISP":"0.00",
>  "PRECIO":"80.0000"}]
>  }

**Resultados y definiciones:**
***ItsLoginResult***: Puede devolver **0** (cero) o **1** (uno). **Cero** cuando es ejecución exitoso y **Uno** es ejecución con errores.

***ItsGetDate***: Es la fecha y hora de última actualización.

***Cantidad***: Indica la cantidad de registros obtenidos.

***ID*** : Es el ID de la tabla contenedora de los precios y stock de ventas.
***FK_ERP_ARTICULOS***: Es el código de artículo.
***DES_ART***: Es la descripción de artículos.

**MODE DEBUG**
Si lo que queremos hacer es un prueba rápida podemos activar el modo debug ingresando la siguiente ruta:

> http://itris.no-ip.com:85/app/pos/erp_pre_ven.php?debug=true

Lo que vamos a tener por resultado es un json con la siguiente información: 

> {"ItsLoginResult":"0","ItsGetDate":"2016\/10\/08 18:43:53","Cantidad":1,"Data":[{"ID":"11","FK_ERP_ARTICULOS":"SC436X8","DES_ART":"Horno Electrico 6 Funciones","FK_ERP_LIS_PRECIO":"2","SAL_DISP":"0.00","PRECIO":"80.0000"}]}

Con esta sencilla prueba nos aseguramos que la aplicación está funcionando correctamente.

----------

**SINCRONIZACION DE DATOS**
Métodos para el envío de datos guardados en la aplicación.
Existe dos formas de enviar información a Itris y otra para enviar los datos guardado por email.

**ItsSync**
La primera opción de envío es ItsSync.php, la misma permite el ingreso de datos en Itris ***únicamente un solo registro por vez***:

![enter image description here](http://pos.itris.com.ar/bak-02-17/img/itssync.png)

> http://itris.no-ip.com:85/app/pos/itssync.php

Recibe las siguientes variables

> 	ws = "Ruta del WebService.";
	base = "Nombre de la base de datos.";
	usuario = "Nombre de usuario.";
	pass = "Contraseña de usuario.";
	id = "Es el ID de registro de la tabla local de la aplicación";
	empresa = "Es el ID de la empresa";
	articulo = "Es el código de artículo";
	precio = "Precio del artículo";
	cantidad = "La cantidad comprada del producto";

***MODO DEBUG***
Si lo que queremos hacer es un prueba rápida podemos activar el modo debug ingresando la siguiente ruta:
Solo tenés que cambiar el valor de la variable del ejemplo que sigue a continuación.

> http://itris.no-ip.com:85/app/pos/itssync.php?debug=true&articulo=234

Si no modificas el código del ID o por error ejecutas la URL dos veces lo que verás es el siguiente mensaje:

> {"ItsLoginResult":"1","motivo":"ItsPostResult dice: El art\u00edculo ya fue informado por la aplicaci\u00f3n"}

Si la solicitud se procesó con éxito entonces el resultado será el siguiente:

> {"ItsLoginResult":"0","id":"987"}

**Resultados y definiciones:**

>***ItsLoginResult***: Puede devolver **0** (cero) o **1** (uno). **Cero** cuando es ejecución exitoso y **Uno** es ejecución con errores.

También devuelve el número de ID de la tabla original de la APP:

> ***id***: Es el número de ID de la tabla original de la APP

----------

**ItsSyncAll**
La segunda opción de envío es ItsSyncAll.php, la misma permite el ingreso de datos en Itris ***de manera masiva***:

![enter image description here](http://pos.itris.com.ar/bak-02-17/img/itssyncall.png)

Al presionar este botón se ejecuta la siguiente lógica 

> http://itris.no-ip.com:85/app/pos/itssyncall.php

Recibe las siguientes variables

> 	ws = "Ruta del WebService.";
	base = "Nombre de la base de datos.";
	usuario = "Nombre de usuario.";
	pass = "Contraseña de usuario.";
	datos = "En formato json";

Este es el formato que se le debe pasar a la variable ***datos*** 

> [{"Datos":{"uuid":"42","id":2,"empresa":" 14931538","articulo":" XA-01-028 ","cantidad":1,"precio":1}}]

El Array debe contiene la siguiente información:

> uuid: "Es el ID único por dispositivo móvil",
> id: "Es el id de la tabla local del dispositivo",
> empresa: "Es el código de la empresa",
> articulo: "Es el código del artículo"
> cantidad: "Es la cantidad vendida",
> precio: "Es el precio del producto"
> 

**MODO DEBUG**
Si lo que queremos hacer es un prueba rápida podemos activar el modo debug ingresando la siguiente ruta:
Solo tenés que cambiar el valor de la variable del ejemplo que sigue a continuación.

Este es el script para ejecutar el ingreso de datos en modo debug: Solo tenés que cambiar el valor de la variable ***uuid***:

> http://itris.no-ip.com:85/app/pos/itssyncall.php?debug=true&datos=[{"Datos":{"uuid":"492","id":2,"empresa":"%2014931538","articulo":"%20XA-01-028%20","cantidad":1,"precio":1}}]

Si no modificaste el valor de la variable ***uuid*** el resultado que verás es el siguiente:

> {"ItsLoginResult":"1","motivo":"El art\u00edculo ya fue informado por la aplicaci\u00f3n","idinsertado":"2"}

Para los casos de inserción exitosa el resultado será el siguiente:

> {"ItsLoginResult":"0","Cantidad":1}


----------


**ItsSyncAllMail**
La tercer opción de envío es ItsSyncAllMail.php, la misma permite enviar a la APP un mail con todos los datos guardados:

![enter image description here](http://pos.itris.com.ar/bak-02-17/img/itssyncallMail.png)

Al presionar este botón en la APP lo que hace es armar un JSON con toda la información guardada en el dispositivo y enviar vía mail.
El array que envía tiene el siguiente formato:

>    [{"Datos":
>    {"id":177,
>    "articulo":"0000013",
>    "deposito":"1",
>    "cantidad":"5",
>    "fecha":20151209}
>    }}]';

El contenido de cada atributo es el siguiente:

> id: "Es el id de la tabla de la aplicación",
> articulo: "Es el código del artículo ",
> deposito: "Es el ID del depósito",
> cantidad: "Es la cantidad del artículo ingresado",
> fecha: "Es la fecha del pedido"

El email que recibirá esta información será la que esté definida en la sección Configuración->email

***MODE DEBUG***
Si lo que queremos hacer es un prueba rápida podemos activar el modo debug ingresando la siguiente ruta:
Solo tenés que cambiar el valor de la variable del ejemplo que sigue a continuación.

Este es el script para ejecutar el ingreso de datos en modo debug: Solo tenés que cambiar el valor de la variable ***imeil***:

> http://itris.no-ip.com:85/app/pos/itssyncallMail.php?debug=true&imeil=lcondori@itris.com.ar

Su ejecución hará que se envíe un mail con información predefinida simulando ser un pedido real, si todo fue bien lo que veremos es el siguiente resultado:

> {"ItsLoginResult":0,"motivo":"\u00a1Email fue enviado con \u00e9xito!"}

Si hubo algún inconveniente con el envío, lo que veremos será esto:

> {"ItsLoginResult":1,"motivo":"SMTP connect() failed. https:\/\/github.com\/PHPMailer\/PHPMailer\/wiki\/Troubleshooting \u00a1Volv\u00e9 a intentarlo!"}

Para corregir este problema simplemente volví a intentarlo.



----------


**REGISTROS DE ACTIVIDAD**
El sistema de servicio web que sirve la información a la APP cuenta con cinco LOG's de actividades para monitorear todos los comportamientos.

La lógica de archivos se arma de manera dinámica respetando la siguiente lógica:

> [URL del servidor][puerto][app][nombre del producto][Nombre de la base de datos][usuario][Nombre de archivo]

Para este ejemplo, la ruta está compuesta por la base de datos [LM_10_09_14] y por el nombre de usuario [administrador], tendrás que reemplazar estos valores para acceder a la actividad de tu aplicación.

***ItsException*** Cada error que se produzca en el servidor quedará registrado en el siguiente archivo:

> http://itris.no-ip.com:85/app/pos/activity/LM_10_09_14/administrador/ItsExceptions.log

***LogActivity*** Cada transacción que ocurra de manera exitosa quedará registrado en el siguiente archivo:

> http://itris.no-ip.com:85/app/pos/activity/LM_10_09_14/administrador/LogActivity.log


***Errores asociados a la base pero no a un usuario***
Para este ejemplo, la ruta está compuesta por la base de datos [LM_10_09_14], tendrás que reemplazar este valor por tu base de datos.

***ItsException*** Cada error que se produzca en el servidor quedará registrado en el siguiente archivo:

> http://itris.no-ip.com:85/app/pos/activity/LM_10_09_14/ItsExceptions.log

***LogActivity*** Cada transacción que ocurra de manera exitosa quedará registrado en el siguiente archivo:

> http://itris.no-ip.com:85/app/pos/activity/LM_10_09_14/LogActivity.log


----------


 Para obtener más información existen también archivos de registro de actividad que son producto de mala configuración o cualquier otro registro no relacionado a una base de datos en particular. Es decir es un registro de actividad que **no se separa por nombre de base de datos ni usuario**.
 
***ItsException***  En este caso a diferencia del anterior este log. de actividades se genera a nivel general, no está relacionado directamente a una base de datos ni usuario.

>  http://itris.no-ip.com:85/app/pos/activity/ItsExceptions.log

***LogActivity*** Cada transacción que ocurra de manera exitosa y que no esté estrictamente relacionado a una base de datos específica ni a un usuario, quedará registrado en el siguiente archivo:

> http://itris.no-ip.com:85/app/pos/activity/LogActivity.log


----------
***OTROS **lOG*****

***URL*** Guarda un registro de todas las URL que probamos desde la aplicación o desde el navegador.
¡Atención este log no es propio de ninguna app en concreto sino que es de todas las pruebas de todos los usuario! 

> http://itris.no-ip.com:85/app/pos/activity/URL.log
