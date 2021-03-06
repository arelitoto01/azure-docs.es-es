---
title: 'Integración del centro de datos de Azure Stack: DNS'
description: Obtenga información sobre cómo integrar el DNS de Azure Stack con el DNS de su centro de datos.
services: azure-stack
author: jeffgilb
manager: femila
ms.service: azure-stack
ms.topic: article
ms.date: 02/12/2019
ms.author: jeffgilb
ms.reviewer: wfayed
ms.lastreviewed: 10/15/2018
keywords: ''
ms.openlocfilehash: 13525fffb7e6720fe81759876ffd0fe71559279c
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2019
ms.locfileid: "56182857"
---
# <a name="azure-stack-datacenter-integration---dns"></a>Integración del centro de datos de Azure Stack: DNS
Para tener acceso a los puntos de conexión de Azure Stack (**portal**, **adminportal**, **management**, **adminmanagement**, etc.) desde fuera de Azure Stack, debe integrar los servicios de DNS de Azure Stack con los servidores DNS que hospedan las zonas DNS que quiere usar en Azure Stack.

## <a name="azure-stack-dns-namespace"></a>Espacio de nombres de DNS de Azure Stack
Se le solicitará que proporcione información importante relacionada con DNS cuando implemente Azure Stack.


|Campo  |DESCRIPCIÓN  |Ejemplo|
|---------|---------|---------|
|Region|Ubicación geográfica de la implementación de Azure Stack.|`east`|
|Nombre de dominio externo|Nombre de la zona que quiere usar para la implementación de Azure Stack.|`cloud.fabrikam.com`|
|Nombre de dominio interno|Nombre de la zona interna que se usa para servicios de infraestructura en Azure Stack.  Está integrado en Directory Service y es privado (no es accesible desde fuera de la implementación de Azure Stack).|`azurestack.local`|
|Reenviador DNS|Servidores DNS que se usan para reenviar consultas DNS, registros y zonas DNS que se hospedan fuera de Azure Stack, ya sea en la intranet corporativa o en la red pública de Internet.|`10.57.175.34`<br>`8.8.8.8`|
|Prefijo de nomenclatura (opcional)|Prefijo de nomenclatura que quiere que tengan los nombres de máquina de instancia de rol de infraestructura de Azure Stack.  Si no se proporciona, el valor predeterminado es `azs`.|`azs`|

El nombre de dominio completo (FQDN) de su implementación y puntos de conexión de Azure Stack es la combinación de los parámetros de región y de nombre de dominio externo. Con los valores de los ejemplos de la tabla anterior, el FQDN para esta implementación de Azure Stack sería el siguiente:

`east.cloud.fabrikam.com`

De esta forma, los ejemplos de algunos de los puntos de conexión de esta implementación tendrían un aspecto parecido a las direcciones URL siguientes:

`https://portal.east.cloud.fabrikam.com`

`https://adminportal.east.cloud.fabrikam.com`

Para usar este espacio de nombres DNS de ejemplo para una implementación de Azure Stack, se deben cumplir las condiciones siguientes:

- La zona `fabrikam.com` está registrada con un registrador de dominios, con un servidor DNS corporativo interno o con ambos, en función de los requisitos de resolución de nombres.
- El dominio secundario `cloud.fabrikam.com` existe en la zona `fabrikam.com`.
- Los servidores DNS que hospedan las zonas `fabrikam.com` y `cloud.fabrikam.com` son accesibles desde la implementación de Azure Stack.

Para poder resolver nombres DNS para puntos de conexión e instancias de Azure Stack desde fuera de Azure Stack, debe integrar los servidores DNS que hospedan la zona DNS externa para Azure Stack con los servidores DNS que hospedan la zona principal que quiere usar.


## <a name="resolution-and-delegation"></a>Resolución y delegación

Existen dos tipos de servidores DNS:

- Un servidor DNS autoritativo hospeda zonas DNS. Solo responde a las consultas DNS de los registros de dichas zonas.
- Un servidor DNS recursivo no hospeda zonas DNS. Responde a todas las consultas DNS, para lo que realiza una llamada a los servidores DNS autoritativos a fin de recopilar los datos que necesita.

Azure Stack incluye servidores DNS autoritativos y recursivos. Los servidores recursivos se usan para resolver todos los nombres, salvo para la zona privada interna y la zona DNS pública externa para esa implementación de Azure Stack. 

![Arquitectura de DNS de Azure Stack](media/azure-stack-integrate-dns/Integrate-DNS-01.png)

## <a name="resolving-external-dns-names-from-azure-stack"></a>Resolver nombres DNS externos desde Azure Stack

Para resolver nombres DNS para puntos de conexión fuera de Azure Stack (por ejemplo, www.bing.com), deberá proporcionar servidores DNS que Azure Stack pueda usar para reenviar las solicitudes DNS para las que Azure Stack no es autoritativo. Para la implementación, se requieren los servidores DNS a los que Azure Stack reenvía las solicitudes en la hoja de cálculo de implementación (en el campo Reenviador DNS). Proporcione al menos dos servidores en este campo por razones de tolerancia a errores. Sin estos valores, se produce un error de implementación de Azure Stack.

### <a name="configure-conditional-dns-forwarding"></a>Configure el reenvío condicional de DNS

> [!IMPORTANT]
> Esto solo se aplica a una implementación de AD FS.

Para habilitar la resolución de nombres con la infraestructura DNS existente, configure el reenvío condicional.

Para agregar un reenviador condicional, debe utilizar el punto de conexión con privilegios.

Para este procedimiento, use un equipo de la red del centro de datos que pueda comunicarse con el punto de conexión con privilegios de Azure Stack.

1. Abra una sesión de Windows PowerShell con privilegios elevados (ejecútela como administrador) y conéctese a la dirección IP del punto de conexión con privilegios. Use las credenciales para la autenticación de CloudAdmin.

   ```
   $cred=Get-Credential 
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $cred
   ```

2. Después de conectarse al punto de conexión con privilegios, ejecute el siguiente comando de PowerShell. Sustituya los valores de ejemplo proporcionados por su nombre de dominio y direcciones IP de los servidores DNS que quiere usar.

   ```
   Register-CustomDnsServer -CustomDomainName "contoso.com" -CustomDnsIPAddresses "192.168.1.1","192.168.1.2"
   ```

## <a name="resolving-azure-stack-dns-names-from-outside-azure-stack"></a>Resolver nombres DNS de Azure Stack desde fuera de Azure Stack
Los servidores autoritativos son los que contienen la información de zona DNS externa y las zonas creadas por el usuario. Realice la integración con estos servidores para habilitar la delegación de zona o el reenvío condicional para resolver nombres DNS de Azure Stack desde fuera de Azure Stack.

## <a name="get-dns-server-external-endpoint-information"></a>Obtener información del punto de conexión externo del servidor DNS

Para integrar la implementación de Azure Stack con la infraestructura DNS, necesitará la información siguiente:

- FQDN del servidor DNS
- Direcciones IP del servidor DNS

Los FQDN de los servidores DNS de Azure Stack tienen el formato siguiente:

`<NAMINGPREFIX>-ns01.<REGION>.<EXTERNALDOMAINNAME>`

`<NAMINGPREFIX>-ns02.<REGION>.<EXTERNALDOMAINNAME>`

Con los valores de ejemplo, los FQDN de los servidores DNS son los siguientes:

`azs-ns01.east.cloud.fabrikam.com`

`azs-ns02.east.cloud.fabrikam.com`


Esta información también se crea al final de todas las implementaciones de Azure Stack en un archivo denominado `AzureStackStampInformation.json`. Este archivo se encuentra en la carpeta `C:\CloudDeployment\logs` de la máquina virtual de implementación. Si no está seguro de qué valores se han usado para la implementación de Azure Stack, puede obtener los valores desde aquí.

Si la máquina virtual de implementación ya no está disponible o no es accesible, puede obtener los valores si se conecta al punto de conexión con privilegios y ejecuta el cmdlet `Get-AzureStackStampInformation` de PowerShell. Para más información, consulte [Punto de conexión con privilegios](azure-stack-privileged-endpoint.md).

## <a name="setting-up-conditional-forwarding-to-azure-stack"></a>Configurar el reenvío condicional a Azure Stack

La manera más sencilla y segura de integrar Azure Stack con la infraestructura de DNS es hacer un reenvío condicional de la zona desde el servidor que hospeda la zona principal. Se recomienda este enfoque si tiene el control directo de los servidores DNS que hospedan la zona principal del espacio de nombres DNS externo de Azure Stack.

Si no está familiarizado con los reenvíos condicionales mediante DNS, consulte el siguiente artículo de TechNet: [Assign a Conditional Forwarder for a Domain Name](https://technet.microsoft.com/library/cc794735) (Asignación de reenviadores condicionales a un nombre de dominio) o la documentación específica de la solución DNS.

Si ha especificado que la zona DNS externa de Azure Stack debe parecer un dominio secundario de su nombre de dominio corporativo, no se puede usar el reenvío condicional. Se debe configurar la delegación DNS.

Ejemplo:

- Nombre de dominio DNS corporativo: `contoso.com`
- Nombre de dominio DNS externo de Azure Stack: `azurestack.contoso.com`

## <a name="delegating-the-external-dns-zone-to-azure-stack"></a>Delegar la zona DNS externa en Azure Stack

Para que los nombres DNS puedan resolverse desde fuera de una implementación de Azure Stack, debe configurar la delegación de DNS.

Cada registrador dispone de sus propias herramientas de administración de DNS para cambiar los registros de servidores de nombres de un dominio. En la página de administración de DNS del registrador, edite los registros NS y reemplace los registros NS de la zona por los de Azure Stack.

La mayoría de los registradores DNS requieren que se proporcione un mínimo de dos servidores DNS para completar la delegación.

## <a name="next-steps"></a>Pasos siguientes

[Integración del firewall](azure-stack-firewall.md)
