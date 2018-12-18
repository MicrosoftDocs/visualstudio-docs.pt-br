---
title: 'Como: migrar projetos de extensibilidade para o Visual Studio 2015 | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, upgrading
ms.assetid: 22491cdc-8f04-4e1c-8eb4-ff33798ec792
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 09b8950a05c4e4181209190af17eb0d6ccdb35ba
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39639702"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2015"></a>Como: migrar projetos de extensibilidade para o Visual Studio 2015
Aqui está como atualizar sua extensão.  
  
> [!IMPORTANT]
>  Se você pretende manter uma versão de sua solução de extensão para uma versão anterior do Visual Studio, certifique-se de fazer uma cópia antes de você atualizá-lo. Pode ser difícil retornar a versão atualizada para seu estado anterior.  
  
### <a name="to-upgrade-an-extensibility-solution"></a>Para atualizar uma solução de extensibilidade  
  
1.  Usando a cópia que você deseja atualizar, abra-o na nova versão. Você será informado de que a atualização não é reversível.  
  
2.  Após a conclusão da atualização, altere o caminho do programa externo para a nova versão do *devenv.exe*. Clique com botão direito no nó do projeto na **Gerenciador de soluções**, em seguida, escolha **propriedades**. No **Debug** guia, localize a caixa de texto por **Iniciar programa externo** e altere o caminho da *devenv.exe* para o caminho do Visual Studio 2015, que deve ser semelhante a:  
  
     *%ProgramFiles%\Microsoft visual Studio 14.0\Common7\IDE\devenv.exe*  
  
3.  Adicione uma referência ao *Microsoft.VisualStudio.Shell.14.0.dll*. (Clique com botão direito no nó do projeto na **Gerenciador de soluções** e, em seguida, escolha **Add** > **referência**. Selecione o **extensões** guia e, em seguida, verifique **Microsoft.VisualStudio.Shell.14.0**.)  
  
4.  Compile a solução. Os arquivos criados são implantados para:  
  
     *%LOCALAPPDATA%\Microsoft\VisualStudio.14.0Exp\Extensions\\< nome do autor\>\\< nome do projeto\>\\< versão do projeto\>\\*.  
  
### <a name="to-update-an-extensibility-project-to-nuget-vs-sdk-reference-assemblies"></a>Para atualizar um projeto de extensibilidade para assemblies de referência do SDK do VS NuGet  
  
1.  Determine os assemblies de referência do SDK do VS que precisa do seu projeto.  Na **Gerenciador de soluções**, expanda o projeto **referências** nó e revise a lista de referências do projeto.  Assemblies de referências do SDK do VS terão o prefixo **Microsoft.VisualStudio** no nome (por exemplo: Microsoft.VisualStudio.Shell.14.0).  
  
2.  Remover os assemblies de referência do SDK do VS do projeto, selecionando-os, mouse e selecione **remover**.  
  
3.  Adicione as versões do NuGet dos assemblies de referência do SDK do VS.  Enquanto estiver na **referências do Gerenciador de soluções** nó, abra o **Manage NuGet Packages** caixa de diálogo.  Se você quiser saber mais sobre essa caixa de diálogo, consulte [Gerenciador de pacotes UI](/NuGet/Tools/Package-Manager-UI). Os assemblies de referência do SDK do VS são publicados no [nuget.org](http://www.nuget.org) pela [VisualStudioExtensibility](http://www.nuget.org/profiles/VisualStudioExtensibility).  
  
4.  Usando o **nuget.org** como seu **origem do pacote**, procure o nome do pacote NuGet que satisfaz o assembly de referência desejado (por exemplo: Microsoft.VisualStudio.Shell.14.0) e instalá-lo no seu projeto.  O NuGet pode adicionar vários assemblies de referência para satisfazer as dependências do assembly inicial.  
  
     Se você preferir, você pode adicionar todos os assemblies de referência do SDK do VS ao mesmo tempo, instalar o SDK do VS [metapacote](http://www.nuget.org/packages/VSSDK_Reference_Assemblies).  
  
5.  Você também pode alternar para usar a versão do NuGet das ferramentas de build do SDK do VS. Este pacote do NuGet está [Microsoft.VSSDK.BuildTools](http://www.nuget.org/packages/Microsoft.VSSDK.BuildTools) e uma vez adicionado ao seu projeto será incluem as ferramentas necessárias e arquivos para permitir que você compile seu projeto de extensibilidade em um computador sem o SDK do VS instalado de destino.  
  
> [!NOTE]
>  Não é necessário que você atualize seus projetos de extensibilidade existentes para usar as ferramentas e assemblies de referência do NuGet.  Eles podem continuar a criar usando assemblies de referência e ferramentas instaladas com o SDK do VS.