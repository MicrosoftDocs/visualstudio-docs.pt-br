---
title: 'Como: registrar um serviço | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- services, registering
ms.assetid: d086be78-ec3c-43cc-b799-5180a71e19f1
caps.latest.revision: 16
manager: douge
ms.openlocfilehash: a1f8026a648b2a0809af17664d4399f815c329be
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49206252"
---
# <a name="how-to-register-a-service"></a>Como: registrar um serviço
A estrutura de pacote gerenciado (MPF) fornece os atributos para controlar o registro de serviços gerenciados. O utilitário RegPkg usa esses atributos para registrar um serviço com [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="example"></a>Exemplo  
 O código a seguir é de [exemplos de VSSDK](../misc/vssdk-samples.md).  
  
 [!code-csharp[VSSDKRegisterService#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkregisterservice/cs/vssdkregisterservicepackage.cs#1)]
 [!code-vb[VSSDKRegisterService#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkregisterservice/vb/vssdkregisterservicepackage.vb#1)]  
  
 O <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> registra o serviço SMyGlobalService com [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para obter mais informações sobre <xref:Microsoft.VisualStudio.Shell.DefaultRegistryRootAttribute> e <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>, consulte [Registrando e Cancelando o registro de VSPackages](../extensibility/registering-and-unregistering-vspackages.md).  
  
 Para registrar um serviço que substitui outro serviço com o mesmo nome, use o <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute> em vez do <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>.  
  
## <a name="robust-programming"></a>Programação robusta  
 Para facilitar recompilar um provedor de serviço sem alterar o cliente do serviço, ou vice-versa, você pode definir o serviço e suas interfaces em um módulo de assembly separado. O código a seguir é do arquivo IMyGlobalService.cs na amostra Reference.Services (c#).  
  
 [!code-csharp[VSSDKRegisterService#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkregisterservice/cs/vssdkregisterservicepackage.cs#2)]
 [!code-vb[VSSDKRegisterService#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkregisterservice/vb/vssdkregisterservicepackage.vb#2)]  
  
 O <xref:System.Runtime.InteropServices.ComVisibleAttribute> é necessária para obter a interface de código não gerenciado.  
  
> [!NOTE]
>  Embora você possa usar o mesmo tipo ou o GUID para o serviço e a interface, é recomendável que você separe as duas como um serviço pode expor interfaces diferentes.  
  
## <a name="see-also"></a>Consulte também  
 [Registrar VSPackages](http://msdn.microsoft.com/en-us/31e6050f-1457-4849-944a-a3c36b76f3dd)   
 [Fundamentos do serviço](../extensibility/internals/service-essentials.md)