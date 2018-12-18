---
title: Gerenciar VSPackages | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
caps.latest.revision: 36
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8cb96dfbdecd5182d328d425a209f52833ede23c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781589"
---
# <a name="managing-vspackages"></a>Gerenciando VSPackages
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na maioria dos casos, você não precisa se preocupar sobre como gerenciar VSPackages, já que os modelos de projeto e item registrarem e carregar o pacote automaticamente. No entanto, em algumas circunstâncias você talvez precise saber um pouco mais para gerenciar seu pacote.  
  
## <a name="using-the-experimental-instance"></a>Usando a instância experimental  
 Para obter mais informações sobre a instância experimental, consulte [a instância Experimental](../extensibility/the-experimental-instance.md).  
  
## <a name="registering-and-unregistering-vspackages"></a>Registrando e cancelando o registro de VSPackages  
 Para saber como registrar e cancelar o registro de VSPackages e outros tipos de extensão, consulte [Registrando e Cancelando o registro de VSPackages](../extensibility/registering-and-unregistering-vspackages.md).  
  
## <a name="loading-a-vspackage"></a>Carregar um VSPackage  
 Os VSPackages pode ser definidos como autoload quando um determinado que CMDUICONTEXT GUID está ativado. Para obter mais informações, consulte [carregar VSPackages](../extensibility/loading-vspackages.md).  
  
## <a name="using-asyncpackage-to-load-vspackages-in-the-background"></a>Usar AsyncPackage para carregar VSPackages em segundo plano  
 A classe AsyncPackage permite que o pacote de carregamento em um thread em segundo plano para melhor capacidade de resposta da interface do usuário no Visual Studio. Para obter mais informações, consulte [como: usar AsyncPackage para carregar VSPackages em segundo plano](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md).  
  
## <a name="rule-based-ui-context-for-extensions"></a>Contexto de interface do usuário baseada em regras para extensões  
 Com base em regras de contextos de interface do usuário permite que os autores de extensão definir as condições precisas sob as quais um contexto de interface do usuário é ativado e carregar VSPackages associados. Para obter mais informações, consulte [como: contexto de interface do usuário baseada em regras de uso para extensões do Visual Studio](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md).  
  
## <a name="troubleshooting-vspackages"></a>Solucionando problemas de VSPackages  
 Descubra as técnicas para solucionar problemas de VSPackages que não são carregados ou estão com erros: [VSPackages de solução de problemas](../extensibility/troubleshooting-vspackages.md)  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)

