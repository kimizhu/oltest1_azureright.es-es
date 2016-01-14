---
description: na
keywords: na
title: Terminology for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
---
# Terminolog&#237;a de Azure Rights Management
¿No entiende una palabra, frase o acrónimo relacionados con Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS)? Busque aquí la definición de los términos y las abreviaturas que son específicos de Azure RMS o que tienen un significado específico cuando se usan en el contexto de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

|Término|Definición|
|-----------|--------------|
|AADRM|Nombre del módulo de Windows PowerShell para Azure Rights Management, que deriva de la abreviatura no oficial de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] cuando se llamaba (Windows) Azure Active Directory Rights Management.|
|activar|Habilitar el servicio de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] para que una organización pueda agregar protección de la información a sus documentos y correos electrónicos. Esta acción también habilita las características de Rights Management en Exchange Online y SharePoint Online.|
|Active Directory Rights Management Services|En ocasiones se abrevia como *AD RMS*.<br /><br />Un rol de Windows Server que brinda protección de la información mediante cifrado y directivas para ayudar a proteger documentos, archivos y correos electrónicos.|
|AD RMS|Consulte *Active Directory Rights Management Services*|
|Administración de los derechos de Azure|En ocasiones, se abrevia como *Azure RMS*.<br /><br />Un servicio de Azure que brinda protección de la información mediante cifrado y directivas para ayudar a proteger documentos, archivos y correos electrónicos.  También se conoce como *servicio de Azure Rights Management*. Entre los nombres anteriores se incluyen:<br /><br />-   *Windows Azure Active Directory Rights Management*: con frecuencia abreviado como Servicio de Windows Azure AD Rights Management.<br />-   *RMS Online*: el nombre que se propuso originalmente, que a veces puede ver en los mensajes de error y las entradas de archivos de registro.|
|Azure RMS|Consulte *Azure Rights Management*.|
|BYOK|Consulte *Traiga su propia clave*.|
|aportar tu propia clave|Con frecuencia abreviado como *BYOK*.<br /><br />Una opción de configuración elegida por una organización que quiere generar y administrar su propia clave de inquilino para [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].|
|clave de contenido|Una clave exclusiva que crean las aplicaciones habilitadas para RMS para cada documento o correo electrónico que está protegido mediante [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] y que ayuda a limitar el riesgo de divulgación de la información.|
|consumir|Desbloquear un archivo para leerlo o usarlo cuando ese archivo está protegido por [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|
|desactivar|Deshabilitar el servicio Rights Management para que la organización ya no use [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].|
|plantilla de departamento|Una plantilla de directiva de derechos que se crea (una plantilla personalizada) y se configura para que esté visible para los usuarios seleccionados, en lugar de que la vean todos los usuarios de la organización.|
|aplicaciones habilitadas|Aplicaciones que admiten de forma nativa Rights Management, lo que incluye las aplicaciones de Office, como Word y Excel. Los fabricantes de software independientes (ISV) y los desarrolladores también pueden escribir aplicaciones que admitan [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] de forma nativa.|
|administración de derechos empresariales|Un término genérico del sector que se usa a menudo para describir los productos y las soluciones que ayudan a las organizaciones a proteger la información patentada o valiosa mediante una combinación de herramientas de autorización mediante cifrado y directivas. Microsoft Rights Management es un ejemplo de una solución de administración de derechos empresariales (ERM).|
|ERM|Consulte *administración de derechos empresariales*|
|protección genérica|Un nivel de protección que cifra cualquier tipo de archivo y evita que gente no autorizada abra el archivo. Después de abrir el archivo, deja de estar cifrado y se puede usar en una aplicación que no admite [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] de forma nativa.|
|protección de la información|En ocasiones abreviada como *PI*.<br /><br />Un término genérico del sector que hace referencia a la protección de los datos y los archivos frente al acceso no autorizado, incluso después de que los datos y los archivos atraviesan los límites de la organización mediante correo electrónico o uso compartido de documentos. Microsoft Rights Management es un ejemplo de una solución de protección de la información (PI).|
|Information Rights Management|Con frecuencia abreviado como *IRM*.<br /><br />Un término usado junto a los servicios de Office, como Exchange Server, Word y SharePoint Online, para describir la capacidad de admitir Rights Management.|
|IRM|Consulte *Information Rights Management*|
|MSDRM|A veces considerada como referencia para el cliente RMS 1.0, que se sustituye por el nuevo cliente RMS, MSIPC. Este cliente anterior admite aplicaciones que se desarrollan con el SDK de RMS 1.0 y admite Office 2010 y Office 2007, Exchange 2010 y Exchange 2013, y SharePoint 2010 y SharePoint 2007.|
|MSIPC|A veces considerada como referencia para el cliente RMS 2.0, que sustituye al antiguo cliente RMS, MSDRM. Este cliente más reciente admite aplicaciones que se desarrollan con el SDK 2.0 de RMS y es compatible con Office 2016 y Office 2013, SharePoint 2013 y la aplicación RMS sharing.|
|protección nativa|Un nivel de protección disponible en todas las aplicaciones habilitadas que evita que gente no autorizada abra un archivo y que, además, aplica directivas más estrictas, como solo lectura y la imposibilidad de imprimir. Además, esta protección permanece con el archivo, incluso cuando el archivo se reenvía a otras personas o se guarda en una ubicación pública a la que otros puedan acceder.|
|.pfile|La extensión del nombre de archivo que se anexa a todos los archivos que Rights Management protege de manera genérica.|
|.ppdf|La extensión del nombre de archivo que Rights Management crea al generar automáticamente una copia en PDF de un archivo (Word, Excel, PowerPoint o PDF) que comparte por correo electrónico, de modo que el archivo pueda leerse (pero no editarse) en todos los dispositivos.|
|nivel de permisos|Una agrupación lógica de derechos de uso que facilitan a los usuarios finales y administradores la elección de opciones de configuración basadas en roles. Por ejemplo, Revisor y Coautor.|
|proteger|Aplicar controles de Rights Management a archivos o mensajes de correo electrónico mediante directivas de cifrado, identidad y control de acceso para ayudar a proteger los datos.|
|publish|Proteger un archivo a fin de evitar el acceso y el uso no autorizados.|
|conector de Rights Management|Una retransmisión de un proxy de salida que puede implementar para los servicios locales, como Exchange Server y SharePoint, para proteger datos mediante Azure Rights Management.|
|servicios de Rights Management|El término genérico que se aplica a la versión en la nube de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]) y a la versión local de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] (AD RMS).|
|Aplicación de uso compartido Rights Management|Una aplicación descargable opcional para dispositivos Windows y la mayoría de los dispositivos móviles más conocidos, que admite el uso compartido seguro de archivos de forma local y por correo electrónico.|
|RMS|Consulte *servicios de Rights Management*|
|conector RMS|Consulte *conector de Rights Management*|
|RMS para usuarios|Una suscripción gratuita para que un usuario use [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] cuando su organización no tenga una suscripción a Office 365 o Azure Active Directory.|
|Aplicación RMS sharing|Consulte *Rights Management sharing*.|
|superusuario|Un grupo de administradores de gran confianza que pueden descifrar y acceder a archivos que la organización ha protegido mediante Rights Management. Normalmente, se necesita este nivel de acceso para la exhibición de documentos electrónicos legales y para los equipos de auditoría.|
|clave de inquilino|También se conoce como la clave del Certificado emisor de licencias de servidor (SLC).<br /><br />La clave que es exclusiva de una organización y que, en definitiva, asegura todas las funciones criptográficas de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] que se relacionan con esta clave de inquilino.|
|desproteger|Quitar controles de Rights Management de archivos o mensajes de correo electrónico que usaban directivas de cifrado, identidad y control de acceso para ayudar a proteger los datos.|
|licencia de uso|Certificado de cada documento que se concede a un usuario que abre un archivo o un mensaje de correo electrónico protegido mediante [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. Este certificado contiene los derechos del usuario relativos al archivo o mensaje de correo electrónico y la clave de cifrado que se usó para cifrar el contenido, así como las restricciones de acceso adicionales definidas en la directiva del documento.|

## Vea también
[Introducción a Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

