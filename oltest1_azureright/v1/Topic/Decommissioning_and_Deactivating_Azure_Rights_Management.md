---
description: na
keywords: na
title: Decommissioning and Deactivating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
---
# Retirada y desactivaci&#243;n de Azure Rights Management
Siempre controla si su organización protege el contenido mediante [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS), y si decide dejar de usar esta solución de protección de información, puede tener la certeza de que no se le bloqueará el acceso al contenido que anteriormente se protegió. Si ya no necesita tener acceso continuo al contenido protegido con anterioridad, simplemente desactive el servicio y deje que su suscripción a Azure Rights Management expire. Por ejemplo, esto sería apropiado cuando haya completado la evaluación de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], antes de implementarlo en un entorno productivo.

Sin embargo, si implementó [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] en producción, asegúrese de que tiene una copia de la clave de inquilino de Azure Rights Management antes de desactivar el servicio, y hágalo antes de que su suscripción expire, porque así se asegurará de mantener el acceso al contenido protegido con Azure Rights Management después de desactivar el servicio. Si usó la solución Aportar su propia clave (BYOK), que genera y administra su propia clave en un HSM, ya dispondrá de su clave de inquilino de Azure Rights Management. Sin embargo, si estaba administrada por Microsoft (valor predeterminado), debe consultar las instrucciones para exportar su clave de inquilino en el tema [Operaciones para su clave de inquilino de Administración de permisos de Azure](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md).

> [!TIP]
> Incluso después de que expire la suscripción, el inquilino de Azure Rights Management sigue estando disponible para consumir contenido durante un período prolongado. Sin embargo, ya no podrá exportar su clave de inquilino.

Cuando tenga su clave de inquilino de Azure Rights Management, puede implementar Rights Management localmente (AD RMS) e importar su clave de inquilino como dominio de publicación de confianza (TPD). A continuación, tiene las siguientes opciones para retirar la implementación de Azure Rights Management:

|Si este es su caso...|… haz esto:|
|-------------------------|---------------|
|Desea que todos los usuarios sigan usando Rights Management, pero usa una solución local en lugar de Azure RMS    →|Use el cmdlet [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) para dirigir a los usuarios existentes a su implementación local cuando consuman contenido protegido después de este cambio. Los usuarios usarán automáticamente la instalación de AD RMS para consumir el contenido protegido.<br /><br />Para que los usuarios consuman contenido que se protegió antes de este cambio, redirija los clientes a la implementación local mediante la clave del Registro **LicensingRedirection** para Office 2016 u Office 2013, como se describe en la sección [Detección del servicio](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) en las notas de implementación del cliente de RMS, y la clave del Registro **LicenseServerRedirection** para Office 2010, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Desea dejar de usar por completo las tecnologías de Rights Management    →|Conceda [derechos de superusuario](https://technet.microsoft.com/library/mt147272.aspx) a un administrador designado y proporciónele la [herramienta de protección de RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Este administrador puede usar la herramienta para descifrar masivamente archivos de carpetas protegidos con Azure Rights Management, de modo que los archivos vuelvan a estar desprotegidos y se puedan leer sin una tecnología de Rights Management, como Azure RMS o AD RMS. Esta herramienta puede usarse con Azure RMS y con AD RMS, por lo que tendrá la posibilidad de descifrar archivos antes o después de desactivar Azure RMS, o una combinación de ambos.|
|No es capaz de identificar todos los archivos que se protegieron con Azure RMS, o desea que todos los usuarios puedan leer automáticamente los archivos protegidos que se perdieron    →|Implemente una configuración del Registro en todos los equipos cliente mediante la clave del Registro **LicensingRedirection** para Office 2016, como se describe en la sección [Detección del servicio](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) en las notas de implementación del cliente de RMS, y la clave del Registro **LicenseServerRedirection** para Office 2010, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Asimismo, implemente otra configuración del Registro para impedir que los usuarios protejan archivos nuevos estableciendo **DisableCreation** en **1**, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Necesita un servicio de recuperación manual y controlada para los archivos que se perdieron    →|Conceda [derechos de superusuario](https://technet.microsoft.com/library/mt147272.aspx) a los usuarios designados de un grupo de recuperación de datos y proporcióneles la [herramienta de protección de RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) para que puedan desproteger archivos cuando se lo soliciten los usuarios estándar.<br /><br />En todos los equipos, implemente la configuración del Registro para impedir que los usuarios protejan archivos nuevos estableciendo **DisableCreation** en **1**, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Para más información sobre los procedimientos descritos en esta tabla, consulte los recursos siguientes:

-   Para obtener información sobre AD RMS y referencias de implementación, vea [Introducción a Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx).

-   Para obtener instrucciones sobre cómo importar la clave de inquilino de Azure RMS como archivo TPD, consulte [Agregar un dominio de publicación de confianza](https://technet.microsoft.com/library/cc771460.aspx).

-   Para instalar el módulo de Windows PowerShell para Azure RMS, para establecer la dirección URL de migración, consulte [Instalación de Windows PowerShell para Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Cuando esté preparado para desactivar el servicio de Azure RMS para su organización, siga las instrucciones que se indican a continuación.

## Desactivación de Rights Management
Use uno de los procedimientos siguientes para desactivar [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

> [!TIP]
> También puede usar el cmdlet [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) de Windows PowerShell para desactivar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### Para desactivar Rights Management desde el centro de administración de Office 365

1.  [Inicie sesión en Office 365 con su cuenta profesional o educativa](https://portal.office.com/) que sea administrador en la implementación de Office 365.

2.  Si no se muestra automáticamente el Centro de administración de Office 365, seleccione el icono del iniciador de aplicaciones en la parte superior izquierda y elija **Administrador**. El icono **Admin** se muestra únicamente a los administradores de Office 365.

    > [!TIP]
    > Para obtener ayuda con el centro de administración, consulte [Sobre el Centro de administración de Office 365: ayuda para el administrador](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  En el panel izquierdo, expanda **CONFIGURACIÓN DEL SERVICIO**.

4.  Haga clic en **Rights Management**.

5.  En la página **RIGHTS MANAGEMENT**, haga clic en **Administrar**.

6.  En la página **Rights Management**, haga clic en **Desactivar**.

7.  Cuando el sistema le pregunte **¿Desea desactivar Rights Management?**, haga clic en **Desactivar**.

Ahora debería ver **Rights Management no está activado** y la opción para activarlo.

#### Para desactivar Rights Management desde el Portal de Azure

1.  Inicie sesión en el [Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

3.  En la página **Active Directory**, haga clic en **RIGHTS MANAGEMENT**.

4.  Seleccione el directorio que desea administrar para [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], haga clic en **DESACTIVAR** y confirme la acción.

El **ESTADO DE RIGHTS MANAGEMENT** debe indicar ahora **Inactivo** y la opción **DESACTIVAR** debe aparecer reemplazada por **ACTIVAR**.

## Vea también
[Configuración de Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

