---
description: na
keywords: na
title: Administering Azure Rights Management by Using Windows PowerShell
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
---
# Administraci&#243;n de Azure Rights Management mediante Windows PowerShell
Aunque puede activar Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) mediante el centro de administración de [!INCLUDE[o365_2](../Token/o365_2_md.md)] o en el Portal de Azure clásico, también puede usar el módulo de Windows PowerShell para que [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (AADRM) lo haga.

Tras haber activado [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], no será necesario seguir con la administración de este servicio. Sin embargo, puede que algunos escenarios de configuración avanzada precisen que se use el módulo Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. La tabla siguiente enumera algunos de los escenarios de configuración avanzada que usan Windows PowerShell. Para una lista completa de los cmdlets disponibles con más información acerca de cada uno de ellos, consulte [Cmdlets de Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Si tiene que instalar el módulo Windows PowerShell para [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], consulte [Instalación de Windows PowerShell para Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

También hay un módulo complementario de Windows PowerShell, **RMSProtection**, que admite Azure RMS y AD RMS. Este módulo permite proteger y desproteger varios archivos para que, por ejemplo, pueda proteger masivamente todos los archivos de una carpeta. Para obtener más información, consulte la sección [Opciones de script para superusuarios](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md#BKMK_RMSProtectionModule) en el tema [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

|Si tienes que…|…usar los cmdlets siguientes|
|------------------|--------------------------------|
|Migrar de Rights Management local (AD RMS o Windows RMS) a [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Conéctese o desconéctese desde el servicio [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] a su organización.|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Genera y administra tu propia clave de inquilino; el escenario Aportar tu propia clave (BYOK).|[Add-AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Active o desactive el servicio [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para su organización.|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Deshabilitar o habilitar el sitio de seguimiento de documentos de Azure Rights Management.|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Configurar los controles de incorporación para una implementación por fases de Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Crea y administra plantilla de directiva de derechos para su organización.|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Configurar el número máximo de días que se puede acceder al contenido que protege su organización sin una conexión a Internet (el período de validez de la licencia de uso).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Administra la función del superusario de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para tu organización.|[Enable–AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629405.aspx)|
|Administra usuarios y grupos que estén autorizados a administrar el servicio [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para tu organización.|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Obtén un registro de las tareas administrativas de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para tu organización.|[Get-AadrmAdminLog](http://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Registre y analice el registro de uso para [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Enable-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629421.aspx)<br /><br />[Get-AadrmUsageLog](http://msdn.microsoft.com/library/azure/dn629401.aspx)<br /><br />[Get-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629425.aspx)<br /><br />[Get-AadrmUsageLogLastCounterValue](http://msdn.microsoft.com/library/azure/dn629423.aspx)<br /><br />[Get-AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629419.aspx)<br /><br />[Set-AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629426.aspx)<br /><br />[Disable-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629404.aspx)|
|Muestre la configuración actual del servicio [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para su organización.|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Migre su organización desde [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] a una implementación de AD RMS local.|[Set-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get–AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

## Vea también
[Administración de los derechos de Azure](../Topic/Azure_Rights_Management.md)

