---
description: na
keywords: na
title: Operations for Your Azure Rights Management Tenant Key
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
---
# Operaciones para su clave de inquilino de Administraci&#243;n de permisos de Azure
En función de la topología de la clave de inquilino (administrada por Microsoft o por el cliente), tiene diferentes niveles de control y responsabilidad para su clave de inquilino de Microsoft Azure Rights Management (Azure RMS) una vez implementada.

Cuando administra su propia clave de inquilino, esto a menudo se denomina aportar tu propia clave (BYOK). Para obtener más información acerca de este escenario y acerca de cómo elegir entre las dos topologías clave, vea [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

La tabla siguiente identifica qué operaciones puede realizar en función de la topología que eligió para su clave de inquilino de Azure RMS.

|Operación del ciclo de vida|Administrada por Microsoft (predeterminada)|Administrada por el cliente (BYOK)|
|-------------------------------|-----------------------------------------------|--------------------------------------|
|Revocar su clave de inquilino|No automática|No automática|
|Vuelva a introducir su clave de inquilino|Sí|Sí|
|Realizar una copia de seguridad y recuperar la clave de inquilino|No|Sí|
|Exportar su clave de inquilino|Sí|No|
|Responder a una infracción|Sí|Sí|
Una vez que identifique qué topología implementó, use una de las siguientes secciones para más información sobre estas operaciones de su clave de inquilino de Azure RMS.

## <a name="BKMK_MSManagedOperations"></a>Administradas por Microsoft: Operaciones de ciclo de vida de clave de inquilino
Si Microsoft administra su clave de inquilino para Azure Rights Management (la predeterminada), use las siguientes secciones para obtener más información acerca de las operaciones del ciclo de vida que son relevantes para esta topología:

-   [Revocar su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRevoke)

-   [Vuelva a introducir su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey)

-   [Realizar una copia de seguridad y recuperar la clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBackup)

-   [Exportar su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSExport)

-   [Responder a una infracción](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBreach)

### <a name="BKMK_MSRevoke"></a>Revocar su clave de inquilino
Cuando anule la suscripción de Azure RMS, Azure RMS dejará de usar su clave de inquilino y no será necesario que realice ninguna acción.

### <a name="BKMK_MSRekey"></a>Vuelva a introducir su clave de inquilino
La acción de volver a introducir la clave también se le conoce como revertir su clave. No vuelva a introducir su clave de inquilino a menos que sea necesario. Otros clientes, como Office 2010, no se diseñaron para tratar cambios de clave correctamente. En este escenario, debe desactivar el estado de RMS en los equipos usando la directiva de grupo o un mecanismo equivalente. Sin embargo, hay algunos eventos legítimos que pueden forzarle a volver a introducir la clave de inquilino. Por ejemplo:

-   La compañía se ha dividido en una o dos compañías. Cuando vuelve a introducir la clave de inquilino, la nueva compañía no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

-   Cree que la copia maestra de su clave de inquilino (la copia en su posesión) se ha puesto en peligro.

Puede volver a introducir su clave de inquilino llamando a los servicios de soporte al cliente de Microsoft (CSS) y demostrando que es el administrador inquilino.

Cuando vuelve a introducir su clave de inquilino, el nuevo contenido está protegido usando la nueva clave de inquilino. Esto sucede en fases, por lo que para un período de tiempo, algún contenido nuevo continuará siendo protegido por la antigua clave de inquilino. El contenido protegido anteriormente permanece protegido para su antigua clave de inquilino. Para admitir este escenario, Azure RMS retiene su clave de inquilino antigua para que pueda emitir licencias para contenido antiguo.

### <a name="BKMK_MSBackup"></a>Realizar una copia de seguridad y recuperar la clave de inquilino
Microsoft es responsable de realizar la copia de seguridad de su clave de inquilino y no se requiere que realice ninguna acción.

### <a name="BKMK_MSExport"></a>Exportar su clave de inquilino
Puede exportar su configuración de Azure RMS y su clave de inquilino siguiendo las instrucciones de estos tres pasos:

##### Paso 1: Iniciar exportación

-   Para ello, póngase en contacto con el Soporte de servicio al cliente (CSS) de Microsoft. Debe probar que es un administrador para su inquilino de Azure RMS.

##### Paso 2: Esperar comprobación

-   Microsoft verifica que la solicitud para liberar su clave de inquilino de RMS es legítima. Este proceso puede tardar hasta 3 semanas.

##### Paso 3: Recibir instrucciones de clave de CSS

-   Los Servicios de soporte al cliente de Microsoft (CSS) le enviarán su configuración de Azure RMS y clave de inquilino como cifrada en un archivo protegido con contraseña que tiene una extensión de nombre de archivo .tpd. Para ello, CSS le envía (como la persona que inició el informe) una herramienta por correo electrónico. Debe ejecutar la herramienta desde un símbolo del sistema de la siguiente manera:

    ```
    AadrmTpd.exe -createkey
    ```
    Esto genera un plan de claves RSA y guarda las mitades públicas y privadas como archivos en la carpeta actual. Por ejemplo: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** y **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Responda al correo electrónico de CSS, adjuntando el archivo cuyo nombre comienza por **PublicKey**. CSS le enviará un archivo TPD como archivo .xml que está cifrado con su clave de RSA. Copie este archivo en la misma carpeta en la que ejecutó la herramienta AadrmTpd originalmente y ejecute la herramienta de nuevo, con el archivo que comienza por **PrivateKey** y el archivo de CSS. Por ejemplo:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    El resultado de este comando deben ser dos archivos: Uno contiene la contraseña de texto simple para el TPD protegido con contraseña y el otro es el propio TPD protegido con contraseña. Para fines de referencias cruzadas, ambos deben tener el mismo GUID que los archivos de clave pública y privada cuando ejecutó el comando AadrmTpd.exe -createkey:

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    Realice una copia de seguridad de estos archivos y guárdelos de manera segura para poder continuar descifrando el contenido protegido con esta clave de inquilino. Además, si está migrando a AD RMS, puede importar este archivo TPD (el archivo que empieza por **ExportedTDP**) a su servidor de AD RMS.

##### Paso 4: En curso: Proteger su clave de inquilino

-   Cuando haya recibido su clave de inquilino, manténgala a buen recaudo, ya que si alguien consigue acceso a ella, podrá descifrar todos los documentos que se hayan protegido con esa clave.

    Si el motivo por el que desea exportar la clave de inquilino es porque no quiere usar más Azure RMS, como procedimiento recomendado, desactive en este momento su inquilino de RMS. No se demore en hacerlo después de recibir su clave de inquilino, ya que esta precaución le ayudará a minimizar las consecuencias si alguien que no debería tener su clave de inquilino consigue acceso a ella. Para obtener instrucciones, vea [Retirada y desactivación de Azure Rights Management](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

### <a name="BKMK_MSBreach"></a>Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegido, se pueden encontrar vulnerabilidades en la tecnología HSM de la generación actual o algoritmos y longitudes de clave actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus activos, Microsoft notificará a sus administradores de inquilino de Azure RMS por correo electrónico usando la dirección que ha suministrado cuando realizó la suscripción.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción. Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta dependerá de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|-----------------------------|----------------------|
|Se ha filtrado su clave de inquilino.|Vuelva a introducir su clave de inquilino. Vea la sección [Vuelva a introducir su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey) de este tema.|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|La nueva introducción de la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft debe actualizar Azure RMS para que admita nuevos algoritmos y longitudes de clave más largas que sean resistentes, e indica a todos los clientes que renueven sus claves de inquilino.|

## <a name="BKMK_BYOKManagedOperations"></a>Administrada por el cliente: Operaciones de ciclo de vida de clave de inquilino
Si administra su clave de inquilino para Azure Rights Management (el escenario Aportar tu propia clave, o BYOK), use las siguientes secciones para obtener más información acerca de las operaciones del ciclo de vida que son relevantes para esta topología:

-   [Revocar su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRevoke)

-   [Vuelva a introducir su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey)

-   [Realizar una copia de seguridad y recuperar la clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBackup)

-   [Exportar su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKExport)

-   [Responder a una infracción](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBreach)

### <a name="BKMK_BYOKRevoke"></a>Revocar su clave de inquilino
Cuando anule la suscripción de Azure RMS, Azure RMS dejará de usar su clave de inquilino y no será necesario que realice ninguna acción.

### <a name="BKMK_BYOKRekey"></a>Vuelva a introducir su clave de inquilino
La acción de volver a introducir la clave también se le conoce como revertir su clave. No vuelva a introducir su clave de inquilino a menos que sea necesario. Otros clientes, como Office 2010, no se diseñaron para tratar cambios de clave correctamente. En este escenario, debe desactivar el estado de RMS en los equipos usando la directiva de grupo o un mecanismo equivalente. Sin embargo, hay algunos eventos legítimos que pueden forzarle a volver a introducir la clave de inquilino. Por ejemplo:

-   La compañía se ha dividido en una o dos compañías. Cuando vuelve a introducir la clave de inquilino, la nueva compañía no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

-   Cree que la copia maestra de su clave de inquilino (la copia en su posesión) se ha puesto en peligro.

Cuando vuelve a introducir su clave de inquilino, el nuevo contenido está protegido usando la nueva clave de inquilino. Esto sucede en fases, por lo que para un período de tiempo, algún contenido nuevo continuará siendo protegido por la antigua clave de inquilino. El contenido protegido anteriormente permanece protegido para su antigua clave de inquilino. Para admitir este escenario, Azure RMS retiene su clave de inquilino antigua para que pueda emitir licencias para contenido antiguo.

Para volver a introducir su clave de inquilino, genere y cree una nueva clave en Internet o en persona, mediante los procedimientos de la sección [Implementación de Aportar tu propia clave (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) del tema [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

### <a name="BKMK_BYOKBackup"></a>Realizar una copia de seguridad y recuperar la clave de inquilino
Es responsable de realizar copias de seguridad de su clave de inquilino. Si ha generado su clave de inquilino en un HSM de Thales, para realizar una copia de seguridad de la clave acortada, el archivo de Word y las tarjetas de administrador.

Si ha transferido su clave siguiendo los procedimientos de la sección [Implementación de Aportar tu propia clave (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) del tema [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md), Azure RMS continuará con el archivo de clave acortado, para proteger frente a los errores de cualquier nodo de Azure RMS. Sin embargo, no considere esto una copia de seguridad completa. Por ejemplo, si alguna vez necesita una copia de texto simple de su clave para usarla fuera de un HSM de Thales, Azure RMS no podrá recuperarla para usted porque solo tiene una copia no recuperable.

### <a name="BKMK_BYOKExport"></a>Exportar su clave de inquilino
Si usa BYOK, no puede exportar su clave de inquilino desde Azure RMS. La copia en Azure RMS es irrecuperable. Si desea eliminar esta clave para que no se pueda volver a usar, póngase en contacto con los servicios de atención al cliente y soporte técnico de Microsoft (CSS).

### <a name="BKMK_BYOKBreach"></a>Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegido, se pueden encontrar vulnerabilidades en la tecnología HSM de la generación actual o algoritmos y longitudes de clave actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus activos, Microsoft notificará a sus administradores de inquilino de Azure RMS por correo electrónico usando la dirección que ha suministrado cuando realizó la suscripción.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción; Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta dependerá de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|-----------------------------|----------------------|
|Se ha filtrado su clave de inquilino.|Vuelva a introducir su clave de inquilino. Vea la sección [Vuelva a introducir su clave de inquilino](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey) de este tema.|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|La nueva introducción de la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en la tecnología HSM de generación actual.|Microsoft debe actualizar los HSM. Si no hay motivos para creer que la vulnerabilidad afectó a las claves, Microsoft indicará a todos los clientes que renueven sus claves de inquilino.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft debe actualizar Azure RMS para que admita nuevos algoritmos y longitudes de clave más largas que sean resistentes, e indica a todos los clientes que renueven sus claves de inquilino.|

## Vea también
[Uso de Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

