---
description: na
keywords: na
title: Activating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
---
# Activar Rights Management de Azure
Cuando activa [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS), su organización puede empezar a proteger datos importantes con aplicaciones y servicios que admiten esta solución de protección de información. Los administradores también pueden administrar y supervisar los correos electrónicos y archivos protegidos que posee su organización. Debe habilitar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para poder empezar a usar las características de Information Rights Management (IRM) en Office, SharePoint y Exchange y proteger los archivos confidenciales o con información importante.

Si desea obtener más información sobre Azure Rights Management antes de activar el servicio (por ejemplo, problemas empresariales que soluciona, algunos casos de uso habitual y su funcionamiento), consulte [¿Qué es Rights Management de Azure?](../Topic/What_is_Azure_Rights_Management_.md)

> [!IMPORTANT]
> Antes de activar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], asegúrese de que la organización tenga un plan de servicios que incluya los de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. De lo contrario, no podrá activar Azure RMS.
> 
> Para obtener más información, consulte la sección [Suscripciones en la nube que son compatibles con Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) en el tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

Una vez activado Azure RMS, todos los usuarios de la organización podrán aplicar la protección de la información a los archivos y abrir (consumir) los archivos protegidos con Azure RMS. Sin embargo, si lo prefiere, puede usar controles de incorporación para restringir quién puede aplicar la protección de la información, a fin de realizar una implementación por fases. Para obtener más información, consulte la sección [Configuración de controles de incorporación para una implementación por fases](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls) de este tema.

## Activación de Rights Management
Use uno de los procedimientos siguientes para activar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

> [!TIP]
> También puede utilizar el cmdlet [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) de Windows PowerShell para activar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### Para activar Rights Management desde el centro de administración de Office 365

1.  Después de registrarse para obtener un plan de Office 365 que incluye Rights Management, [inicie sesión en Office 365 con su cuenta profesional o educativa](https://portal.office.com/) que sea administrador de su implementación de Office 365.

2.  Si el centro de administración de Office 365 no se muestra automáticamente, seleccione el icono del iniciador de aplicaciones en la parte superior izquierda y elija **Admin**. El icono **Admin** se muestra únicamente a los administradores de Office 365.

    > [!TIP]
    > Para obtener ayuda con el centro de administración, consulte [Sobre el Centro de administración de Office 365: ayuda para el administrador](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  En el panel izquierdo, expanda **CONFIGURACIÓN DEL SERVICIO**.

4.  Haga clic en **Rights Management**.

    > [!NOTE]
    > Si no ve esta opción, es posible que sea porque su plan de servicios o la versión del producto no pueden admitir Rights Management, o porque todavía no ha sido actualizado para ser compatible con Rights Management.
    > 
    > Use la información que aparece en la sección [Suscripciones en la nube que son compatibles con Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) del tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) para confirmar la compatibilidad. Si su plan de servicio o la versión del producto es compatible, pero no ve la opción Rights Management, es posible que se deba a que el servicio no se ha actualizado todavía. Para obtener ayuda con este problema, envíe un mensaje de correo electrónico a [askipteam](mailto:askipteam@microsoft.com?subject=I%20cannot%20activate%20RMS).

5.  En la página **RIGHTS MANAGEMENT**, haga clic en **Administrar**.

6.  En la página **Rights Management**, haga clic en **Activar**.

7.  Cuando se le pregunte **¿Desea activar Rights Management?**, haga clic en **Activar**.

Ahora debería ver **Rights Management está activada** y la opción para desactivar.

#### Para activar Rights Management desde el Portal de Azure clásico

1.  Después de registrarse para obtener la cuenta de Azure, [inicie sesión en el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

3.  En la página **Active Directory**, haga clic en **RIGHTS MANAGEMENT**.

4.  Seleccione el directorio que administrará para [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], haga clic en **ACTIVAR** y confirme la acción.

    > [!NOTE]
    > Si ve un error de activación, es posible que el plan de servicio o la versión del producto no sean compatibles con [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].
    > 
    > Use la información que aparece en la sección [Suscripciones en la nube que son compatibles con Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) del tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) para confirmar la compatibilidad de RMS. Para obtener ayuda con este problema, envíe un mensaje de correo electrónico a [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).

El **ESTADO DE RIGHTS MANAGEMENT** debe indicar ahora **Activo** y la opción **ACTIVAR** debe aparecer reemplazada por **DESACTIVAR**.

### Descripciones y valores de estado de Rights Management en el Portal de Azure clásico.
Además del estado **Activo**, que indica que el servicio de Rights Management está habilitado y listo para usarse, es posible que también vea **Inactivo**, **No disponible** o **No autorizado**.

|Valor de estado|Descripción|
|-------------------|---------------|
|**Activa**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] está habilitado y listo para usarse.|
|**Inactivo**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] está deshabilitado y se debe activar antes de que la organización pueda proteger archivos.|
|**No disponible**|El servicio [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] está inactivo. Inténtelo de nuevo más tarde.|
|**No autorizado**|No tiene permisos para ver el estado del servicio [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. Por ejemplo, su cuenta está bloqueada o no es el administrador global del inquilino seleccionado.|

## <a name="BKMK_OnboardingControls"></a>Configuración de controles de incorporación para una implementación por fases
Si no desea que todos los usuarios puedan proteger los archivos de forma inmediata con Azure RMS, puede configurar controles de incorporación para el usuario mediante el comando [Set AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) de Windows PowerShell. Puede ejecutar este comando antes o después de activar Azure RMS.

> [!IMPORTANT]
> Para usar este comando, debe tener al menos la versión **2.1.0.0** del [módulo Azure RMS Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Para comprobar la versión instalada, ejecute: **(Get-Module aadrm –ListAvailable).Version**

Por ejemplo, si en principio desea que solo los administradores del grupo "Departamento de TI" (con un identificador de objeto de fbb99ded-32a0-45f1-b038-38b519009503) puedan proteger el contenido con fines de prueba, use el comando siguiente:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Tenga en cuenta que para esta opción de configuración, debe especificar un grupo; no puede especificar usuarios individuales.

O bien, si desea asegurarse de que solo los usuarios con licencias adecuadas para usar Azure RMS puedan proteger el contenido:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Al usar estos controles de incorporación, todos los usuarios de la organización podrán consumir siempre el contenido protegido por el subconjunto de usuarios, pero no podrán aplicar la protección de la información ellos mismos desde aplicaciones cliente. Por ejemplo, no verán en sus clientes de Office las plantillas predeterminadas publicadas automáticamente al activar Azure RMS o las plantillas personalizadas que pueda configurar.  Las aplicaciones de servidor, como Exchange, pueden implementar sus propios controles por usuario para la integración de RMS lograr el mismo resultado.

## Pasos siguientes
Ahora que ha activado [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] para su organización, use la [Plan para la implementación de Azure Rights Management](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) para comprobar si hay otros pasos de configuración que puedan ser necesarios antes de revertir [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] a usuarios y administradores. Por ejemplo, es posible que desee utilizar [plantillas personalizadas](http://technet.microsoft.com/library/dn642472.aspx) para permitir que para los usuarios sea más fácil aplicar la protección de la información a los archivos, conectarse a los servidores locales para usar [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] a través de la instalación del [conector RMS](http://technet.microsoft.com/library/dn375964.aspx) e implementar la [aplicación de Rights Management sharing](http://technet.microsoft.com/library/jj585031.aspx) que es compatible con la protección de todos los tipos de archivo en todos los dispositivos. Servicios de Office, como Exchange Online y SharePoint Online requieren configuración adicional para poder usar sus características de Information Rights Management (IRM). Sin embargo, si no es necesario ningún otro paso de configuración, vea [Uso de Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) para obtener instrucciones de funcionamiento para apoyar una implementación correcta en su organización.

Para obtener información sobre cómo funcionan las aplicaciones con [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], consulte [Cómo son compatibles las aplicaciones con Azure Rights Management](../Topic/How_Applications_Support_Azure_Rights_Management.md).

## Vea también
[Configuración de Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

