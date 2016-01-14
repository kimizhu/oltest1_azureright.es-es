---
description: na
keywords: na
title: Configuring Usage Rights for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
---
# Configuraci&#243;n de los derechos de uso para Azure Rights Management
Cuando establece la protección en archivos o correos electrónicos con Azure Rights Management (Azure RMS) y no usa ninguna plantilla, debe configurar los derechos de uso usted mismo. Además, al configurar plantillas personalizadas para Azure RMS, se seleccionan los derechos de uso que se aplicarán automáticamente cuando los usuarios, administradores o servicios configurados seleccionen la plantilla. Por ejemplo, en el Portal de Azure clásico, puede seleccionar los roles que configuran una agrupación lógica de derechos de uso o puede configurar los derechos individuales.

Use este tema para ayudarlo a configurar los derechos de uso que desea para la aplicación que esté usando y para entender cómo las aplicaciones interpretan estos derechos.

## Derechos de uso y descripciones
En la tabla siguiente se enumeran y se describen los derechos de uso que admite Rights Management y cómo se usan y se interpretan. En esta tabla, el **Nombre común** es normalmente cómo se muestra o se referencia el derecho de uso, como una versión más descriptiva del valor de una sola palabra que se usa en el código (el valor **Codificación en la directiva**).**Constante o valor de API** es el nombre de SDK para una llamada de API de MSIPC, que se usa al escribir una aplicación habilitada para RMS que comprueba un derecho de uso o agrega un derecho de uso a una directiva.

|Nombre común|Codificación en la directiva|Descripción|Implementación en los derechos personalizados de Office|Nombre en el Portal de Azure clásico|Nombre en las plantillas de AD RMS|Constante o valor de API|Información adicional|
|----------------|--------------------------------|---------------|-----------------------------------------------------------|----------------------------------------|--------------------------------------|----------------------------|-------------------------|
|Editar contenido, Editar|DOCEDIT|Permite al usuario modificar, reorganizar, formatear o filtrar el contenido dentro de la aplicación. No concede el derecho a guardar la copia modificada.|Como parte de las opciones **Cambiar** y **Control total**.|**Editar contenido**|**Editar**|No aplicable|En las aplicaciones de Office, este derecho también permite al usuario guardar el documento.|
|Guardar|EDITAR|Permite al usuario guardar el documento en su ubicación actual.|Como parte de las opciones **Cambiar** y **Control total**.|**Guardar archivo**|**Guardar**|IPC_GENERIC_WRITEL"EDIT"|En las aplicaciones de Office, este derecho también permite al usuario modificar el documento.|
|Comentario|COMMENT|Habilita la opción para agregar anotaciones o comentarios al contenido.|No implementado|No implementado|No implementado|IPC_GENERIC_COMMENTL"COMMENT"|Este derecho está disponible en el SDK como directiva ad hoc en el módulo de protección de RMS para Windows PowerShell y se implementó en algunas aplicaciones de proveedores de software. Sin embargo, no se usa extensamente y no es compatible actualmente con las aplicaciones de Office.|
|Guardar como, Exportar|EXPORTAR|Habilita la opción para guardar el contenido con un nombre de archivo diferente (Guardar como). Según la aplicación, el archivo puede guardarse sin protección.|Como parte de las opciones **Cambiar** y **Control total**.|**Exportar contenido (Guardar como)**|**Exportar (Guardar como)**|IPC_GENERIC_EXPORTL"EXPORT"|Este derecho también permite al usuario realizar otras opciones de exportación en las aplicaciones, como **Enviar a OneNote**.|
|Reenviar|REENVIAR|Habilita la opción para reenviar un mensaje de correo electrónico y agregar destinatarios a las líneas **Para** y **CO**.|Se deniega al usar la directiva estándar **No reenviar**.|**Reenviar**|**Reenviar**|IPC_EMAIL_FORWARDL"FORWARD"|No permite que el reenviador conceda derechos a otros usuarios como parte de la acción de reenvío.|
|Control total|OWNER|Concede todos los derechos para el documento; se pueden realizar todas las acciones disponibles.|Como la opción personalizada **Control total**.|**Control total**|**Control total**|IPC_GENERIC_ALLL"OWNER"|Incluye la capacidad de quitar la protección.|
|Imprimir|PRINT|Habilita las opciones para imprimir el contenido.|Como la opción **Imprimir contenido** en los permisos personalizados. No se trata de un valor por destinatario.|**Imprimir**|**Imprimir**|IPC_GENERIC_PRINTL"PRINT"|Sin información adicional|
|Responder|RESPONDER|Habilita la opción Respuesta en un cliente de correo electrónico, sin permitir que se realicen cambios en las líneas **Para** o **CO**.|No aplicable|**Responder**|**Responder**|IPC_EMAIL_REPLY|Sin información adicional|
|Responder a todos|REPLYALL|Habilita la opción **Responder a todos** en un cliente de correo electrónico, pero no permite al usuario agregar a destinatarios a las líneas **Para** o **CO**.|No aplicable|**Responder a todos**|**Responder a todos**|IPC_EMAIL_REPLYALLL"REPLYALL"|Sin información adicional|
|Ver, Abrir, Leer|VER|Permite al usuario abrir el documento y ver el contenido.|Como la opción **Ver** de la directiva personalizada **Leer**.|**Ver contenido**|**Vista**|IPC_GENERIC_READL"VIEW"|Sin información adicional|
|Copiar|EXTRACT|Habilita las opciones para copiar los datos del documento en el mismo documento o en otro documento.|Como la opción de directiva personalizada **Permitir a los usuarios con acceso de lectura copiar contenido**.|**Copiar y Extraer contenido**|**Extracción**|IPC_GENERIC_EXTRACTL"EXTRACT"|En algunas aplicaciones, también permite que todo el documento se guarde en sin protección.|
|Ver derechos|VIEWRIGHTSDATA|Permite al usuario ver la directiva que se aplica al documento.|No implementado|**Ver derechos asignados**|**Ver derechos**|IPC_READ_RIGHTSL"VIEWRIGHTSDATA"|Algunas aplicaciones no lo tienen en cuenta.|
|Cambiar derechos|EDITRIGHTSDATA|Permite al usuario cambiar la directiva que se aplica al documento. Incluye la eliminación de la protección.|No implementado|**Cambiar derechos**|**Editar derechos**|IPC_WRITE_RIGHTSL"EDITRIGHTSDATA"|Sin información adicional|
|Permitir macros|OBJMODEL|Habilita la opción para ejecutar macros u obtener acceso remoto o mediante programación al contenido de un documento.|Como la opción de directiva personalizada **Permitir el acceso mediante programación**. No se trata de un valor por destinatario.|**Permitir macros**|**Permitir macros**|No aplicable|Sin información adicional|

## Derechos incluidos en los niveles de permisos
Algunas aplicaciones agrupan derechos de uso en niveles de permisos para facilitar la selección de derechos de uso que suelen utilizarse de forma conjunta. Estos niveles de permisos ayudan a resumir un nivel de complejidad de los usuarios para que puedan elegir opciones basadas en roles.  Por ejemplo, **Revisor** y **Coautor**. Aunque estas opciones suelen mostrar a los usuarios un resumen de los derechos, puede que no incluyan todos los derechos enumerados en la tabla anterior.

Utilice la tabla siguiente para ver una lista de estos niveles de permisos y una lista completa de los derechos que contienen.

|Nivel de permisos|Aplicaciones|Derechos incluidos (nombre común)|
|---------------------|----------------|-------------------------------------|
|Visor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer<br /><br />Responder<br /><br />Responder a todos|
|Revisor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer<br /><br />Guardar<br /><br />Editar contenido, Editar<br /><br />Responder<sup>*</sup><br /><br />Responder a todos<sup>*</sup><br /><br />Reenviar<sup>*</sup>|
|Coautor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer<br /><br />Guardar<br /><br />Editar contenido, Editar<br /><br />Copiar<br /><br />Ver derechos<br /><br />Cambiar derechos<br /><br />Permitir macros<br /><br />Guardar como, Exportar<br /><br />Imprimir<br /><br />Responder<sup>*</sup><br /><br />Responder a todos<sup>*</sup><br /><br />Reenviar<sup>*</sup>|
|Copropietario|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer<br /><br />Guardar<br /><br />Editar contenido, Editar<br /><br />Copiar<br /><br />Ver derechos<br /><br />Cambiar derechos<br /><br />Permitir macros<br /><br />Guardar como, Exportar<br /><br />Imprimir<br /><br />Responder<sup>*</sup><br /><br />Responder a todos<sup>*</sup><br /><br />Reenviar<sup>*</sup><br /><br />Control total|
<sup>*</sup> No aplicable a la aplicación de uso compartido Rights Management para Windows

## Derechos incluidos en las plantillas predeterminadas
Los derechos que se incluyen con las plantillas predeterminadas son los siguientes:

|Nombre para mostrar|Derechos incluidos (nombre común)|
|-----------------------|-------------------------------------|
|&lt;nombreDeOrganización&gt;- Solo vista confidencial|Ver, Abrir, Leer|
|&lt;nombreDeOrganización&gt; - Confidencial|Ver, Abrir, Leer<br /><br />Guardar<br /><br />Editar contenido, Editar<br /><br />Ver derechos<br /><br />Permitir macros<br /><br />Reenviar<br /><br />Responder<br /><br />Responder a todos|

## Vea también
[Configuración de Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

