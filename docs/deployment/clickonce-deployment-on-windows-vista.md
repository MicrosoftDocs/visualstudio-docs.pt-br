---
title: Implantação do ClickOnce no Windows Vista | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0389665349ae9c39a0f820bc047af6cc4db2b683
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867527"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Implantação do ClickOnce no Windows Vista

Criando aplicativos no Visual Studio para controle de conta de usuário (UAC) no Windows Vista normalmente gera um manifesto inserido, como dados binários codificados XML no arquivo executável do aplicativo.  Aplicativos ClickOnce e COM sem registro exigem um manifesto externo, portanto, o Visual Studio gera um arquivo para esses projetos que contém os dados UAC em vez de um manifesto inserido. Para implantações do ClickOnce e COM sem registro, o Visual Studio usa informações de um arquivo chamado *manifest* para gerar informações de manifesto de UAC externo. Todos os outros casos, o Visual Studio insere os dados UAC no arquivo executável do aplicativo. 

Visual Studio fornece as seguintes opções para geração de manifesto:  
  
- Use um manifesto inserido. Inserir dados UAC no arquivo executável do aplicativo e executar como usuário normal.  
  
   Isso é a configuração padrão (a menos que você usa o ClickOnce). Essa configuração oferece suporte a da maneira normal em que o Visual Studio funciona no Windows Vista, com a geração de interno e externo de manifesto usando `AsInvoker`.  
  
- Use um manifesto externo. Gerar um manifesto externo usando *manifest*.  
  
   Isso gera apenas o manifesto externo usando as informações em *manifest*. Quando você publica um aplicativo usando o ClickOnce ou COM sem registro, o Visual Studio adiciona *manifest* ao projeto e, em seguida, adiciona essa opção.  
  
- Não use nenhum manifesto. Crie o aplicativo sem um manifesto.  
  
   Essa abordagem também é conhecido como *virtualização*. Use esta opção para compatibilidade com aplicativos existentes de versões anteriores do Visual Studio.  
  
  As novas propriedades estão disponíveis na **aplicativo** página do Designer de projeto (Visual c# somente para projetos) e no formato de arquivo de projeto MSBuild.  
  
  O método para configurar a geração de manifesto de UAC no IDE do Visual Studio difere dependendo do tipo de projeto (Visual c# ou Visual Basic).  
  
  * Para obter informações sobre como configurar projetos do Visual c# para geração de manifesto, consulte [página de aplicativo, Designer de projeto (c#)](../ide/reference/application-page-project-designer-csharp.md).  
  
  * Para obter informações sobre como configurar projetos do Visual Basic para geração de manifesto, consulte [página de aplicativo, Designer de projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md).  
  
## <a name="see-also"></a>Consulte também  
 [Implantação e segurança do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Permissões de usuário e o Visual Studio](https://msdn.microsoft.com/library/d5c55084-1e7b-4b61-b478-137db01c0fc0)   
 [Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md)   
 [Página de Aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)