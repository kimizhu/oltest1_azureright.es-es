---
description: na
keywords: na
title: Installing Windows PowerShell for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
---
# Instalaci&#243;n de Windows PowerShell para Azure Rights Management
Use la información siguiente para instalar Windows PowerShell para Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS).

Puede utilizar este módulo de Windows PowerShell para administrar [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] desde la línea de comandos mediante el uso de cualquier equipo que tenga una conexión a Internet y que cumpla los requisitos previos enumerados en la sección siguiente. Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] admite el uso de scripting para la automatización o puede que sea necesario para escenarios de configuración avanzada. Para obtener más información acerca de las tareas de administración y las configuraciones que admite el módulo, consulte [Administración de Azure Rights Management mediante Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Requisitos previos
Esta tabla enumera los requisitos previos para instalar Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

|Requisito|Más información|
|-------------|-------------------|
|Una versión de Windows que admita el módulo de administración [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]|Revise la lista de sistemas operativos compatibles en la sección **Requisitos del sistema** de la [página de descargas de la herramienta de administración de Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Versión mínima de Windows PowerShell: 2.0|El soporte para el módulo de administración [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] se presenta en Windows PowerShell 2.0.<br /><br />De forma predeterminada, la mayoría de sistemas operativos de Windows se instalan con una versión 2.0 de Windows PowerShell, como mínimo. Si necesita instalar Windows PowerShell 2.0, consulte [Instalación de Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx).<br /><br />Sugerencia: Puede confirmar la versión de Windows PowerShell que se está ejecutando. Para ello, escriba **$PSVersionTable** en una sesión de Windows PowerShell.|
|Versión mínima de Microsoft .NET Framework: 4.5<br /><br />Nota: Esta versión de Microsoft .NET Framework está incluida con los últimos sistemas operativos, por lo que solo tendrá que instalarla manualmente en el caso de que el sistema operativo del cliente sea anterior a Windows 8.0 o de que el sistema operativo del servidor sea anterior a Windows Server 2012.|Si la versión mínima de Microsoft .NET Framework todavía no está instalada, puede descargar [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Esta versión mínima de Microsoft .NET Framework es necesaria para algunas de las clases que usa el módulo de administración de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|
|Ayudante para el inicio de sesión de Microsoft Online Services 7.0|Microsoft Online Services - Ayudante para el inicio de sesión es obligatorio para la autenticación de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].<br /><br />Para obtener más información, vea [Centro de descarga: Ayudante de Microsoft Online Services para profesionales de TI RTW](http://www.microsoft.com/en-us/download/details.aspx?id=41950).|

## Cómo instalar el módulo de administración Rights Management

1.  Vaya al Centro de descarga de Microsoft y [descargue la herramienta de administración de Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721), que contiene el módulo de administración de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] para Windows PowerShell.

2.  En la carpeta local en la que descargó y guardó el archivo de instalación de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], haga doble clic en el archivo ejecutable que descargó para su plataforma (WindowsAzureADRightsManagementAdministration_x64 o WindowsAzureADRightsManagementAdministration_x86.exe) para iniciar el asistente para la configuración de administración Azure AD Rights Management.

3.  Completa el asistente.

Ahora ya se ha instalado Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

## Pasos siguientes
Para consultar los cmdlets disponibles, inicie Windows PowerShell con la opción **Ejecutar como administrador** y escriba lo que se indica a continuación:

```
Get-Command -Module aadrm
```
Use el comando `the Get-Help <cmdlet_name>` para consultar la Ayuda para un cmdlet específico.

Para obtener más información:

-   Lista completa de cmdlets disponibles: [Cmdlets de Azure Rights Management](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Lista de los principales escenarios de configuración que admiten Windows PowerShell: [Administración de Azure Rights Management mediante Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

Antes de poder ejecutar cualquier comando que configure el servicio de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], debe conectarse al servicio con el cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx). Cuando termine de ejecutar los comandos de configuración que desea, desconéctese del servicio con el cmdlet [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx).

> [!NOTE]
> Si todavía no ha activado [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], puede hacerlo después de haberse conectado al servicio, mediante el cmdlet [Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx).

## Vea también
[Administración de Azure Rights Management mediante Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

