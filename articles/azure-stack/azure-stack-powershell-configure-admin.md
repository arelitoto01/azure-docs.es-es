---
title: Conexión a Azure Stack con PowerShell como operador | Microsoft Docs
description: Obtenga información sobre cómo conectarse a Azure Stack con PowerShell como operador
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: article
ms.date: 02/11/2019
ms.author: mabrigg
ms.reviewer: thoroet
ms.lastreviewed: 01/24/2019
ms.openlocfilehash: d5b2b1a73a15874072caacd7549c1c328e7edb26
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56116565"
---
# <a name="connect-to-azure-stack-with-powershell-as-an-operator"></a>Conexión a Azure Stack con PowerShell como operador

*Se aplica a: sistemas integrados de Azure Stack y Kit de desarrollo de Azure Stack*

Puede configurar Azure Stack para usar PowerShell a fin de administrar recursos como la creación de ofertas, planes, cuotas y alertas. Este tema le ayuda a configurar el entorno de operador.

## <a name="prerequisites"></a>Requisitos previos

Implemente los siguientes requisitos previos desde el [kit de desarrollo](./asdk/asdk-connect.md#connect-with-rdp) o desde un cliente externo basado en Windows si se [conecta al ASDK mediante VPM](./asdk/asdk-connect.md#connect-with-vpn). 

 - Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).  
 - Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).  

## <a name="connect-with-azure-ad"></a>Conexión con Azure AD

Configuración del entorno de operador de Azure Stack con PowerShell Ejecute uno de los siguientes scripts: Reemplace los valores de tenantName de Azure Active Directory (Azure AD) y el punto de conexión de Azure Resource Manager por la configuración de su propio entorno. <!-- GraphAudience endpoint -->

```PowerShell  
    # Register an Azure Resource Manager environment that targets your Azure Stack instance. Get your Azure Resource Manager endpoint value from your service provider.
Add-AzureRMEnvironment -Name "AzureStackAdmin" -ArmEndpoint "https://adminmanagement.local.azurestack.external"

    # Set your tenant name
    $AuthEndpoint = (Get-AzureRmEnvironment -Name "AzureStackAdmin").ActiveDirectoryAuthority.TrimEnd('/')
    $AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com"
    $TenantId = (invoke-restmethod "$($AuthEndpoint)/$($AADTenantName)/.well-known/openid-configuration").issuer.TrimEnd('/').Split('/')[-1]

    # After signing in to your environment, Azure Stack cmdlets
    # can be easily targeted at your Azure Stack instance.
    Add-AzureRmAccount -EnvironmentName "AzureStackAdmin" -TenantId $TenantId
```

## <a name="connect-with-ad-fs"></a>Conexión con AD FS

Conéctese al entorno de operador de Azure Stack con PowerShell con Azure Active Directory Federated Services (Azure AD FS). Para el Kit de desarrollo de Azure Stack, este punto de conexión de Azure Resource Manager se establece en `https://adminmanagement.local.azurestack.external`. Para obtener el punto de conexión de Azure Resource Manager para los sistemas integrados de Azure Stack, póngase en contacto con su proveedor de servicios.

<!-- GraphAudience endpoint -->

  ```PowerShell  
  # Register an Azure Resource Manager environment that targets your Azure Stack instance. Get your Azure Resource Manager endpoint value from your service provider.
  Add-AzureRMEnvironment -Name "AzureStackAdmin" -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Sign in to your environment
  Login-AzureRmAccount -EnvironmentName "AzureStackAdmin"
  ```

> [!Note]  
> AD FS solo admite la autenticación interactiva con identidades de usuario. Si se requiere un objeto de credencial, debe usar una entidad de servicio (SPN). Para más información acerca de cómo configurar una entidad de servicio con Azure Stack y AD FS como servicio de administración de identidades, consulte [Administración de una entidad de servicio para AD FS](azure-stack-create-service-principals.md#manage-service-principal-for-ad-fs).

## <a name="test-the-connectivity"></a>Prueba de la conectividad

Ahora que todo está configurado, use PowerShell para crear recursos en Azure Stack. Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual. Use el comando siguiente para crear un grupo de recursos denominado **MyResourceGroup**.

```PowerShell  
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Pasos siguientes

 - [Desarrollo de plantillas para Azure Stack](user/azure-stack-develop-templates.md)
 - [Implementación de plantillas con PowerShell](user/azure-stack-deploy-template-powershell.md)
