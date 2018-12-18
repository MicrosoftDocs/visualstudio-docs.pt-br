---
title: A instância Experimental | Microsoft Docs
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
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
caps.latest.revision: 37
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b529ba3a0ea8b38a27d06e03ce15106cbd7512a5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787985"
---
# <a name="the-experimental-instance"></a>A instância experimental
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para proteger seu ambiente de desenvolvimento do Visual Studio de aplicativos não testados que pode alterá-lo, VSSDK fornece um espaço de experimental que você pode usar para fazer experiências. Desenvolver novos aplicativos usando o Visual Studio como de costume, mas você pode executá-los usando essa instância experimental.  
  
 Todos os aplicativos que tem um pacote VSIX inicia a instância experimental do Visual Studio no modo de depuração.  
  
 Se você quiser iniciar a instância experimental do Visual Studio fora de uma solução específica, execute o seguinte comando na janela de comando:  
  
 "*\<Caminho de instalação do visual studio >* \Common7\IDE\devenv.exe" RootSuffix Exp  
  
> [!NOTE]
>  A instância experimental é gravada no registro sob o `<version number>Exp` e `<version number>Exp_Config` nós. Por exemplo é a área de registro experimental do Visual Studio 2015  
>   
>  `HKCU\Software\Microsoft\VisualStudio\14.0Exp` e `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`  
  
 É recomendável que você execute sua extensão na instância experimental, enquanto estiver desenvolvendo-o. Quando você implanta a extensão, ele é executado na instância de desenvolvimento. Para obter mais informações sobre como registrar aplicativos, consulte [registrar VSPackages](../extensibility/internals/registering-vspackages.md).

