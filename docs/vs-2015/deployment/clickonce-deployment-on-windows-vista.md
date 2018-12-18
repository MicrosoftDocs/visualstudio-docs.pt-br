---
title: Implantação do ClickOnce no Windows Vista | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- UAC manifest generation
- ClickOnce deployment, Windows
- manifest generation
- Windows, ClickOnce deployment
ms.assetid: b21a0ebc-0ff6-4f49-8993-7d1ad3f8cac2
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: a0b8b4b5cff478a2dbe03f3f72115da3c0696c4e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49852045"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Implantação do ClickOnce no Windows Vista
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Criando aplicativos no Visual Studio para controle de conta de usuário (UAC) no Windows Vista normalmente gera um manifesto inserido, como dados binários codificados XML no arquivo executável do aplicativo. Como os aplicativos ClickOnce e COM sem registro requerem um manifesto externo, o Visual Studio gera um arquivo para esses tipos de projetos que contém os dados UAC em vez de um manifesto inserido. Por padrão, o Visual Studio usa informações de um arquivo chamado manifest para gerar informações de manifesto de UAC externas (para implantação do ClickOnce e COM sem registro), ou para inseri-la no arquivo executável do aplicativo (para todos os outros casos). Visual Studio fornece as seguintes opções para geração de manifesto:  
  
- Use um manifesto inserido. Inserir dados UAC no arquivo executável do aplicativo e executar como usuário normal.  
  
   Isso é a configuração padrão (a menos que você usa o ClickOnce). Essa configuração oferecerá suporte da maneira normal em que o Visual Studio funciona no Windows Vista; ou seja, a geração de um manifesto interno e externo, ambos usando `AsInvoker`.  
  
- Use um manifesto externo. Gere um manifesto externo usando o manifest.  
  
   Isso gera apenas o manifesto externo usando as informações no App. manifest. Quando você publica um aplicativo usando o ClickOnce ou COM sem registro, o Visual Studio adiciona manifest para o projeto e adiciona essa opção.  
  
- Não use nenhum manifesto. Crie o aplicativo sem um manifesto.  
  
   Essa abordagem também é conhecido como *virtualização*. Use esta opção para compatibilidade com aplicativos existentes de versões anteriores do Visual Studio.  
  
  As novas propriedades estão disponíveis na **aplicativo** página do Designer de projeto (Visual c# somente para projetos) e no formato de arquivo de projeto MSBuild.  
  
  Observe que o método para configurar a geração de manifesto de UAC no IDE do Visual Studio difere dependendo do tipo de projeto (Visual c# e Visual Basic).  
  
  Para obter informações sobre como configurar projetos do Visual c# para geração de manifesto, consulte [página de aplicativo, Designer de projeto (c#)](../ide/reference/application-page-project-designer-csharp.md).  
  
  Para obter informações sobre como configurar projetos do Visual Basic para geração de manifesto, consulte [página de aplicativo, Designer de projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md).  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Permissões de usuário e o Visual Studio](http://msdn.microsoft.com/en-us/d5c55084-1e7b-4b61-b478-137db01c0fc0)   
 [Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md)   
 [Página de Aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)



