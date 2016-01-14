---
description: na
keywords: na
title: Migrating from AD RMS to Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
---
# Migraci&#243;n desde AD RMS a Azure Rights Management
Use el siguiente conjunto de instrucciones para migrar su implementación de Active Directory Rights Management Services (AD RMS) en Azure Rights Management (Azure RMS). Después de la migración, los usuarios seguirán teniendo acceso a documentos y mensajes de correo electrónico que su organización protege mediante AD RMS, mientras que el contenido protegido recientemente usará Azure RMS.

¿No está seguro de si esta migración de AD RMS es conveniente para su organización?

-   Para obtener una introducción a Azure RMS, los problemas empresariales que puede resolver, cómo lo ven administradores y usuarios y cómo funciona, consulte [¿Qué es Rights Management de Azure?](../Topic/What_is_Azure_Rights_Management_.md)

-   Para obtener una comparación entre Azure RMS y AD RMS, consulte [Comparación entre Azure Rights Management y AD RMS](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md).

## Requisitos previos para la migración desde AD RMS a Azure RMS.
Antes de iniciar la migración a Azure RMS, asegúrese de que se cumplen los siguientes requisitos previos y de que conoce las limitaciones.

|Requisito|Más información|
|-------------|-------------------|
|Una implementación de RMS compatible|Todas las versiones de Windows Server 2008 a Windows Server 2012 R2 de AD RMS admiten una migración a Azure RMS:<br /><br />-   Windows Server 2008 (x86 o x64)<br />-   Windows Server 2008 R2 (x64)<br />-   Windows Server 2012 (x64)<br />-   Windows Server 2012 R2 (x64) **Note:** Si está ejecutando Windows RMS en Windows Server 2003, esta versión del sistema operativo quedará fuera del soporte técnico durante 2015. Puede migrar esta versión de RMS a Azure RMS, pero este proceso solo se admite si todavía se admite el sistema operativo. Como alternativa, puede importar el dominio de publicación de confianza (TPD) a una versión de AD RMS que es compatible y, a continuación, volver a importar el TPD sin la opción de compatibilidad de RMS 1.0. Para obtener más información sobre TPD, consulte [Dominio de publicación de confianza](http://technet.microsoft.com/library/dd996639%28v=ws.10%29.aspx)<br />Se admiten todas las topologías de AD RMS válidas:<br /><br />-   Bosque único, un solo clúster de RMS<br />-   Bosque único, varios clústeres de RMS solo con licencias<br />-   Varios bosques, varios clústeres de RMS **Note:** De forma predeterminada, varios clústeres de RMS se migran a un solo inquilino de Azure RMS. Si desea distintos inquilinos de RMS, debe tratarlos como migraciones diferentes. No se puede importar una clave de un clúster de RMS a más de un inquilino de Azure RMS.|
|Todos los requisitos para ejecutar Azure RMS, lo que incluye un inquilino de Azure RMS (no activado)|Consulte [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).<br /><br />Aunque debe tener un inquilino de Azure RMS para poder migrar desde AD RMS, se recomienda que no active el servicio Rights Management antes de la migración. El proceso de migración incluye este paso después de exportar las claves y plantillas de AD RMS e importarlas en Azure RMS. Sin embargo, aunque esté activado Azure RMS, puede migrar desde AD RMS.|
|Preparación para Azure RMS:<br /><br />-   Sincronización de directorios entre el directorio local y Azure Active Directory<br />-   Grupos habilitados para correo en Azure Active Directory|Consulte [Preparación de Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).|
|Si ha usado la funcionalidad Information Rights Management (IRM) de Exchange Server (por ejemplo, las reglas de transporte y Outlook Web Access) o SharePoint Server con AD RMS:<br /><br />-   Plan durante un breve período de tiempo si IRM no estará disponible en estos servidores|Aún puede utilizar IRM en estos servidores con Azure RMS después de la migración. Sin embargo, uno de los pasos de migración es deshabilitar temporalmente el servicio IRM, instalar y configurar un conector, volver a configurar los servidores y, a continuación, volver a habilitar IRM.<br /><br />Se trata de la única interrupción del servicio durante el proceso de migración.|
Limitaciones:

-   Aunque el proceso de migración permite migrar la clave del certificado de licencias del servidor (SLC) a un módulo de seguridad de hardware (HSM) para Azure RMS, Exchange Online actualmente no admite esta configuración. Si desea usar Exchange Online con Azure RMS, la clave del inquilino de Azure RMS debe estar [administrada por Microsoft](http://technet.microsoft.com/library/dn440580.aspx). Como alternativa, puede ejecutar IRM con funcionalidad reducida en Exchange Online cuando sea el usuario quien  administre el inquilino de Azure RMS (BYOK). Para obtener más información acerca del uso de Exchange Online con Azure RMS, vea [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration) en estas instrucciones.

-   Si tiene software y clientes que no son compatibles con Azure RMS, no podrá proteger o consumir contenido protegido por Azure RMS. Asegúrese de consultar la sección de clientes y aplicaciones compatibles en el tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

-   Si importa su clave de local a Azure RMS como archivada (sin establecer el TPD como activo durante el proceso de importación) y migra los usuarios en lotes en una migración por fases, el contenido protegido recientemente por los usuarios migrados no será accesible para los usuarios que permanecen en AD RMS. En este escenario, siempre que sea posible, mantenga un tiempo de migración corto y migre los usuarios en lotes lógicos, de forma que si colaboran entre sí se miren juntos.

    Esta limitación no se aplica cuando se establece el TPD como activo durante el proceso de importación, porque todos los usuarios protegerán el contenido con la misma clave. Se recomienda esta configuración, ya que le permite migrar todos los usuarios de forma independiente y a su propio ritmo.

-   Si colabora con asociados externos (por ejemplo, mediante el uso de la federación o de dominios de usuario de confianza), estos también deberán migrar a Azure RMS al mismo tiempo o tan pronto como sea posible una vez haya completado la migración. Para seguir teniendo acceso al contenido previamente protegido por su organización con AD RMS, se deberán realizar cambios en la configuración del cliente similares a los que realice el usuario, incluidos en este documento.

    Debido a las posibles variaciones de configuración de los asociados, las instrucciones exactas para este cambio de configuración están fuera del ámbito de este documento. Para obtener ayuda, póngase en contacto con los servicios de soporte al cliente de Microsoft (CSS).

## Pasos para la migración desde AD RMS a Azure RMS

|Pasos del proceso de migración|Más información|
|----------------------------------|-------------------|
|**1. Descargue las herramientas de administración de Azure RMS.**|Para obtener instrucciones, consulte [Step 1: Download the Azure Rights Management Administration Tool](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step1Migration).|
|**2. Exporte los datos de configuración de AD RMS e impórtelos en Azure RMS.**|Exporte los datos de configuración (claves, plantillas y direcciones URL) de AD RMS a un archivo XML y, luego, cargue ese archivo en Azure RMS mediante el cmdlet Import-AadrmTPD de Windows PowerShell. Podrían ser necesarios pasos adicionales, dependiendo de la configuración de claves de AD RMS:<br /><br />-   Migración entre claves protegidas de software: De claves basadas en contraseña administradas centralmente en AD RMS a clave de inquilino de Azure RMS administrada por Microsoft. Esta es la ruta de migración más sencilla y no se necesita ningún paso adicional.<br />-   Migración entre claves protegidas por HSM: De claves almacenadas por un módulo de seguridad de hardware (HSM) para AD RMS a clave de inquilino de Azure RMS administrada por el cliente (el escenario "aporte su propia clave" o BYOK). Esto requiere pasos adicionales para transferir la clave de HSM de Thales local a HSM de Azure RMS.<br />-   Migración de clave protegida por software a clave protegida por HSM: Claves basadas en contraseña administradas centralmente en AD RMS para la clave del inquilino de Azure RMS administrada por clientes (el escenario "bring your own key" o "BYOK"). Aquí es necesario realizar la mayor parte de la configuración, porque debe extraer primero la clave de software e importarla a un HSM local y, a continuación, realizar los pasos adicionales para transferir la clave del HSM local de Thales al HSM de Azure RMS.<br /><br />Para obtener instrucciones, consulte [Step 2. Export configuration data from AD RMS and import it to Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step2Migration).|
|**3. Active el inquilino de RMS.**|Si es posible, realice este paso después del proceso de importación y no antes.<br /><br />Para obtener más información e instrucciones sobre este tema, consulte [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).|
|**4. Configure las plantillas importadas.**|Al importar las plantillas de directiva de derechos, su estado se archiva. Si quiere que los usuarios puedan verla y usarla, debe cambiar el estado de la plantilla a publicada en el Portal de Azure clásico.<br /><br />Para obtener instrucciones, consulte [Step 4. Configure imported templates](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step4Migration).|
|**5. Vuelva a configurar los clientes para usar Azure RMS.**|Debe volver a configurar los equipos de Windows existentes para utilizar el servicio de Azure RMS en lugar de AD RMS. Este paso se aplica a los equipos de su organización y en los equipos de las organizaciones asociadas si ha colaborado con ellas al ejecutar AD RMS.<br /><br />Además, si ha implementado las [extensiones para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx) para admitir dispositivos móviles como iPads y teléfonos iOS, teléfonos y tabletas Android, Windows Phone y equipos Mac, debe quitar los registros SRV en DNS que redirigen estos clientes para usar AD RMS.<br /><br />Para obtener instrucciones, consulte [Step 5. Reconfigure clients to use Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step5Migration).|
|**6. Configure la integración de IRM con Exchange Online.**|Este paso es necesario si desea usar Exchange Online con Azure RMS.<br /><br />Para obtener instrucciones, consulte [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration).|
|**7. Implemente el conector RMS.**|Este paso es necesario si desea utilizar cualquiera de los siguientes servicios locales con Azure RMS:<br /><br />-   Exchange Server (por ejemplo, las reglas de transporte y Outlook Web Access)<br />-   Servidor de SharePoint<br />-   Windows Server que se ejecuta la infraestructura de clasificación de archivos<br /><br />Para obtener instrucciones, consulte [Paso 7. Retire AD RMS](#BKMK_Step7Migration).|
|**8. Retire AD RMS**.|Cuando haya confirmado que todos los clientes usan Azure RMS y ya no obtienen acceso a los servidores de AD RMS, puede retirar la implementación de AD RMS.<br /><br />Para obtener instrucciones, consulte [Paso 8. Vuelva a usar su clave del inquilino de Azure RMS](#BKMK_Step8Migration).|
|**9. Vuelva a escribir su clave de inquilino de Azure RMS.**|Este paso es necesario si no estaba realizando la ejecución en modo criptográfico 2 antes de la migración y es opcional pero recomendado para que todas las migraciones ayuden a proteger la seguridad de la clave de inquilino de Azure RMS.<br /><br />Para obtener instrucciones, consulte [Step 9. Re-key your Azure RMS tenant key](#BKMK_Step9Migration).|

### <a name="BKMK_Step1Migration"></a>Paso 1: Descargue la herramienta de administración de Azure Rights Management
Vaya al Centro de descarga de Microsoft y descargue la [herramienta de administración de Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721), que contiene el módulo de administración de Azure RMS para Windows PowerShell.

### <a name="BKMK_Step2Migration"></a>Paso 2. Exporte los datos de configuración de AD RMS e impórtelos en Azure RMS.
Este paso es un proceso de dos fases:

1.  Exporte los datos de configuración de AD RMS mediante la exportación de los dominios de publicación de confianza (TPD) a un archivo .xml. Este proceso es el mismo para todas las migraciones.

2.  Importe los datos de configuración a Azure RMS. Hay diferentes procesos para este paso, según la configuración de la implementación de AD RMS actual y la topología preferida para su clave de inquilino de Azure RMS.

#### Exportar los datos de configuración de AD RMS
Siga este procedimiento en todos los clústeres de AD RMS, para todos los dominios de publicación confianza que tienen contenido protegido de su organización. No es necesario ejecutar esto en clústeres solo para licencias.

> [!NOTE]
> Si utiliza Windows Server 2003 Rights Management, en lugar de estas instrucciones, siga el procedimiento [Exportar clave privada de SLC, TUD, TPD y RMS](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) desde el tema [Migración desde Windows RMS a AD RMS en una estructura distinta](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx).

###### Para exportar los datos de configuración (información del dominio de publicación de confianza)

1.  Inicie sesión en el clúster de AD RMS como un usuario con permisos de administración de AD RMS.

2.  Desde la consola de administración de AD RMS (**Active Directory Rights Management Services**), expanda el nombre del clúster de AD RMS, expanda **Directivas de confianza** y luego haga clic en **Dominios de publicación de confianza**.

3.  En el panel de resultados, seleccione el dominio de publicación de confianza y luego, en el panel Acciones, haga clic en **Exportar dominio de publicación de confianza**.

4.  En el cuadro de diálogo **Exportar dominio de publicación de confianza**:

    -   Haga clic en **Guardar como** y guárdelo en la ruta de acceso con un nombre de archivo de su elección. Asegúrese de especificar **.xml** como la extensión de nombre de archivo (no se adjunta automáticamente).

    -   Especifique y confirme una contraseña segura. Recuerde esta contraseña, porque la necesitará más adelante, al importar los datos de configuración a Azure RMS.

    -   No seleccione la casilla para guardar el archivo de dominio de confianza en RMS 1.0.

Cuando se exportan todos los dominios de publicación de confianza, está listo para empezar el procedimiento para importar estos datos en Azure RMS.

#### Importar los datos de configuración a Azure RMS
Los procedimientos exactos para este paso dependen de la configuración actual de la implementación de AD RMS y de la topología preferida para su clave de inquilino de Azure RMS.

La implementación de AD RMS actual usará una de las siguientes configuraciones con la clave del certificado emisor de licencias de servidor (SLC):

-   Protección con contraseña de la base de datos de AD RMS. Se trata de la configuración predeterminada.

-   Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales.

-   Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales.

-   Contraseña protegida mediante un proveedor criptográfico externo.

> [!NOTE]
> Para obtener más información acerca del uso de módulos de seguridad de hardware con AD RMS, consulte [Uso de AD RMS con módulos de seguridad de hardware](http://technet.microsoft.com/library/jj651024.aspx).

Las dos opciones de topología de clave de inquilino de Azure RMS son: Microsoft administra su clave de inquilino (**administrada por Microsoft**), o bien es el usuario quien se encarga de ello (**administrada por el cliente**). Cuando administra su propia clave de inquilino de Azure RMS, esto se conoce a veces como "aporte su propia clave" (BYOK) y requiere un módulo de seguridad de hardware (HSM) de Thales. Para obtener más información, consulte la sección [Elija su topología de clave de inquilino: Administrada por Microsoft (opción predeterminada) o por usted (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ChooseTenantKey) en el tema [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

> [!IMPORTANT]
> Actualmente, BYOK de Azure RMS no es compatible con Exchange Online.  Si desea usar BYOK después de la migración y planea usar Exchange Online, asegúrese de que comprende de qué forma esta configuración reduce la funcionalidad IRM para Exchange Online. Revise la información de la sección [Precio y restricciones de BYOK](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) del tema [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) para ayudarle a elegir la mejor topología de clave de inquilino de Azure RMS para la migración.

Utilice la tabla siguiente para identificar qué procedimiento se utilizará para la migración. No se admiten las combinaciones que no aparecen.

|Implementación de AD RMS actual|Topología de clave de inquilino de Azure RMS elegida|Instrucciones de migración|
|-----------------------------------|--------------------------------------------------------|------------------------------|
|Protección con contraseña de la base de datos de AD RMS|Administrada por Microsoft:|Consulte el procedimiento **Migración entre claves protegidas por software** después de esta tabla.<br /><br />Esta es la ruta de migración más sencilla y solo requiere que transfiera los datos de configuración a Azure RMS.|
|Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales nShield|Administrada por el cliente (BYOK)|Consulte el procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.<br /><br />Esto requiere el conjunto de herramientas BYOK y dos conjuntos de pasos para transferir la clave del HSM local al HSM de Azure RMS y, a continuación, transferir los datos de configuración a Azure RMS.|
|Protección con contraseña de la base de datos de AD RMS|Administrada por el cliente (BYOK)|Consulte el procedimiento **Migración de clave protegida por software a clave protegida por HSM** después de esta tabla.<br /><br />Esto requiere el conjunto de herramientas BYOK y tres conjuntos de pasos para, primero, extraer la clave de software e importarla en un HSM local, después transferir la clave del HSM local al HSM de Azure RMS y, por último, transferir los datos de configuración a Azure RMS.|
|Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales.|Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor de HSM para obtener instrucciones sobre cómo transferir su clave de este HSM a un módulo de seguridad de hardware (HSM) de Thales nShield. A continuación, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|
|Contraseña protegida mediante un proveedor criptográfico externo.|Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor criptográfico para obtener instrucciones sobre cómo transferir su clave a un módulo de seguridad de hardware (HSM) de Thales nShield. A continuación, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|
Antes de iniciar estos procedimientos, asegúrese de que puede tener acceso a los archivos .xml que creó anteriormente cuando exportó los dominios de publicación de confianza. Por ejemplo, estos podrían estar guardados en una unidad USB que se transfiere desde el servidor de AD RMS a la estación de trabajo conectada a Internet.

> [!NOTE]
> Independientemente de cómo almacene estos datos, aplique las prácticas de seguridad recomendadas para protegerlos, ya que estos incluyen la clave privada.

##### Migración entre claves protegidas por software
Utilice este procedimiento para importar la configuración de AD RMS a Azure RMS, que resulta en que la clave del inquilino de Azure RMS la administre Microsoft.

###### Para importar los datos de configuración a Azure RMS

1.  En una estación de trabajo conectada a Internet, descargue e instale el módulo de Windows PowerShell para Azure RMS (versión mínima 2.1.0.0), que incluye el cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Si ya descargó e instaló el módulo, compruebe el número de versión. Para ello, ejecute: `(Get-Module aadrm -ListAvailable).Version`

    Para conocer las instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

2.  Inicie Windows PowerShell con la opción **Ejecutar como administrador** y use el cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) para conectarse al servicio de Azure RMS:

    ```
    Connect-AadrmService
    ```
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

3.  Use el cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) para cargar el primer archivo del dominio de publicación de confianza (.xml) exportado. Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que desee usar en Azure RMS para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Por ejemplo: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Cuando se le pida, escriba la contraseña que especificó anteriormente y confirme que desea realizar esta acción.

4.  Cuando se haya completado el comando, repita el paso 3 en cada archivo .xml restante que se creó mediante la exportación de los dominios de publicación de confianza. Pero en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import. Por ejemplo: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) para desconectarse del servicio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Ahora puede ir al [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### Migración entre claves protegidas por HSM
Es un procedimiento de dos partes para importar la clave HSM y la configuración de AD RMS a Azure RMS, que tiene como resultado la clave de inquilino de Azure RMS que administra el propio usuario (BYOK).

Primero debe empaquetar su clave HSM para prepararla para transferirla a Azure RMS y, luego, importarla con los datos de configuración.

###### Parte 1: Empaquetar la clave HSM para que esté preparada para transferirla a Azure RMS

1.  Siga los pasos descritos en la sección [Implementación de Aportar tu propia clave (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) de [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md); para ello, use el procedimiento **Generar y transferir su clave de inquilino a través de Internet** con la excepción siguiente:

    -   No siga los pasos que se indican en **Generar su clave de inquilino**, porque ya tiene el equivalente por su implementación de AD RMS. Debe identificar la clave utilizada por el servidor de AD RMS de la instalación de Thales y usar esta clave durante la migración. Los archivos de claves cifradas de Thales suelen denominarse **key_(keyAppName)_(keyIdentifier)** de forma local en el servidor.

    -   No siga los pasos para **Transferir su clave de inquilino a Azure RMS**, que usa el comando Add-AadrmKey.  En su lugar, transferirá la clave HSM preparada cuando se cargue el dominio de publicación de confianza exportado, mediante el comando Import-AadrmTpd.

2.  En la estación de trabajo conectada a Internet, en la sesión de Windows PowerShell, vuelva a conectar con el servicio de Azure RMS.

Ahora que ha preparado su clave HSM para Azure RMS, está listo para importar el archivo de clave HSM y los datos de configuración de AD RMS.

###### Part 2: Importar la clave HSM y los datos de configuración a Azure RMS

1.  En la estación de trabajo conectada a Internet y en la sesión de Windows PowerShell, cargue el primer archivo del dominio de publicación de confianza exportado (.xml). Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que corresponda a la clave HSM que desee usar en Azure RMS para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Por ejemplo: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Cuando se le pida, escriba la contraseña que especificó anteriormente y confirme que desea realizar esta acción.

2.  Cuando se haya completado el comando, repita el paso 1 en cada archivo .xml restante que se creó mediante la exportación de los dominios de publicación de confianza. Pero en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import.  Por ejemplo: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desconectarse del servicio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Ahora puede ir al [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### Migración de clave protegida por software a clave protegida por HSM
Es un procedimiento de tres partes para importar la configuración de AD RMS a Azure RMS, que resulta en que la clave del inquilino de Azure RMS la administre el propio usuario (BYOK).

Debe extraer la clave del primer certificado emisor de licencias de servidor (SLC) de los datos de configuración y transferir la clave a un HSM de Thales local, empaquetar y transferir la clave de HSM a Azure RMS y, a continuación, importe los datos de configuración.

###### Parte 1: Extraer el SLC de los datos de configuración e importar la clave al HSM local

1.  Siga los pasos siguientes que aparecen en la sección [Implementación de Aportar tu propia clave (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) del tema [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md):

    -   **Generar y transferir su clave de inquilino a través de Internet**: **Preparar la estación de trabajo conectada a Internet**

    -   **Generar y transferir su clave de inquilino a través de Internet**: **Prepare su estación de trabajo desconectada.**

    Debe seguir los pasos para generar la clave de inquilino, puesto que ya tiene el equivalente en el archivo de datos de configuración exportado (.xml). En su lugar, se ejecutará un comando para extraer esta clave del archivo e importarla en el HSM local.

2.  En la estación de trabajo desconectada, ejecute el siguiente comando:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Por ejemplo, para Norteamérica: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Información adicional:

    -   El parámetro ImportRmsCentrallyManagedKey indica que la operación es importar la clave de SLC.

    -   Si no especifica la contraseña en el comando, se le pedirá que la especifique.

    -   El parámetro KeyIdentifier es un nombre descriptivo de clave que crea el nombre del archivo de clave. Debe utilizar únicamente caracteres en minúsculas ASCII.

    -   El parámetro ExchangeKeyPackage especifica un paquete de claves de intercambio de claves (KEK) específico de la región cuyo nombre comienza por BYOK-KEK-pkg-.

    -   El parámetro NewSecurityWorldPackage especifica un paquete internacional de seguridad específico de la región cuyo nombre comienza por BYOK-SecurityWorld-pkg-.

    Este comando genera lo siguiente:

    -   Un archivo de clave de HSM: %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   Archivo de datos de configuración de RMS con el SLC quitado: %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  Si tiene más de un archivo de datos de configuración de RMS, repita el paso 2 para el resto de estos archivos.

Ahora que se ha extraído el SLC para que sea una clave de HSM, está listo para empaquetar y transferirla a Azure RMS.

###### Part 2: Empaquetar y transferir su clave de HSM a Azure RMS

1.  Siga los pasos siguientes que aparecen en la sección [Implementación de Aportar tu propia clave (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) de [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md):

    -   **Generar y transferir su clave de inquilino a través de Internet**: **Preparar su clave de inquilino para transferirla**

    -   **Generar y transferir su clave de inquilino a través de Internet**: **Transferir su clave de inquilino a Azure RMS**

Ahora que ha transferido su clave de HSM a Azure RMS, está listo para importar los datos de configuración de AD RMS, que contienen solo un puntero a la clave del inquilino recién transferido.

###### Part 3: Importar los datos de configuración a Azure RMS

1.  Aún en la estación de trabajo conectada a Internet y en la sesión de Windows PowerShell, copie los archivos de configuración de RMS con el SLC quitado (desde la estación de trabajo desconectada, %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  Cargue el primer archivo. Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que corresponda a la clave HSM que desee usar en Azure RMS para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Por ejemplo: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Cuando se le pida, escriba la contraseña que especificó anteriormente y confirme que desea realizar esta acción.

3.  Cuando se haya completado el comando, repita el paso 2 en cada archivo .xml restante que se creó mediante la exportación de los dominios de publicación de confianza. Pero en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import. Por ejemplo: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desconectarse del servicio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Ahora puede ir al [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

### <a name="BKMK_Step3Migration"></a>Paso 3: Active el inquilino de RMS.
Las instrucciones de este paso se tratan íntegramente en el tema [Activar Rights Management de Azure](../Topic/Activating_Azure_Rights_Management.md).

> [!TIP]
> Si tiene una suscripción de Office 365, puede activar Azure RMS desde el centro de administración de Office 365 o el Portal de Azure clásico. Se recomienda usar el Portal de Azure clásico, ya que usará este portal de administración para completar el paso siguiente.

**¿Qué ocurre si ya está activado el inquilino de Azure RMS?** Si el servicio de Azure RMS ya está activado en su organización, es posible que los usuarios ya hayan usado Azure RMS para proteger el contenido con una clave de inquilino generada automáticamente (y las plantillas predeterminadas) en lugar de las claves (y plantillas) existentes de AD RMS. Esto es improbable que ocurra en equipos que estén bien administrados en la intranet, ya que se configuran automáticamente para su infraestructura de AD RMS. Pero esto puede suceder en equipos de grupo de trabajo o equipos que se conectan con poca frecuencia a la intranet. Desafortunadamente, también es difícil identificar estos equipos, motivo por el que se recomienda no activar el servicio antes de importar los datos de configuración de AD RMS.

Si ya está activado el inquilino de Azure RMS y puede identificar estos equipos, asegúrese de que ejecuta el script CleanUpRMS_RUN_Elevated.cmd en estos equipos, tal como se describe en el paso 5. La ejecución de este script les obliga a reinicializar el entorno de usuario, así descargan la clave de inquilino y las plantillas importadas actualizadas.

### <a name="BKMK_Step4Migration"></a>Paso 4. Configure las plantillas importadas.
Dado que las plantillas que importó tienen un estado predeterminado de **Archivada**, debe cambiar este estado a **Publicada** si desea que los usuarios puedan utilizar estas plantillas con Azure RMS.

Además, si sus plantillas de AD RMS usaban el grupo **TODOS**, este grupo desaparecerá automáticamente al importar las plantillas a Azure RMS; debe agregar manualmente el grupo o usuarios equivalentes y los mismos derechos a las plantillas importadas. El grupo equivalente de Azure RMS se llama **AllStaff-&lt;tenant_GUID&gt;@&lt;tenant_name&gt;.onmicrosoft.com**. Por ejemplo, este grupo puede tener un aspecto similar al siguiente para Contoso: **AllStaff-9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a@contoso.onmicrosoft.com**.

Si no está seguro de si las plantillas de AD RMS incluyen el grupo CUALQUIERA, expanda la sección [PowerShell script to identify AD RMS templates that include the ANYONE group](#BKMK_ScriptForANYONE) en este paso para copiar y usar el script de PowerShell de ejemplo para identificar estas plantillas. Para más información sobre el uso de Windows PowerShell con AD RMS, consulte [Uso de Windows PowerShell para administrar AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx).

Puede ver el grupo creado automáticamente de su organización si copia una de las plantillas de directiva de permisos predeterminadas en el Portal de Azure clásico e identifica el **NOMBRE DE USUARIO** en la página **PERMISOS**. Sin embargo, no puede usar el portal clásico para agregar este grupo a una plantilla que se creó o importó manualmente; en su lugar, debe usar una de las siguientes opciones de Azure RMS PowerShell:

-   Use el cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) de PowerShell para definir el grupo "AllStaff" y los derechos como un objeto de definición de derechos, y ejecute de nuevo este comando para cada uno de los demás grupos o usuarios a los que ya se les ha otorgado derechos en la plantilla original además de para el grupo CUALQUIERA. A continuación, agregue estos objetos de definición de derechos a las plantillas mediante el cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx).

-   Use el cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar la plantilla a un archivo .XML que puede editar para agregar el grupo "AllStaff" y los derechos a los grupos y derechos existentes y, a continuación, use el cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para importar este cambio de nuevo en Azure RMS.

> [!NOTE]
> Este grupo equivalente "AllStaff" no es exactamente igual que el grupo TODOS de AD RMS:  el grupo "AllStaff" incluye todos los usuarios de su inquilino de Azure, mientras que el grupo TODOS incluye todos los usuarios autenticados, que podrían estar fuera de su organización.
> 
> Debido a esta diferencia entre los dos grupos, puede que tenga que agregar también usuarios externos además del grupo "AllStaff". Actualmente no se admiten direcciones de correo electrónico externas para grupos.

Las plantillas que se importan de AD RMS tienen el mismo aspecto y comportamiento que las plantillas personalizadas que se pueden crear en el Portal de Azure clásico. Para cambiar las plantillas importadas para publicarlas de modo que los usuarios puedan verlas y seleccionarlas desde las aplicaciones o para realizar otros cambios en las plantillas, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

> [!TIP]
> Para obtener una experiencia más coherente para los usuarios durante el proceso de migración, no realice cambios en las plantillas importadas aparte de estos dos y no publique las dos plantillas predeterminadas que vienen con Azure RMS ni cree plantillas nuevas en este momento. En su lugar, espere hasta que se complete el proceso de migración y haya dado de baja los servidores de AD RMS.

#### <a name="BKMK_ScriptForANYONE"></a>Script de ejemplo de Windows PowerShell para identificar plantillas de AD RMS que incluyen el grupo CUALQUIERA
Esta sección contiene el script de ejemplo que le ayuda a identificar plantillas de AD RMS que tienen definido el grupo CUALQUIERA, tal como se ha descrito en la sección anterior.

*&#42;&#42;Aviso de declinación de responsabilidades&#42;&#42;: Este script de ejemplo no es compatible en ningún servicio o programa de soporte estándar de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.*

```
import-module adrmsadmin New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force $ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate foreach($Template in $ListofTemplates) { $templateID=$Template.id $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright $templateName=$Template.DefaultDisplayName if ($rights.usergroupname -eq "anyone") { $templateName = $Template.defaultdisplayname write-host "Template " -NoNewline write-host -NoNewline $templateName -ForegroundColor Red write-host " contains rights for " -NoNewline write-host ANYONE  -ForegroundColor Red } } Remove-PSDrive MyRmsAdmin -force
```

### <a name="BKMK_Step5Migration"></a>Paso 5. Vuelva a configurar los clientes para usar Azure RMS.
Para los clientes de Windows:

1.  [Descargue los scripts de migración](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Estos scripts restablecen la configuración en los equipos de Windows para que usen el servicio de Azure RMS en lugar de AD RMS.

2.  Siga las instrucciones del script de redirección (Redirect_OnPrem.cmd) para modificarlo de forma que señale al nuevo inquilino de Azure RMS.

3.  En los equipos Windows, ejecute estos scripts con privilegios elevados en el contexto del usuario.

Para clientes de dispositivos móviles y equipos Mac:

-   Quite los registros de DNS SRV que creó cuando implementó la [extensión de AD RMS para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx).

#### Cambios realizados por los scripts de migración
En esta sección se documentan los cambios que hacen los scripts de migración. Puede utilizar esta información sólo con fines de referencia o para solucionar problemas o si prefiere hacer estos cambios usted mismo.

CleanUpRMS_RUN_Elevated.cmd:

-   Elimine el contenido de las carpetas %userprofile%\AppData\Local\Microsoft\DRM y %userprofile%\AppData\Local\Microsoft\MSIPC, incluidas todas las subcarpetas y los archivos con nombres de archivo largos.

-   Elimine el contenido de las claves del Registro siguientes:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Elimine los siguientes valores del Registro:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Cree los siguientes valores del Registro para cada dirección URL proporcionada como un parámetro en cada una de las siguientes ubicaciones:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Cada entrada tiene un valor REG_SZ de **https://OldRMSserverURL/_wmcs/licensing** con los datos en el siguiente formato: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* tiene el formato siguiente: **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Por ejemplo:  5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Para encontrar este valor, identifique el valor **RightsManagementServiceId** cuando ejecute el cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para Azure RMS.

### <a name="BKMK_Step6Migration"></a>Paso 6. Configure la integración de IRM en Exchange Online.
Si ha importado anteriormente el TDP desde AD RMS a Exchange Online, debe quitarlo para evitar conflictos de plantillas y directivas después de haber migrado a Azure RMS. Para ello, use el cmdlet [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) de Exchange Online.

Si eligió una topología de clave de inquilino de Azure RMS de **administrada por Microsoft**:

-   Vea la sección [Exchange Online: Configuración de IRM](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline) del tema [Configuración de aplicaciones para Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md). Esta sección incluye la ejecución de comandos típicos que conectan con el servicio de Exchange Online, importan la clave de inquilino de Azure RMS y habilitan la funcionalidad IRM para Exchange Online. Después de completar estos pasos, tendrá la funcionalidad completa de RMS con Exchange Online.

Si ha elegido una topología de clave de inquilino de Azure RMS **administrada por el cliente (BYOK)**:

-   Habrá reducido la funcionalidad de RMS con Exchange Online, como se describe en la sección [Precio y restricciones de BYOK](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) del tema [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

### <a name="BKMK_Step7Migration"></a>Paso 7. Implemente el conector RMS.
Si ha utilizado la funcionalidad Information Rights Management (IRM) de Exchange Server o SharePoint Server con AD RMS, primero debe deshabilitar IRM en estos servidores y quitar la configuración de AD RMS. A continuación, implemente el conector de Rights Management (RMS), que actúa como interfaz de comunicaciones (una retransmisión) entre los servidores locales y Azure RMS.

Por último, para este paso, si ha importado varios TPD en Azure RMS que se usaron para proteger los mensajes de correo electrónico, debe editar manualmente el registro en los equipos de Exchange Server para redirigir todas las direcciones URL de TPD al conector RMS.

> [!NOTE]
> Antes de empezar, compruebe las versiones admitidas de los servidores locales que son compatibles con el conector RMS en "Servidores locales compatibles con Azure RMS" [Aplicaciones que son compatibles con Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) del tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

##### Deshabilitar IRM en servidores de Exchange y quitar la configuración de AD RMS

1.  En cada servidor de Exchange, busque la carpeta siguiente y elimine todas las entradas de esa carpeta: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Desde uno de los servidores de Exchange, use el cmdlet [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) de Exchange para deshabilitar primero las características de IRM para los mensajes enviados a destinatarios internos:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  A continuación, utilice el mismo cmdlet para deshabilitar las características de IRM para los mensajes enviados a destinatarios externos:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  A continuación, use el mismo cmdlet para deshabilitar IRM en Microsoft Office Outlook Web App y en Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Por último, use el mismo cmdlet para borrar los certificados almacenados en la memoria caché:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  En cada Exchange Server, restablezca ahora IIS, por ejemplo, mediante la ejecución de un símbolo del sistema como administrador y escriba **iisreset**.

##### Deshabilitar IRM en servidores de SharePoint y quitar la configuración de AD RMS

1.  Asegúrese de que no hay ningún documento desprotegido desde bibliotecas protegidas con RMS. Si hay, quedarán inaccesibles al final de este procedimiento.

2.  En el sitio web de Administración central de SharePoint, en la sección **Inicio rápido**, haga clic en **Seguridad**.

3.  En la página **Seguridad**, en la página **Directiva de información**, haga clic en **Configurar Information Rights Management**.

4.  En la página **Information Rights Management**, en la sección **Information Rights Management**, seleccione **No use IRM en este servidor** y luego haga clic en **Aceptar**.

5.  En cada uno de los equipos de SharePoint Server, elimine el contenido de la carpeta \ProgramData\Microsoft\MSIPC\Server\*&lt;SID de la cuenta que ejecuta SharePoint Server&gt;*.

##### Instalar y configurar el conector RMS

-   Use las instrucciones del tema [Implementación del conector de Azure Rights Management](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

##### En Exchange solo y varios TPD: Editar el registro

-   En cada servidor Exchange, agregue manualmente las claves del Registro siguientes para cada TPD adicional que ha importado, para redirigir las direcciones URL de los TPD al conector RMS. Estas entradas del Registro son específicas para la migración y no se agregan mediante la herramienta de configuración de servidor para el conector RMS de Microsoft.

    Al realizar estas modificaciones del registro, utilice las siguientes instrucciones:

    -   Reemplace *ConnectorFQDN* por el nombre que definió en el DNS para el conector. Por ejemplo, **rmsconnector.contoso.com**.

    -   Use el prefijo HTTP o HTTPS para la dirección URL del conector, en función de si ha configurado el conector para usar HTTP o HTTPS para comunicarse con los servidores locales.

    **Para Exchange 2013:**

    |Ruta de acceso del registro|Tipo|Valor|Datos|
    |-------------------------------|--------|---------|---------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Intranet Licensing URL&gt;/_wmcs/licensing|Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/licensing<br />-   https://&lt;connectorName&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Extranet Licensing URL&gt;/_wmcs/licensing|Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/licensing<br />-   https://&lt;connectorFQDN&gt;/_wmcs/licensing|
    **Para Exchange Server 2010:**

    |Ruta de acceso del registro|Tipo|Valor|Datos|
    |-------------------------------|--------|---------|---------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Intranet Licensing URL&gt;/_wmcs/licensing|Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/licensing<br />-   https://&lt;connectorName&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Extranet Licensing URL&gt;/_wmcs/licensing|Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/licensing<br />-   https://&lt;connectorName&gt;/_wmcs/licensing|

Después de completar estos procedimientos, asegúrese de leer la sección **Pasos siguientes** del tema [Implementación del conector de Azure Rights Management](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

### <a name="BKMK_Step8Migration"></a>Paso 8. Retire AD RMS
Opcional: Quite el punto de conexión de servicio (SCP) de Active Directory para evitar que los equipos detecten la infraestructura local de Rights Management. Esta acción es opcional debido al redireccionamiento configurado en el registro (por ejemplo, al ejecutar el script de migración). Para quitar el punto de conexión de servicio, use la herramienta de registro de AD SCP desde el [kit de herramientas de administración de Rights Management Services](http://www.microsoft.com/download/details.aspx?id=1479).

Supervise la actividad de los servidores de AD RMS. Para ello, por ejemplo, compruebe las [solicitudes en el informe de mantenimiento del sistema](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [tabla ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) o realice una [auditoría del acceso de los usuarios a contenido protegido](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Cuando haya confirmado que los clientes de RMS ya no se comunican con estos servidores y que los clientes están utilizando Azure RMS correctamente, puede quitar el rol de servidor de AD RMS de estos servidores. Si usa servidores dedicados, es preferible aplicar una medida de cautela basada en cerrar primero los servidores durante un período de tiempo para asegurarse de que no hay ningún problema notificado que requiera reiniciar estos servidores para garantizar la continuidad del servicio mientras investiga por qué los clientes no usan Azure RMS.

Después de retirar los servidores de AD RMS, seguramente le interese revisar las plantillas en el Portal de Azure clásico y consolidarlas para que los usuarios tengan menos opciones entre las que elegir, volver a configurarlas o incluso agregar plantillas nuevas. También sería una buena oportunidad para publicar las plantillas predeterminadas. Para obtener más información, vea [Configuración de plantillas personalizadas para Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

### <a name="BKMK_Step9Migration"></a>Step 9. Vuelva a escribir su clave de inquilino de Azure RMS.
Este paso es necesario cuando la migración está completa si la implementación de AD RMS usaba el modo criptográfico 1 de RMS, porque al volver a escribir la clave se crea una nueva clave de inquilino que usa el modo criptográfico 2 de RMS. Se admite el uso de Azure RMS con el modo criptográfico 1 únicamente durante el proceso de migración.

Este paso es opcional pero se recomienda cuando la migración se ha completado incluso si estuviera ejecutando el modo criptográfico 2 de RMS, porque ayuda a proteger la clave de inquilino de Azure RMS de posibles infracciones de seguridad para su clave de AD RMS. Si vuelve a definir la clave de inquilino de Azure RMS (lo que también se conoce como "revertir su clave"), se crea una nueva clave y se archiva la clave original. Sin embargo, dado que el paso de una clave a otra no es inmediato, sino que requiere unas cuantas semanas, no espere hasta sospechar de una infracción de la clave original y, en su lugar, vuelva a definir la clave del inquilino de RMS en cuanto se complete la migración.

Vuelva a definir la clave del inquilino de Azure RMS:

-   Si Microsoft administra su clave de inquilino de RMS: llame a los servicios de soporte técnico de Microsoft (CSS) y demuestre que es el administrador del inquilino de RMS.

-   Si la clave de inquilino de RMS está administrada por el usuario (BYOK): Repita el procedimiento BYOK para generar y crear una nueva clave a través de Internet o en persona.

Para obtener más información acerca de la administración de la clave de inquilino de RMS, consulte [Operaciones para su clave de inquilino de Administración de permisos de Azure](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md).

## Vea también
[Configuración de Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

