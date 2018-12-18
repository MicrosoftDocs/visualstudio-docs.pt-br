---
title: Gerenciar VSPackages | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 14aa17f4692857d650cb3bc9fe1a3498fc4f147a
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39639547"
---
# <a name="manage-vspackages"></a>Gerenciar VSPackages
Na maioria dos casos, você não precisa se preocupar sobre como gerenciar VSPackages, já que os modelos de projeto e item registrarem e carregar o pacote automaticamente. No entanto, em algumas circunstâncias você talvez precise saber um pouco mais para gerenciar seu pacote.  
  
## <a name="use-the-experimental-instance"></a>Usar a instância experimental  
 Para obter mais informações sobre a instância experimental, consulte [a instância experimental](../extensibility/the-experimental-instance.md).  
  
## <a name="register-and-unregister-vspackages"></a>Registrar e cancelar o registro de VSPackages  
 Para saber como registrar e cancelar o registro de VSPackages e outros tipos de extensão, consulte [registrar e cancelar o registro de VSPackages](../extensibility/registering-and-unregistering-vspackages.md).  
  
## <a name="load-a-vspackage"></a>Carregar um VSPackage  
 Os VSPackages pode ser definidos como autoload quando um determinado que CMDUICONTEXT GUID está ativado. Para obter mais informações, consulte [carregar VSPackages](../extensibility/loading-vspackages.md).  
  
## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>Usar AsyncPackage para carregar VSPackages em segundo plano  
 O `AsyncPackage` classe permite o carregamento do pacote em um thread em segundo plano para melhor capacidade de resposta da interface do usuário no Visual Studio. Para obter mais informações, consulte [como: usar AsyncPackage para carregar VSPackages em segundo plano](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md).  
  
## <a name="rule-based-ui-context-for-extensions"></a>Contexto de interface do usuário baseada em regras para extensões  
 Com base em regras de contextos de interface do usuário permite que os autores de extensão definir as condições precisas sob as quais um contexto de interface do usuário é ativado e carregar VSPackages associados. Para obter mais informações, consulte [como: usar o contexto de interface do usuário baseada em regras para extensões do Visual Studio](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md).  
  
## <a name="diagnose-extension-performance"></a>Diagnosticar o desempenho da extensão  
Extensões podem afetar o desempenho de carga de solução e de inicialização. Saiba como é calculado o impacto de extensão do Visual Studio e como podem ser analisado em localmente para testar se uma extensão pode ser mostrada como um desempenho afetando a extensão. Para obter mais informações, consulte [como: diagnosticar o desempenho da extensão](how-to-diagnose-extension-performance.md). 
  
## <a name="troubleshoot-vspackages"></a>Solucionar problemas de VSPackages  
 Descubra as técnicas para solucionar problemas de VSPackages que não são carregados ou estão com erros: [solucionar problemas de VSPackages](../extensibility/troubleshooting-vspackages.md)  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)