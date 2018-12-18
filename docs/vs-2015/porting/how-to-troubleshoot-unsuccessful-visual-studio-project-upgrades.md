---
title: 'Como: Solucionar problemas de atualizações de projeto malsucedidas | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VisualStudio.SourceControl.CannotOpenFromSourceControlDSW
- vs.UpgradeProjectSolution.8.0
helpviewer_keywords:
- upgrading applications, Visual Studio
- upgrading projects [Visual Studio]
- projects [Visual Studio], upgrading
- Visual Studio Conversion Wizard
- Conversion wizard
ms.assetid: 842fe448-c044-4343-8eae-d81711cf48ba
caps.latest.revision: 31
author: kraigb
ms.author: kraigb
manager: ghogen
ms.openlocfilehash: 6b50bbaaf7e5b018709f3cf0dece3c0ae38410f8
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53064784"
---
# <a name="how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades"></a>Como: Solucionar problemas de atualizações de projeto do Visual Studio malsucedidas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Às vezes, o Visual Studio não pode converter totalmente um projeto de uma versão anterior do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Se as dicas nas seções a seguir não resolverem seu problema específico, você poderá encontrar mais informações sobre o TechNet [Wiki: Portal de desenvolvimento](http://go.microsoft.com/fwlink/?LinkId=254808).

## <a name="the-project-does-not-run-because-files-are-not-found"></a>O projeto não será executado porque os arquivos não foram localizados
 Um arquivo de projeto contém os caminhos de arquivo codificados que o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] usa para executar o projeto quando você pressiona F5. Esses caminhos podem incluir o local do devenv.exe e outros arquivos necessários. Em uma versão atualizada do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], os caminhos desses arquivos podem ter sido alterados.

#### <a name="to-resolve-incorrect-file-paths"></a>Para resolver caminhos de arquivos incorretos

1.  Abra o arquivo de projeto em um editor de texto.

2.  Examine os caminhos de arquivo que podem estar incorretos, especialmente os que contêm um número de versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].

3.  Modifique caminhos de arquivos incorretos de modo que apontem para novos destinos.

## <a name="the-project-does-not-build-because-references-are-not-valid"></a>O projeto não será compilado porque as referências não são válidas
 Quando você atualiza o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], também pode estar atualizando a versão do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Se o projeto contiver as referências que estão descontinuadas na versão mais recente do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], elas podem não ser resolvidas corretamente. Isso é especialmente provável para referências que incluem números de versão, por exemplo, `Microsoft.VisualStudio.Shell.Interop.8.0`.

 Se seu código tiver muitas referências inválidas, a solução mais fácil pode ser usar o recurso de vários destinos do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para destinar uma versão anterior do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].

#### <a name="to-resolve-incorrect-references"></a>Para resolver referências incorretas

1. Abra o arquivo de projeto em um editor de texto.

2. Abra as propriedades do projeto.

3. Selecione o valor correto de **Estrutura de Destino**. De maneira alternativa, você pode modificar o valor do elemento `<TargetFrameworkVersion>` diretamente no arquivo de projeto.

   Se você quiser que seu projeto seja executado na versão atualizada do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], deverá atualizar as referências do projeto, e também atualizar todas as instruções de `Imports` ou `Using` que chamam as referências. Se o projeto for carregado no IDE, você poderá atualizar as referências usando o **Gerenciador de Soluções** ou a caixa de diálogo **Gerenciador de Referências**.

## <a name="see-also"></a>Consulte também
 [/ Atualização (devenv.exe)](../ide/reference/upgrade-devenv-exe.md) [convertendo para o ASP.NET 4](http://msdn.microsoft.com/library/790147c6-36c1-41b5-a52d-30b9ccd2bd10)
