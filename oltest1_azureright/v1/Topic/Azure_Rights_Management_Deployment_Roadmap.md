---
description: na
keywords: na
title: Azure Rights Management Deployment Roadmap
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
---
# Plan para la implementaci&#243;n de Azure Rights Management
Use los siguientes pasos para prepararse para la implementación y administre Azure Rights Management (Azure RMS) en su organización.

Sin embargo, si desea probar rápidamente Azure RMS por sí solo, en lugar de implementarlo en un entorno de producción, vea [Tutorial de inicio rápido de Azure Rights Management](../Topic/Quick_Start_Tutorial_for_Azure_Rights_Management.md).

> [!IMPORTANT]
> Antes de seguir estos pasos, asegúrate de que ha revisado el tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

## Paso 1: Confirme que tiene una suscripción que incluye Azure Rights Management.
Hay más de un tipo de suscripción que incluye [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Vea la sección [Suscripciones en la nube que son compatibles con Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) del tema [Requisitos de Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) y compruebe que la suscripción incluye la funcionalidad que desea usar en su organización; para ello, consulte la tabla que aparece en [Ofertas de comparación de Rights Management Services (RMS)](https://technet.microsoft.com/dn858608).

## Paso 2: Preparar tu cuenta de inquilino para usar Rights Management
Antes de empezar a usar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], realice los siguientes pasos previos:

1.  Asegúrese de que el inquilino de Azure o de Office 365 contenga las cuentas de usuario y los grupos que se usarán en Azure RMS para autenticar a los usuarios de su organización. Si es necesario, cree estas cuentas y grupos, o sincronícelos desde el directorio local. Para obtener más información, vea [Preparación de Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).

2.  Decide si quieres que Microsoft administre tu clave de inquilino (la predeterminada) o generarla y administrarla tú mismo (conocido como Aportar tu propia clave, o BYOK). Tenga en cuenta que actualmente, no se puede usar BYOK si se usa Exchange Online. Para obtener más información, vea [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

3.  Instale el módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] en al menos un equipo que tenga acceso a Internet. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, vea [Instalación de Windows PowerShell para Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

4.  Si actualmente utiliza Rights Management Services de forma local: Realice una migración para mover las claves, plantillas y direcciones URL a la nube. Para obtener más información, vea [Migración desde AD RMS a Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).

5.  Activa Rights Management para que puedas empezar a usar el servicio. Si se requiere una implementación en fases, configure los controles de incorporación de usuarios para restringir el uso a usuarios específicos. Para obtener más información, vea [Activar Rights Management de Azure](../Topic/Activating_Azure_Rights_Management.md).

De forma opcional, considera configurar lo siguiente:

-   Plantillas personalizadas si las plantillas de directiva de derechos predeterminadas no son suficientes para tu organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, vea [Configuración de plantillas personalizadas para Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

-   Registro de uso para que puedas controlar cómo se usa Rights Management en tu organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, vea [Registro y análisis del uso de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

## Paso 3: Configure las aplicaciones y servicios para Rights Management.
La configuración de tus aplicaciones puede incluir la instalación de la aplicación de uso compartido Rights Management y la habilitación de la ayuda para las funciones de Information Rights Management (IRM) en SharePoint Online o Exchange Online. Para obtener más información, vea [Configuración de aplicaciones para Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

Si tiene servicios de TI existentes que necesita para inspeccionar los archivos que se van a proteger con Azure RMS, como soluciones de prevención de pérdida de datos (DPL), puertas de enlace de cifrado de contenido (CEG) y productos antimalware, configure las cuentas de servicio como superusuarios para Azure RMS. Para obtener más información, vea [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

Si tienes servicios locales que quieres usar con Azure Rights Management, instala y configura el conector de Rights Management. Para obtener más información, vea [Implementación del conector de Azure Rights Management](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

## Paso 4: Publicar y consumir contenido protegido por derechos
Ahora está listo para publicar y consumir contenido protegido, y registrar cómo su empresa usa Rights Management. Para obtener más información, vea [Uso de Azure Rights Management](../Topic/Using_Azure_Rights_Management.md).

## Paso 5: Administrar Rights Management para tu cuenta de inquilino según sea necesario
Cuando empiece a usar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], quizá encuentre útil el módulo [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para Windows PowerShell para facilitar el uso de scripts o automatización en la aplicación de cambios administrativos. Para obtener más información, vea [Administración de Azure Rights Management mediante Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Vea también
[Configuración de Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

