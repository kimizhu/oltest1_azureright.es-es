---
description: na
keywords: na
title: RMS for Individuals and Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
---
# RMS para usuarios y Azure Rights Management
RMS para usuarios es una suscripción gratuita de autoservicio para usuarios de una organización a quienes se enviaron archivos confidenciales protegidos por Microsoft Azure Rights Management (Azure RMS), pero que no pueden autenticarse porque su departamento de TI no administra una cuenta para ellos en Azure. Por ejemplo, el departamento de TI no tiene Office 365 o no usa los servicios de Azure.

Estos usuarios pueden solicitar una cuenta profesional o educativa gratuita para usarla con Azure RMS y descargar e instalar la aplicación para uso compartido de Rights Management. Como resultado, los usuarios ya pueden autenticarse para demostrar que son la persona a la que se enviaron los archivos protegidos y, a continuación, leer los archivos protegidos en equipos o dispositivos móviles.

Con la aplicación para uso compartido de Rights Management en equipos Windows, los usuarios también pueden proteger los archivos en contexto o enviarlos por correo electrónico a personas que forman parte de la organización o de fuera de esta. Si los destinatarios del correo electrónico que envían trabajan en una organización que tampoco administra cuentas de usuario en Azure, pueden registrarse para obtener una cuenta de RMS para usuarios para leer los archivos adjuntos protegidos del correo electrónico.

> [!IMPORTANT]
> Esta suscripción gratuita garantiza que las personas autorizadas siempre puedan leer archivos que se hayan protegido. Actualmente, también puede utilizar esta suscripción gratuita para proteger documentos y crear nuevos mensajes de correo electrónico protegidos, pero la capacidad de crear nuevo contenido protegido solo está prevista en modo de prueba y podría eliminarse en el futuro. Para obtener más información y conocer cualquier cambio en el uso de RMS para usuarios para proteger contenido, consulte las [Condiciones de servicio de Microsoft Rights Management](https://portal.aadrm.com/Legal/Service).

Para obtener más información sobre cómo puede proteger los archivos mediante el uso de la aplicación de Rights Management sharing gratis, consulte la [Guía de usuario de la aplicación de Rights Management sharing](http://technet.microsoft.com/library/dn339006.aspx).

RMS para usuarios es un ejemplo de una suscripción de autoservicio que es compatible con Azure Active Directory. Para más información sobre cómo funciona, consulte [¿Qué es la suscripción de autoservicio de Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/) en la documentación de Microsoft Azure. Use las secciones siguientes para obtener más información específica sobre RMS para usuarios:

-   [Cómo se registran los usuarios a RMS para individuos](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_SignUp)

    -   [Información técnica general](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TechnicalOverview)

-   [Cómo pueden los administradores controlar las cuentas creadas para RMS para usuarios](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts)

-   [Cómo averiguar si los usuarios se suscribieron para obtener RMS para usuarios](#BKMK_Detect)

## <a name="BKMK_SignUp"></a>Cómo se registran los usuarios a RMS para individuos
Para registrarse en esta cuenta gratuita, debe solicitarla visitando la [página de Microsoft Rights Management](https://portal.aadrm.com/) y proporcionar su dirección de correo electrónico profesional o educativa. La forma más habitual de redirigirle a esta página de suscripción es mediante un mensaje de correo electrónico con un archivo adjunto protegido, que contiene instrucciones sobre cómo suscribirse. Recibirá un correo electrónico de respuesta de Microsoft, tras lo cual podrá completar el proceso de suscripción introduciendo los detalles para crear la cuenta. Cuando reciba una confirmación por correo electrónico de Microsoft, este mensaje de correo electrónico final le enviará a una página donde podrá descargar la aplicación de uso compartido para diferentes dispositivos e incluirá un vínculo a la guía del usuario.

#### Para registrarse en RMS como usuarios

1.  Con un equipo Windows o Mac, vaya a la [página de Microsoft Rights Management](https://portal.aadrm.com).

2.  Escriba la dirección de correo electrónico que usa para la empresa, como **janetm@contoso.com** o **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > No se admiten cuentas de correo electrónico personales, de modo que no se puede introducir una cuenta Microsoft (conocida anteriormente como Microsoft Live ID) u otra cuenta personal que pueda usar en casa perteneciente a tu proveedor de Internet.

3.  Haga clic en **Introducción**.

    Microsoft usa su dirección de correo electrónico para comprobar si su organización ya tiene una [suscripción de pago que incluya Azure RMS](https://technet.microsoft.com/library/dn655136.aspx). Si ese es el caso, no necesita RMS para usuarios, por lo que iniciará sesión inmediatamente y se cancelará la suscripción de autoservicio de RMS para usuarios. Si no se encuentra una suscripción de pago a Azure RMS, continuará con el paso siguiente.

4.  Espere un mensaje de correo electrónico de confirmación, que se enviará a la dirección que haya suministrado. Procederá de Microsoft (DoNotReply@microsoft.com) y en el asunto se leerá **Microsoft RMS**.

5.  Cuando reciba el correo electrónico, haga clic en el vínculo de las instrucciones para finalizar el proceso de registro.

6.  El vínculo le lleva a una página de **Microsoft Rights Management** nueva para que suministre los detalles de su cuenta. Escriba su nombre y su apellido, escriba y confirme una contraseña de su elección, seleccione su país en la lista desplegable (o el país más cercano si el suyo no aparece) y, a continuación, haga clic en **Crear**.

7.  Espere recibir otro mensaje de correo electrónico de Microsoft que confirmará que la cuenta ya está lista para usarse.

8.  Cuando reciba el correo electrónico, haga clic en el vínculo para iniciar sesión y lea las instrucciones para descargar e instalar la aplicación de uso compartido, o haga clic en el vínculo Ayuda para leer la guía de usuario de la aplicación de uso compartido.

Una vez se ha creado la cuenta, ya puede empezar el proceso de protección de archivos y de lectura de archivos protegidos por otros usuarios. Cuando se le pida que inicie sesión para proteger o leer archivos protegidos, escriba la dirección de correo electrónico y la contraseña que ha usado para crear la cuenta para RMS para usuarios.

### <a name="BKMK_TechnicalOverview"></a>Información técnica general
RMS para usuarios usa un proceso de suscripción de autoservicio empleado también por otros servicios que usan la tecnología basada en la nube de Microsoft para autenticar a los usuarios.

Esto es lo que sucede en segundo plano cuando un usuario se suscribe a RMS para usuarios y su organización no tiene una suscripción a Office 365 o a Azure y, por lo tanto, tampoco tiene ningún directorio de Azure para autenticar a los usuarios:

1.  Cuando el primer usuario de una organización solicita un suscripción de RMS para usuarios, el nombre de dominio que proporcione en su dirección de correo electrónico se comprobará para consultar si ya está asociado con un inquilino de Azure. Si no hay ningún inquilino, se crea automáticamente un nuevo inquilino y un directorio de Azure para la organización, que contiene una cuenta para este primer usuario. A diferencia de lo que sucede con una suscripción de pago de Azure, esta primera cuenta no es un administrador global, sino un usuario estándar. La nueva cuenta utiliza la dirección de correo electrónico y la contraseña que el usuario proporcionó.

    > [!NOTE]
    > Algunos nombres de dominio no se pueden utilizar para crear el directorio y, por tanto, no se pueden usar en RMS para individuos. La lista de nombres de dominio bloqueados se puede ver en este archivo de Notación de objetos JavaScript: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Si se encuentra un inquilino, se comprueba si ya tiene una suscripción para Azure RMS. Si no se encuentra ninguna suscripción, puede agregarse la suscripción a RMS para usuarios gratuita.

2.  A la organización se le concede una suscripción a RMS para individuos. Ahora, este usuario puede ser autenticado por Azure, por lo que ya puede proteger archivos y leer los que otros usuarios protegiesen mediante Azure Rights Management. Para proteger archivos y leer los protegidos, el usuario debe tener una aplicación habilitada para RMS, como la [aplicación para uso compartido de Rights Management](https://technet.microsoft.com/library/dn919648.aspx) gratuita.

3.  Cuando un segundo usuario de la misma organización solicita una suscripción a RMS para usuarios, se agregará una nueva cuenta de usuario al directorio de Azure creado anteriormente, mediante la suscripción a RMS para usuarios de la organización. Este segundo usuario podrá hacer lo mismo que puede hacer el primer usuario (proteger archivos y leer los protegidos), pero, además, estos dos usuarios podrán colaborar desde este momento con más facilidad y seguridad, ya que podrán aplicar plantillas predeterminadas de forma muy rápida a archivos que limitan el acceso a cuentas del directorio de Azure de su organización.

4.  Los usuarios posteriores de la misma organización seguirán el mismo patrón, es decir, agregarán cuentas de usuario (cuando se suscriban nuevos usuarios) al directorio de Azure de la organización. Cuantas más cuentas se agreguen al directorio, más usuarios podrán colaborar de forma segura con compañeros de trabajo y socios, y les resultará más sencillo evitar que personas no autorizadas lean archivos a los que no deberían tener acceso.

A lo largo de este proceso, no hay cargos adicionales para la organización y no es preciso que se efectúe ningún tipo de trabajo por parte del departamento de TI. Sin embargo, el departamento de TI podría optar por hacer alguna de las siguientes acciones:

-   **Administrar las cuentas y el proceso de suscripción**: Los administradores de TI pueden asumir la titularidad de las cuentas y el directorio creados automáticamente en Azure. Pueden administrar las cuentas mediante la implementación de soluciones de integración del directorio, como sincronización de contraseña e inicio de sesión único. O bien, pueden impedir que los usuarios creen cuentas o se suscriban a RMS para usuarios.

    Para obtener más información, consulte la sección siguiente, [Cómo pueden los administradores controlar las cuentas creadas para RMS para usuarios](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts).

-   **Administrar Rights Management**: Los administradores de TI pueden convertir la suscripción a RMS para usuarios de la organización a una suscripción de pago que incluya Azure Rights Management. Cuando lleven a cabo esta conversión, el directorio y las cuentas existentes de Azure no podrán ser objeto de una transición sencilla para usuarios existentes que estén usando RMS para usuarios. Cualquier archivo que los usuarios hayan protegido con anterioridad permanecerá protegido con las mismas directivas y las personas a las que les garantizaron permisos para usar los archivos todavía podrán usar los archivos del mismo modo.

    Cuando emprenda este proceso, su organización se beneficiará de poder integrar Rights Management en sus flujos de trabajo, servicios y almacenes de datos. Además, podrá administrar Rights Management porque tendrá el control sobre la clave de inquilino de su organización para Azure Rights Management. Ahora puedes tomar las decisiones siguientes:

    -   Configurar Exchange y SharePoint para admitir Azure Rights Management, aunque se estén ejecutando de forma local. Exchange y SharePoint son servicios en línea compatibles de forma nativa y son admitidos por un conector para los servidores locales. Para obtener más información, vea:

        -   Las secciones Exchange Online y SharePoint Online de [Office 365: Configuración para clientes y servicios en línea](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365) en el tema [Configuración de aplicaciones para Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md)

        -   [Implementación del conector de Azure Rights Management](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)

    -   Llevar a cabo descubrimientos electrónicos en los datos pertenecientes a una compañía, de modo que pueda, si es necesario, descifrar archivos que estuviesen protegidos usando Rights Management. Para obtener más información, vea [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

    -   Registrar toda la actividad de cómo se ha usado Rights Management en su organización. Esta es una acción muy potente, ya que no solo puede supervisar qué archivos están protegidos y quién está accediendo a esos archivos protegidos, sino que también puede identificar comportamientos sospechosos potenciales procedentes de personas no autorizadas, que estén intentando acceder a los archivos protegidos. Para obtener más información, vea [Registro y análisis del uso de Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

    -   Proporcionar a los usuarios la capacidad de realizar un seguimiento de sus documentos protegidos y revocarlos, si estas características son compatibles con su [suscripción a Azure RMS](https://technet.microsoft.com/dn858608). Para más información, consulte [Realizar un seguimiento de los archivos y revocarlos](https://technet.microsoft.com/library/dn986611.aspx) en la [Guía de usuario de la aplicación para uso compartido de RMS](https://technet.microsoft.com/library/dn339006.aspx).

    -   Implemente una solución "Aporta tu propia clave" (BYOK) para que la clave de inquilino para Azure Rights Management se genere de forma local, siguiendo las políticas de TI y se transfiera de modo seguro a Microsoft mediante un módulo de seguridad de hardware (HSM). Para obtener más información, vea [Planificación e implementación de tu clave de inquilino de Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

## <a name="BKMK_TakeControlofAccounts"></a>Cómo pueden los administradores controlar las cuentas creadas para RMS para usuarios
Si no desea convertir su suscripción de RMS para usuarios de la organización en una suscripción de pago, todavía puede controlar las cuentas de usuario del directorio de Azure que creó para su organización de los modos que se indican a continuación:

-   Implemente soluciones de integración de directorio para Azure Active Directory y su infraestructura de servicios de dominio de Active Directory. Puede sincronizar cuentas y contraseñas para que los usuarios no tengan que crear nuevas cuentas para utilizar Rights Management y se aplicarán sus políticas de contraseñas locales a las cuentas nuevas de Azure. También puede sincronizar contraseñas para que los usuarios no tengan que recordar una contraseña diferente para utilizar Rights Management.

-   Puede impedir que los usuarios se suscriban para usar Azure Rights Management con la suscripción a RMS para usuarios. En la mayoría de casos, existen muy pocas ventajas en hacerlo, ya que los usuarios o bien compartirán archivos sin protección (lo que podría poner a la compañía en riesgo) o bien utilizarán otro mecanismo de protección de archivos que no le dé la opción al departamento de TI de tener acceso a los datos. Sin embargo, si quiere evitar que los usuarios se suscriban para usar RMS para usuarios, lleve a cabo uno de los procedimientos siguientes después de asumir la titularidad del directorio de su organización en Azure:

    -   Impida que todos los usuarios se suscriban para obtener suscripciones de autoservicio, lo que incluye RMS para individuos.  Actualmente, no puede establecer esto por servicio; la configuración se aplica a todas las suscripciones de Azure que usan el proceso de autoservicio. Para ello, establezca el parámetro **AllowAdHocSubscriptions** en False con el cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) del módulo de Windows PowerShell para Azure Active Directory. Por ejemplo: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Impida que los usuarios creen una cuenta nueva en Azure, lo que significa que solo los usuarios que ya tienen una cuenta de Azure pueden suscribirse para obtener suscripciones de autoservicio, lo que incluye RMS para usuarios.  Para ello, establezca el parámetro **AllowEmailVerifiedUsers** en False con el cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) del módulo de Windows PowerShell para Azure Active Directory. Por ejemplo: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Sincronice su infraestructura de Servicios de dominio de Active Directory con Azure Active Directory. Esta acción evita que se creen cuentas nuevas cuando los usuarios se suscriben para obtener suscripciones de autoservicio como RMS para usuarios, y puede suprimir o deshabilitar cuentas creadas previamente en el directorio de Azure.

Para controlar las cuentas de usuario en el directorio de Azure, o para impedir que los usuarios se suscriban a RMS para usuarios, debe tener una suscripción de Azure y ser titular del directorio. Si todavía no tiene una suscripción a Azure, puede obtener una sin cargo alguno. Si se creó un directorio automáticamente durante el proceso de autoservicio, asuma la titularidad del dominio que se usó para crearla. Si ya tiene un directorio en Azure pero los usuarios especificaron un dominio nuevo que se usa en su organización, combine ese dominio con el directorio existente. Para obtener más información, consulte las instrucciones de [¿Qué es la suscripción de autoservicio de Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)

## <a name="BKMK_Detect"></a>Cómo averiguar si los usuarios se suscribieron para obtener RMS para usuarios
Como administrador, ¿cómo sabes si tus usuarios se han registrado para RMS para usuarios? Puede usar uno de estos métodos o combinarlos según su criterio:

-   Pregunte a los usuarios cómo protegen archivos muy confidenciales, especialmente cuando colaboran con otras personas de fuera de la organización.

-   Si tiene una suscripción de Azure para su organización, use el cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) para ver si **RIGHTSMANAGEMENT_ADHOC** se devuelve como una de las suscripciones. Si es así, se trata de la suscripción RMS para usuarios que se concedió a la organización, con un conjunto de unidades activas disponibles para los usuarios que utilicen el proceso de suscripción de autoservicio.

-   Use una solución de administración de sistemas, como System Center Configuration Manager, para inventariar el software instalado y el software en uso. La aplicación de Rights Management sharing se ejecuta mediante el programa **ipviewer.exe** y se puede [descargar e instalar la aplicación](http://go.microsoft.com/fwlink/?LinkId=303970) gratis para identificar otras características sobre esta aplicación que luego usará para el inventario de software.

-   Manténgase atento a las extensiones de nombre de archivos creadas por la aplicación de uso compartido Rights Management. Las extensiones del nombre de archivo .pfile y .ppdf son el ejemplo más notorio, pero hay otros archivos que cambian su extensión de nombre de archivo cuando están protegidos de forma nativa por Rights Management. Para obtener más información, consulte la sección [Tipos de archivo y extensiones de nombre de archivo compatibles](http://technet.microsoft.com/library/dn339003.aspx) en la [Guía del administrador de la aplicación de Rights Management sharing](http://technet.microsoft.com/library/dn339003.aspx).

## Vea también
[Introducción a Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

