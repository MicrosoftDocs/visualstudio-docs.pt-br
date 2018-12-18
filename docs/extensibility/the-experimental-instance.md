---
title: A instância Experimental | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c80c071866e46528fe7edd287e082df3af166973
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31138919"
---
# <a name="the-experimental-instance"></a>A instância Experimental
Para proteger seu ambiente de desenvolvimento do Visual Studio de aplicativos não testados que alterá-la, o VSSDK fornece um espaço experimental que você pode usar para testar. Desenvolver novos aplicativos usando o Visual Studio como de costume, mas você pode executá-los usando esta instância experimental.  
  
 Todos os aplicativos que tem um pacote do VSIX inicia a instância experimental do Visual Studio no modo de depuração.  
  
 Se você deseja iniciar a instância experimental do Visual Studio fora de uma solução específica, execute o seguinte comando na janela de comando:  
  
 "*\<Caminho de instalação do visual studio >* \Common7\IDE\devenv.exe" RootSuffix Exp  
  
> [!NOTE]
>  A instância experimental é gravada no registro sob o `<version number>Exp` e `<version number>Exp_Config` nós. Por exemplo é a área de registro experimental do Visual Studio 2015  
>   
>  `HKCU\Software\Microsoft\VisualStudio\14.0Exp` e `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`  
  
 É recomendável que você execute sua extensão na instância experimental enquanto você estiver desenvolvendo-o. Quando você implantar a extensão, ele é executado na instância de desenvolvimento. Para obter mais informações sobre o registro de aplicativos, consulte [VSPackages registrar](../extensibility/internals/registering-vspackages.md).