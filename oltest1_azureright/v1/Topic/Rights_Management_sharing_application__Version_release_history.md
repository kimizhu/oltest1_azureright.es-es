---
description: na
keywords: na
title: Rights Management sharing application: Version release history
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
---
# Aplicaci&#243;n de uso compartido Rights Management Historial de publicaci&#243;n de versiones
El equipo de Rights Management actualiza periódicamente la aplicación para uso compartido de Rights Management con correcciones y nuevas funcionalidades. Use la información siguiente para ver las novedades o los cambios de una versión. La versión más reciente aparece en primer lugar.

No se enumeran las versiones anteriores al 1 de enero de 2015.

> [!NOTE]
> Si tiene comentarios o alguna pregunta sobre la aplicación de uso compartido de RMS, envíe un mensaje de correo electrónico a [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question).

## Versión 1.0.2004.0
**Lanzamiento**: 11/12/2015

**Correcciones**:

-   Mejoras para los mensajes de error (precisión y claridad).

-   Mejoras de rendimiento para cifrar y descifrar el contenido.

**Nuevas características**:

-   Soporte para instalación por parte de usuarios que no sean administradores para que los usuarios estándar puedan instalar la aplicación de uso compartido RMS.

    Hay algunas restricciones para los usuarios estándar que ejecuten Office 2010. Para obtener más información, consulte la sección [Si no es un administrador local y usa Office 2010](../Topic/Download_and_install_the_Rights_Management_sharing_application.md#BKMK_SetupOffice2010) en las instrucciones de usuario [Descargar e instalar la aplicación para uso compartido de Rights Management](../Topic/Download_and_install_the_Rights_Management_sharing_application.md).

## Versión 1.0.1908.0
**Lanzamiento**: 16/9/2015

**Correcciones**:

-   Compatibilidad con Multi-Factor Authentication (MFA) para Azure RMS, que también elimina la dependencia del Ayudante para el inicio de sesión de Microsoft en aplicaciones que usan la autenticación moderna.

    Para más información, consulte la sección [Multi-Factor Authentication (MFA) y Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_MFA) de [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

## Versión 1.0.1784.0
**Lanzamiento**: 30/7/2015

**Correcciones**:

-   El intervalo de actualización predeterminado para las plantillas de directiva de derechos se reduce de 7 días a 1 día.

-   Número reducido de regresiones y errores menores.

## Versión 1.0.1770.0
**Lanzamiento**: 25/4/2015

**Correcciones**:

-   Ahora, solo los propietarios y los copropietarios pueden quitar la protección. Los coautores no pueden quitar la protección.

-   Ahora se pueden proteger los archivos que están en un recurso compartido de red.

**Nuevas características**:

-   Compatibilidad con la revocación y el seguimiento de documentos. Para obtener más información, vea [Seguimiento y revocación de documentos cuando se utiliza la aplicación RMS sharing](../Topic/Track_and_revoke_your_documents_when_you_use_the_RMS_sharing_application.md).

-   Compatibilidad con plantillas al elegir **Uso compartido seguro**:

    -   ahora puede seleccionar plantillas.

    -   En lugar del control deslizante, verá un cuadro de lista que incluye las plantillas y los permisos personalizados.

    -   Ya no verá las opciones **Permitir consumo en todos los dispositivos** y **Aplicar restricciones de uso**. En su lugar, se activa automáticamente **Protección genérica**, en función del tipo de archivo.

    Para obtener más información, vea [Opciones del cuadro de diálogo para la aplicación Rights Management sharing](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md).

## Versión 1.0.1667.0
**Lanzamiento**: 19/1/2015

**Correcciones**:

-   Compatibilidad con fuentes del idioma chino en el visor de PPDF de la aplicación de uso compartido de RMS.

-   Control de errores y mensajería mejorados.

-   Corrección de un problema con la notificación de actualización automática cuando hay una versión más reciente de la aplicación disponible para descargar.

**Nuevas características**:

-   **Compatibilidad con varios dominios de correo electrónico dentro de su organización**: si usa AD RMS y los usuarios de su organización tienen varios dominios de correo electrónico, esta actualización permite que los usuarios consuman el contenido que protegieron los usuarios de su organización en otros dominios. Para más información, consulte la sección [Solo AD RMS: Compatibilidad con varios dominios de correo electrónico dentro de su organización](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains) en la [Guía de administrador de la aplicación de uso compartido Rights Management](../Topic/Rights_Management_sharing_application_administrator_guide.md).

