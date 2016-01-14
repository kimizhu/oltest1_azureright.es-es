---
description: na
keywords: na
title: Rights Management sharing application administrator guide
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
---
# Gu&#237;a de administrador de la aplicaci&#243;n de uso compartido Rights Management
Use la siguiente información si es responsable de la aplicación Microsoft Rights Management sharing en una red de empresa, o si desea más información técnica que la que aparece en [Guía de usuario de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_user_guide.md) o en [Preguntas frecuentes sobre la aplicación Microsoft Rights Management sharing para Windows](http://go.microsoft.com/fwlink/?LinkId=303971):

-   [Implementación automática de la aplicación Microsoft Rights Management sharing](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ScriptedInstall)

    -   [Comprobación de que la instalación se ha realizado correctamente](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)

    -   [Comandos de desinstalación](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_uninstallscripted)

    -   [Supresión de actualizaciones automáticas](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SuppressAutomaticUpdates)

    -   [Solo Azure RMS: configuración del seguimiento de documentos](#BKMK_DocumentTracking)

    -   [Solo AD RMS: Compatibilidad con varios dominios de correo electrónico dentro de su organización](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains)

-   [Información general técnica de la aplicación Microsoft Rights Management sharing](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_AdminOverview)

    -   [Niveles de protección: nativo y genérico](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection)

    -   [Tipos de archivo y extensiones de nombre de archivo admitidos](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes)

    -   [Cambio del nivel de protección predeterminado de los archivos](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection)

> [!TIP]
> Si está familiarizado con la aplicación RMS sharing o desea obtener más información, consulte [Cómo RMS protege todos los tipos de archivo mediante la aplicación RMS sharing](https://curah.microsoft.com/191031/how-rms-protects-all-file-types-by-using-the-rms-sharing-app).

La aplicación RMS resulta más adecuada para trabajar con Azure RMS, puesto que esta configuración de implementación admite el envío de datos adjuntos protegidos a los usuarios de otra organización, así como opciones tales como notificaciones por correo electrónico y seguimiento de documentos con revocación.  Sin embargo, también funciona con la versión local, AD RMS, pero con algunas limitaciones. Para obtener una comparación exhaustiva de las características que son compatibles con Azure RMS y AD RMS, consulte [Comparación de Azure Rights Management y AD RMS](https://technet.microsoft.com/library/jj739831.aspx). Si tiene AD RMS y quiere migrar a Azure RMS, consulte [Migración de AD RMS a Azure Rights Management](https://technet.microsoft.com/library/dn858447.aspx).

## <a name="BKMK_ScriptedInstall"></a>Implementación automática de la aplicación Microsoft Rights Management sharing
La versión de Windows de la aplicación RMS sharing admite una instalación con scripts, lo que la convierte en adecuada para las implementaciones empresariales.

Los únicos requisitos previos para las instalaciones son que los equipos ejecuten una versión mínima de Windows 7 Service Pack 1 y que esté instalado Microsoft Framework, versión mínima 4.0. Si necesita instalar Microsoft .NET Framework 4.0, puede [descargarlo para la instalación desde el Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=17718).

#### Para descargar la aplicación RMS sharing para la implementación automática

1.  Vaya a la página [Aplicación Microsoft Rights Management sharing para Windows](http://www.microsoft.com/download/details.aspx?id=40857) en el Centro de descarga de Microsoft y haga clic en **Descargar**.

2.  Seleccione y descargue los archivos que necesita. Hay dos paquetes de instalación de cliente: uno para Windows de 64 bits (Microsoft Rights Management sharing application x64.zip) y otro para Windows de 32 bits (Microsoft Rights Management sharing application x86.zip).

3.  Extraiga los archivos de los paquetes de instalación comprimidos haciendo doble clic en ellos, por ejemplo. A continuación, copie los archivos extraídos en una ubicación de red a la que puedan tener acceso los equipos cliente.

Los paquetes de instalación de la aplicación RMS sharing admiten distintos escenarios de implementación e incluyen lo siguiente:

|Descripción|Escenario de implementación|
|---------------|-------------------------------|
|Ayudante para el inicio de sesión en línea de Microsoft|Necesario para lo siguiente:<br /><br />-   Office 2010 y Azure RMS<br />-   Office 2013 y Azure RMS si no ha instalado la [actualización del 9 de junio de 2015 para Office 2013](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Revisión para Office (KB 2596501)|Necesario para lo siguiente:<br /><br />-   Office 2010 y Azure RMS<br />-   Office 2010 y Active Directory RMS|
|Revisión para permitir que el cliente de AD RMS 1.0 funcione con Azure RMS (KB 2843630 KB)|Necesario para lo siguiente:<br /><br />-   Office 2010 y Azure RMS<br />-   Office 2010 y Active Directory RMS|
|El cliente de AD RMS y la aplicación RMS sharing|Necesario para lo siguiente:<br /><br />-   Office 2016 u Office 2013 y Azure RMS o Active Directory RMS<br />-   Office 2010 y Azure RMS<br />-   Office 2010 y Active Directory RMS<br />-   Aplicación RMS sharing y solo el complemento de Office|
|Complemento de Office de la cinta de opciones|Necesario para lo siguiente:<br /><br />-   Office 2016 u Office 2013 y Azure RMS o Active Directory RMS<br />-   Office 2010 y Azure RMS<br />-   Office 2010 y Active Directory RMS<br />-   Aplicación RMS sharing y solo el complemento de Office|
|Herramienta de preparación de Azure Active Directory Rights Management|Necesario para lo siguiente:<br /><br />-   Office 2010 y Azure RMS|
Use los siguientes procedimientos para identificar los comandos necesarios para implementar la aplicación RMS sharing en estos escenarios de implementación:

-   **Office 2016 u Office 2013 y Azure RMS o Active Directory RMS**

    Los usuarios ejecutan Office 2016 u Office 2013, su organización usa Azure RMS o Active Directory RMS y los usuarios colaborar con otras organizaciones que usan Azure RMS o Active Directory RMS.

-   **Office 2010 y Azure RMS**

    Los usuarios ejecutan Office 2010, su organización usa Azure RMS o Active Directory RMS y los usuarios colaboran con otras organizaciones que usan Azure RMS o Active Directory RMS.

-   **Office 2010 y Active Directory RMS**

    Los usuarios ejecutan Office 2010, su organización usa Azure RMS o Active Directory RMS y los usuarios colaboran con otras organizaciones que usan Azure RMS o Active Directory RMS.

-   **Aplicación RMS sharing y solo el complemento de Office**

    Los usuarios ejecutan Office 2016, Office 2013 u Office 2010, su organización usa Azure RMS o Active Directory RMS y los usuarios no necesitan colaboran con otras organizaciones que usan Azure RMS. Esta instalación le permite instalar solamente la aplicación de uso compartido y el complemento de Office.

> [!NOTE]
> En estos casos, si su organización ejecuta AD RMS, los usuarios pueden recibir contenido protegido de otras organizaciones que usan Azure RMS, pero los usuarios no pueden enviar contenido protegido a los usuarios de una organización que usa Azure RMS. Sin embargo, si su organización ejecuta Azure RMS, los usuarios pueden enviar y recibir contenido protegido de otras organizaciones.

Para completar la instalación de cada procedimiento, debe reiniciar el equipo. Puede iniciar un reinicio automático mediante un comando como shutdown /i.

#### Para implementar la aplicación RMS sharing para Office 2016 u Office 2013 y Azure RMS o Active Directory RMS

-   En cada equipo en el que quiera instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando con privilegios elevados:

    ```
    setup.exe /s
    ```

Para comprobar que se ejecuta correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) de este tema.

#### Para implementar la aplicación RMS sharing para Office 2010 y Azure RMS

1.  Debe ser el administrador global del inquilino de Office 365 o Azure Active Directory para poder obtener la dirección URL del servicio de certificación de su organización mediante la ejecución de la herramienta de preparación Azure Active Directory Rights Management. Debe ejecutar esta herramienta solo una vez, en un único equipo. Usará la dirección URL del servicio de certificación al instalar la aplicación RMS sharing en cada equipo:

    1.  Inicie sesión un equipo con una cuenta de administrador local.

    2.  En ese equipo, [descargue e instale el Ayudante para el inicio de sesión de Microsoft Online](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Ejecute el siguiente comando para mostrar en la pantalla la dirección URL del servicio de certificación, que luego puede copiar y guardar para el siguiente paso:

        -   Para Windows 8.1 y Windows 8, 64 bits:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para Windows 8.1 y Windows 8, 64 bits:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para Windows 7, 64 bits:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Este comando podría solicitarle que especifique sus credenciales de Azure. Si el equipo no está unido a un dominio, se le pedirán. Si el equipo está unido a un dominio, es posible que la herramienta pueda usar las credenciales almacenadas en caché.

2.  En cada equipo en el que vaya a instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando con privilegios elevados:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  En cada equipo en el que vaya a instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando (no necesita privilegios elevados). Esto se puede hacer de diferentes maneras, como por ejemplo, pedir al usuario que ejecute el comando (desde un vínculo en un mensaje de correo electrónico o un vínculo en el portal del servicio de asistencia), o bien puede agregarlo a su script de inicio de sesión:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

Para comprobar que se ejecuta correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) de este tema.

#### Para implementar la aplicación RMS sharing para Office 2010 y Active Directory RMS

1.  En cada equipo en el que vaya a instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando con privilegios elevados:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  En cada equipo en el que vaya a instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando (no necesita privilegios elevados). Esto se puede hacer de diferentes maneras, como por ejemplo, pedir al usuario que ejecute el comando (desde un vínculo en un mensaje de correo electrónico o un vínculo en el portal del servicio de asistencia), o bien puede agregarlo a su script de inicio de sesión:

    -   Para Windows 10, Windows 8.1 y Windows 8, 64 bits:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Para Windows 10, Windows 8.1 y Windows 8, 32 bits:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Para Windows 7, 64 bits:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

Para comprobar que se ejecuta correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) de este tema.

#### Para instalar la aplicación RMS sharing y solo el complemento de Office

1.  Instale el cliente de AD RMS y la aplicación RMS sharing mediante el siguiente comando:

    -   Para Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   Para Windows de 32 bits:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Por ejemplo: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Instale el complemento de Office mediante los siguientes comandos:

    -   Para la versión de Office de 64 bits:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   Para la versión de Office de 32 bits:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    Por ejemplo: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

Para comprobar que se ejecuta correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) de este tema.

### <a name="BKMK_verifyscripted"></a>Comprobación de que la instalación se ha realizado correctamente
Puede usar los archivos de registro de instalación para comprobar si la instalación se realizó correctamente.

##### Para comprobar que la instalación de la aplicación RMS sharing para Office 2016 u Office 2013 y Azure RMS o Active Directory RMS se ha realizado correctamente

-   Para comprobar que el comando Setup.exe se ha ejecutado correctamente, busque en cada equipo el archivo de registro de instalación **RMInstaller.log** en la carpeta *%temp%\RMS_installer_&lt;guid&gt;* y, luego, identifique el código de salida.

    Una instalación correcta tiene un código de salida de 0 y cualquier otro número indica un error en la instalación.

    Nombre de archivo de registro de ejemplo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

##### Para comprobar que la instalación de la aplicación RMS sharing para Office 2010 y Azure RMS se ha realizado correctamente

1.  Para comprobar que el comando Setup.exe se ha ejecutado correctamente, busque en cada equipo el archivo de registro de instalación **RMInstaller.log** en la carpeta *%temp%\RMS_installer_&lt;guid&gt;* y, luego, identifique el código de salida.

    Una instalación correcta tiene un código de salida de 0 y cualquier otro número indica un error en la instalación.

    Nombre de archivo de registro de ejemplo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para comprobar que el comando RMSSetup.exe se ha ejecutado correctamente, el usuario debe tener los siguientes archivos creados en su carpeta *%localappdata%\microsoft\drm*:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    Ejemplo de un archivo CLC-&#42;.drm:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

##### Para comprobar que la instalación de la aplicación RMS sharing para Office 2010 y Active Directory RMS se ha realizado correctamente

1.  Para comprobar que el comando Setup.exe se ha ejecutado correctamente, busque en cada equipo el archivo de registro de instalación en la carpeta *%temp%\RMS_installer_&lt;guid&gt;* e identifique el código de salida.

    Una instalación correcta tiene un código de salida de 0 y cualquier otro número indica un error en la instalación.

    Nombre de archivo de registro de ejemplo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para comprobar que el comando aadrmprep.exe se ha ejecutado correctamente, busque en cada equipo el siguiente texto en el archivo de registro de instalación: **aadrmprep.exe exited with status SUCCESS**

    > [!NOTE]
    > En ocasiones, la instalación puede ejecutarse dos veces; la primera vez resulta incorrecta y la segunda correcta.

    Si quiere comprobar manualmente los cambios que realiza esta herramienta en el Registro, son estos:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

##### Para comprobar que la instalación de la aplicación RMS sharing y solo el complemento de Office se ha realizado correctamente

1.  Para comprobar que el comando Setup_ipviewer.exe se ha ejecutado correctamente, busque el siguiente texto en el archivo de registro de instalación: **Installation success or error status: 0**

    Líneas de ejemplo de una instalación correcta:

    **MSI (s) (F0:B8) [14:19:57:854]: Product: Active Directory Rights Management Services Client 2.1 -- Installation completed successfully.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer installed the product. Product Name: Active Directory Rights Management Services Client 2.1. Product Version: 1.0.1179.1. Product Language: 1033. Fabricante: Microsoft Corporation Resultado de la instalación: 0.**

2.  Para comprobar que el complemento de Office se ha instalado correctamente, busque el siguiente texto en el archivo de registro de instalación: **Installation success or error status: 0**

    Líneas de ejemplo de una instalación correcta:

    **MSI (s) (9C:88) [18:49:04:007]: Product: Microsoft RMS Office Addins -- Installation completed successfully.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer installed the product. Product Name: Microsoft RMS Office Addins. Product Version: 1.0.7. Product Language: 1033. Fabricante: Microsoft. Installation success or error status: 0.**

### <a name="BKMK_uninstallscripted"></a>Comandos de desinstalación
No todos los comandos de instalación necesarios para estas implementaciones admiten un comando de desinstalación. Puede desinstalar el cliente de AD RMS y la aplicación de uso compartido, y puede desinstalar el complemento de Office. Use los siguientes comandos para desinstalar estos elementos.

##### Para desinstalar el cliente de AD RMS y la aplicación RMS sharing

-   Use los siguientes comandos:

    -   Para Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   Para Windows de 32 bits:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

##### Para desinstalar el complemento de Office

-   Use los siguientes comandos:

    -   Para la versión de Office de 64 bits:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   Para la versión de Office de 32 bits:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

### <a name="BKMK_SuppressAutomaticUpdates"></a>Supresión de actualizaciones automáticas
De forma predeterminada, los usuarios reciben una notificación si hay una versión posterior de la aplicación RMS sharing y se les pide que la descarguen. Puede suprimir esta notificación realizando el siguiente cambio en el Registro:

1.  Vaya a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** y, si no aparece ya ahí, cree una nueva clave denominada **RmsSharingApp**.

2.  Seleccione **RmsSharingApp**, cree un nuevo valor DWORD de **AllowUpdatePrompt** y establezca el valor en **0**.

Dado que la aplicación RMS sharing no es compatible con WSUS, puede usar la siguiente técnica para probar las nuevas versiones de dicha aplicación antes de implementarla para todos los usuarios:

1.  En los equipos de todos los usuarios, ejecute un script para suprimir las actualizaciones automáticas. En los equipos que usan los administradores para probar nuevas versiones, no ejecute este script.

2.  Cuando hay disponible una nueva versión, los administradores la descargan y la prueban.

3.  Cuando la prueba está completa y los posibles problemas se han resuelto, implemente la versión más reciente para todos los usuarios mediante las instrucciones de implementación automática de esta guía.

### <a name="BKMK_DocumentTracking"></a>Solo Azure RMS: configuración del seguimiento de documentos
Si tiene una [suscripción que admite el seguimiento de documentos](https://technet.microsoft.com/en-us/dn858608), el sitio de seguimiento de documentos está habilitado de forma predeterminada para todos los usuarios de su organización.  El seguimiento de documentos mostrará información, como las direcciones de correo electrónico de las personas que intentaron acceder a documentos protegidos que los usuarios compartieron, cuándo estas personas intentaron obtener acceso a ellos y su ubicación. Si mostrar esta información en su organización está prohibido debido a los requisitos de privacidad, puede deshabilitar el acceso al sitio de seguimiento de documentos mediante el cmdlet [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). Puede volver a habilitar el acceso al sitio en cualquier momento, mediante el uso de [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), y puede comprobar si acceso está actualmente habilitado o deshabilitado mediante [Get AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

 Para ejecutar estos cmdlets, debe tener como mínimo la versión **2.3.0.0** del módulo Azure RMS para Windows PowerShell.  Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx).

> [!TIP]
> Si anteriormente descargó e instaló el módulo, compruebe el número de versión ejecutando: `(Get-Module aadrm –ListAvailable).Version`

Las direcciones URL siguientes se usan para el seguimiento de documentos y se deben permitir (por ejemplo, agregarlas a sus sitios de confianza si está usando Internet Explorer con seguridad mejorada):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > Esta dirección URL es para mapas de Bing.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### <a name="BKMK_FederatedDomains"></a>Solo AD RMS: Compatibilidad con varios dominios de correo electrónico dentro de su organización
Si usa AD RMS y los usuarios de su organización tienen varios dominios de correo electrónico, quizás como resultado de una fusión o adquisición, debe realizar la siguiente modificación en el Registro:

1.  Vaya a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** y, si no aparece ya ahí, cree una nueva clave denominada **RmsSharingApp**.

2.  Seleccione **RmsSharingApp**, cree un nuevo valor de cadena múltiple denominado **FederatedDomains** y, luego, agregue los dominios y todos los subdominios que usa la organización. No se admiten caracteres comodín.

    Por ejemplo: La compañía Coho Vineyard &amp; Winery tiene un dominio de correo electrónico estándar de **cohovineyardandwinery.com**, pero como resultado de fusiones, también usan los dominios de correo electrónico **cohowinery.com**, **eastcoast.cohowinery.com** y **cohovineyard**. Para los datos de valor **FederatedDomains**, el administrador escribe: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Si no realiza este cambio en el Registro, los usuarios no podrán consumir contenido que han protegido otros usuarios de su organización. Esta modificación del Registro no es necesaria si usa Azure RMS.

## <a name="BKMK_AdminOverview"></a>Información general técnica de la aplicación Microsoft Rights Management sharing
La aplicación Microsoft Rights Management sharing es una aplicación opcional descargable para Microsoft Windows y otras plataformas, que ofrece lo siguiente:

-   Protección de un solo archivo o protección masiva de varios archivos, así como de todos los archivos dentro de una carpeta seleccionada.

-   Compatibilidad completa con la protección de cualquier tipo de archivo y un visor integrado para los tipos de archivo de texto e imagen usados más comúnmente.

-   Protección genérica para los archivos que no admiten la protección de RMS.

-   Interoperabilidad completa con los archivos protegidos mediante Office Information Rights Management (IRM).

-   Interoperabilidad completa con archivos PDF protegidos con SharePoint, FCI y herramientas de creación de PDF admitidas.

La aplicación Microsoft Rights Management sharing usa el nuevo [tiempo de ejecución del cliente de AD RMS 2.1](http://www.microsoft.com/download/details.aspx?id=38396). Mediante el uso de la funcionalidad de AD RMS 2.1, la aplicación Microsoft Rights Management sharing proporciona a los usuarios finales una experiencia sencilla de protección y el consumo.

Con la versión de RMS del 13 de octubre de 2013, puede proteger documentos de forma nativa mediante Office 2010 y enviarlos a personas de otra compañía, quienes pueden consumirlos entonces con Azure RMS. Además, con esta versión, si usa AD RMS en modo criptográfico 2, puede usar RMS para individuos y consumir contenido de personas de otra compañía que use Azure RMS. Para obtener más información sobre el modo criptográfico 2, consulte [Modos criptográficos de AD RMS](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

### <a name="BKMK_LevelsofProtection"></a>Niveles de protección: nativo y genérico
La aplicación Microsoft Rights Management sharing admite la protección en dos niveles distintos, como se describe en la tabla siguiente.

|Tipo de protección|Nativa|Genérico|
|----------------------|----------|------------|
|Descripción|Para archivos de texto, imagen, Microsoft Office (Word, Excel, PowerPoint), archivos .pdf y otros tipos de archivo de aplicaciones compatibles con AD RMS, la protección nativa ofrece un fuerte nivel de protección que incluye tanto cifrado como aplicación de derechos (permisos).|Para todas las demás aplicaciones y tipos de archivo, la protección genérica proporciona un nivel de protección que incluye encapsulación de archivos mediante el tipo de archivo .pfile, y autenticación para comprobar si un usuario está autorizado para abrir el archivo.|
|Protección|Los archivos están completamente cifrados y la protección se aplica de las siguientes maneras:<br /><br />-   Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que reciben el archivo por correo electrónico o que se les concede acceso a él mediante permisos de archivo o recurso compartido.<br />-   Además, cuando el contenido se presenta en el Visor de IP (en el caso de archivos de texto e imagen protegidos) o en la aplicación asociada (en el caso de todos los demás tipos de archivo admitidos), se aplican completamente los derechos de uso y le directiva definida por el propietario del contenido cuando se protegen los archivos.|La protección de los archivos se aplica de las siguientes formas:<br /><br />-   Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que están autorizadas para abrir el archivo o que se les proporciona acceso a él. Si la autorización da error, el archivo no se abre.<br />-   Se muestran los derechos de uso y la directiva establecida por el propietario del contenido para informar a los usuarios autorizados de la directiva de uso previsto.<br />-   Tiene lugar el registro de auditoría de los usuarios autorizados a abrir y obtener acceso a los archivos; sin embargo, no se aplican derechos de uso por parte de las aplicaciones no admitidas.|
|Valor predeterminado para tipos de archivo|Es el nivel predeterminado de protección para los siguientes tipos de archivo:<br /><br />-   Archivos de texto e imagen<br />-   Archivos de Microsoft Office (Word, Excel, PowerPoint)<br />-   Formato de documento portátil (.pdf)<br /><br />Para obtener más información, consulte la sección siguiente, [Tipos de archivo y extensiones de nombre de archivo admitidos](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes).|Se trata de la protección predeterminada para todos los demás tipos de archivo (por ejemplo, .vsdx, .rtf etc.) que no son compatibles con la protección completa.|
Puede cambiar el nivel de protección predeterminado que aplica la aplicación RMS sharing. Puede cambiar el nivel predeterminado de nativo a genérico, de genérico a nativo, e incluso impedir que la aplicación RMS sharing aplique protección. Para obtener más información, consulte la sección [Cambio del nivel de protección predeterminado de los archivos](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection) de este tema.

### <a name="BKMK_SupportFileTypes"></a>Tipos de archivo y extensiones de nombre de archivo admitidos
En la tabla siguiente se enumeran los tipos de archivo que admite de forma nativa la aplicación Microsoft Rights Management sharing. En estos tipos de archivo, la extensión de nombre de archivo original se cambia cuando se aplica el archivo nativo protegido, y estos archivos se vuelven de solo lectura.

Además, cuando la aplicación RMS sharing protege de forma nativa un archivo de Word, Excel o PowerPoint que protegen los usuarios mediante uso compartido, esta acción crea automáticamente un segundo archivo que es una copia del original con el mismo nombre pero con una extensión **.ppdf**¹. Esta versión del archivo garantiza que los destinatarios que instalan la aplicación RMS sharing siempre pueden abrir el archivo al que se le ha aplicado protección nativa.

En el caso de los archivos que están protegidos de manera genérica, la extensión del nombre de archivo original siempre se cambia a .pfile.

> [!WARNING]
> Si dispone de firewalls, servidores proxy web o software de seguridad que inspeccionan o realizan acciones en función de las extensiones de nombre de archivo, puede que tenga que volver a configurar estos para admitir las nuevas extensiones de nombre de archivo.

|Extensión de nombre de archivo original|Extensión de nombre de archivo con protección de RMS|
|-------------------------------------------|--------------------------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|.png|.ppng|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.giff|.pgiff|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jif|.pjif|
|.jt|.pjt|
¹ Representación de PDF con tecnología Foxit. Copyright © 2003–2014 by Foxit Corporation.

En la tabla siguiente se enumeran los tipos de archivo que admite de forma nativa la aplicación Microsoft Rights Management sharing en Microsoft Office 2016, Office 2013 y Office 2010. En estos archivos, la extensión de nombre de archivo permanece igual después de que el archivo se ha protegido con RMS.

|Tipos de archivo admitidos por Office|Tipos de archivo admitidos por Office|
|-----------------------------------------|-----------------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="BKMK_ChangeDefaultProtection"></a>Cambio del nivel de protección predeterminado de los archivos
Puede cambiar la manera en que la aplicación RMS sharing protege los archivos mediante la modificación del Registro. Por ejemplo, puede forzar que los archivos que admiten la protección nativa estén protegidos de forma genérica por la aplicación RMS sharing.

Puede que quiera hacer esto por los siguientes motivos:

-   Para asegurarse de que todos los usuarios pueden abrir el archivo desde sus dispositivos móviles.

-   Para asegurarse de que todos los usuarios pueden abrir el archivo si no tienen una aplicación que admite la protección nativa.

-   Para tener en cuenta sistemas de seguridad que realizan acciones sobre los archivos por su extensión de nombre de archivo y que se pueden reconfigurar para que tengan en cuenta la extensión de nombre de archivo .pfile pero no para admitir varias extensiones de nombre de archivo para la protección nativa.

De igual forma, puede forzar que la aplicación RMS sharing aplique protección nativa a archivos a los que, de forma predeterminada, se les aplicaría protección genérica. Esto podría resultar adecuados si tiene una aplicación que admite las API de RMS, por ejemplo, una aplicación de línea de negocio que han escrito sus desarrolladores internos o una aplicación adquirida a un fabricante de software independiente (ISV).

También puede forzar que la aplicación RMS sharing boquee la protección de los archivos, es decir, que no aplique protección nativa ni protección genérica. Por ejemplo, esto podría ser necesario si tiene una aplicación o un servicio automatizados que deben poder abrir un archivo específico para procesar su contenido. Cuando se bloquea la protección para un tipo de archivo, los usuarios no pueden usar la aplicación RMS sharing para proteger un archivo con ese tipo de archivo. Cuando lo intentan, verán un mensaje que dice que el administrador ha impedido la protección y deben cancelar su acción para proteger el archivo.

Para configurar la aplicación RMS sharing para aplicar protección genérica a todos los archivos a los que, de forma predeterminada, se les aplicaría protección nativa, realice las siguientes modificaciones en el Registro:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Cree una nueva clave llamada **&#42;**.

    Este valor indica archivos con cualquier extensión de nombre de archivo.

2.  En la clave recién agregada de **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\&#42;**, cree un nuevo valor de cadena (REG_SZ) llamado **Encryption** que tenga el valor de datos de **Pfile**.

    Este valor da como resultado la aplicación de protección genérica por parte de la aplicación RMS sharing.

Estos dos valores provocarán que la aplicación RMS sharing aplique protección genérica a todos los archivos que tiene una extensión de nombre de archivo. Si éste es su objetivo, no es necesario configurar nada más. Sin embargo, puede definir excepciones para tipos de archivo específicos para que sigan estando protegidos de forma nativa. Para ello, debe realizar tres modificaciones adicionales en el Registro para cada tipo de archivo:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Agregue una nueva clave que tenga el nombre de la extensión de nombre de archivo (sin el punto delante).

    Por ejemplo, para los archivos que tienen una extensión .docx, cree una clave denominada **DOCX**.

2.  En la clave de tipo de archivo recién agregada (por ejemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), cree un nuevo valor DWORD llamado **AllowPFILEEncryption** que tenga un valor de **0**.

3.  En la clave de tipo de archivo recién agregada (por ejemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), cree un nuevo valor DWORD llamado **Encryption** que tenga un valor de **Native**.

Como resultado de esta configuración, todos los archivos están protegidos genéricamente, excepto los archivos que tienen una extensión de nombre de archivo .docx, que están protegidos de forma nativa por la aplicación RMS sharing.

Repita estos tres pasos con otros tipos de archivo que quiera definir como excepciones porque admiten la protección nativa y no quiere que la aplicación RMS sharing los proteja de forma genérica.

Puede realizar modificaciones parecidas en el Registro para otras situaciones cambiando el valor de la cadena **Encryption** que admite los siguientes valores:

-   **Pfile**: Protección genérica

-   **Native**: Protección nativa

-   **Off**: Bloquear protección

## Vea también
[Guía de usuario de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_user_guide.md)

