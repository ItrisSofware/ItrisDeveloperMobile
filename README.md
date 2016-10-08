**"Application service provider para Itris Software"**
Es una interfaz para obtener datos de una base de datos usando la arquitectura nativa de Itris Software. 
Las siguientes funcionalidades son utilizadas por la aplicación "com.pedidositrisv2.app" ver la ficha del producto.
https://play.google.com/store/apps/details?id=com.pedidositrisv2.app&hl=es
Todos los resultados darán por resultado texto en formato JSON.


----------
![enter image description here](http://pos.itris.com.ar/img/botonesdered.png)

**CONEXIÓN**
Con este servicio verificamos si la URL del WebService de la aplicación está on line o no.  Recibe una sola variable.
Esta URL se ejecuta cuando en la app se presiona el botón (Configuración->Conexión).

> Ingresa en tu navegador con la variable y valor deseado: 
> http://itris.no-ip.com:85/app/pos/itstestws.php
> 
> Definición de variable 
> **ws** = {url respetando el formato [http] y el [www]}
> 
> Modo de uso: (usamos como ejemplo el dominio de Itris Software)
> http://itris.no-ip.com:85/app/pos/itstestws.php?ws=http://www.itris.com.ar

**MODE DEBUG**

> Si lo que queremos hacer es un prueba rápida podemos activar el modo debut ingresando la siguiente ruta:
> http://itris.no-ip.com:85/app/pos/itstestws.php?debug=true

El atributo [debug] debe tener el siguiente valor: True.
El sistema realizará un test usando la página (http://www.itris.com.ar).

**RESULTADO**
> {"valor":1,"Status":"200","url":"http:\/\/iserver.itris.com.ar:3000\/ITSWS\/ItsCliSvrWS.asmx?WSDL"}

----------
**LOGIN**
Con este servicio la app prueba los datos de login al WebService de Itris Software.
Ingresa en tu navegador y la variable y valor deseado: 

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
Podemos probar la ruta en modo debut ingresando la siguiente dirección pasando como variable **debug = true** esto significa que la el ItsLogin será ejecutado con datos predefinidos.

> http://itris.no-ip.com:85/app/pos/itslogin.php?debug=true

El resultado será el siguiente:

> {"ItsLoginResult":"0","session":"{F5D4CDEE-D0D9-4629-8EE9-7276F07F76EF}"}

**Resultados y definiciones:**
*ItsLoginResult*: Puede devolver **0** (cero) o **1** (uno). **Cero** cuando es ejecución exitoso y **Uno** es ejecución con errores.

*session*: Es un string de sesión que devuelve el WebService para luego poder utilizar todos los métodos.


----------

**DESCARGAR CLIENTES**
Con esta funcionalidad la aplicación obtiene los clientes de la base de datos pasada por parámetros. Recibe cuatro variable.

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
Si lo que queremos hacer es un prueba rápida podemos activar el modo debut ingresando la siguiente ruta:
> http://itris.no-ip.com:85/app/pos/downloadclient.php?debug=true

El resultado será el siguiente:

> {"ItsLoginResult":"0","ItsGetDate":"2016\/10\/08 14:35:51","Cantidad":2,"Data":[{"ID":" 14931538","DESCRIPCION":"Martin Coste","TE":"15-5133-4525","NUM_DOC":"14.931.538","FK_ERP_LIS_PRECIO":"1","SALDO":13212.12},{"ID":"00000000","DESCRIPCION":"%","TE":"15-4960-0422","NUM_DOC":"00.000.000","FK_ERP_LIS_PRECIO":"2","SALDO":0}]}


----------

