---
description: na
keywords: na
title: Configuring Custom Templates for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
---
# Configuraci&#243;n de plantillas personalizadas para Azure Rights Management
Tras activar Azure Rights Management (Azure RMS), los usuarios pueden automáticamente usar dos plantillas predeterminadas, lo que les facilita la aplicación de directivas para archivos confidenciales para los que desean restringir el acceso solamente a usuarios autorizados de su organización. Estas dos plantillas presentan las restricciones de directivas de derechos siguientes:

-   Visualización de solo lectura para el contenido protegido

    -   Nombre para mostrar: **&lt;nombre de organización&gt; - Solo vista confidencial**

    -   Permiso específico: Ver contenido

-   Lectura o modificación de permisos de contenido protegido

    -   Nombre para mostrar: **&lt;nombre de organización&gt; - Confidencial**

    -   Permisos específicos: Ver contenido, Guardar archivo, Editar contenido, Ver derechos asignados, Permitir macros, Reenviar, Responder y Responder a todos

Además, la [aplicación RMS sharing](http://technet.microsoft.com/library/dn339006.aspx) permite a los usuarios definir su propio conjunto de permisos. Y, para el cliente de Outlook y Outlook Web Access, los usuarios pueden seleccionar la opción **No reenviar** para los mensajes de correo electrónico.

Para muchas organizaciones, las plantillas predeterminadas pueden ser suficientes. Pero si quieres crear tus propias plantillas de directivas de derechos personalizadas, puedes hacerlo. Entre los motivos para crear una plantilla personalizada encontramos los siguientes:

-   Quieres una plantilla que garantice los derechos a una red secundaria de usuarios de la organización, más que a todos los usuarios.

-   Desea que solo un subconjunto de usuarios puedan ver y seleccionar una plantilla (plantilla de departamento) de las aplicaciones, en lugar de que todos los usuarios de la organización vean y puedan seleccionar la plantilla.

-   Quieres definir un derecho personalizado para una plantilla, como Ver y Editar, pero no Copiar e Imprimir.

-   Quieres configurar opciones adicionales en una plantilla, entre las cuales se incluye una fecha de caducidad y si se puede acceder al contenido sin conexión a Internet.

Para que los usuarios puedan seleccionar una plantilla personalizada que contenga una configuración como estas, en primer lugar, debes crear una plantilla personalizada, configurarla y, a continuación, publicarla.

Usa las secciones siguientes para tratar de configurar y usar plantillas personalizadas:

-   [Cómo crear, configurar y publicar una plantilla personalizada](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToConfigureCustomTemplates)

-   [Cómo copiar una plantilla](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates)

-   [Cómo quitar (archivar) plantillas](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToArchiveTemplates)

-   [Actualización de plantillas para usuarios](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates)

-   [Referencia de Windows PowerShell](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_PowerShellTemplates)

## <a name="BKMK_HowToConfigureCustomTemplates"></a>Cómo crear, configurar y publicar una plantilla personalizada
En el Portal de Azure clásico puede crear y administrar plantillas personalizada. Puede hacerlo directamente desde el Portal de Azure clásico o puede iniciar sesión en el Centro de administración de Office 365 y elegir **Características avanzadas** para Rights Management, lo que le redirigirá al Portal de Azure clásico.

Usa los procedimientos siguientes para crear, configurar y publicar plantillas personalizadas para Rights Management.

#### Para crear una plantilla personalizada

1.  En función de si inicia sesión en el Centro de administración de Office 365 o en el Portal de Azure clásico, emplee uno de los siguientes procedimientos:

    -   En el [Centro de administración de Office 365](https://portal.office.com/):

        1.  En el panel izquierdo, haga clic en**Configuración del servicio**.

        2.  En la página **Configuración del servicio**, haga clic en **Rights Management**.

        3.  En la sección **Proteja su información**, haga clic en **Administrar**.

        4.  En la sección **Rights Management**, haga clic en **Características avanzadas**.

            > [!NOTE]
            > Si no ha activado todavía Rights Management, haga clic primero en **Activar** y confirme la acción. Para obtener más información, vea [Activar Rights Management de Azure](../Topic/Activating_Azure_Rights_Management.md).
            > 
            > Si no ha hecho clic en **Características avanzadas** antes, después de activar Rights Management, siga las instrucciones que aparecen en pantalla para obtener una suscripción gratuita de Azure, necesaria para poder acceder al Portal de Azure clásico.

            Al hacer clic en **Características avanzadas**, se carga el Portal de Azure clásico, donde puede administrar **RIGHTS MANAGEMENT** para Azure Active Directory de su organización.

    -   Desde el [Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

        2.  En la página **Active Directory**, haga clic en **RIGHTS MANAGEMENT**.

        3.  Selecciona el directorio que administrarás para Rights Management.

        4.  Si no ha activado todavía Rights Management, haga clic en **ACTIVAR** y confirme la acción.

            > [!NOTE]
            > Para obtener más información, vea [Activar Rights Management de Azure](../Topic/Activating_Azure_Rights_Management.md).

2.  Crea una plantilla nueva:

    -   En el Portal de Azure clásico, en la página de inicio rápido **Introducción a Rights Management**, haga clic en **Crear una nueva plantilla de directiva de permisos**.

        Si no ve inmediatamente esta página tras seguir las instrucciones de Office 365, use las instrucciones de navegación del Portal de Azure clásico, enumeradas anteriormente.

3.  En la página **Agregar una nueva plantilla de directiva de permisos**, seleccione un idioma en el que tendrá que escribir el nombre de la plantilla y la descripción que verán los usuarios (puede agregar más idiomas más adelante). A continuación, escribe un nombre y una descripción únicos, y haz clic en el botón Completado.

En la página de inicio rápido **Empiece a trabajar con Rights Management**, haga clic en **Administrar sus plantillas de directivas de permisos**. Verá la plantilla recién creada agregada a la lista de plantillas, con el estado **Archivada**. En esta fase, la plantilla se ha creado pero no se ha configurado, y no es visible para los usuarios.

#### Para configurar y publicar una plantilla personalizada

1.  Seleccione la plantilla recién creada en la página **PLANTILLAS** del Portal de Azure clásico.

2.  En la página de inicio rápido **Se ha agregado la plantilla**, haga clic en **Introducción** en el paso 1, **Configurar permisos de usuarios y grupos**, elija **EMPEZAR AHORA** o **AGREGAR** y seleccione los usuarios y grupos que tendrán permisos para usar el contenido protegido con la nueva plantilla.

    > [!NOTE]
    > Los usuarios o grupos que selecciones deben disponer de una dirección de correo electrónico. En un entorno productivo, no será un problema, pero en un entorno de pruebas simple, es posible que tengas que agregar direcciones de correo electrónico para cuentas de usuario o grupos.

    Se recomienda usar grupos más que usuarios, lo cual simplifica la administración de las plantillas. Si tiene Active Directory localmente y está sincronizando con Azure AD, puede usar grupos habilitados para correo electrónico que sean grupos de seguridad o grupos de distribución. Sin embargo, si desea conceder derechos a todos los usuarios de la organización, resultará más eficiente copiar una de las plantillas predeterminadas en lugar de especificar varios grupos. Para obtener más información, consulte la sección [Cómo copiar una plantilla](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates) de este tema.

    > [!TIP]
    > Más tarde puede agregar usuarios de fuera de su organización a la plantilla mediante el [módulo Windows PowerShell para Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx) y uno de los métodos siguientes:
    > 
    > -   **Use un objeto de Rights Definition para actualizar una plantilla**:    especifique las direcciones de correo electrónico externas y sus derechos en un objeto de Rights Definition, que después usará para actualizar su plantilla. Especifique el objeto de Rights Definition mediante el cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para crear una variable y, a continuación, suministrar esta variable al parámetro -RightsDefinition con el cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) para modificar una plantilla existente. Sin embargo, si agrega estos usuarios a una plantilla existente, también tendrá que definir objetos de Rights Definition para los grupos existentes en las plantillas y no solo los usuarios externos nuevos.
    > -   **Exportar, editar e importar la plantilla actualizada**: use el cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar la plantilla en un archivo que pueda editar para agregar las direcciones de correo electrónico externas de estos usuarios y sus derechos en los grupos y derechos existentes. A continuación, use el cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para importar este cambio de nuevo en Azure RMS.

3.  Haz clic en el botón Siguiente y, a continuación, asigna uno de los derechos enumerados a tus usuarios y grupos seleccionados.

    Use la descripción mostrada para obtener más información acerca de cada derecho (y para derechos personalizados). También hay información más detallada disponible en [Configuración de los derechos de uso para Azure Rights Management](../Topic/Configuring_Usage_Rights_for_Azure_Rights_Management.md). Sin embargo, las aplicaciones que son compatibles con RMS pueden variar en la forma de aplicar estos derechos. Consulte su documentación y realice sus propias pruebas con las aplicaciones que usan los usuarios para comprobar el comportamiento antes de implementar la plantilla para los usuarios. Para hacer que esta plantilla solo puedan verla los administradores para la realización de las pruebas, defínala como una plantilla de departamento (paso 6).

4.  Si seleccionó **Personalizar**, haga clic en el botón Siguiente y seleccione permisos personalizados.

    Aunque puedas usar cualquier combinación de derechos individuales disponible, en algunas aplicaciones, hay derechos que pueden depender de otros derechos individuales. Cuando es sí, se seleccionan de forma automática los derechos dependientes.

    > [!TIP]
    > Considere la posibilidad de agregar el permiso **Copiar y extraer contenido** y concedérselo a algunos administradores o personal de otros roles que sean responsables de la recuperación de información. Este derecho les permite quitar la protección, si es necesario, de archivos y correos electrónicos que se protegerán con esta plantilla. Esta capacidad de quitar la protección en el nivel de plantilla proporciona un control más minucioso que el uso de la característica de superusuario.

5.  Haz clic en el botón Completar.

6.  En cambio, si desea que la plantilla pueda verla solo un subconjunto de usuarios cuando vean una lista de plantillas en las aplicaciones: Haga clic en **ÁMBITO** para configurar esto como una plantilla de departamento y haga clic en **COMENZAR AHORA**. De lo contrario, vaya al paso 9.

    Obtener más información acerca de las plantillas de departamento: De forma predeterminada, todos los usuarios del directorio de Azure verán todas las plantillas publicadas y, a continuación, pueden seleccionarlas en las aplicaciones cuando deseen proteger el contenido. Si desea que solo usuarios específicos vean algunas de las plantillas publicadas, debe definir el ámbito de las plantillas para estos usuarios. A continuación, solo dichos usuarios podrán seleccionar estas plantillas. Los usuarios no especificados no verán las plantillas y por lo tanto, no pueden seleccionarlas. Esta técnica puede facilitar a los usuarios la elección de la plantilla adecuada, especialmente al crear plantillas que están diseñadas para que las usen grupos o departamentos concretos. Por tanto, los usuarios solo pueden ver las plantillas que se les han designado.

    Por ejemplo, ha creado una plantilla para el departamento de recursos humanos que aplica el permiso de solo lectura a los miembros del departamento de finanzas. Para que solo los miembros del departamento de recursos humanos puedan aplicar esta plantilla al usar la aplicación de uso compartido de Administración de derechos, debe definir el ámbito de la plantilla para el grupo habilitado para correo electrónico denominado RecursosHumanos. A continuación, solo los miembros de este grupo pueden ver y aplicar esta plantilla.

7.  En **VISIBILIDAD DE PLANTILLA**, seleccione los usuarios y grupos que podrán ver y seleccionar la plantilla desde las aplicaciones habilitadas para RMS. Como antes, como procedimiento recomendado, utilice grupos en lugar de usuarios, y los grupos o usuarios que seleccione deben tener una dirección de correo electrónico.

8.  Haga clic en el botón Siguiente y decida si es necesario configurar la compatibilidad de aplicaciones para la plantilla de departamento. Si lo hace, haga clic en **COMPATIBILIDAD DE APLICACIÓN**, active la casilla y haga clic en **Completa**.

    ¿Por qué debe configurar la compatibilidad de aplicaciones? No todas las aplicaciones pueden admitir plantillas de departamento. Para ello, la aplicación debe autenticarse primero con el servicio RMS antes de descargar las plantillas. Si el proceso de autenticación no se realiza, de forma predeterminada, ninguna de las plantillas de departamento se descargan. Puede invalidar este comportamiento especificando que se deberían descargar todas las plantillas departamentales. Para ello, configure la compatibilidad de aplicaciones y active la casilla **Mostrar esta plantilla a todos los usuarios cuando las aplicaciones no admiten la identidad de usuario**.

    Por ejemplo, si no configura la compatibilidad de aplicaciones para la plantilla de departamento en nuestro ejemplo de recursos humanos, solo los usuarios del departamento de recursos humanos verán la plantilla de departamento cuando utilizan la aplicación de uso compartido de RMS, pero ningún usuario verá la plantilla de departamento al usar Outlook Web Access (OWA) de Exchange Server 2013 porque Exchange OWA y Exchange ActiveSync no son compatibles actualmente con las plantillas de departamento. Si invalida este comportamiento predeterminado mediante la configuración de la compatibilidad de aplicaciones, solo los usuarios del departamento de recursos humanos verán la plantilla de departamento cuando usen la aplicación de uso compartido de RMS, pero todos los usuarios podrán ver la plantilla de departamento al usar Outlook Web Access (OWA). Si los usuarios utilizan OWA o Exchange ActiveSync desde Exchange Online, las plantillas de departamento las verán todos los usuarios o bien ninguno, en función del estado de la plantilla (archivado o publicado) en Exchange Online.

    Office 2016 admite de forma nativa plantillas de departamento, y Office 2013 también con las últimas actualizaciones de Office ([KB 3054853](https://support.microsoft.com/kb/3054853)).

    > [!NOTE]
    > Si tiene aplicaciones que aún no admiten de forma nativa las plantillas departamentales, use un script personalizado de descarga de plantillas RMS u otras herramientas para implementar estas plantillas en la carpeta local del cliente de RMS. A continuación, estas aplicaciones mostrarán correctamente las plantillas de departamento solo a los usuarios y grupos que ha seleccionado para el ámbito de la plantilla:
    > 
    > -   Para Office 2010, la carpeta de cliente es **%localappdata%\Microsoft\DRM\Templates**.
    > -   Desde un equipo cliente que ha descargado todas las plantillas, puede copiar los archivos de plantilla y pegarlos en otros equipos.
    > 
    > Puede [descargar el script de plantillas personalizadas de RMS desde el sitio de Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Si ve un error al hacer clic en este vínculo, probablemente no se haya registrado en Microsoft Connect.   Para registrarse:
    > 
    > 1.  Vaya al [sitio de Microsoft Connect](http://www.connect.microsoft.com) e inicie sesión con su cuenta Microsoft.
    > 2.  Haga clic en **Directorio** y seleccione la categoría **Ver los productos Connect que no aceptan comentarios**.
    > 3.  Busque **Rights Management Services** y, para el programa **Microsoft RMS Enterprise Features**, haga clic en **Unirse**.

9. Haz clic en **CONFIGURAR** y agrega los idiomas adicionales que usen los usuarios, junto con el nombre y la descripción de esta plantilla en ese idioma. Cuando tienes usuarios multilingües, es importante agregar todos los idiomas que usen; además debes proporcionar un nombre y una descripción en ese idioma. Los usuarios verán entonces el nombre y la descripción de la plantilla en el mismo idioma que su sistema operativo, lo cual garantiza que entenderán la directiva que se aplica a un documento o a un mensaje de correo electrónico. Si no coinciden con el idioma del sistema operativo cliente, el nombre y la descripción que ven se cambiarán al idioma y la descripción que tú hayas definido cuando creaste por primera vez la plantilla.

    Después, comprueba si quieres hacer algún cambio en las configuraciones siguientes:

    |Setting|Más información|
    |-----------|-------------------|
    |**expiración de contenido**|Define una fecha o un número de días para esta plantilla cuando los archivos que están protegidos por dicha plantilla no deben abrirse. Puedes especificar una fecha o un número de días a partir del momento en que se aplica la protección al archivo.<br /><br />Cuando se especifica una fecha, entra en vigor a medianoche en su zona horaria actual.|
    |**acceso sin conexión**|Usa esta configuración para equilibrar los requisitos de seguridad que tengas frente al requisito de que los usuarios deben poder abrir archivos protegidos cuando no disponen de conexión a Internet.<br /><br />Si especificas que el contenido no está disponible sin conexión a Internet o que el contenido está disponible solamente durante un número concreto de días, cuando se supere ese umbral, los usuarios deberán volver a autenticarse y se registrará su acceso. Cuando esto sucede, si sus credenciales no se han almacenado en la memoria caché, se pedirá a los usuarios que inicien sesión antes de que puedan abrir el archivo.<br /><br />Además de la reautenticación, también se vuelve a evaluar la directiva y la pertenencia al grupos de usuarios. De modo que los usuarios podrían experimentar diferentes resultados de acceso para el mismo archivo si se producen cambios en la directiva o la pertenencia al grupo desde la última vez que se accedió al archivo.|

10. Cuando esté seguro de que la plantilla está configurada correctamente para los usuarios, haga clic en **PUBLICAR** para que la plantilla esté visible para los usuarios y elija **GUARDAR**.

11. En el Portal clásico, haga clic en el botón para volver a la página **PLANTILLAS**, donde la plantilla tiene ahora el estado actualizado de **Publicada**.

Para realizar cualquier cambio en tu plantilla, selecciónala y, a continuación, usa los pasos de inicio rápido otra vez. O selecciona una de las opciones siguientes:

-   Para agregar más usuarios y grupos, y definir sus derechos: Haga clic en **PERMISOS** y elija **AGREGAR**.

-   Para quitar los usuarios o grupos que has seleccionado anteriormente: Haga clic en**PERMISOS**, seleccione el usuario o grupo en la lista y elija **ELIMINAR**.

-   Para cambiar qué usuarios pueden ver las plantillas para seleccionarlas desde las aplicaciones: Haga clic en**ÁMBITO**, elija **AGREGAR**, **ELIMINAR** o **COMPATIBILIDAD DE APLICACIÓN**.

-   Para que la plantilla ya no sea visible para todos los usuarios: Haga clic en **CONFIGURAR**, elija **ARCHIVO** y haga clic en **GUARDAR**.

-   Para realizar otros cambios de configuración: Haga clic en **CONFIGURAR**, realice los cambios y elija **GUARDAR**.

> [!WARNING]
> Cuando realices cambios en una plantilla que has guardado antes, los clientes no verán dichos cambios en la plantilla hasta que se actualicen en sus equipos. Para obtener más información, consulte la sección [Actualización de plantillas para usuarios](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates) de este tema.

## <a name="BKMK_HowToCopyTemplates"></a>Cómo copiar una plantilla
Si desea crear una plantilla nueva que tenga una configuración muy similar a una plantilla existente, seleccione la plantilla original en la página **PLANTILLAS**, haga clic en **COPIAR**, especifique un nombre único y haga los cambios necesarios.

> [!IMPORTANT]
> Al copiar una plantilla, se copia también el estado **Publicada** o **Archivada**. De modo que si copia una plantilla publicada, se publicará su estado inmediato, a menos que lo cambie.

Puedes copiar plantillas personalizadas y plantillas predeterminadas. Como práctica recomendada, copie una de las plantillas predeterminadas en lugar de crear una nueva plantilla personalizada si desea que la plantilla conceda derechos a todos los usuarios de su organización. Este método significa que no debe crear o seleccionar varios grupos para especificar todos los usuarios. En este escenario, sin embargo, asegúrese de especificar un nombre y una descripción nuevos para la plantilla copiada para idiomas adicionales.

## <a name="BKMK_HowToArchiveTemplates"></a>Cómo quitar (archivar) plantillas
Las plantillas predeterminadas no se pueden eliminar, pero se pueden archivar para que los usuarios no las vean.

De forma similar, si ha publicado una plantilla personalizada y ya no desea que los usuarios puedan verla, edite la plantilla y elija **ARCHIVAR**, **GUARDAR** en la página **CONFIGURAR**. O bien seleccione la plantilla en la página **PLANTILLAS** y seleccione **ARCHIVAR**.

Dado que no puede editar las plantillas predeterminadas, para archivar estas plantillas, debe utilizar la opción **ARCHIVAR** en la página **PLANTILLAS**. No se puede archivar la opción de Outlook **No reenviar**.

#### Para quitar una plantilla predeterminada

-   En la página **PLANTILLAS**, seleccione la plantilla predeterminada y haga clic en **ARCHIVAR**.

El estado cambia de **Publicada** a **Archivada**. Si cambia de opinión, seleccione la plantilla y haga clic en **PUBLICAR**.

## <a name="BKMK_RefreshingTemplates"></a>Actualización de plantillas para usuarios
Cuando usas Azure RMS, se descargan de forma automática plantillas a los ordenadores cliente para que los usuarios puedan seleccionarlas desde sus aplicaciones. Sin embargo, es posible que tengas que tomar medidas adicionales si quieres efectuar cambios en las plantillas:

|Aplicación o servicio|Cómo se actualizan las plantillas tras los cambios|
|-------------------------|------------------------------------------------------|
|Exchange Online|Configuración manual precisa para actualizar plantillas.<br /><br />Para seguir los pasos de la configuración, expanda la sección siguiente, [Solamente Exchange Online: Cómo configurar Exchange para descargar las plantillas personalizadas que se han cambiado](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_ExchangeOnlineTemplatesUpdate).|
|Office 365|Actualización automática: no se requieren pasos adicionales.|
|Office 2016 y Office 2013<br /><br />Aplicaciones de uso compartido de RMS para Windows|Actualización automática – programada:<br /><br />-   Para estas versiones posteriores de Office: el intervalo de actualización predeterminado es cada 7 días.<br />-   Para la aplicación de uso compartido de RMS para Windows: a partir de la versión 1.0.1784.0, el intervalo de actualización predeterminado es cada día. Las versiones anteriores tienen un intervalo de actualización predeterminado de 7 días.<br /><br />Para que la actualización se lleve a cabo antes de lo programado, expanda la sección siguiente, [Office 2016, Office 2013 y la aplicación RMS sharing para Windows: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado](#BKMK_Office2013ForceUpdate).|
|Office 2010|Se actualiza cuando los usuarios inician sesión.<br /><br />Para forzar una actualización, pide u obliga a los usuarios a cerrar sesión y volver a iniciar la sesión. O bien, vea la sección siguiente: [Solamente para Office 2010: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado](#BKMK_Office2010ForceUpdate).|
Para los dispositivos móviles que usan la aplicación de uso compartido de RMS, se descargan automáticamente plantillas (y se actualizan si es necesario) sin que sea precisa una nueva configuración.

### <a name="BKMK_ExchangeOnlineTemplatesUpdate"></a>Solamente Exchange Online: Cómo configurar Exchange para descargar las plantillas personalizadas que se han cambiado
Si ya has configurado Information Rights Management (IRM) para Exchange Online, no se descargarán plantillas personalizadas para usuarios hasta que realices los cambios siguientes mediante Windows PowerShell en Exchange Online.

> [!NOTE]
> Para obtener más información acerca de cómo usar Windows PowerShell en Exchange Online, consulte [Usar PowerShell con Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Debes efectuar este procedimiento cada vez que cambies una plantilla.

##### Para actualizar plantillas para Exchange Online

1.  Conéctese al servicio mediante Windows PowerShell en Exchange Online:

    1.  Especifique el nombre de usuario y la contraseña de Office 365:

        ```
        $Cred = Get-Credential
        ```

    2.  Conecte con el servicio Exchange Online mediante la ejecución de los dos comandos siguientes:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Usa el cmdlet [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) para volver a importar tu Dominio de publicación de confianza (TPD) desde Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Por ejemplo, si su nombre TPD es **RMS Online - 1** (un nombre habitual en muchas organizaciones), escriba: **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Para comprobar tu nombre de TPD, puedes usar el cmdlet [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx).

3.  Para confirmar que se han importado correctamente las plantillas, espere unos minutos y, a continuación, ejecute el cmdlet [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) y, en Tipo, especifique Todas. Por ejemplo:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > Es útil conservar una copia de la salida, con el fin de poder copiar fácilmente los nombres de plantilla o los GUID si posteriormente se archiva una plantilla.

4.  Por cada plantilla importada que desea que esté disponible en la aplicación web de Outlook, debe usar el cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) y establecer Tipo en Distribuido:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Dado que Outlook Web Access almacena en caché la interfaz de usuario durante las 24 horas, es posible que los usuarios no puedan ver la plantilla nueva hasta un día después.

Además, si archivas una plantilla (personalizada o predeterminada) y usas Exchange Online con Office 365, los usuarios continuarán viendo las plantillas archivadas si usan la aplicación web de Outlook o dispositivos móviles que usen el protocolo Exchange ActiveSync.

Para que los usuarios no vean estas plantillas, conéctate al servicio mediante Windows PowerShell en Exchange Online y, a continuación, usa el cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) y ejecuta este comando:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

### <a name="BKMK_Office2013ForceUpdate"></a>Office 2016, Office 2013 y la aplicación RMS sharing para Windows: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado
Si modifica el Registro de los equipos que ejecutan Office 2016, Office 2013 o la aplicación Rights Management (RMS) sharing, puede cambiar la programación automática para que las plantillas cambiadas se actualicen en los equipos con más frecuencia que la indicada en sus valores predeterminados. También puede forzar una actualización inmediata eliminando los datos existentes en un valor del Registro.

> [!WARNING]
> Si usas el Editor del Registro de forma incorrecta, es posible que ocasiones problemas serios que puedan hacer preciso que reinstales el sistema operativo. Microsoft no puede garantizar que seas capaz de resolver problemas ocasionados por el uso inapropiado del Editor del Registro. Usa el Editor del Registro bajo tu propia responsabilidad.

##### Para cambiar la programación automática

1.  Con un editor del Registro, cree y establezca uno de los valores del Registro siguientes:

    -   Para establecer una frecuencia de actualización en días (mínimo de 1 día):  cree un nuevo valor del Registro denominado **TemplateUpdateFrequency** y defina un valor entero para los datos, que especifique la frecuencia en días para descargar los cambios en una plantilla descargada. Use la tabla siguiente para localizar la ruta de acceso del Registro y crear este nuevo valor del Registro.

        |Ruta de acceso del registro|Tipo|Valor|
        |-------------------------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequency|

    -   Para establecer una frecuencia de actualización en segundos (mínimo de 1 segundo):  cree un nuevo valor del Registro denominado **TemplateUpdateFrequencyInSeconds** y defina un valor entero para los datos, que especifique la frecuencia en segundos para descargar los cambios en una plantilla descargada. Use la tabla siguiente para localizar la ruta de acceso del Registro y crear este nuevo valor del Registro.

        |Ruta de acceso del registro|Tipo|Valor|
        |-------------------------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequencyInSeconds|

    Asegúrese de crear y establecer uno de estos valores del Registro, no ambos. Si ambos están presentes, **TemplateUpdateFrequency** se omite.

2.  Si desea forzar una actualización inmediata de las plantillas, vaya al procedimiento siguiente. En caso contrario, reinicie ahora las aplicaciones de Office y las instancias del Explorador de archivos.

##### Para forzar una actualización inmediata

1.  Con un editor del Registro, elimine los datos del valor **LastUpdatedTime**. Por ejemplo, en los datos puede aparecer **2015-04-20T15:52**. Elimine 2015-04-20T15:52 para que no se muestre ningún dato. Use la tabla siguiente para localizar la ruta de acceso del Registro y eliminar estos datos del valor del Registro.

    |Ruta de acceso del registro|Tipo|Valor|
    |-------------------------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\&lt;MicrosoftRMS_FQDN&gt;\Template|REG_SZ|LastUpdatedTime|
    > [!TIP]
    > En la ruta de acceso del Registro, *&lt;MicrosoftRMS_FQDN&gt;* hace referencia al FQDN de servicio de Microsoft RMS. Si desea comprobar este valor:
    > 
    > 1.  Ejecute el cmdlet [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para Azure RMS. Si no ha instalado todavía el módulo Windows PowerShell para Azure RMS, consulte [Instalación de Windows PowerShell para Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).
    > 2.  En la salida, identifique el valor **LicensingIntranetDistributionPointUrl**.
    > 
    >     Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  En el valor, quite **https://** y **/_wmcs/licensing** de esta cadena. El valor restante es el FQDN de servicio de Microsoft RMS. En nuestro ejemplo, el FQDN de servicio de Microsoft RMS sería el valor siguiente:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Elimine la carpeta siguiente y todos los archivos que contenga: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie las aplicaciones de Office y las instancias del Explorador de archivos.

### <a name="BKMK_Office2010ForceUpdate"></a>Solamente para Office 2010: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado
Si modifica el Registro de los equipos que ejecutan Office 2010, puede establecer un valor para que las plantillas cambiadas se actualicen en los equipos sin esperar a que los usuarios cierren la sesión y vuelvan a iniciarla. También puede forzar una actualización inmediata eliminando los datos existentes en un valor del Registro.

> [!WARNING]
> Si usas el Editor del Registro de forma incorrecta, es posible que ocasiones problemas serios que puedan hacer preciso que reinstales el sistema operativo. Microsoft no puede garantizar que seas capaz de resolver problemas ocasionados por el uso inapropiado del Editor del Registro. Usa el Editor del Registro bajo tu propia responsabilidad.

##### Para cambiar la frecuencia de actualización

1.  Con un editor del Registro, cree un nuevo valor del Registro denominado **UpdateFrequency** y defina un valor entero para los datos, que especifique la frecuencia en días para descargar los cambios en una plantilla descargada. Use la tabla siguiente para localizar la ruta de acceso del Registro y crear este nuevo valor del Registro.

    |Ruta de acceso del registro|Tipo|Valor|
    |-------------------------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_DWORD|UpdateFrequency|

2.  Si desea forzar una actualización inmediata de las plantillas, vaya al procedimiento siguiente. En caso contrario, reinicie ahora las aplicaciones de Office.

##### Para forzar una actualización inmediata

1.  Con un editor del Registro, elimine los datos del valor **LastUpdatedTime**. Por ejemplo, en los datos puede aparecer **2015-04-20T15:52**. Elimine 2015-04-20T15:52 para que no se muestre ningún dato. Use la tabla siguiente para localizar la ruta de acceso del Registro y eliminar estos datos del valor del Registro.

    |Ruta de acceso del registro|Tipo|Valor|
    |-------------------------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_SZ|lastUpdatedTime|

2.  Elimine la carpeta siguiente y todos los archivos que contenga: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie las aplicaciones de Office.

## <a name="BKMK_PowerShellTemplates"></a>Referencia de Windows PowerShell
Todo lo que puede hacer en el Portal de Azure clásico para crear y administrar plantillas puede hacerlo desde la línea de comandos con Windows PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües.

También puede utilizar la exportación e importación para restaurar y hacer una copia de seguridad de sus plantillas personalizadas. Como práctica recomendada, haga una copia de seguridad de sus plantillas personalizadas periódicamente, de modo que si realiza un cambio que no pretendía, pueda revertir fácilmente a una versión anterior.

> [!IMPORTANT]
> Para usar Windows PowerShell para crear y administrar plantillas de directiva de permisos de Azure RMS, debe tener al menos la versión 2.0.0.0 del [módulo de Windows PowerShell para Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Si ya instaló este módulo de Windows PowerShell, ejecute el comando siguiente en una ventana de PowerShell para comprobar el número de versión: `(Get-Module aadrm -ListAvailable).Version`

Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Los cmdlets que admite la creación y administración de plantillas:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)

## Pasos siguientes
Después de configurar plantillas personalizadas para Azure Rights Management, consulte [Plan para la implementación de Azure Rights Management](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) para comprobar si hay otros pasos de configuración que puedan ser necesarios antes de implementar [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] en usuarios y administradores. Si no es necesario ningún otro paso de configuración, consulte [Uso de Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) para obtener instrucciones operativas para apoyar una implementación correcta en su organización.

## Vea también
[Configuración de Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

