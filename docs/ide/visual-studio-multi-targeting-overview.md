---
title: Direcionar ao .NET Framework no Visual Studio
ms.date: 02/06/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- targeting .NET Framework [Visual Studio]
- multi-targeting [Visual Studio]
- multitargeting [Visual Studio]
- framework targeting [Visual Studio]
- .NET framework targeting [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: cba93b86d6ecebf249e11d18bd6e4b6b86e59fda
ms.sourcegitcommit: a8e01952be5a539104e2c599e9b8945322118055
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32425083"
---
# <a name="visual-studio-multi-targeting-overview"></a>Visão geral de multiplataforma no Visual Studio

No Visual Studio, é possível especificar a versão ou o perfil do .NET Framework que você deseja que o projeto tenha como destino. Para que um aplicativo seja executado em outro computador, a versão do Framework de destino do aplicativo deve ser compatível com a versão do Framework instalada no computador.

Também é possível criar uma solução que contém projetos que têm como destino versões diferentes da estrutura. A definição de destino da estrutura ajuda a assegurar que o aplicativo use apenas a funcionalidade disponível na versão especificada da estrutura.

> [!TIP]
> Também é possível definir aplicativos como destino para plataformas diferentes. Para obter mais informações, consulte [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md).

## <a name="framework-targeting-features"></a>Recursos de definição de destino da estrutura

A definição de destino da estrutura inclui os seguintes recursos:

- Ao abrir um projeto que tem como destino uma versão anterior do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)], o Visual Studio pode fazer upgrade dele ou deixar o destino no estado em que se encontra.

- Ao criar um projeto, é possível especificar a versão do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] que você deseja definir como destino.

- É possível alterar a versão do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] que um projeto existente tem como destino.

- É possível definir como destino uma versão diferente do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] em cada um dos vários projetos na mesma solução.

- Ao alterar a versão do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] que um projeto tem como destino, o [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] faz as alterações necessárias nas referências e nos arquivos de configuração.

Ao trabalhar em um projeto que tem como destino uma versão anterior do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)], o Visual Studio altera dinamicamente o ambiente de desenvolvimento, da seguinte maneira:

- Ele filtra os itens das caixas de diálogo **Adicionar Novo Item**, **Adicionar Nova Referência** e **Adicionar Referência de Serviço** para omitir as opções que não estão disponíveis na versão de destino.

- Ele filtra os controles personalizados da **Caixa de ferramentas** para remover aqueles que não estão disponíveis na versão de destino e mostrar somente os controles mais atualizados quando vários controles estão disponíveis.

- Ele filtra o **IntelliSense** para omitir os recursos de idioma que não estão disponíveis na versão de destino.

- Ele filtra as propriedades na janela **Propriedades** para omitir aquelas que não estão disponíveis na versão de destino.

- Ele filtra as opções de menu para omitir as opções que não estão disponíveis na versão de destino.

- Para builds, ele usa a versão do compilador e as opções do compilador apropriadas para a versão de destino.

> [!NOTE]
> A definição de destino da estrutura não assegura que o aplicativo será executado corretamente. É necessário testar o aplicativo para ter certeza de que ele é executado na versão de destino. Não é possível definir como destino versões de estrutura anteriores ao .NET Framework 2.0.

## <a name="select-a-target-framework-version"></a>Selecionar uma versão de estrutura de destino

Ao criar um projeto, selecione a versão do .NET Framework de destino na caixa de diálogo **Novo Projeto**. A lista de estruturas disponíveis inclui as versões da estrutura instalada que são aplicáveis para o tipo de modelo selecionado. Para os tipos de modelo que não exigem o .NET Framework, por exemplo modelos do .NET Core, a lista suspensa **Estrutura** está oculta.

![A lista suspensa Estrutura na caixa de diálogo Novo Projeto](media/vside-newproject-framework.png)

Em um projeto existente, é possível alterar a versão [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] de destino na caixa de diálogo das propriedades do projeto. Para obter mais informações, consulte [Como direcionar a uma versão do .NET Framework](../ide/how-to-target-a-version-of-the-dotnet-framework.md).

## <a name="resolve-system-and-user-assembly-references"></a>Resolver referências de assembly do sistema e do usuário

Para definir uma versão do .NET Framework como destino, é necessário primeiro instalar as referências de assembly apropriadas. É possível baixar pacotes de desenvolvedor para diferentes versões do .NET Framework na página de [downloads do .NET](https://www.microsoft.com/net/download/windows).

A caixa de diálogo **Adicionar Referência** desabilita assemblies do sistema que não pertencem à versão [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] de destino, para que eles não possam ser adicionados a um projeto acidentalmente. (Assemblies do sistema são arquivos *.dll* incluídos em uma versão do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)].) As referências que pertencem a uma versão do Framework posterior à versão de destino não serão resolvidas e os controles que dependem dessa referência não podem ser adicionados. Se você desejar habilitar essa referência, redefina o destino [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] do projeto para um que inclua a referência.  Para obter mais informações, consulte [Como direcionar a uma versão do .NET Framework](../ide/how-to-target-a-version-of-the-dotnet-framework.md).

Para obter mais informações sobre referências de assembly, consulte [Resolver assemblies em tempo de design](../msbuild/resolving-assemblies-at-design-time.md).

## <a name="enable-linq"></a>Habilitar LINQ

Ao direcionar ao .NET Framework 3.5 ou posterior, uma referência ao **System.Core** e uma importação no nível do projeto para <xref:System.Linq> (somente no Visual Basic) são adicionadas automaticamente. Se você desejar usar recursos do LINQ, também precisará ativar `Option Infer` (somente no Visual Basic). A referência e a importação serão removidas automaticamente se você alterar o destino para uma versão anterior do .NET Framework. Para obter mais informações, consulte [Trabalhar com o LINQ](/dotnet/csharp/tutorials/working-with-linq).

## <a name="see-also"></a>Consulte também

- [Multiplataforma (MSBuild)](../msbuild/msbuild-multitargeting-overview.md)
- [Como modificar a estrutura de destino e o conjunto de ferramentas da plataforma (C++)](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset)