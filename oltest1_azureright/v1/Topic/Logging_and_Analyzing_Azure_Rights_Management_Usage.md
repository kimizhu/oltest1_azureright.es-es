---
description: na
keywords: na
title: Logging and Analyzing Azure Rights Management Usage
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
---
# Registro y an&#225;lisis del uso de Azure Rights Management
Use la información de este tema para comprender cómo puede usar el registro de uso con Azure Rights Management (Azure RMS). El servicio Azure Rights Management permite registrar todas las solicitudes que realice para su organización, lo que incluye solicitudes de usuarios, acciones llevadas a cabo por administradores de Rights Management en su organización y acciones llevadas a cabo por operadores de Microsoft para admitir su implementación de Azure Rights Management.

A continuación, puede usar estos registros de Azure Rights Management para admitir los siguientes escenarios empresariales:

-   Analizar enfoques empresariales.

    Azure Rights Management escribe los registros con el formato de registro extendido W3C en una cuenta de almacenamiento de Azure proporcionada por el usuario. Entonces puede dirigir estos registros al repositorio que elija (como una base de datos, un sistema de procesamiento analítico en línea (OLAP) o un sistema de asignar-reducir) para analizar la información y producir informes. Por ejemplo, podría notificar quién está accediendo a sus datos protegidos con RMS. Puede determinar a qué datos protegidos con RMS está accediendo la gente y desde dónde y desde qué dispositivos. Puede averiguar si estas personas logran leer contenido protegido. También puede identificar qué personas han leído un documento importante que estaba protegido.

-   Supervisar para controlar el abuso.

    La información del registro de Azure Rights Management está a su disposición casi en tiempo real, de manera que puede supervisar de manera continua el uso que se haga en su empresa de Azure Rights Management. El 99,9% de los registros están disponibles en un plazo de 15 minutos de una acción iniciada por RMS.

    Por ejemplo, puede que desee que se le alerte de si surge un aumento repentino de las personas que leen datos protegidos por RMS fuera de las hora laborales estándar, lo que podrían indica que un usuario malintencionado está recopilando información para venderla a competidores. O bien, si el mismo usuario aparentemente accede a los datos desde dos direcciones IP diferentes dentro de un breve intervalo de tiempo, lo que podría indicar que se ha puesto en peligro una cuenta de usuario.

-   Realice un análisis forense.

    Si tiene una pérdida de información, es probable que se le pregunte quién accedió recientemente a documentos específicos y a qué información accedió la persona sospechosa. Puede responder a este tipo de preguntas con Azure Rights Management y los registros, porque las personas que usan el contenido protegido siempre deben obtener una licencia de Azure Rights Management para abrir documentos e imágenes que estén protegidos con Azure Rights Management, incluso en el caso de que dichos archivos se muevan por correo electrónico o se copien en unidades USB u otras unidades de almacenamiento. Esto significa que puede usar los registros de Azure Rights Management como el origen fundamental de la información para realizar el análisis forense cuando protege sus datos con Azure Rights Management.

> [!NOTE]
> Si solo está interesado en el registro de las tareas administrativas para Azure Rights Management y no desea realizar un seguimiento del modo en que los usuarios usan Rights Management, puede usar el cmdlet [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) de Windows PowerShell de Azure Rights Management.
> 
> También puede usar el Portal de Azure clásico para ver informes de uso de alto nivel que incluyen **Uso de RMS**, **Usuarios de RMS más activos**, **Uso de dispositivos RMS** y **Uso de aplicaciones con RMS habilitado**. Para poder acceder a estos informes desde el Portal de Azure clásico, haga clic en **Active Directory**, seleccione un directorio y ábralo y, luego, haga clic en **INFORMES**.

Use las secciones siguientes para obtener más información sobre el registro de uso de Azure Rights Management.

-   [Cómo habilitar el registro de uso de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_EnableRMSLogging)

-   [Cómo acceder a los registros de uso de Azure Rights Management y usarlos](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs)

-   [Cómo administrar el almacenamiento de registro de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_ManageStorage)

-   [Cómo delegar el acceso a los registros de uso de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate)

-   [Cómo interpretar los registros de uso de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret)

-   [Referencia de Windows PowerShell](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_PowerShell)

## <a name="BKMK_EnableRMSLogging"></a>Cómo habilitar el registro de uso de Azure Rights Management
El registro de uso de Azure Rights Management es opcional, por lo que, si desea usarlo, debe llevar a cabo pasos específicos. El uso del registro de uso de Azure Rights Management no implica ningún cambio en la manera en que Rights Management funciona. Además, el propio proceso es gratuito. Sin embargo, debe proporcionar una cuenta de almacenamiento de Azure para los registros y se le cobrará por este almacenamiento.

Antes de comenzar, asegúrese de que cumpla los siguientes requisitos previos para usar el registro de uso de Azure Rights Management:

|Requisito|Más información|
|-------------|-------------------|
|Una suscripción administrada por TI que incluye Azure Rights Management|Debe tener una suscripción a Microsoft Azure Rights Management administrada por su organización. Las organizaciones que usen RMS para usuarios individuales no pueden usar el registro de uso de Azure Rights Management.<br /><br />Si su organización tiene usuarios que emplean RMS para usuarios, el registro de uso de Azure Rights Management ofrece una razón empresarial muy atractiva para convertir RMS para usuarios en una suscripción a Microsoft Azure Rights Management.<br /><br />Para obtener más información sobre las suscripciones que incluyen Azure RMS, vea la sección [Suscripciones en la nube que son compatibles con Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) del tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).<br /><br />Para obtener más información sobre RMS para usuarios, consulte [RMS para usuarios y Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)|
|la suscripción a Azure|Debe tener una suscripción a Azure y almacenamiento suficiente en Azure para sus registros de Azure Rights Management.|
|Windows PowerShell para Azure Rights Management|Si no lo ha hecho ya, descargue e instale el módulo de Windows PowerShell para Azure Rights Management. Para configurar y administrar sus registros de uso de Azure Rights Management, tendrá que cmdlets de Windows PowerShell.<br /><br />Para obtener más información, vea [Instalación de Windows PowerShell para Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).|
Use el siguiente procedimiento para habilitar el registro de uso de Azure Rights Management, que incluye los pasos para crear una cuenta de almacenamiento de Azure y, después, configure Azure para usar esta cuenta de almacenamiento para sus registros de Rights Management.

> [!NOTE]
> Este procedimiento supone que dispone de una cuenta de Azure. El registro de uso de Azure Rights Management admite cuentas individuales pero, como procedimiento recomendado, use cuentas profesionales o educativas. Además, recomendamos que cree una cuenta de almacenamiento dedicado para sus registros de Rights Management. Debe compartir las claves de acceso de almacenamiento con Azure Rights Management y, potencialmente, con otras personas si también ellas van a usar los archivos de registro.
> 
> Para obtener más información sobre Almacenamiento de Azure, consulte la [documentación de Azure para Almacenamiento](http://azure.microsoft.com/documentation/services/storage/).

#### Cómo crear una cuenta de almacenamiento y habilitar el registro de uso de Azure Rights Management

1.  Inicie sesión en el [Portal de Azure](https://portal.azure.com/).

2.  En el menú del concentrador, seleccione **Nuevo** -&gt; **Datos y almacenamiento** -&gt; **Cuenta de almacenamiento**.

    > [!TIP]
    > Si no ve esta opción, compruebe que dispone de una suscripción de Azure además de la suscripción para Rights Management.

3.  Conserve el modelo de implementación predeterminado **Clásico** y haga clic en **Crear**.

    Especifique el nombre de su cuenta de almacenamiento y, si es necesario, cambie las opciones seleccionadas de los campos **Plan de tarifa**, **Grupo de recursos** y **Suscripción** e indique si desea usar la opción **Anclar al panel**. Después, haga clic en **CREAR**. Espere a que finalice la actividad **Creando cuenta de almacenamiento**.

4.  Haga clic en la cuenta de almacenamiento recién creada y, después, en **Configuración**.

5.  En la hoja **Configuración**, haga clic en el icono **Claves**.

6.  En la hoja **Administrar claves**, copie el valor de la **CLAVE DE ACCESO PRINCIPAL** y cierre la hoja.

7.  Inicie Windows PowerShell con la opción **Ejecutar como administrador**. Ejecute el comando [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) para conectarse al servicio de Azure Rights Management:

    ```
    Connect-AadrmService
    ```

8.  Use el comando [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) para especificar dónde desea conservar sus registros de uso de Azure Rights Management. Para ello, sustituya *&lt;Access_Key&gt;* por la clave de acceso principal que ha copiado en el paso 6 y *&lt;StorageAccount&gt;* por el nombre de la cuenta de almacenamiento que ha creado en el paso 3:

    ```
    $accesskey = convertto-securestring -asplaintext -force –string <Access_Key> Set-AadrmUsageLogStorageAccount -AccessKey $accesskey -StorageAccount <StorageAccount>
    ```

9. Use el comando [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx) para habilitar el registro de uso de Azure Rights Management:

    ```
    Enable-AadrmUsageLogFeature
    ```
    Debe ver el siguiente mensaje: **La característica de registro de uso está habilitada para el servicio de Rights Management Service.**

Ahora que el registro de uso está habilitado, Azure Rights Management puede empezar a registrar todas las acciones relativas a su organización y a guardar esta información en su cuenta de almacenamiento. La información de registro no está disponible antes de este punto.

Para obtener más información sobre cómo crear cuentas de almacenamiento, consulte la sección [Crear una cuenta de almacenamiento](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/) en [Acerca de las cuentas de almacenamiento de Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/), en la documentación de Azure.

## <a name="BKMK_AccesAndUseLogs"></a>Cómo acceder a los registros de uso de Azure Rights Management y usarlos
Azure Rights Management escribe registros en su cuenta de almacenamiento de Azure como una serie de blobs. Cada blob contiene uno o más registros, en formato de registro extendido W3C. Los nombres de blob son números, en el orden en que se crearon. La sección [Cómo interpretar los registros de uso de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret) que aparece más adelante en este documento contiene más información acerca del contenido del registro y su creación.

Puede que los registros tarden en aparecer en su cuenta de almacenamiento después de realizar alguna acción de Azure Rights Management. La mayoría de los registros aparecen en 15 minutos.

La cuenta de almacenamiento que ha creado para sus registros de uso de Azure Rights Management es similar a un buzón de correo y admite la lectura directamente desde la cuenta de almacenamiento, pero no está optimizada para usarse de esta manera. En su lugar, para lograr un mejor rendimiento y para ayudar a reducir costos, recomendamos que descargue los registros en el almacenamiento local, como una carpeta local, una base de datos o un repositorio de asignar-reducir.

Puede descargar sus registros de uso de dos maneras:

-   Use el cmdlet de Windows PowerShell [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx).

    Esta es la manera más sencilla de acceder a los registros de uso. Este cmdlet descarga registros en su equipo, descargando cada blob como un archivo en la ubicación que especifique.

-   Utilice el [SDK de Almacenamiento de Azure](http://www.windowsazure.com/en-us/develop/net/) para escribir su propia aplicación personalizada para descargar los registros.

    Una aplicación personalizada puede ofrecer mayor flexibilidad que el cmdlet Get-AadrmUsageLogs. Por ejemplo, puede que desee delegar la descarga de los registros a alguien o a un proceso que no deba usar sus credenciales administrativas de Azure Rights Management. O bien, puede que desee sondear los registros en tiempo real porque desea supervisar el uso incorrecto.

#### Descargar sus registros de uso mediante PowerShell

-   Inicie Windows PowerShell con la opción **Ejecutar como administrador** y ejecute **Get-AadrmUsageLog –Path &lt;location&gt;**. Por ejemplo, después de crear una carpeta denominada **logs** en la unidad E:

    -   Para descargar todos los registros disponibles en su carpeta E:\logs: `Get-AadrmUsageLog -Path "e:\logs"`

    -   Para descargar un intervalo específico de blobs: `Get-AadrmUsageLog –Path "e:\logs" –FromCounter 1024 –ToCounter 2047`

Cuando ejecuta estos cmdlets, Windows PowerShell muestra el nombre del último blob que se descargó. Puede asignar este nombre a una variable, lo que le permite ejecutar Get-AadrmUsageLog en un bucle o trabajo de programación, descargando solo los registros incrementales cada vez.

Por ejemplo:

**PS C:\&gt; $LastBlobName = Get-AadrmUsageLog –Path "e:\logs"**

**1527**

**PS C:\&gt; $LastBlobName**

**1527**

> [!TIP]
> Puede agrupar todos los archivos de registro descargados en un formato CSV mediante el uso del [Analizador del registro de Microsoft](http://www.microsoft.com/download/details.aspx?id=24659), una herramienta para realizar conversiones entre diversos formatos de archivo conocidos. También puede usar esta herramienta para convertir datos al formato SYSLOG o importarlo a un base de datos. Una vez que haya instalado la herramienta, ejecute **LogParser.exe /?** para obtener ayuda e información para usar esta herramienta. Por ejemplo, puede ejecutar el siguiente comando para importar toda la información en un formato de archivo .log: **logparser –i:w3c –o:csv “SELECT &#42; INTO AllLogs.csv FROM &#42;.log”**.

Puede suspender y reanudar el uso del registro de uso. Cuando suspende el registro, Azure Rights Management conserva la información de su cuenta de almacenamiento, de manera que puede reanudar el registro con facilidad.

#### Suspender y reanudar el registro de uso

-   Para suspender el registro, use el siguiente cmdlet: [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   Para reanudar el registro, use el siguiente cmdlet: [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   Para comprobar si el registro está habilitado o deshabilitado, use el siguiente cmdlet: [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

    El valor **True** indica que el registro de uso está habilitado para Azure Rights Management, y el valor **False** indica que el registro de uso está deshabilitado.

## <a name="BKMK_ManageStorage"></a>Cómo administrar el almacenamiento de registro de Azure Rights Management
Se le cobra por el espacio de almacenamiento que se usa para conservar sus registros de Azure Rights Management.

Azure Rights Management no administra automáticamente los archivos del registro de uso. Si no realiza ninguna acción, permanecerán en su cuenta de almacenamiento. Sin embargo, para conservar el espacio y reducir los costes de almacenamiento, puede que desee eliminarlos tras su descarga. O bien, puede elegir qué archivos desea eliminar. Con una excepción, Azure Rights Management no usa estos archivos de registro, por lo que no hay restricciones acerca de cuándo puede eliminarlos.

El archivo que no debe eliminar (ni modificar) es el que se llama **metadata** que se encuentra en el contenedor **rms-metadata**. Azure Rights Management usa este blob para realizar un seguimiento del último número de blob que se use. Si se elimina este archivo, Azure Rights Management empieza un nuevo contenedor para los registros con un número de blob que empieza por 1. Todas las descargas futuras que usen el cmdlet Get-AadrmUsageLog usarán este nuevo contenedor para descargar archivos de registro. Como resultado, se retienen los registros del contenedor original pero huérfanos. La única manera de descargar estos registros huérfanos es usar el SDK de almacenamiento de Azure.

> [!TIP]
> En lugar de administrar el almacenamiento del registro de Azure Rights Management el propio usuario, puede delegar esta función de administración en otra empresa compartiendo su nombre de cuenta de almacenamiento y la clave de acceso. Para obtener más información, consulte la sección [Cómo delegar el acceso a los registros de uso de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate) que aparece más adelante en este tema.

En algunas circunstancias, puede que desee regenerar sus claves de acceso de almacenamiento. Por ejemplo:

-   Cambia la empresa que administra sus registros de uso de Azure Rights Management.

-   Sospecha que se ha puesto en peligro la clave de acceso de almacenamiento.

Si le sucede esto, es cuando usa la clave de acceso secundaria (suponiendo que anteriormente estuviera usando la clave de acceso primaria) para garantizar la continuidad del servicio. Cuando vuelva a generar la clave de acceso que no estuviera usando anteriormente, configurará Azure Rights Management para que use la nueva clave. Use el siguiente procedimiento para volver a generar la clave de acceso secundaria y configurar Azure Rights Management para que la use:

#### Volver a generar la clave de acceso secundaria

1.  Inicie sesión en el [Portal de Azure](https://portal.azure.com/).

2.  Haga clic en **Todos los recursos** y, para buscar su almacenamiento, escriba el nombre del almacenamiento en el cuadro de texto.

3.  Seleccione el almacenamiento y haga clic en **Configuración**.

4.  Haga clic en el icono **Claves**.

5.  En la sección **Administrar claves**, haga clic en **Regenerar clave secundaria**, haga clic en Sí para confirmar que desea regenerar la clave de acceso secundaria y copie la nueva clave en el portapapeles.

    No cierre el Portal de Azure.

6.  Inicie Windows PowerShell con la opción **Ejecutar como administrador** y use el cmdlet [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) para configurar Azure Rights Management para usar esta nueva clave de acceso. Para ello, sustituya *&lt;StorageAccount&gt;* por el nombre de la cuenta de almacenamiento y *&lt;Access_Key&gt;* por la clave de acceso secundaria regenerada que acaba de copiar:

    ```
    Set-AadrmUsageLogStorageAccount -StorageAccount <StorageAccount>-AccessKey <Access_Key>
    ```
    > [!WARNING]
    > Aunque puede cambiar a otra cuenta de almacenamiento cuando ejecute este comando, esta acción deja huérfanos sus registros previos, con lo que ya no se podrá acceder a ellos con el cmdlet Set-AadrmUsageLogStorageAccount o con funciones y comandos de administración similares.

7.  En el Portal de Azure, en la sección **Administrar claves**, regenere su clave de acceso principal.

Para obtener más información sobre la manera de administrar las claves de acceso de almacenamiento, consulte la sección [Administración de las claves de acceso de almacenamiento](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/) en [Acerca de las cuentas de almacenamiento de Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/), en la documentación de Azure.

## <a name="BKMK_Delegate"></a>Cómo delegar el acceso a los registros de uso de Azure Rights Management
Puede delegar el acceso a sus registros de RMS compartiendo su clave de acceso y nombre de cuenta de almacenamiento. Puede que desee delegar el acceso a otro usuario administrativo, a un desarrollador de su propia organización o a un proveedor de software independiente (ISV). Dado que no tendrán sus credenciales de administrador de RMS, no pueden usar el cmdlet Get-AardrmUsageLog para descargar los registros de RMS. En su lugar, deben usar el SDK de almacenamiento de Windows para descargar los registros. Como alternativa, puede escribir una aplicación para que lea los registros directamente desde el almacenamiento de almacenamiento de Azure.

Es seguro compartir su clave de acceso y su nombre de cuenta de almacenamiento de esta manera cuando la cuenta de almacenamiento está dedicada a sus registros de RMS. Incluso cuando otras personas tienen su clave de acceso, no pueden usarla para acceder a ninguna otra cuenta de almacenamiento o usar su cuenta de inquilino de RMS.

## <a name="BKMK_Interpret"></a>Cómo interpretar los registros de uso de Azure Rights Management
Use la siguiente información como ayuda para interpretar los registros de uso de Azure Rights Management.

### El diseño de la cuenta de almacenamiento
La primera vez que Azure Rights Management escribe registros en la cuenta de almacenamiento, crea los siguientes dos contenedores:

-   **Rms-metadata**: este contenedor está reservado para Azure Rights Management. No modifique ni elimine este contenedor.

-   **Rms-logs-&lt;guid&gt;**: en este contenedor Azure Rights Management crea y guarda los registros. Puede eliminar de manera segura los archivos de este contenedor si ya no desea la información de registro que pueden contener.

Con el tiempo, Azure Rights Management puede crear contenedores **Rms-logs-&lt;guid&gt;** adicionales. Por ejemplo, si el contenedor **Rms-metadata** se daña o se elimina de manera accidental, Azure Rights Management restablece su contenido y crea un nuevo contenedor **Rms-logs-&lt;guid&gt;** para todos los registros futuros. Los registros antiguos del contenedor antiguo no se eliminan pero están huérfanos.

### La secuencia de registro
Azure Rights Management escribe los registros como una serie de blobs. Cada blob contiene uno o más registros, en formato de registro W3C extendido.

El nombre de cada blob es un número. Dentro de cada contenedor de registro, el primer blob se denomina 000000001. Cada blob se denomina secuencialmente en el orden en que se creó. Cada blob contiene uno o más registros. Cada registro tiene una marca de tiempo UTC que indica el momento en el que la solicitud correspondiente recibió el servicio de Azure Rights Management.

> [!IMPORTANT]
> El sistema de registro de Azure Rights Management se optimiza para proporcionarle registros con rapidez, en lugar de en estricto orden secuencial. El orden de los blobs, así como el orden de los registros dentro de un blob, puede que esté fuera de la secuencia cronológica. El único motivo por el que se asignan nombres a los blobs de manera secuencial es para habilitarle su descarga efectiva de manera incremental.
> 
> Dos ejemplos de resultados de secuencia de registro:
> 
> -   Los registros del blob 000000004 se pueden superponer cronológicamente con los registros del blob 000000003. En casos extremos, todos los registros del blob 000000004 podrían haberse generados antes que todos los registros del blob 000000003.
> -   El segundo registro se podría haber generado antes que el primer registro pero se escribió en el almacenamiento en el orden inverso.

Antes de analizar sus registros de uso de Azure Rights Management, recomendamos que descargue e importe el registro en un repositorio donde pueda ordenar los registros en función de los registros basados en su marca de tiempo. Para obtener más información sobre cómo descargar los archivos, consulte la sección [Cómo acceder a los registros de uso de Azure Rights Management y usarlos](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs) de este tema.

Dado que los registros no son necesariamente cronológicos, sino que la mayoría de ellos se escriben a los 15 minutos de la solicitud, cuando identifique los registros que desea usando su marca de tiempo, agregue 15 minutos al tiempo en el que está interesado. A continuación, descargue estos registros. Esta estrategia debe garantizar que obtiene casi todos los registros.

Otra cuestión que hay que recordar es que la marca de tiempo de cada registro corresponde a la hora local del servicio de Azure Rights Management que procesó la solicitud. Dado que Azure Rights Management se ejecuta en varios servidores de varios centros de datos, a veces puede parecer que los registros estén fuera de secuencia, aunque estén ordenados por su marca de tiempo. Sin embargo, la diferencia es mínima y generalmente se encuentra en un margen de un minuto. En la mayoría de los casos, este asunto no sería un problema para análisis de registros.

### El formato del blob
Cada blob está en formato de registro extendido W3C. Empieza por las siguientes dos líneas:

**#Software: RMS**

**#Version: 1.1**

La primera línea identifica que se trata de registros de Azure Rights Management. La segunda línea identifica que el resto del blob sigue la especificación de la versión 1.1. Recomendamos que las aplicaciones que analicen estos registros comprueben estas dos líneas antes de continuar analizando el resto del blob.

La tercera enumera una lista de nombres de campos separados por pestañas:

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip**

Cada una de las líneas posteriores es un registro. Los valores de los campos se encuentran en el mismo orden que la línea anterior y están separados por pestañas. Use la siguiente tabla para interpretar los campos.

|Nombre de campo|Tipo de datos W3C|Descripción|Valor de ejemplo|
|-------------------|---------------------|---------------|--------------------|
|date|Fecha|Fecha UTC cuando se realizó el servicio de la solicitud.<br /><br />El origen es el reloj local del servidor que realizó el servicio de la solicitud.|2013-06-25|
|time|Hora|Hora UTC en formato de 24 hora cuando se realizó el servicio de la solicitud.<br /><br />El origen es el reloj local del servidor que realizó el servicio de la solicitud.|21:59:28|
|row-id|Texto|GUID único para este registro.<br /><br />Este valor es útil cuando agrega registros o copia registros en otro formato.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Nombre|Nombre de la API de RMS que se solicitó.|AcquireLicense|
|user-id|Cadena|El usuario que realizó la solicitud.<br /><br />El valor se incluye entre comillas únicas. Algunos tipos de solicitudes son anónimos, en cuyo caso el valor es ”.|‘joe@contoso.com’|
|result|Cadena|‘Success’ si se realizó el servicio de la solicitud correctamente.<br /><br />El tipo de error entre comillas si se produjo un error de la solicitud.|‘Success’|
|correlation-id|Texto|GUID que es común entre el registro del cliente de RMS y el registro del servidor para una solicitud proporcionada.<br /><br />Este valor puede ser útil para ayudar a solucionar problemas del cliente.|cab52088-8925-4371-be34-4b71a3112356|
|content-id|Texto|GUID, entre llaves, que identifica el contenido protegido (por ejemplo, un documento).<br /><br />Este campo tiene un valor solo si request-type es AcquireLicense y está en blanco para todos los demás tipos de solicitudes.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|Cadena|Dirección de correo electrónico del propietario del documento.|alice@contoso.com|
|issuer|Cadena|Dirección de correo electrónico del emisor del documento.|alice@contoso.com (o) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Template-id|Cadena|Identificador de la plantilla que se usa para proteger el documento.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|File-name|Cadena|Nombre de archivo del documento que se ha protegido.|TopSecretDocument.docx|
|Date-published|Fecha|Fecha en la que se ha protegido el documento.|2015-10-15T21:37:00|
|c-info|Cadena|Información acerca de la plataforma del cliente que está realizando la solicitud.<br /><br />La cadena específica varía, en función de la aplicación (por ejemplo, el sistema operativo o el explorador).|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|Address|Dirección IP del cliente que realiza la solicitud.|64.51.202.144|

#### Excepciones para el campo user-id
Aunque el campo user-id suele indicar el usuario que hay realizado la solicitud, hay dos excepciones en las que el valor no se asigna a un usuario real:

-   El valor **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**.

    Esto indica que un servicio de Office 365, como Exchange Online o Sharepoint Online, están realizando la solicitud. En la cadena, *&lt;YourTenantID&gt;* es el GUID de su inquilino y *&lt;region&gt;* es la región donde se registra el inquilino. Por ejemplo, **na** representa a Norteamérica, **eu** representa a Europa y **ap** representa a Asia.

-   Si está usando el conector RMS.

    Las solicitudes de este conector se registran con el nombre de entidad de servicio que RMS genera automáticamente al instalar el conector RMS.

#### Tipos de solicitudes típicas
Hay muchos tipos de solicitudes de Azure Rights Management, pero en la tabla siguiente se identifican algunos de los tipos que normalmente se usan más.

|Tipo de solicitud|Descripción|
|---------------------|---------------|
|AcquireLicense|Un cliente solicita desde un equipo basado en Windows una licencia para contenido protegido con RMS.|
|AcquirePreLicense|Un cliente, en nombre del usuario, solicita una licencia para contenido protegido con RMS.|
|AcquireTemplates|Se ha realizado una llamada para adquirir plantillas basadas en identificadores de plantilla.|
|AcquireTemplateInformation|Se ha realizado una llamada para obtener los identificadores de la plantilla del servicio.|
|AddTemplate|Se realiza una llamada desde el Portal de Azure clásico para agregar una plantilla.|
|BECreateEndUserLicenseV1|Se realiza una llamada desde un dispositivo móvil para crear una licencia de usuario final.|
|BEGetAllTemplatesV1|Se realiza una llamada desde un dispositivo móvil (back-end) para obtener todas las plantillas.|
|Certify|El cliente está certificando el contenido para la protección.|
|Decrypt|El cliente está intentando descifrar el contenido protegido con RMS.|
|DeleteTemplateById|Se realiza una llamada desde el Portal de Azure clásico para eliminar una plantilla por identificador de plantilla.|
|ExportTemplateById|Se realiza una llamada desde el Portal de Azure clásico para exportar una plantilla en función de un identificador de plantilla.|
|FECreateEndUserLicenseV1|Similar a la solicitud AcquireLicense pero desde dispositivos móviles.|
|FECreatePublishingLicenseV1|Lo mismo que Certify y GetClientLicensorCert combinados, desde clientes móviles.|
|FEGetAllTemplates|Se realiza una llamada desde un dispositivo móvil (front-end) para obtener las plantillas.|
|GetAllTemplates|Se realiza una llamada desde el Portal de Azure clásico para obtener todas las plantillas.|
|GetClientLicensorCert|El cliente está solicitando un certificado de publicación (que se utiliza posteriormente para proteger contenido) desde un equipo con Windows.|
|GetConfiguration|Se llama a un cmdlet de Azure PowerShell para obtener la configuración del inquilino de Azure RMS.|
|GetConnectorAuthorizations|Se realiza una llamada desde los conectores de RMS para obtener su configuración de la nube.|
|GetTenantFunctionalState|El Portal de Azure clásico está comprobando si Azure RMS está activado.|
|GetTemplateById|Se realiza una llamada desde el Portal de Azure clásico para obtener una plantilla especificando un identificador de plantilla.|
|ExportTemplateById|Se está realizando una llamada desde el Portal de Azure clásico para exportar una plantilla especificando un identificador de plantilla.|
|FindServiceLocationsForUser|Se realiza una llamada para consultar las direcciones URL, que se usan para llamar a Certify o AcquireLicense.|
|ImportTemplate|Se realiza una llamada desde el Portal de Azure clásico para importar una plantilla.|
|ServerCertify|Se realiza una llamada desde un cliente habilitado para RMS (como SharePoint) para certificar el servidor.|
|SetUsageLogFeatureState|Se realiza una llamada para habilitar el registro de uso.|
|SetUsageLogStorageAccount|Se realiza una llamada para especificar la ubicación de los registros de Azure RMS.|
|SignDigest|Se realiza una llamada cuando se usa una clave con la intención de firmar. Suele llamarse una vez por cada elemento AcquireLicence (o FECreateEndUserLicenseV1), Certify y GetClientLicensorCert (o FECreatePublishingLicenseV1).|
|UpdateTemplate|Se realiza una llamada desde el Portal de Azure clásico para actualizar una plantilla existente.|

## <a name="BKMK_PowerShell"></a>Referencia de Windows PowerShell
Use los siguientes cmdlets de Windows PowerShell como ayuda para configurar y usar el registro de uso de Azure Rights Management:

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Para obtener más información sobre el uso de Windows PowerShell para Azure Rights Management, consulte [Administración de Azure Rights Management mediante Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Vea también
[Uso de Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

