---
title: Visão geral de multissegmentação | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- targeting .NET Framework version [Visual Studio]
- versions [Visual Studio], targeting .NET Framework version
- multi-targeting [Visual Studio]
- multitargeting [Visual Studio]
ms.assetid: b1702c33-0672-4ebc-b779-2b324d6ea880
caps.latest.revision: 39
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 54aabe4871ee7f40e32d42cefd8d291276f361cb
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53049781"
---
# <a name="visual-studio-multi-targeting-overview"></a>Visão geral de multissegmentação do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Nesta versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], é possível especificar a versão do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] necessária para seu aplicativo. Portanto, se você desejar usar essa versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para continuar desenvolvendo um projeto iniciado em uma versão anterior, não será necessário alterar o destino da estrutura. Também é possível criar uma solução que contém projetos que têm como destino versões diferentes da estrutura. A definição de destino da estrutura também ajuda a assegurar que o aplicativo use apenas a funcionalidade disponível na versão especificada da estrutura.

> [!TIP]
>  Também é possível definir aplicativos como destino para plataformas diferentes. Para obter mais informações, consulte [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md)

## <a name="framework-targeting-features"></a>Recursos de definição de destino da estrutura
 A definição de destino da estrutura inclui os seguintes recursos:

- Ao abrir um projeto que tem como destino uma versão anterior do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], o [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] pode atualizá-lo ou deixar o destino no estado em que se encontra.

- Ao criar um projeto, é possível especificar a versão do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] que você deseja definir como destino.

- É possível alterar a versão do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] que um projeto existente tem como destino.

- É possível definir como destino uma versão diferente do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] em cada um dos vários projetos na mesma solução.

- Ao alterar a versão do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] que um projeto tem como destino, o [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] faz as alterações necessárias nas referências e nos arquivos de configuração.

  Ao trabalhar em um projeto que tem como destino uma versão anterior do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], o Visual Studio altera dinamicamente o ambiente de desenvolvimento, da seguinte maneira:

- Ele filtra os itens das caixas de diálogo **Novo Projeto**, **Adicionar Novo Item**, **Adicionar Nova Referência** e **Adicionar Referência de Serviço** para omitir as opções que não estão disponíveis na versão de destino.

- Ele filtra os controles personalizados da **Caixa de ferramentas** para remover aqueles que não estão disponíveis na versão de destino e mostrar somente os controles mais atualizados quando vários controles estão disponíveis.

- Ele filtra o IntelliSense para omitir os recursos de idioma que não estão disponíveis na versão de destino.

- Ele filtra as propriedades na janela **Propriedades** para omitir aquelas que não estão disponíveis na versão de destino.

- Ele filtra as opções de menu para omitir as opções que não estão disponíveis na versão de destino.

- Para builds, ele usa a versão do compilador e as opções do compilador apropriadas para a versão de destino.

> [!NOTE]
>  A definição de destino da estrutura não assegura que o aplicativo será executado corretamente. É necessário testar o aplicativo para ter certeza de que ele é executado na versão de destino. Não é possível definir como destino versões de estrutura anteriores ao .NET Framework 2.0.

## <a name="selecting-a-target-framework-version"></a>Selecionando uma versão de estrutura de destino
 Ao criar um projeto, selecione a versão [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] de destino na caixa de diálogo **Novo Projeto**. A lista de modelos de projeto disponíveis é filtrada com base na seleção. Em um projeto existente, é possível alterar a versão [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] de destino na caixa de diálogo das propriedades do projeto. Confira mais informações em [Como: Direcionar a uma versão do .NET Framework](../ide/how-to-target-a-version-of-the-dotnet-framework.md).

> [!NOTE]
>  Nas edições Express do Visual Studio, não é possível definir a estrutura de destino na caixa de diálogo **Novo Projeto**.

## <a name="resolving-system-and-user-assembly-references"></a>Resolvendo referências de assembly do sistema e do usuário
 Para definir uma versão do .NET Framework como destino, é necessário primeiro instalar as referências de assembly apropriadas. As referências de assembly do .NET Framework versões 2.0, 3.0 e 3.5 são incluídas no .NET Framework 3.5 SP1, que podem ser baixadas no [Centro de Download da Microsoft, site do Microsoft Visual Studio](http://go.microsoft.com/fwlink/?LinkId=227602). As referências de assembly do .NET Framework 3.5 Client Profile, .NET Framework 4, .NET Framework 4 Client Profile e Silverlight também estão disponíveis no site [Downloads do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=179687).

> [!NOTE]
>  Um perfil de cliente do .NET Framework é um subconjunto do .NET Framework que fornece um conjunto limitado de bibliotecas e recursos. Para obter mais informações sobre perfis de cliente, consulte [.NET Framework Client Profile](http://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1).

 A caixa de diálogo **Adicionar Referência** desabilita assemblies do sistema que não pertencem à versão [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] de destino, para que eles não possam ser adicionados a um projeto acidentalmente. (Assemblies do sistema são arquivos .dll incluídos em uma versão [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].) As referências que pertencem a uma versão do Framework posterior à versão de destino não serão resolvidas e os controles que dependem dessa referência não podem ser adicionados. Se você desejar habilitar essa referência, redefina o destino [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] do projeto para um que inclua a referência.  Para obter mais informações, consulte [Introdução ao Designer de Projeto](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).

 Para obter mais informações sobre referências de assembly, consulte [Resolvendo assemblies em tempo de design](../msbuild/resolving-assemblies-at-design-time.md).

## <a name="enabling-linq"></a>Habilitando o LINQ
 Ao definir o .NET Framework 3.5 ou posterior como destino, uma referência ao System.Core e uma importação no nível do projeto para System.Linq (somente no Visual Basic) são adicionadas automaticamente. Se você desejar usar recursos do LINQ, também será necessário ativar a Opção Infer (somente no Visual Basic). A referência e a importação serão removidas automaticamente se você alterar o destino para uma versão anterior do .NET Framework. Confira mais informações em [Como: Criar um projeto LINQ](http://msdn.microsoft.com/library/a929e653-09a3-44be-881f-68ca33f192b2).

## <a name="see-also"></a>Consulte também
 [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md) [.NET Framework Multi-Targeting para projetos Web ASP.NET](http://msdn.microsoft.com/library/8b8145a9-62f6-4fc4-8a83-47b0487cbe76) [requisitos de sistema e compatibilidade de plataforma](http://www.microsoft.com/visualstudio/eng/products/compatibility)
