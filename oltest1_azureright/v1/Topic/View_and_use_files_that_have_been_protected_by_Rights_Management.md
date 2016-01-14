---
description: na
keywords: na
title: View and use files that have been protected by Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
---
# Ver y usar archivos que han sido protegidos con Rights Management
Cuando la [aplicación de uso compartido Rights Management (RMS) está instalada en el equipo](https://technet.microsoft.com/library/dn574734%28v=ws.10%29.aspx), puede ver un archivo protegido simplemente haciendo doble clic en él. El archivo puede ser un archivo adjunto en un mensaje de correo electrónico, o podría verlo al usar el Explorador de archivos.

> [!NOTE]
> Para poder ver el archivo protegido, RMS debe confirmar primero que está autorizado para ver el archivo, para lo que comprueba su nombre de usuario y contraseña. En algunos casos, esto se puede almacenar en caché y no verá un mensaje que le solicite sus credenciales. En otros casos, se le pedirá que proporcione sus credenciales.
> 
> Si su organización no usa Azure Rights Management (Azure RMS) o AD RMS, puede solicitar una cuenta gratuita que acepte sus credenciales para que pueda abrir los archivos protegidos mediante RMS:
> 
> -   Para solicitar esta cuenta, haga clic en el vínculo para solicitar [RMS para usuarios](http://go.microsoft.com/fwlink/?LinkId=309469).
> 
>     Al suscribirse, use la dirección de correo electrónico de su empresa en lugar de una dirección de correo electrónico personal. Si va a suscribirse porque le enviaron un archivo adjunto protegido por correo electrónico, use la misma dirección de correo electrónico que se usó para enviarle el mensaje de correo electrónico.
> -   Para obtener más información, vea [RMS para usuarios y Microsoft Azure Rights Management](http://technet.microsoft.com/library/dn592127.aspx).

## <a name="BKMK_ViewPFILE"></a>Para ver un archivo protegido
Usando el Explorador de archivos o el mensaje de correo electrónico que contiene el archivo adjunto, haga doble clic en el archivo protegido y escriba sus credenciales si se le solicita que lo haga.

Si ve dos versiones del archivo pero con extensiones de nombre de archivo diferentes, abra el archivo que tiene una extensión de archivo .ppdf únicamente si el otro archivo no se abre. Si tampoco puede abrir la versión .ppdf, instale primero la [aplicación para uso compartido de RMS](http://technet.microsoft.com/library/dn574734.aspx), que sabe cómo abrir los archivos que tienen una extensión de nombre de archivo .ppdf.

> [!NOTE]
> Para obtener más información, consulte “[¿Qué es el archivo .ppdf que se crea automáticamente?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_PPDF)”.

La manera en que se abre el archivo depende de cómo se protegió, lo que se puede saber por la extensión de nombre de archivo. En cualquier caso, el proceso de abrir el archivo podría auditarse, y sigue auditándose mientras esté protegido. Además, si el archivo se envió como un archivo adjunto por correo electrónico, es posible que el remitente reciba una notificación por correo electrónico cada vez que abra el archivo.

|Extensión de nombre de archivo y protección|Más información|
|-----------------------------------------------|-------------------|
|El archivo tiene una extensión de nombre de archivo **.pfile**.<br /><br />El archivo se protegió de forma genérica.|Al abrir el archivo, verá el cuadro de diálogo **archivo protegido** de la aplicación de uso compartido que indica la persona que protegió el archivo y que se espera que respete los permisos de copropietario. Haga clic en **Abrir** para leer el archivo.<br /><br />![](../Image/ADRMS_MSRMSApp_PfilePermission.png)|
|El archivo tiene una extensión de nombre de archivo **.ppdf** o es un archivo de texto o imagen protegido (como **.ptxt** o **.pjpg**).<br /><br />El archivo se protegió de forma nativa como una copia de solo lectura.|El archivo se abre mediante el visor que se instala con la aplicación para uso compartido de RMS. Este archivo es de solo lectura, aunque lo guarde en otra ubicación o le cambie el nombre.|
|Otras extensiones de nombre de archivo.<br /><br />El archivo se protegió de forma nativa.|El archivo se abre con la aplicación que está asociada con la extensión de nombre de archivo original y se muestra una pancarta de restricción en la parte superior del archivo. La pancarta puede mostrar los permisos que se aplican al archivo o puede proporcionar un vínculo para mostrarlos. Por ejemplo, podría ver lo siguiente, donde debe hacer clic en **El permiso está restringido actualmente** para ver los permisos reales que se aplican al archivo y a las personas que pueden tener acceso a él:<br /><br />![](../Image/ADRMS_MSRMSApp_RestrictedAccess.png)|
Para ver una lista completa de extensiones de nombre de archivo admitidas por Rights Management, consulte las secciones [Tipos de archivo y extensiones de nombre de archivo admitidos](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes) secciones en [Guía de administrador de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_administrator_guide.md). Si su extensión de nombre de archivo no se incluye, realice una búsqueda web para ver si es una extensión de nombre de archivo admitida por otra aplicación.

> [!NOTE]
> Si después de confirmar que el archivo está protegido por Rights Management este no se abre, descargue y use la [herramienta RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Siga las instrucciones de la herramienta para detectar problemas en su equipo que puedan impedir que se abra un documento protegido.

## <a name="BKMK_UserDefined"></a>Para usar archivos que están protegidos (por ejemplo, editar e imprimir el archivo)
Si, tras abrir el archivo protegido, desea hacer algo más que simplemente leerlo (como editarlo, copiarlo e imprimirlo):

|Extensión de nombre de archivo|Instrucciones|
|----------------------------------|-----------------|
|El archivo tiene una extensión de nombre de archivo **.pfile**.|Guarde el archivo abierto y asígnele una nueva extensión de nombre de archivo que esté asociada a la aplicación que desea usar.<br /><br />Por ejemplo, si un archivo se protegió con el nombre de archivo document.vsdx.pfile, visualice el archivo y, en el Explorador de archivos, guárdelo como document.vsdx.<br /><br />El nuevo archivo ya no está protegido. Si desea protegerlo, debe hacerlo manualmente. Para obtener instrucciones, vea [Proteger un archivo en un dispositivo &#40;proteger en contexto&#41; mediante la aplicación para uso compartido de Rights Management.](../Topic/Protect_a_file_on_a_device__protect_in-place__by_using_the_Rights_Management_sharing_application.md).|
|El archivo tiene una extensión de nombre de archivo **.ppdf** o es un archivo de texto o imagen protegido (como **.ptxt** o **.pjpg**).|Solo puede ver el archivo, y si le cambia el nombre o si lo mueve, el archivo sigue estando protegido.|
|Otras extensiones de nombre de archivo.|El dispositivo debe tener una aplicación que entienda Rights Management para usar estos archivos. Estas aplicaciones se denominan aplicaciones habilitadas para RMS. Las aplicaciones de Office 2016, Office 2013 y Office 2010 (como Word, Excel, PowerPoint y Outlook) son ejemplos de aplicaciones que están habilitadas para Rights Management. Sin embargo, las aplicaciones que no proceden de Microsoft, como las de otras empresas de software y sus propias aplicaciones de línea de negocio, también podrían estar habilitadas para Rights Management.<br /><br />Las aplicaciones que están habilitadas para Rights Management saben cómo abrir los archivos que se protegieron mediante otras aplicaciones habilitadas para Rights Management. Además, conservan la protección que tenían aplicada, aun cuando modifique el archivo o lo guarde con otro nombre de archivo o en otra ubicación. Estas aplicaciones permiten usar el archivo según los permisos que tenga aplicados actualmente, por lo que si tiene permisos para usar el archivo, puede hacerlo. Por ejemplo, es posible que pueda editar el archivo pero no imprimirlo.|

## Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [¿Qué desea hacer?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Vea también
[Guía de usuario de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_user_guide.md)

