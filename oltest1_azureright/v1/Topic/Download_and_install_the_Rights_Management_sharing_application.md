---
description: na
keywords: na
title: Download and install the Rights Management sharing application
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
---
# Descargar e instalar la aplicaci&#243;n para uso compartido de Rights Management
No hace falta que sea un administrador local para instalar la aplicación RMS sharing. Sin embargo, si no lo es y usa Office 2010, hay algunas limitaciones. Para obtener más información, consulte la sección [Si no es un administrador local y usa Office 2010](#BKMK_SetupOffice2010) de este tema.

### Para descargar e instalar la aplicación Rights Management sharing

1.  Vaya a la página de [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft.

2.  En la sección **Equipos**, haga clic en el icono de la **aplicación RMS para Windows** y guarde el archivo **Setup.exe** para instalar la aplicación Microsoft Rights Management sharing.

3.  Haga doble clic en el archivo Setup.exe que se descargó. Si el sistema le pregunta si desea continuar, haga clic en **Sí**.

4.  En la página **Instalar Microsoft RMS**, haga clic en **siguiente** y espere a que finalice la instalación.

    > [!NOTE]
    > La aplicación RMS sharing requiere Microsoft .NET Framework, versión mínima 4.0. El programa de instalación comprueba si está instalado y, si no es así, verá un mensaje con un vínculo para instalarlo.

5.  Cuando finalice la instalación, haga clic en **Reiniciar** para reiniciar el equipo y completar la instalación. O bien, haga clic en **Cerrar** y reinicie el equipo más tarde para completar la instalación.

Ahora ya puede empezar a proteger sus archivos o a leer los archivos protegidos por otros usuarios.

## <a name="BKMK_SetupOffice2010"></a>Si no es un administrador local y usa Office 2010
Si inicia sesión en el equipo y no tiene derechos administrativos locales y el programa de instalación detecta que tiene instalado Office 2010, verá un mensaje de advertencia en el que se le indicará que algunos escenarios no funcionarán con tal configuración. Los escenarios son los siguientes:

-   Si su organización usa Azure RMS en lugar de una versión local de RMS:

    -   Las características de Information Rights Management (IRM) de Office no estarán disponibles. Por ejemplo, la opción **No reenviar** de los mensajes de correo electrónico y los permisos **Restringir acceso** que puede establecer desde el menú **Archivo** de Word y Excel. Puede usar la opción Uso compartido protegido de la cinta y las opciones del botón derecho del Explorador de archivos.

-   Si su organización usa una versión local de RMS en lugar de Azure RMS:

    -   No podrá leer un documento protegido que le envíe alguien de otra organización que use Azure RMS.

Si no es un administrador local y usa Office 365 u Office 2013, no verá este mensaje y se admitirán estos escenarios.

Puede continuar la instalación con estas limitaciones conocidas. Asimismo, puede detener la instalación y volver a ejecutarla con la opción **Ejecutar como administrador** al ejecutar Setup.exe en el paso 3, o bien pedirle a un administrador que se lo instale. Los administradores pueden [crear un script para esta instalación](https://technet.microsoft.com/library/dn339003.aspx) para que se instale automáticamente.

## Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [¿Qué desea hacer?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Vea también
[Guía de usuario de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_user_guide.md)

