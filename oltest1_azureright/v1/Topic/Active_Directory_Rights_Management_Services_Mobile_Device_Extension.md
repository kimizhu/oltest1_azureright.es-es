---
description: na
keywords: na
title: Active Directory Rights Management Services Mobile Device Extension
search: na
ms.date: na
ms.tgt_pltfrm: na
ms.assetid: a69ead9d-7dd3-4b38-9830-4728e9757341
robots: noindex,nofollow
---
# Extensi&#243;n para dispositivos m&#243;viles de Active Directory Rights Management Services
La extensión para dispositivos móviles de Active Directory Rights Management Services (AD RMS) se ejecuta sobre una implementación de AD RMS existente. Esto permite a los usuarios con dispositivos móviles proteger y consumir datos confidenciales si su dispositivo es compatible con el cliente de RMS más reciente y usa aplicaciones habilitadas para RMS. Por ejemplo, los usuarios con estos dispositivos pueden hacer lo siguiente:

-   Usar la aplicación para uso compartido de RMS con el fin de consumir archivos de texto protegidos en formatos diferentes (incluidos .txt, .csv y .xml).

-   Usar la aplicación para uso compartido de RMS con el fin de consumir archivos de imagen protegidos (incluidos .jpg, .gif y .tif).

-   Usar la aplicación para uso compartido de RMS con el fin de abrir cualquier archivo que se haya protegido de forma genérica (formato .pfile).

-   Usar la aplicación para uso compartido de RMS con el fin de proteger archivos de imagen en el dispositivo.

-   Usar un visor de PDF habilitado para RMS para dispositivos móviles con el fin de abrir archivos PDF protegidos con la aplicación para uso compartido de RMS para Windows u otra aplicación habilitada para RMS.

-   Usar otras aplicaciones de proveedores de software que proporcionan aplicaciones habilitadas para RMS que admiten tipos de archivo compatibles con RMS de forma nativa.

-   Usar aplicaciones habilitadas para RMS desarrolladas internamente que se hayan escrito con el SDK de RMS.

> [!NOTE]
> Puede descargar la aplicación para uso compartido de RMS de la página [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) del sitio web de Microsoft.
> 
> Para obtener más información sobre los distintos tipos de archivo que admite RMS, consulte la sección [Tipos de archivo y extensiones de nombre de archivo compatibles](http://technet.microsoft.com/library/dn339003.aspx) en la Guía del administrador de la aplicación para uso compartido de Rights Management.

No necesita la extensión para dispositivos móviles si desea consumir o crear correos electrónicos protegidos en dispositivos que usan aplicaciones de correo electrónico compatibles con Exchange ActiveSync IRM. Esta compatibilidad nativa con RMS y dispositivos móviles se introdujo con Exchange 2010 Service Pack 1.

Consulte las siguientes secciones para implementar la extensión para dispositivos móviles de Active Directory Rights Management Services (AD RMS):

-   [Requisitos previos de la extensión para dispositivos móviles de AD RMS](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_Preqs)

    -   [Configurar AD FS para la extensión para dispositivos móviles de AD RMS](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS)

    -   [Configurar AD FS para la extensión para dispositivos móviles de AD RMS](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS)

-   [Especificar los registros de servidor DNS para la extensión para dispositivos móviles de AD RMS](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_SRV)

-   [Implementar la extensión para dispositivos móviles de AD RMS](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_Deploy)

## <a name="BKMK_Preqs"></a>Requisitos previos de la extensión para dispositivos móviles de AD RMS
Antes de instalar la extensión para dispositivos móviles de AD RMS, asegúrese de que estas dependencias están en vigor.

|Requisito|Información adicional|
|-------------|-------------------------|
|Implementación existente de AD RMS en Windows Server 2012 R2 o Windows Server 2012. **Note:** AD RMS debe usar una base de datos completa de Microsoft SQL basada en servidor en un servidor independiente, en lugar de Windows Internal Database, que a menudo se usa para realizar pruebas en el mismo servidor.|Para obtener documentación sobre AD RMS, consulte [Active Directory Rights Management Services](http://technet.microsoft.com/library/hh831364.aspx) en la biblioteca de Windows Server.|
|AD FS implementado en Windows Server 2012 R2|Para obtener documentación sobre AD FS, consulte [Guía de implementación de Windows Server 2012 R2 AD FS](http://technet.microsoft.com/library/dn486820.aspx) en la biblioteca de Windows Server.<br /><br />AD FS debe configurarse para la extensión para dispositivos móviles. Para obtener instrucciones, consulte la sección [Configurar AD FS para la extensión para dispositivos móviles de AD RMS](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_ADFS) de este tema.|
|Registros de servidor DNS|Cree uno o más registros de servidor en los dominios de la empresa:<br /><br />-   Un registro para cada sufijo de dominio de correo electrónico que usarán los usuarios<br />-   Un registro para cada FQDN usado por los clústeres de RMS para proteger el contenido<br /><br />Cuando los usuarios proporcionan su dirección de correo electrónico desde un dispositivo móvil, se usa el sufijo de dominio para identificar si se debe usar una infraestructura de AD RMS o Azure RMS. Cuando se encuentra el registro de servidor, los clientes se redirigen al servidor de AD RMS que responde a esa dirección URL.<br /><br />Cuando los usuarios consumen contenido protegido con un dispositivo móvil, la aplicación cliente busca en DNS un registro que coincida con el FQDN de la dirección URL del clúster que protegió el contenido. A continuación, el dispositivo se dirige al clúster de AD RMS especificado en el registro de DNS y adquiere una licencia para abrir el contenido. En la mayoría de los casos, el clúster de RMS será el mismo clúster que protegió el contenido.<br /><br />Para obtener información sobre cómo especificar registros de SRV, consulte la sección [Especificar los registros de servidor DNS para la extensión para dispositivos móviles de AD RMS](../Topic/Active_Directory_Rights_Management_Services_Mobile_Device_Extension.md#BKMK_SRV) de este tema.|
|Clientes admitidos actualmente:<br /><br />-   Dispositivos Android que usan la última versión de la aplicación para uso compartido de RMS para Android|Versión mínima: Android 4.0.3.<br /><br />Descargue la aplicación para uso compartido de RMS para Android desde el [sitio de Microsoft Connect](https://connect.microsoft.com/site1170/Downloads) y transfiérala localmente al dispositivo.|

### <a name="BKMK_ADFS"></a>Configurar AD FS para la extensión para dispositivos móviles de AD RMS
Primero debe configurar AD FS y, a continuación, autorizar la aplicación para uso compartido de RMS para Android.

##### Paso 1: Para configurar AD FS

-   Puede ejecutar un script de Windows PowerShell para configurar automáticamente AD FS de modo que admita la extensión para dispositivos móviles de AD RMS, o bien puede especificar manualmente los valores y las opciones de configuración:

    -   Para configurar automáticamente AD FS, copie y pegue lo siguiente en un archivo de script de Windows PowerShell y después ejecútelo:

        ```
        # This Script Configures the Microsoft Rights Management Mobile Device Extension and Claims used in the ADFS Server

        # Check if Microsoft Rights Management Mobile Device Extension is configured on the Server 
        $CheckifConfigured = Get-AdfsRelyingPartyTrust -Identifier "api.rms.rest.com"
        if ($CheckifConfigured)
        {
        Write-Host "api.rms.rest.com Identifer used for Microsoft Rights Management Mobile Device Extension is already configured on this Server"
        Write-Host $CheckifConfigured 
        }
        else
        {
        Write-Host "Configuring  Microsoft Rights Management Mobile Device Extension "

        # TransformaRules used by Microsoft Rights Management Mobile Device Extension
        # Claims: E-mail, UPN and ProxyAddresses
        $TransformRules = @"
        @RuleTemplate = "LdapClaims"
        @RuleName = "Jwt Token"
        c:[Type ==
        "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname",
        Issuer == "AD AUTHORITY"]
         => issue(store = "Active Directory", types =
        ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn",
        "http://schemas.xmlsoap.org/claims/ProxyAddresses"), query =
        ";mail,userPrincipalName,proxyAddresses;{0}", param = c.Value);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through"
        c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"]
         => issue(claim = c);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through"
        c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"]
         => issue(claim = c);

        @RuleTemplate = "PassThroughClaims"
        @RuleName = "JWT pass through Proxy addresses"
        c:[Type == "http://schemas.xmlsoap.org/claims/ProxyAddresses"]
         => issue(claim = c);
        "@

        # AuthorizationRules used by Microsoft Rights Management Mobile Device Extension
        # Allow All users
        $AuthorizationRules = @"
        @RuleTemplate = "AllowAllAuthzRule"
         => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit",
        Value = "true");
        "@

        # Add a Relying Part Truest with Name -"Microsoft Rights Management Mobile Device Extension" Identifier "api.rms.rest.com"
        Add-ADFSRelyingPartyTrust -Name "Microsoft Rights Management Mobile Device Extension" -Identifier "api.rms.rest.com" -IssuanceTransformRules $TransformRules -IssuanceAuthorizationRules  $AuthorizationRules

        Write-Host "Microsoft Rights Management Mobile Device Extension Configured"
        }
        ```

    -   Para configurar manualmente AD FS, use estos valores:

        |Configuración|Value|
        |-----------------|---------|
        |**Relación de confianza para usuario autenticado**|api.rms.rest.com|
        |**Regla de notificaciones**|**Almacén de atributos**:  Active Directory<br /><br />**Direcciones de correo electrónico**:  E-Mail-Address<br /><br />**Nombre principal de usuario**:  UPN<br /><br />**Dirección del proxy**:  https://schemas.xmlsoap.org/claims/ProxyAddresses|

##### Paso 2: Autorizar la aplicación para uso compartido de RMS para Android

-   Ejecute el siguiente comando de Windows PowerShell para agregar compatibilidad para dispositivos Android:

    ```
    Add-AdfsClient -Name "RMSsharingAndroid" -ClientId "com.microsoft.ipviewer" -RedirectUri @("com.microsoft.ipviewer://authorize")
    ```

### <a name="BKMK_SRV"></a>Especificar los registros de servidor DNS para la extensión para dispositivos móviles de AD RMS
Debe crear registros de servidor DNS para cada dominio de correo electrónico que usen los usuarios. Si todos los usuarios usan dominios secundarios de un solo dominio primario y todos los usuarios de este espacio de nombres contiguo usan el mismo clúster de RMS, puede usar un solo registro de servidor en el dominio primario, y RMS encontrará los registros de DNS apropiados.

Los registros de servidor tienen el formato siguiente: _rmsdisco._http._tcp. *&lt;sufijo de correo electrónico&gt;**&lt;número de puerto&gt;**&lt;FQDN de clúster de RMS&gt;*

Por ejemplo, si su empresa tiene usuarios con las siguientes direcciones de correo electrónico:

-   user@contoso.com

-   user@sales.contoso.com

-   user@fabrikam.com

- y no hay otros dominios secundarios para contoso.com que usen un clúster de RMS distinto al denominado **rmsserver.contoso.com**, cree dos registros de servidor DNS que tengan estos valores:

-   _rmsdisco._http._tcp.contoso.com 443 rmsserver.contoso.com

-   _rmsdisco._http._tcp.fabrikam.com 443 rmsserver.contoso.com

Además de estos registros de servidor DNS para los dominios de correo electrónico, debe crear otro registro de servidor DNS en los dominios de usuario. Este registro debe especificar las direcciones URL de su clúster de RMS que protege el contenido. Todos los archivos protegidos por RMS incluyen la dirección URL del clúster que protege dichos archivos. Los dispositivos móviles usan el registro de servidor DNS y el FQDN de la dirección URL especificado en el registro para encontrar el clúster de RMS que puede admitir dispositivos móviles.

Por ejemplo, si el clúster de RMS es **rmsserver.contoso.com**, cree un registro de servidor DNS que tenga los siguientes valores: **_rmsdisco._http._tcp.rmsserver.contoso.com 443 rmsserver.contoso.com**

## <a name="BKMK_Deploy"></a>Implementar la extensión para dispositivos móviles de AD RMS
Antes de instalar la extensión para dispositivos móviles de AD RMS, asegúrese en primer lugar de que se cumplen los requisitos previos de la sección anterior y de que conoce la dirección URL de su servidor de AD FS. A continuación, haga lo siguiente:

1.  Descargue la extensión de dispositivo móvil de AD RMS del [sitio de Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=397245).

2.  Ejecute Setup.exe para iniciar el Asistente para la instalación de la extensión para dispositivos móviles de Active Directory Rights Management Services.

3.  Cuando se le solicite, escriba la dirección URL del servidor de AD FS que configuró anteriormente.

4.  Complete el asistente.

Ejecute este asistente en todos los nodos del clúster de RMS.

