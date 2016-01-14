---
description: na
keywords: na
title: Dialog box options for the Rights Management sharing application
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a
---
# Opciones del cuadro de di&#225;logo para la aplicaci&#243;n Rights Management sharing
Use esta información para especificar las opciones en el cuadro de diálogo **Agregar protección** o en el cuadro de diálogo **Uso compartido seguro** de la aplicación de uso compartido de RMS. Verá este cuadro de diálogo cuando [proteja un archivo para compartirlo](http://technet.microsoft.com/library/dn574735.aspx) o cuando [proteja un archivo en contexto](http://technet.microsoft.com/library/dn574733.aspx) y elija permisos personalizados.

> [!IMPORTANT]
> Si las opciones que ve son diferentes de las mostradas aquí, probablemente no tiene instalada la versión más reciente de la aplicación. Puede descargar la versión más reciente en la página [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970).
> 
> ¿Cómo puede saber si tiene la versión más reciente? Busque **Aplicación para uso compartido de Microsoft Rights Management** en Programas y características y compruebe el número de versión. Para poder ver y usar las opciones de la tabla, la versión debe ser al menos **1.0.1770.0**. Puede comprobar el número de versión más reciente en la página de descarga.

Además de las opciones que puede elegir, es posible que también se pregunte lo siguiente:

-   [¿Qué es el archivo .ppdf que se crea automáticamente?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_PPDF)

-   [¿Cuál es la diferencia entre la protección genérica y la protección incorporada (nativa)?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative)

|Opción|Descripción|
|----------|---------------|
|**USUARIOS**|Si todavía no especificó una dirección de correo electrónico de Outlook, escriba las direcciones de correo electrónico de las personas que desea que puedan abrir el archivo.<br /><br />Si su organización usa la versión local de Rights Management (AD RMS), las direcciones de correo electrónico que puede especificar se limitan a personas de su organización. En este caso, cuando intente especificar direcciones de correo electrónico externas, verá un mensaje que indica que la configuración de la empresa permite el uso compartido de contenido protegido únicamente dentro de la empresa. Sin embargo, si su organización usa Azure RMS, estas direcciones de correo electrónico pueden ser de personas de su organización o de personas de otra organización.<br /><br />Por ejemplo, janetm@contoso.com o p.dover@fabrikam.com.|
|**Protección genérica**|Si está seleccionada esta opción, significa que el archivo seleccionado no se puede proteger de forma nativa. Para obtener más información, vea [¿Cuál es la diferencia entre la protección genérica y la protección incorporada (nativa)?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative) en este tema.|
|**Visor – Solo ver**<br /><br />**Revisor – Ver y editar**<br /><br />**Coautor – Ver, editar, copiar e imprimir**<br /><br />**Copropietario – Todos los permisos** **Note:** Todas estas opciones tienen un icono redondo antes del nombre, que representa un globo terráqueo. Se usa este icono porque, normalmente, se selecciona una de estas opciones cuando se envía un archivo adjunto a una persona de otra organización.|Seleccione una de estas opciones si desea definir los derechos del documento protegido. Haga clic en cada opción para ver una descripción.<br /><br />Cuando elija una de estas opciones, solo las personas que indique en **USUARIOS** tienen los derechos que especifique para abrir y usar el documento. Por ejemplo, si reenvían el documento a otra persona, no se abrirá.|
|Plantillas de directiva que configura el administrador.<br /><br />Por ejemplo, si el nombre de la empresa es Contoso, Ltd: **Contoso, Ltd - Solo vista confidencial** **Note:** Todas estas opciones tienen un icono cuadrado antes del nombre, que representa un edificio de oficinas. Se usa este icono porque, normalmente, se selecciona una de estas opciones cuando se envía un archivo adjunto a una persona de la misma organización.|Al compartir un documento con personas que trabajan en su organización, verá las plantillas de directiva disponibles que configura el administrador. Elija una de estas plantillas cuando no se deba compartir el documento fuera de su organización.<br /><br />Cuando se elija una de estas opciones, el administrador definirá los derechos del documento y quién puede abrirlo.|
|**Estos documentos expiran el**|Seleccione esta opción solo para los archivos sujetos a limitación temporal que los usuarios seleccionados no deben poder abrir después de la fecha que especifique. Usted seguirá pudiendo abrir el archivo original, pero después de la medianoche (de su zona horaria actual) del día que especifique, nadie más podrá abrir el archivo.<br /><br />Esta opción no está disponible si selecciona una plantilla de directiva configurada por el administrador.|
|**Enviarme un correo electrónico cuando alguien trate de abrir estos documentos**|**Note:** Esta opción está disponible actualmente en vista previa.<br />Seleccione esta opción si desea recibir notificaciones por correo electrónico cuando alguien intente abrir el documento que está protegiendo. El mensaje de correo electrónico dirá quién intentó abrirlo, cuándo y si lo consiguió.<br /><br />Esta opción está disponible solo si su organización usa Azure RMS. Si su organización usa la versión local de Rights Management (AD RMS), no verá esta opción.|
|**Permítame revocar el acceso a estos documentos de forma instantánea**|Elija esta opción si necesita revocar el acceso a los documentos más adelante a través del sitio de seguimiento de documentos y si la revocación debe surtir efecto de inmediato. Sin embargo, si establece esta opción, mientras el documento no se revoque, los usuarios siempre necesitarán una conexión a Internet para leer el documento cada vez que accedan a él. Pueden darse casos en los que los usuarios no puedan conectar su dispositivo a Internet y no puedan leer el documento tal como se pretende.<br /><br />Si no elige esta opción, todavía puede revocar los documentos más adelante, a través del sitio de seguimiento de documentos. Sin embargo, dado que los usuarios no siempre necesitan una conexión a Internet para leer el documento, no sabrán inmediatamente que el documento está revocado y podrán seguir leyéndolo hasta que vuelvan a autenticarse con Azure RMS. De forma predeterminada, el número máximo de días que alguien puede seguir leyendo un documento protegido revocado es 30 días, pero un administrador puede cambiar este valor para que sea mayor o menor que 30 días.<br /><br />Esta opción está disponible solo si su organización usa Azure RMS. Si su organización usa la versión local de Rights Management (AD RMS), no verá esta opción.|

## <a name="BKMK_GenericNative"></a>¿Cuál es la diferencia entre la protección genérica y la protección incorporada (nativa)?

-   Cuando se **protege genéricamente un archivo**, las personas no autorizadas no pueden abrir el archivo. Sin embargo, cuando una persona autorizada abre el archivo, puede reenviarlo desprotegido a otras personas o guardarlo en una ubicación a la que podrían acceder otros usuarios. A pesar de ello, verán un mensaje que les informa de los permisos que tienen para el archivo y se les solicitará que los respeten, aunque no es posible obligar al cumplimiento de esta protección. Además, al proteger un archivo de forma genérica, no es posible restringir los permisos más allá de la autorización. Por ejemplo, no se puede restringir el contenido a Solo ver, o a No imprimir.

    > [!NOTE]
    > Un archivo protegido genéricamente siempre tiene la extensión de nombre de archivo **.pfile**.

-   En cambio, cuando se usa la **protección integrada (nativa)** de Rights Management con aplicaciones que la admiten (por ejemplo, archivos de Office), la protección se aplica al archivo incluso si este se envía a otra persona o si se guarda en otra ubicación. Además, al proteger estos archivos, puede usar permisos restrictivos, como el permiso de solo lectura o el permiso para editar pero no imprimir ni copiar. Por ejemplo, puede seleccionar **Visor – Solo ver**, de modo que el contenido no se pueda editar, imprimir ni copiar.

Para obtener más información técnica, consulte la sección [Niveles de protección: nativo y genérico](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection) de [Guía de administrador de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_administrator_guide.md).

## <a name="BKMK_PPDF"></a>¿Qué es el archivo .ppdf que se crea automáticamente?

-   Cuando se comparte un archivo protegido por correo electrónico (uso compartido seguro), la aplicación de uso compartido de RMS crea automáticamente una versión **.ppdf** del archivo de Word, Excel, PowerPoint o PDF. Se trata de una versión protegida de solo lectura del archivo que únicamente pueden abrir las personas autorizadas, y garantiza que los destinatarios siempre puedan leer los archivos adjuntos, incluso si usan un dispositivo móvil que no tiene una aplicación que admita Rights Management de forma nativa. Estas personas podrán leer los datos adjuntos siempre y cuando tengan instalada la aplicación de uso compartido de RMS.

    En este escenario, a diferencia de lo que sucede en el caso de un archivo protegido de forma genérica, se aplica la restricción de uso. El destinatario no podrá guardar esta versión del archivo y, si reenvía el archivo adjunto a otra persona, las restricciones originales seguirán en vigor en el documento. Solo los usuarios que recibieron una autorización para el documento protegido podrán abrirlo.

    > [!NOTE]
    > Se crea automáticamente un archivo .ppdf cuando se hace un uso compartido seguro (compartir por correo electrónico), pero no se crea cuando se protege en contexto.

## Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [¿Qué desea hacer?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Vea también
[Guía de usuario de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_user_guide.md)

