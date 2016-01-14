---
description: na
keywords: na
title: Scenario - Executives Securely Exchange Privileged Information
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e18cf5df-859e-4028-8d19-39b0842df33d
---
# Escenario: ejecutivos intercambian de forma segura informaci&#243;n confidencial
Esta sección contiene instrucciones de administrador e indicaciones para obtener instrucciones de usuario.Debe completar las instrucciones para administradores antes de informar a los usuarios acerca de esta configuración.

## Instrucciones para administradores
![](../Image/AzRMS_AdminBanner.png)

Siga estas instrucciones para que los ejecutivos puedan intercambiar mensajes de correo electrónico y datos adjuntos por correo electrónico con otros de forma segura y para que las directivas restrinjan automáticamente el acceso a los ejecutivos sin requerir ninguna acción especial por su parte.Los correos electrónicos y los datos adjuntos estarán protegidos por Azure Rights Management.

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Los ejecutivos comparten información confidencial entre sí que no se debe compartir con otros usuarios.

-   Los ejecutivos no necesitan hacer nada más que enviar estos correos electrónicos a una dirección de correo electrónico de trabajo en lugar de a una dirección de correo electrónico personal.

## Requisitos para este escenario
Para que funcionen las instrucciones para este escenario, debe disponer de lo siguiente:

|Check|Requisito|Si necesita más información|
|---------|-------------|-------------------------------|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Preparó las cuentas y los grupos para Office 365 o Azure Active Directory:<br /><br />-   Un grupo habilitado para correo electrónico denominado **Ejecutivos**<br />-   Todos los ejecutivos son miembros del grupo **Ejecutivos**|[Preparación de Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Microsoft administra su clave de inquilino de Azure Rights Management; no se usa BYOK|[Planificación e implementación de tu clave de inquilino de Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Azure Rights Management no está activado|[Activar Rights Management de Azure](https://technet.microsoft.com/library/jj658941.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Exchange Online está habilitado para Azure Rights Management|Expanda la sección [Exchange Online: Configuración de IRM](https://technet.microsoft.com/library/jj585031.aspx) en [Configuración de aplicaciones para Azure Rights Management](https://technet.microsoft.com/library/jj585031.aspx).|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Configuró una plantilla personalizada tal y como se describe a continuación|[Configuración de plantillas personalizadas para Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|![](../Image/4d269a30-a873-45c5-87de-30ee6558e7b0.gif)|Configuró una regla de protección de transporte para IRM, tal y como se describe a continuación|[Crear una regla de protección de transporte](https://technet.microsoft.com/library/dd302432.aspx)|

#### Para configurar la plantilla personalizada para los correos electrónicos de los ejecutivos:

1.  En el Portal de Azure. Cree una nueva plantilla personalizada para Azure Rights Management, que contenga estos valores y configuraciones:

    -   Nombre: **Ejecutivos**

    -   Derechos:  Conceda al grupo habilitado para correo electrónico Ejecutivos derechos de **copropietario**

2.  Publique la nueva plantilla.

3.  Actualice las plantillas para Exchange Online mediante el comando de Windows PowerShell para Exchange Online:

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates –RMSOnline
    ```

#### Para configurar la protección automática de los mensajes de correo electrónico desde y hacia los ejecutivos:

-   En el centro de administración de Exchange: Cree una nueva regla de flujo de correo, que contenga estos valores y configuraciones:

    -   Haga clic en el icono Nuevo y, a continuación, seleccione **Aplicar protección de derechos a los mensajes**

    -   En la página **Nueva regla**:

        -   Especifique un nombre como **Aplicar las plantillas de Ejecutivos a los correos electrónicos de los ejecutivos**

        -   Para **Aplicar esta regla si**, seleccione **El remitente** .... **es miembro de este grupo** y seleccione **Ejecutivos**.

        -   Haga clic en **Agregar condición**, seleccione **El destinatario** .... **es miembro de este grupo** y seleccione **Ejecutivos**.

        -   Para **Hacer lo siguiente**, asegúrese de que está seleccionado **Aplicar la protección de derechos al mensaje con**, haga clic en **Seleccionar una** para seleccionar la plantilla **Ejecutivos**.

        -   Asegúrese de que está seleccionado **Elegir un modo para esta regla**, **Exigir**.

        -   Haga clic en **Guardar**.

## Instrucciones para usuarios
No hay instrucciones específicas para los usuarios en este escenario porque la protección de mensajes de correo electrónico desde y hacia ejecutivos no requiere ninguna acción especial por su parte.Los mensajes de correo electrónico y los datos adjuntos se protegen automáticamente para que solo los miembros del grupo Ejecutivos puedan acceder a ellos.Sin embargo, deberá informar de ello a los ejecutivos y al departamento de soporte técnico y deberá indicarles cómo puede restringir esto el uso de estos correos electrónicos.Por ejemplo, otras personas no podrán leerlos correctamente si más adelante se reenvían los mensajes de correo electrónico o datos adjuntos a otros usuarios.

El siguiente ejemplo se podría enviar como una comunicación de correo electrónico estándar a los ejecutivos, después de configurar Exchange Online para este escenario.

### Documentación de usuario de ejemplo
![](../Image/AzRMS_ExampleBanner.png)

##### Anuncio de TI: Ahora los correos electrónicos se protegerán automáticamente

-   De ahora en adelante, siempre que se envíen correos electrónicos a otro ejecutivo de la empresa, el contenido de los correos electrónicos y los datos adjuntos se protegerán automáticamente de modo que solo otro ejecutivo de la empresa pueda acceder a ellos para leer la información, imprimirlo, copiarlo, etc.Esta restricción se aplica incluso si se reenvía el mensaje de correo electrónico a otros usuarios o si se guardan los datos adjuntos.Esta protección ayuda a evitar la pérdida de datos confidenciales o importantes.

    Tenga en cuenta que si desea que otros usuarios puedan leer y editar la información de estos correos electrónicos, debe enviarla por separado.

    Al enviar información confidencial de la empresa a otro ejecutivo, recuerde que debe enviarlo a su dirección de correo electrónico de trabajo y no a una dirección de correo electrónico personal.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico: helpdesk@vanarsdelltd.com

