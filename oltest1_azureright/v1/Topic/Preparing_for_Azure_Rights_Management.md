---
description: na
keywords: na
title: Preparing for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
---
# Preparaci&#243;n de Azure Rights Management
Después de haberse registrado para una suscripción en la nube y haber provisto a su organización de una cuenta para [!INCLUDE[o365_1](../Token/o365_1_md.md)] o Azure Active Directory, está preparado para habilitar el servicio [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

Sin embargo, antes de hacerlo, asegúrese de contar con lo siguiente:

-   Cuentas y grupos de usuarios en la nube que crea manualmente o que se crean y se sincronizan automáticamente desde los Servicios de dominio de Active Directory (AD DS).

    Al sincronizar sus cuentas y grupos locales, no es necesario sincronizar todos los atributos. Consulte una lista de los atributos que deben sincronizarse para Azure RMS en esta [sección Azure RMS](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectsync-attributes-synchronized/) de la documentación de Azure Active Directory. Para que la implementación resulte más sencilla, recomendamos que use [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) para conectar sus directorios locales con Azure Active Directory, pero puede usar cualquier método de sincronización de directorios con el que se obtenga el mismo resultado.

-   Grupos habilitados para correo en la nube que usará con Rights Management. Pueden ser grupos integrados o creados manualmente que contengan usuarios que usarán Rights Management.

    Si tiene Exchange Online, puede crear y usar grupos habilitados para correo mediante el centro de administración de Exchange. Si tiene AD DS y va a sincronizar con Azure AD, puede crear y usar grupos habilitados para correo que sean grupos de seguridad o grupos de distribución.

## Habilitar Rights Management
De forma predeterminada, [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] está deshabilitado cuando registra su cuenta de [!INCLUDE[o365_2](../Token/o365_2_md.md)] o Azure AD. Para habilitar [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] para su organización, debe activar el servicio. Para obtener más información, vea [Activar Rights Management de Azure](../Topic/Activating_Azure_Rights_Management.md).

## Vea también
[Configuración de Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

