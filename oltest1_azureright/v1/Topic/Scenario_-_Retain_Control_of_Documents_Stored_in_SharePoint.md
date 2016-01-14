---
description: na
keywords: na
title: Scenario - Retain Control of Documents Stored in SharePoint
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89
---
# Escenario: mantener el control de los documentos almacenados en SharePoint
Esta sección contiene instrucciones de administrador e indicaciones para obtener instrucciones de usuario.Debe completar las instrucciones para administradores antes de informar a los usuarios acerca de esta configuración.

## Instrucciones para administradores
![](../Image/AzRMS_AdminBanner.png)

Siga estas instrucciones para asegurarse de que los documentos de Office almacenados en SharePoint permanecen bajo su control mediante bibliotecas protegidas.Por ejemplo, los documentos están protegidos automáticamente frente a filtraciones accidentales o intencionadas por parte de los usuarios y puede bloquear el acceso al contenido incluso después de descargarlo o sincronizarlo.Los archivos que desea proteger podrían usarse para colaborar en el diseño de documentos o planes o para realizar entregas.Al configurar bibliotecas protegidas para SharePoint, los archivos de Office almacenados en ellas estarán protegidos con Azure Rights Management.

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Los empleados comparten y colaboran con documentos de Office.

-   Los documentos contienen información que no es pública, pero que tampoco es necesariamente exclusiva de uso interno.

-   Los empleados no necesitan establecer ni cambiar los permisos que establece un administrador en el nivel de la biblioteca.

## Requisitos para este escenario
Para que este escenario funcione, debe disponer de lo siguiente:

|Check|Requisito|Si necesita más información|
|---------|-------------|-------------------------------|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Ha preparado cuantas y grupos para Office 365 o Azure Active Directory|[Preparación de Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Azure Rights Management no está activado|[Activar Rights Management de Azure](https://technet.microsoft.com/library/jj658941.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Si va a usar SharePoint Server: Implementar el conector RMS y configurarlo para SharePoint|[Implementación del conector de Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Configurar SharePoint para IRM y bibliotecas protegidas|[Configuración de Information Rights Management (IRM) en el centro de administración de SharePoint](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[Aplicar Information Rights Management a una lista o biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

## Instrucciones para usuarios
No hay instrucciones específicas para los usuarios sobre este escenario porque las bibliotecas protegidas no requieren ninguna acción especial por su parte.Los documentos se protegen automáticamente, según los permisos que establezca un administrador de SharePoint para el sitio.Sin embargo, deberá informar a los usuarios y al departamento de soporte técnico sobre qué bibliotecas están protegidas y cómo puede restringir esto el uso de los documentos.Por ejemplo, debido a las limitaciones actuales, estos documentos pueden verse pero no editarse con dispositivos móviles.

El siguiente ejemplo puede enviarse como una comunicación de correo electrónico estándar al departamento o equipo pertinente, después de configurar una biblioteca de SharePoint para usar Azure RMS.

### Documentación de usuario de ejemplo
![](../Image/AzRMS_ExampleBanner.png)

##### Anuncio de TI: Cambios en el sitio de informes y previsiones de ventas

-   El sitio de SharePoint **Previsiones e informes de ventas** ahora está configurado para poder colaborar de forma segura.De ahora en adelante, se deben modificar las hojas de cálculo y los documentos de Word almacenados directamente en este sitio. No se podrán, por ejemplo, guardar en una ubicación diferente para su posterior edición ni enviarlos por correo electrónico a otra persona.Pueden verse con dispositivos móviles, pero es necesario un equipo con Windows para modificarlos.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico: helpdesk@vanarsdelltd.com

