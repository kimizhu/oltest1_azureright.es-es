---
description: na
keywords: na
title: How Applications Support Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
---
# C&#243;mo son compatibles las aplicaciones con Azure Rights Management
Use la información siguiente para tratar de comprender cómo las aplicaciones de usuario final (como las aplicaciones de Office, Word, Excel, PowerPoint y Outlook) y los servicios (como Exchange y SharePoint) pueden utilizar Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] con la idea de proteger los datos de su organización:

-   [Aplicación de uso compartido RMS para Windows y plataformas móviles](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharingAppIntro)

-   [Aplicaciones de Office: Word, Excel, PowerPoint, Outlook](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_OfficeAppsIntro)

    -   [Exchange Online y Exchange Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_ExchangeIntro)

    -   [SharePoint Online y SharePoint Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharePointIntro)

-   [Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_FCIIntro)

-   [Otras aplicaciones compatibles con las API de RMS](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_APIAppsIntro)

> [!NOTE]
> Para comprobar las aplicaciones y versiones que son compatibles con [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS), consulte [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

En algunos casos, la protección de la información se aplica de manera automática, según lo previsto en las directivas que tú mismo configuras. Por ejemplo, este es el caso con bibliotecas de SharePoint, archivos clasificados y reglas de transporte de Exchange. En otros casos, los usuarios deben aplicar ellos mismos la protección de la información desde sus aplicaciones, ya sea seleccionando una plantilla o unas opciones específicas. Por ejemplo, este es el caso cuando los usuarios comparten un archivo por correo electrónico, o protegen un archivo in situ restringiendo el acceso o el uso a usuarios seleccionados o a usuarios externos a la organización.

Las plantillas facilitan a los usuarios (y a los administradores que configuran las directivas) la aplicación del nivel de protección adecuado y restringen el acceso a personas de dentro de la organización. Aunque [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] viene con dos plantillas predeterminadas, es probable que quiera crear plantillas personalizadas para reducir las veces que se tienen que especificar opciones individuales. Para obtener más información, vea [Configuración de plantillas personalizadas para Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

Para los casos en que los usuarios deban aplicar ellos mismos la protección de información, asegúrate de proporcionarles las instrucciones y las directrices sobre cómo y cuándo deben hacerlo. Las instrucciones deberían ser específicas para la aplicación y las versiones que usan y sobre cómo usarlas, y las directrices sobre cuándo y cómo es apropiado para tu negocio aplicar la protección de información. Para obtener más información, vea [Ayudar a los usuarios a proteger archivos mediante la Administración de permisos de Azure](../Topic/Helping_Users_to_Protect_Files_by_Using_Azure_Rights_Management.md).

Para obtener información sobre cómo configurar estas aplicaciones para Azure RMS, consulte [Configuración de aplicaciones para Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

> [!TIP]
> Para consultar ejemplos y capturas de pantalla de aplicaciones que usan Azure RMS, consulte la sección [Azure RMS en acción: Qué ven los administradores y los usuarios](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures) del tema [¿Qué es Rights Management de Azure?](../Topic/What_is_Azure_Rights_Management_.md).

## <a name="BKMK_SharingAppIntro"></a>Aplicación de uso compartido RMS para Windows y plataformas móviles
La aplicación de uso compartido RMS es una aplicación gratuita y descargable que es necesaria para admitir Office 2010, pero también se recomienda para equipos con Windows, equipos con Mac y dispositivos móviles. Una de sus ventajas es que puede aplicar protección genérica para aplicaciones y archivos que no admiten [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] de forma nativa, lo que significa que se pueden proteger todos los archivos. Para obtener más información acerca de los diferentes niveles de protección, consulte la sección [Niveles de protección: nativo y genérico](http://technet.microsoft.com/library/dn339003.aspx) en la [Guía del administrador de la aplicación de uso compartido de Rights Management](http://technet.microsoft.com/library/dn339003.aspx).

Cuando los usuarios protegen sus archivos mediante la aplicación de uso compartido de RMS, también pueden realizar el seguimiento de los documentos que han protegido y, si es necesario, revocar el acceso a ellos. Para ello, pueden utilizar el [sitio de seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562).

Para ordenadores con Windows, la aplicación de uso compartido RMS se integra de forma discreta con las aplicaciones que los usuarios ya usan y las mejora:

-   Se instala un completo de Office para Word, Excel, PowerPoint y Outlook. De este modo, los usuarios disponen del botón **Compartir protegido** en la cinta de opciones, que abre un sencillo cuadro de diálogo de configuración que se usa normalmente para proteger archivos que se enviarán por correo electrónico. Este botón también proporciona una forma rápida de obtener acceso al sitio de seguimiento de documentos.

-   Una nueva opción con un clic en el botón secundario para el Explorador de archivos. De este modo, los usuarios disponen de la opción **Proteger en contexto**, que abre un sencillo cuadro de diálogo de configuración que se usa normalmente para proteger archivos almacenados en un disco.

-   Un visor para abrir archivos que se hayan protegido con [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. Este visor de invoca automáticamente cuando no hay otra aplicación instalada que pueda abrir el archivo protegido.

-   Configuración de back-end para Office 2010 que permite que Word, Excel, PowerPoint y Outlook funcionen sin problemas con [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

Aunque la aplicación para uso compartido de RMS para Windows puede descargarse e instalarse en un solo equipo desde la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970), también admite una implementación empresarial para la instalación silenciosa y la configuración personalizada. Para obtener más información, vea los recursos siguientes:

-   [Guía de administrador de la aplicación de uso compartido Rights Management](http://technet.microsoft.com/library/dn339003.aspx)

-   [Guía de usuario de la aplicación de uso compartido Rights Management](http://technet.microsoft.com/library/dn339006.aspx)

La aplicación de uso compartido RMS para dispositivos móviles admite los dispositivos móviles más usados, como iPad e iPhone, Android, Windows Phone y Windows RT. Los usuarios pueden descargar esta aplicación desde la tienda pertinente, y se pueden encontrar enlaces a estas desde la [página de Rights Management de Microsoft](http://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="BKMK_OfficeAppsIntro"></a>Aplicaciones de Office: Word, Excel, PowerPoint, Outlook
Estas aplicaciones admiten de forma nativa Rights Management mediante Information Rights Management (IRM) y permiten a los usuarios aplicar protección a un documento guardado o a un mensaje de correo electrónico que se enviará. Los usuarios pueden aplicar plantillas o elegir configuraciones muy personalizadas para restricciones de acceso, derechos y uso. Por ejemplo, los usuarios pueden configurar un archivo para que solamente pueda acceder a él gente de tu organización, o controlar si se puede editar el archivo o si se restringe a solo lectura, o si se impide que se pueda imprimir. Para archivos sujetos a limitación temporal, se puede configurar una fecha de caducidad (directamente por parte de los usuarios o aplicando una plantilla) en la que ya no se podrá acceder al archivo. Para Outlook, los usuarios también pueden elegir la opción **No reenviar** con el fin de evitar la fuga de datos.

### <a name="BKMK_ExchangeIntro"></a>Exchange Online y Exchange Server
Cuando usas Exchange Online o Exchange Server, puedes utilizar la integración de Information Rights Management (IRM), que proporciona más soluciones de protección de la información:

-   **Exchange ActiveSync IRM** para que los dispositivos móviles puedan proteger y consumir mensajes de correo electrónico protegidos.

-   Compatibilidad de RMS con **Outlook Web App**, que se implementa de forma similar al cliente de Outlook, para que los usuarios puedan proteger mensajes de correo electrónico mediante plantillas o especificando opciones individuales. Y los usuarios pueden leer y usar los mensajes de correo electrónico protegidos que se les hayan enviado.

-   **Reglas de protección** para clientes de Outlook que un administrador configura para aplicar automáticamente plantillas RMS a mensajes de correo electrónico para destinatarios concretos. Por ejemplo, cuando se envían correos electrónicos internos a tu departamento legal, solo los miembros del departamento legal pueden leerlos y no se pueden reenviar. Los usuarios consultan la protección que se aplicará al mensaje de correo electrónico antes de enviarlo y, de forma predeterminada, pueden quitarla si deciden que no es necesaria. Los correos electrónicos se cifran antes de enviarlos. Para obtener más información, consulte [Reglas de protección de Outlook](http://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) y [Crear una regla de protección de Outlook](http://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Reglas de transporte** que un administrador configura para aplicar automáticamente plantillas de RMS a mensajes de correo electrónico en función de propiedades como el remitente, el destinatario, el asunto del mensaje y el contenido. Dichas reglas son similares en concepto a las reglas de protección, pero no permiten a los usuarios quitar la protección. Se pueden aplicar a Outlook Web Access y a correos electrónicos enviados mediante dispositivos móviles, y no cifra mensajes de correo electrónico antes de que el cliente los envíe. Para obtener más información, consulte [Crear una regla de protección de transporte](http://technet.microsoft.com/library/dd302432.aspx) en la biblioteca de Exchange.

-   **Directivas de prevención de la pérdida de datos (DLP)** que contienen conjuntos de condiciones para filtrar mensajes de correo electrónico y tomar medidas para tratar de evitar la pérdida de contenido confidencial (por ejemplo, información personal o de tarjetas de crédito). Las sugerencias de las directivas se pueden usar cuando se detectan datos sensibles, para alertar a los usuarios de que es posible que sea necesario aplicar protección de la información, en función de la información del mensaje de correo electrónico. Para obtener más información, consulte [Prevención de pérdida de datos](http://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Cifrado de mensajes de Office 365** que usa reglas de transporte para enviar correos electrónicos cifrados a personas que están fuera de su compañía y que leen el correo en un explorador con una interfaz similar a la de Outlook Web App. Puedes personalizar el texto de aviso y el texto de cabecera en los correos electrónicos cifrados de tu compañía e, incluso, agregar el logotipo de la compañía. Para obtener más información, consulte [Cifrado de mensajes de Office 365](http://office.microsoft.com/o365-message-encryption-FX104179182.aspx) en el sitio web de Office.

Si usa Exchange Server, puede utilizar las características de protección de la información con [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] si implementa el conector RMS, que actúa como un transmisor entre sus servidores locales y el servicio en la nube de RMS. Para obtener más información, vea [Implementación del conector de Azure Rights Management](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

### <a name="BKMK_SharePointIntro"></a>SharePoint Online y SharePoint Server
Cuando usas SharePoint Online y SharePoint Server, puedes utilizar la integración Information Rights Management (IRM), que permite a los administradores proteger listas o bibliotecas para que cuando un usuario consulte un documento, el archivo esté protegido para que solo personas autorizadas puedan verlo y usarlo según las directivas de protección de la información que hayas especificado. Por ejemplo, el archivo podría ser de solo lectura, deshabilitar el copiado del texto, evitar que se guarde una copia local e impedir que se pueda imprimir.

Para listas y bibliotecas, la protección de la información siempre se aplica por un administrador, nunca por un usuario final. Y se aplica en el nivel de la lista o la biblioteca para todos los documentos de ese contenedor, en lugar de en archivos individuales.  Si utiliza SharePoint Online, los usuarios también pueden aplicar IRM a su biblioteca de OneDrive para la Empresa.

En primer lugar, el servicio IRM se debe habilitar para SharePoint. A continuación, especifique Information Rights Management para una biblioteca. En el caso de SharePoint Online y OneDrive para la Empresa, los usuarios pueden especificar también Information Rights Management para su biblioteca de OneDrive para la Empresa. SharePoint no usa plantillas de directiva de derechos, aunque hay valores de configuración de SharePoint que se pueden seleccionar que coinciden estrechamente con la configuración que se puede especificar en las plantillas.

Si usas SharePoint Server, puedes utilizar las funciones de protección de la información con [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] implementando el conector RMS, que actúa como una retransmisión entre tus servidores locales y el servicio en la nube de RMS. Para obtener más información, vea [Implementación del conector de Azure Rights Management](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

> [!NOTE]
> Actualmente, hay algunas limitaciones al utilizar IRM con SharePoint:
> 
> -   No puede usar las plantillas predeterminadas o personalizadas que se administran en el Portal de Azure clásico.
> -   Los archivos que tienen una extensión de nombre de archivo .PPDF para archivos PDF protegidos no se admiten. Los archivos que tienen una extensión de nombre de archivo .PDF y que han sido protegidos forma nativa por RMS se admiten cuando se utiliza un lector PDF que admita RMS de forma nativa.
> -   Dado que Office en dispositivos móviles no admite aún RMS, estos dispositivos deben utilizar un explorador para ver los archivos que han sido protegidos con RMS, y los archivos son de solo lectura.

Azure RMS aplica el uso de restricciones y cifrado de datos para documentos cuando se descargan de SharePoint y no cuando el documento se crea primero en SharePoint o se carga en la biblioteca. Para obtener información sobre cómo se protegen los documentos antes de descargarse, consulte [Cifrado de datos en OneDrive para la Empresa y SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) en la documentación de SharePoint.

Para obtener más información acerca del uso de Azure RMS con SharePoint, vea la siguiente entrada del blog de Office: [What’s New with Information Rights Management in SharePoint and SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/) (Novedades de Information Rights Management en SharePoint y SharePoint Online)

## <a name="BKMK_FCIIntro"></a>Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)
Cuando configuras Windows Server para usar Infraestructura de clasificación de archivos, esta característica del administrador de recursos del servidor de archivos puede examinar archivos locales y determinar si contienen datos sensibles. Para archivos que cumplan este criterio, se etiquetan con propiedades de clasificación que define un administrador. Entonces, la Infraestructura de clasificación de archivos puede tomar medidas, según lo estipulado en la clasificación. Una de estas acciones es aplicar la protección de la información mediante [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] y la implementación del conector Rights Management (también conocido como conector RMS). Los archivos de Office se protegen así automáticamente con Azure RMS.

Para proteger todos los tipos de archivo, no utilice el conector RMS sino que, en su lugar, ejecute un script de Windows PowerShell, usando cmdlets de la [herramienta de protección de RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256).

Las directivas de clasificación se pueden configurar completamente y son enormemente ampliables para que puedas prevenir la pérdida potencial de datos de usuarios autorizados y no autorizados. Incluso pueden ayudar a reducir el riesgo de que los administradores de la red pierdan datos, ya que se pueden configurar directivas que no requieran que dichos administradores tengan acceso a los archivos.

Para obtener instrucciones acerca de la instalación y configuración del conector de RMS para archivos de Office, consulte [Implementación del conector de Azure Rights Management](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

Para obtener instrucciones acerca del uso del de Windows PowerShell para todos los tipos de archivo, consulte [Protección de RMS con la infraestructura de clasificación de archivos &#40;FCI&#41; de Windows Server](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md).

## <a name="BKMK_APIAppsIntro"></a>Otras aplicaciones compatibles con las API de RMS
Con RMS SDK, sus desarrolladores internos pueden escribir aplicaciones de línea de negocio que admitan [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] de forma nativa. Cómo se integre la protección de la información con estas aplicaciones depende del modo en que estén escritas. Por ejemplo, la integración se podría aplicar automáticamente con un requisito mínimo de interacción del usuario o, para una experiencia más personalizada, los usuarios podrían recibir un aviso para configurar los valores a fin de aplicar la protección de la información a los archivos. Para obtener más información sobre el SDK, consulte [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx).

De forma parecida, muchos proveedores de software suministran aplicaciones que ofrecen soluciones para la protección de la información, también conocidos como productos de Enterprise Rights Management (ERM). Un ejemplo habitual es un lector de PDF que admita [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para plataformas concretas. Puede usar la tabla en la sección [Capacidades de dispositivo de cliente](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities) del tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) para identificar las aplicaciones que son compatibles con RMS (aplicaciones preparadas para RMS) y, a continuación, realizar una búsqueda web para adquirir o descargar la aplicación.

> [!TIP]
> Para estar al tanto de las aplicaciones publicadas recientemente, consulte los canales de la comunidad de RMS, que se enumeran en [Información y servicio de atención de Azure Rights Management](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

## Vea también
[Introducción a Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

