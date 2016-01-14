---
description: na
keywords: na
title: RMS Client Deployment Notes
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
---
# Notas de la implementaci&#243;n del cliente de RMS
La versión de cliente (cliente de RMS) de Rights Management Service 2 también se conoce como cliente MSIPC. Es el software para equipos Windows que se comunica con Microsoft Rights Management Services en el entorno local o en la nube para ayudar a proteger el acceso a la información que fluye a través de aplicaciones y dispositivos, y el uso de esta, dentro de los límites de su organización, o fuera de esos límites administrados. Además de incluirse con la [aplicación de uso compartido de Rights Management](https://technet.microsoft.com/library/dn919648.aspx), el cliente RMS está disponible [como descarga opcional](http://www.microsoft.com/download/details.aspx?id=38396) que, con la confirmación y la aceptación de su contrato de licencia, se puede distribuir libremente con software de terceros para que los clientes puedan proteger y consumir contenido protegido con Rights Management Services.

En este tema se incluyen las secciones siguientes:

-   [Redistribución del cliente RMS](#BKMK_RedistributeInstaller)

-   [Instalación del cliente RMS](#BKMK_InstallClient)

-   [Preguntas y respuestas sobre el cliente RMS](#BKMK_QA)

-   [Configuración del cliente RMS](#BKMK_Settings)

-   [Solo AD RMS: Limitación del cliente RMS para usar servidores de AD RMS de confianza](#BKMK_UsingTrustedServers)

-   [Detección del servicio de RMS](#BKMK_ServiceDiscovery)

## <a name="BKMK_RedistributeInstaller"></a>Redistribución del cliente RMS
El cliente RMS se puede redistribuir libremente e incluirse con otras aplicaciones y soluciones de TI. Si es un desarrollador de aplicaciones o un proveedor de soluciones y desea redistribuir el cliente RMS, tiene dos opciones:

-   Recomendado: Inserte el instalador del cliente RMS en la instalación de la aplicación y ejecútela en modo silencioso (el modificador **/quiet**, detallado en la sección siguiente).

-   Convierta el cliente RMS en un requisito previo para la aplicación. Con esta opción, tendrá que proporcionar a los usuarios instrucciones adicionales para que obtengan, instalen y actualicen sus equipos con el cliente para poder usar la aplicación.

## <a name="BKMK_InstallClient"></a>Instalación del cliente RMS
El cliente RMS está incluido en un archivo ejecutable de instalador denominado **setup_msipc_***&lt;arch&gt;***.exe**, donde *&lt;arch&gt;* es **x86** (para equipos cliente de 32 bits) o **x64** (para equipos cliente de 64 bits). El paquete del instalador de 64 bits (x 64) instala un ejecutable de tiempo de ejecución de 32 bits para la compatibilidad con las aplicaciones de 32 bits que se ejecutan en una instalación de sistema operativo de 64 bit, y un archivo ejecutable de tiempo de ejecución de 64 bits para la compatibilidad con aplicaciones nativas de 64 bits. No se ejecutará el programa de instalación de 32 bits (x 86) en una instalación de Windows de 64 bits.

> [!NOTE]
> Necesita privilegios elevados para instalar el cliente RMS, como ser miembro del grupo Administradores en el equipo local.

Puede instalar al cliente RMS mediante cualquiera de los siguientes métodos de instalación:

-   **Modo silencioso.** Mediante el uso del modificador **/quiet** como parte de las opciones de línea de comandos, puede instalar de forma silenciosa el cliente RMS en los equipos. En el ejemplo siguiente se muestra una instalación en modo silencioso del cliente RMS en un equipo cliente de 64 bits:

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **Modo interactivo.** Como alternativa, puede instalar al cliente RMS mediante el programa de instalación basado en GUI proporcionado por el Asistente para la instalación del cliente RMS. Para ello, haga doble clic en el paquete del instalador del cliente RMS (**setup_msipc_***&lt;arch&gt;***.exe**) en la carpeta en la que se copió o descargó en el equipo local.

## <a name="BKMK_QA"></a>Preguntas y respuestas sobre el cliente RMS
La siguiente sección contiene las preguntas más frecuentes sobre el cliente RMS y las respuestas a ellas.

### ¿Qué sistemas operativos son compatibles con el cliente RMS?
El cliente RMS es compatible con los siguientes sistemas operativos:

|Sistema operativo Windows Server|Sistema operativo cliente de Windows|
|------------------------------------|----------------------------------------|
|Windows Server 2012 R2|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 con SP1 como mínimo|
|Windows Server 2008 (solo AD RMS)|Windows Vista con SP 2 como mínimo (solo AD RMS)|

### ¿Qué procesadores o plataformas son compatibles con el cliente RMS?
El cliente RMS es compatible con plataformas informáticas x86 y x64.

### ¿Donde está instalado el cliente RMS?
De forma predeterminada, el cliente RMS se instala en %ProgramFiles%\Active Directory Rights Management Services Client 2.&lt;número de versión secundario&gt;.

### ¿Qué archivos están asociados con el software cliente de RMS?
Los siguientes archivos se instalan como parte del software cliente de RMS:

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

Además de estos archivos, el cliente RMS instala también archivos de compatibilidad con la interfaz de usuario multilingüe (MUI) en 44 idiomas. Para comprobar los idiomas admitidos, ejecute la instalación del cliente RMS y, una vez completada, revise el contenido de las carpetas de compatibilidad multilingüe en la ruta de acceso predeterminada.

### ¿Se incluye el cliente RMS de forma predeterminada al instalar un sistema operativo compatible?
No. Esta versión del cliente RMS se distribuye como una descarga opcional que puede instalarse por separado en equipos que ejecuten versiones compatibles del sistema operativo Microsoft Windows.

### ¿Se actualiza automáticamente el cliente RMS con Microsoft Update?
Si instaló el cliente RMS usando la opción de instalación silenciosa, este hereda la configuración actual de Microsoft Update. Si instaló el cliente RMS mediante el programa de instalación basado en GUI, el Asistente para la instalación del cliente RMS le pregunta si desea habilitar Microsoft Update.

## <a name="BKMK_Settings"></a>Configuración del cliente RMS
La siguiente sección contiene información de configuración sobre el cliente RMS. Esta información puede resultar útil si tiene problemas con aplicaciones o servicios que usan el cliente RMS.

> [!NOTE]
> Algunas opciones dependen de si la aplicación habilitada para RMS se ejecuta como una aplicación en modo cliente (como Microsoft Word y Outlook, o la aplicación de uso compartido de RMS) o una aplicación en modo servidor (por ejemplo, SharePoint y Exchange).  En las tablas siguientes, estos valores se identifican como **modo cliente** y **modo servidor**, respectivamente.

### Dónde almacena el cliente RMS las licencias en los equipos cliente
El cliente RMS almacena las licencias en el disco local y también almacena en caché alguna información en el Registro de Windows.

|Descripción|Rutas de acceso de modo cliente|Rutas de acceso de modo servidor|
|---------------|-----------------------------------|------------------------------------|
|Ubicación del almacén de licencias|%localappdata%\Microsoft\MSIPC|%allusersprofile%\Microsoft\MSIPC\Server\*&lt;SID&gt;*\|
|Ubicación del almacén de plantillas|%localappdata%\Microsoft\MSIPC\Templates|%allusersprofile%\Microsoft\MSIPC\Server\Templates\*&lt;SID&gt;*\|
|Ubicación del Registro|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local Settings<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*&lt;SID&gt;*|
> [!NOTE]
> *&lt;SID&gt;* es el identificador de seguridad (SID) de la cuenta con la que se ejecuta la aplicación de servidor. Por ejemplo, si la aplicación se ejecuta con la cuenta integrada de Servicio de red, reemplace *&lt;SID&gt;* por el valor del SID conocido de esa cuenta (S-1-5-20).

### Configuración del Registro de Windows para el cliente RMS
Puede usar las claves del Registro de Windows para establecer o modificar algunas configuraciones del cliente RMS. Por ejemplo, como administrador de aplicaciones habilitadas para RMS que se comunican con servidores de AD RMS, podría actualizar la ubicación de servicio empresarial (reemplazar el servidor de AD RMS seleccionado actualmente para publicación) en función de la ubicación actual del equipo cliente dentro de la topología de Active Directory. O bien, podría habilitar el seguimiento de RMS en el equipo cliente, para ayudar a solucionar un problema con una aplicación habilitada para RMS. Use la tabla siguiente para identificar la configuración del Registro que puede cambiar para el cliente RMS.

|Tarea|Configuración|
|---------|-----------------|
|Solo AD RMS: Para actualizar la ubicación del servicio de empresa para un equipo cliente|Actualice las siguientes claves del Registro:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />    REG_SZ: default<br />    **Valor:**&lt;http o https&gt;:// *RMS_Cluster_Name*/_wmcs/Certification<br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />    REG_SZ: default<br />    **Valor:** &lt;http o https&gt;:// *RMS_Cluster_Name*/_wmcs/Licensing|
|Para habilitar y deshabilitar el seguimiento|Actualice la siguiente clave del Registro:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />    REG_DWORD: Trace<br />    **Valor:** 1 para habilitar el seguimiento, 0 para deshabilitar el seguimiento (valor predeterminado)|
|Para cambiar la frecuencia en días de actualización de las plantillas|Los siguientes valores del Registro especifican la frecuencia con que se actualizan las plantillas en el equipo del usuario si no se establece el valor TemplateUpdateFrequencyInSeconds.  Si ninguno de estos valores se establecen, el intervalo de actualización predeterminado para las aplicaciones que usan el cliente RMS (versión 1.0.1784.0) para descargar las plantillas es de 1 día. Las versiones anteriores a esta tienen un valor predeterminado de cada 7 días.<br /><br />**Modo cliente:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Valor:** Valor entero que especifica el número de días (mínimo de 1) entre descargas.<br /><br />**Modo servidor:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt;SID&gt;*<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Valor:** Valor entero que especifica el número de días (mínimo de 1) entre descargas.|
|Para cambiar la frecuencia en segundos de actualización de las plantillas **Important:** Si se especifica, se omite el valor para actualizar la frecuencia de las plantillas en días. Especifique una o la otra, no ambas.|Los siguientes valores del Registro especifican la frecuencia con que se actualizan las plantillas en el equipo del usuario. Si este valor, o el valor para cambiar la frecuencia en días (TemplateUpdateFrequency) no se establece, el intervalo de actualización predeterminado para las aplicaciones que usan el cliente RMS (versión 1.0.1784.0) para descargar las plantillas es de 1 día. Las versiones anteriores a esta tienen un valor predeterminado de cada 7 días.<br /><br />**Modo cliente:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Valor:** Valor entero que especifica el número de segundos (mínimo de 1) entre descargas.<br /><br />**Modo servidor:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt;SID&gt;*<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Valor:** Valor entero que especifica el número de segundos (mínimo de 1) entre descargas.|
|Solo AD RMS: Para descargar plantillas de inmediato en la siguiente solicitud de publicación|Durante las pruebas y evaluaciones, puede usar el cliente RMS para descargar plantillas lo antes posible. Para ello, quite la siguiente clave del Registro y el cliente RMS descargará las plantillas inmediatamente en la siguiente solicitud de publicación en lugar de esperar el tiempo especificado por el valor del Registro TemplateUpdateFrequency:<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\&lt;Server Name&gt;\Template **Note:** &lt;Server Name&gt; podría tener URL externas (corprights.contoso.com) e internas (corprights) y, por lo tanto, dos entradas diferentes.|
|Solo AD RMS: Para habilitar la compatibilidad con la autenticación federada|Si el equipo cliente RMS se conecta a un clúster de AD RMS mediante una confianza federada, debe configurar el dominio de inicio de la federación.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_SZ: FederationHomeRealm<br />    **Valor:** El valor de esta entrada del Registro es el identificador uniforme de recursos (URI) para el servicio de federación (por ejemplo, "https://fs-01.contoso.com").|
|Solo AD RMS: Para admitir servidores de federación asociados que requieren autenticación basada en formularios para la entrada de usuario|De forma predeterminada, el cliente RMS funciona en modo silencioso y no es necesaria la intervención del usuario. Los servidores de federación asociados, sin embargo, pueden configurarse para requerir la entrada del usuario, como la autenticación basada en formularios. En este caso, debe configurar el modo silencioso para omitir al cliente RMS, de modo que el formulario de autenticación federado aparezca en una ventana del explorador y se promueva la autenticación del usuario.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_DWORD: EnableBrowser **Note:** Si el servidor de federación está configurado para usar la autenticación basada en formularios, esta clave es obligatoria. Si el servidor de federación está configurado para usar la autenticación integrada de Windows, esta clave no es obligatoria.|
|Solo AD RMS: Para bloquear el consumo del servicio ILS|De forma predeterminada, el cliente RMS permite el consumo de contenido protegido por el servicio ILS, pero puede configurar el cliente para bloquear este servicio mediante la configuración de la siguiente clave del Registro. Si esta clave del Registro se configura para bloquear el servicio ILS, cualquier intento de abrir y consumir contenido protegido por el servicio ILS devolverá el siguiente error:<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: **DisablePassportCertification**<br />    **Valor:** 1 para bloquear el consumo de ILS, 0 para permitir el consumo de ILS (valor predeterminado)|

### Administración de la distribución de plantillas para el cliente RMS
Las plantillas facilitan a los usuarios y administradores la aplicación de protección de Rights Management rápidamente y el cliente RMS descarga automáticamente las plantillas de sus servidores o del servicio de RMS. Si coloca las plantillas en la siguiente ubicación de carpeta, el cliente RMS no descarga ninguna plantilla de su ubicación predeterminada sino que, en su lugar, descarga las plantillas que ha colocado en esta carpeta. El cliente RMS puede seguir descargando plantillas de otros servidores RMS disponibles.

**Modo cliente:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Modo servidor:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\*&lt;SID&gt;*

Cuando use esta carpeta, no hay ninguna convención de nomenclatura especial necesaria, excepto que las plantillas debe emitirlas el servidor o servicio RMS y que deben tener la extensión de nombre de archivo .xml. Por ejemplo, Contoso-Confidential.xml o Contoso-ReadOnly.xml son nombres válidos.

## <a name="BKMK_UsingTrustedServers"></a>Solo AD RMS: Limitación del cliente RMS para usar servidores de AD RMS de confianza
El cliente RMS se puede limitar a usar únicamente servidores de AD RMS de confianza específicos si se realizan los siguientes cambios en el Registro de Windows en los equipos locales.

**Para habilitar la limitación del cliente RMS al uso exclusivo de servidores de AD RMS de confianza**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD: AllowTrustedServersOnly

    **Valor:** Si se especifica un valor distinto de cero, el cliente RMS confiará únicamente en los servidores especificados que están configurados en la lista TrustedServers y el servicio de Azure Rights Management.

**Para agregar a miembros a la lista de servidores de AD RMS de confianza**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ: *&lt;URL_or_HostName&gt;*

    **Valor:** Los valores de cadena que agregó en esta ubicación de la clave del Registro pueden tener un formato de nombre de dominio DNS (por ejemplo, **adrms.contoso.com**) o URL completas a servidores de AD RMS de confianza (por ejemplo, **https://adrms.contoso.com**). Si una URL especificada comienza con **https://**,  el cliente RMS usará SSL o TLS para ponerse en contacto con el servidor de AD RMS especificado.

## <a name="BKMK_ServiceDiscovery"></a>Detección del servicio de RMS
La detección del servicio de RMS permite al cliente RMS comprobar con qué servicio o servidor de RMS se comunica antes de proteger el contenido. La detección de servicios también puede producirse cuando el cliente RMS consume contenido protegido, pero esta situación es menos frecuente porque la directiva asociada al contenido contiene el servidor o servicio de RMS preferido, y solo si estos no tienen éxito, el cliente ejecutará la detección de servicios.

La detección de servicios busca primero una versión local de Rights Management (AD RMS). Si no tiene éxito, la detección de servicios busca automáticamente la versión de la nube de Rights Management (Azure RMS).

Para realizar la detección de servicios para una implementación local, el cliente RMS comprueba lo siguiente:

1.  El Registro de Windows en el equipo local: Si la configuración de detección de servicios está configurada en el Registro, primero se intenta esta configuración.  De forma predeterminada, esta configuración no se configura en el Registro.

2.  Servicios de dominio de Active Directory: Un equipo unido al dominio consulta Active Directory para ver si existe un punto de conexión de servicio (SCP). Si un SCP está registrado, se devuelve la URL del servidor de RMS para que la use el cliente RMS.

### Solo AD RMS: Habilitación de la detección de servicios de servidor mediante Active Directory
Si la cuenta tiene privilegios suficientes (administradores de empresa y administrador local para el servidor de AD RMS), puede registrar automáticamente un punto de conexión de servicio (SCP) al instalar el servidor de clúster raíz de AD RMS. Si ya existe un SCP en el bosque, debe eliminarlo primero antes de registrar uno nuevo.

Puede registrar y eliminar un SCP después de instalar AD RMS mediante el procedimiento siguiente. Antes de comenzar, asegúrese de que su cuenta disponga de los privilegios necesarios (administrador de empresa y administrador local para el servidor de AD RMS).

##### Para habilitar la detección de servicios de AD RMS mediante el registro de un SCP en Active Directory

1.  Abra la consola de servicios de administración de Active Directory en el servidor de AD RMS:

    -   Si usa Windows Server 2008 R2 o Windows Server 2008, haga clic en **Inicio**, **Herramientas administrativas** y, luego, en **Active Directory Rights Management Services**.

    -   Si usa Windows Server 2012 R2 o Windows Server 2012, haga clic en **Herramientas** y, luego, en **Active Directory Rights Management Services**.

2.  En la consola de AD RMS, haga clic con el botón derecho e el clúster de AD RMS y, luego, haga clic en **Propiedades**.

3.  Haga clic en la pestaña **SCP**.

4.  Active la casilla **Cambiar SCP**.

5.  Seleccione la opción **Establecer SCP en el clúster de certificación actual** y,luego, haga clic en **Aceptar**.

### Habilitación de la detección de servicios del cliente con el Registro de Windows
Como alternativa al uso de un SCP o en aquellos casos en los que no exista uno, puede configurar el Registro en el equipo cliente para que el cliente RMS pueda encontrar su servidor de AD RMS.

##### Para habilitar la detección de servicios de AD RMS en el cliente mediante el Registro de Windows

1.  Abra el Editor del Registro de Windows, Regedit.exe:

    -   En el equipo cliente, en la ventana Ejecutar, escriba **regedit** y, luego, presione ENTRAR para abrir el Editor del Registro.

2.  En el Editor del Registro, desplácese hasta **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!IMPORTANT]
    > Si está ejecutando una aplicación de 32 bits en un equipo de 64 bits, la ruta de acceso será la siguiente: 
    > **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  Para crear la subclave ServiceLocation, haga clic en **MSIPC**, seleccione **Nuevo**, haga clic en **Clave** y, luego, escriba **ServiceLocation**.

4.  Para crear la subclave EnterpriseCertification, haga clic en **MSIPC**, seleccione **Nuevo**, haga clic en **Clave** y, luego, escriba **EnterpriseCertification**.

5.  Para establecer la dirección URL de certificación de empresa, haga doble clic en el valor **(Predeterminado)**, en la subclave **EnterpriseCertification** y, cuando aparezca el cuadro de diálogo **Editar cadena**, en **Información del valor**, escriba &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Certification y, luego, haga clic en **Aceptar**.

6.  Para crear la subclave EnterprisePublishing, haga clic con el botón derecho en **ServiceLocation**, seleccione **Nuevo**, haga clic en **Clave** y, luego, escriba EnterprisePublishing.

7.  Para configurar la URL de publicación de empresa, haga doble clic en **(Predeterminado)**, en la subclave **EnterprisePublishing**, y cuando aparezca el cuadro de diálogo **Editar cadena**, escriba en **Información del valor** lo siguiente &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Licensing y, luego, haga clic en **Aceptar**.

8.  Cierre el Editor del Registro.

Si el cliente RMS no puede encontrar un SCP al consultar Active Directory y no se especifica en el Registro, las llamadas de detección de servicios de AD RMS darán error.

### Redirección del tráfico del servidor de licencias
En algunos casos, deberá redirigir el tráfico durante la detección de servicios, por ejemplo, cuando se combinan dos organizaciones y el servidor de licencias antiguo de una organización se retira, se debe redirigir a los clientes a un nuevo servidor de licencias. O bien, migre de AD RMS a Azure RMS. Para habilitar la redirección de las licencias, use el procedimiento siguiente.

##### Para habilitar la redirección de licencias de RMS mediante el Registro de Windows

1.  Abra el Editor del Registro de Windows, Regedit.exe:

    -   En el equipo cliente, en la ventana Ejecutar, escriba **regedit** y, luego, presione ENTRAR para abrir el Editor del Registro.

2.  En el Editor del Registro, desplácese a una de las subclaves siguientes:

    -   Para la versión de 64 bits de Office en una plataforma x64: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   Para la versión de 32 bits de Office en una plataforma x64: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Cree una subclave LicensingRedirection; para ello, haga clic con el botón derecho en **Servicelocation**, seleccione **Nuevo**, haga clic en **Clave** y, luego, escriba **LicensingRedirection**.

4.  Para establecer la redirección de licencia, haga clic en la subclave **LicensingRedirection**, seleccione **Nuevo** y, luego, seleccione **Valor de cadena**.  En **Nombre**, especifique la URL del servidor de licencias anterior, y en **Valor**, especifique la URL del nuevo servidor de licencias.

    Por ejemplo, para redirigir las licencias de un servidor en Contoso.com a uno en Fabrikam.com, puede escribir los valores siguientes:

    **Nombre:** `https://contoso.com/_wmcs/licensing`

    **Valor:** `https://fabrikam.com/_wmcs/licensing`

    > [!NOTE]
    > Si el servidor de licencias anterior tiene especificadas direcciones de intranet y extranet, se debe definir una nueva asignación de nombre y valor para ambas URL en la clave LicensingRedirection.

5.  Repita el paso anterior para todos los servidores que deben redirigirse.

6.  Cierre el Editor del Registro.

