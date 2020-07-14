---
title: Estruturas .NET de destino
ms.date: 03/31/2020
ms.topic: overview
helpviewer_keywords:
- targeting .NET Framework [Visual Studio]
- framework targeting [Visual Studio]
- .NET framework targeting [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b7c3c2b6b81f8f7793bda35c6b220e43caee9b5f
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770446"
---
# <a name="framework-targeting-overview"></a>Visão geral do direcionamento de estrutura

No Visual Studio, é possível especificar a versão do .NET que você deseja que o projeto tenha como destino. O direcionamento de estrutura ajuda a garantir que o aplicativo use apenas a funcionalidade disponível na versão da estrutura especificada. Para que os aplicativos .NET Framework sejam executados em outro computador, a versão da estrutura de destino do aplicativo precisa ser compatível com a versão da estrutura instalada no computador.

Uma solução do Visual Studio pode conter projetos destinados a diferentes versões do .NET.  No entanto, observe que você só pode compilar em uma única versão do .NET usando condicionais de referência para uma única compilação ou criar recursivamente diferentes binários para cada versão.  Para obter mais informações sobre estruturas de destino, confira [Estruturas de destino](/dotnet/standard/frameworks).

> [!TIP]
> Também é possível definir aplicativos como destino para plataformas diferentes. Para obter mais informações, consulte [multidirecionamento](../msbuild/msbuild-multitargeting-overview.md).

## <a name="framework-targeting-features"></a>Recursos de definição de destino da estrutura

A definição de destino da estrutura inclui os seguintes recursos:

- Quando você abre um projeto direcionado a uma versão de estrutura anterior, o Visual Studio pode atualizar o projeto automaticamente ou deixar o destino no estado em que se encontra.

- Ao criar um projeto .NET Framework, especifique a versão do .NET Framework que deseja definir como destino.

- Você pode [ter várias estruturas de destino](/dotnet/standard/frameworks#how-to-specify-target-frameworks) em um único projeto.

- É possível definir outra versão do .NET como destino em cada um dos vários projetos na mesma solução.

- Altere a versão do .NET que um projeto existente tem como destino.

   Ao alterar a versão do .NET que um projeto tem como destino, o Visual Studio faz as alterações necessárias nas referências e nos arquivos de configuração.

Quando você trabalha em um projeto direcionado a uma versão de estrutura anterior, o Visual Studio altera dinamicamente o ambiente de desenvolvimento da seguinte maneira:

- Ele filtra os itens das caixas de diálogo **Adicionar Novo Item**, **Adicionar Nova Referência** e **Adicionar Referência de Serviço** para omitir as opções que não estão disponíveis na versão de destino.

- Ele filtra os controles personalizados da **Caixa de ferramentas** para remover aqueles que não estão disponíveis na versão de destino e mostrar somente os controles mais atualizados quando vários controles estão disponíveis.

- Ele filtra o **IntelliSense** para omitir as funcionalidades de linguagem que não estão disponíveis na versão de destino.

- Ele filtra as propriedades na janela **Propriedades** para omitir aquelas que não estão disponíveis na versão de destino.

- Ele filtra as opções de menu para omitir as opções que não estão disponíveis na versão de destino.

- Para builds, ele usa a versão do compilador e as opções do compilador apropriadas para a versão de destino.

> [!NOTE]
> - A definição de destino da estrutura não assegura que o aplicativo será executado corretamente. É necessário testar o aplicativo para ter certeza de que ele é executado na versão de destino.
> - Não é possível ter versões de estrutura de destino abaixo do .NET Framework 2.0.

## <a name="select-a-target-framework-version"></a>Selecionar uma versão de estrutura de destino

Ao criar um projeto .NET Framework, selecione a versão do .NET Framework de destino depois de selecionar um modelo de projeto. A lista de estruturas disponíveis inclui as versões da estrutura instalada que são aplicáveis para o tipo de modelo selecionado. Para modelos de projeto que não são do .NET Framework, por exemplo, modelos do .NET Core, a lista suspensa **Estrutura** não é exibida.

::: moniker range="vs-2017"

![Lista suspensa Estrutura no VS 2017](media/vside-newproject-framework.png)

::: moniker-end

::: moniker range=">=vs-2019"

![Lista suspensa Estrutura no VS 2019](media/vs-2019/configure-new-project-framework.png)

::: moniker-end

## <a name="change-the-target-framework"></a>Alterar a estrutura de destino

Em um projeto existente do Visual Basic, C# ou F#, você altera a versão do .NET de destino na caixa de diálogo das propriedades do projeto. Para saber mais sobre como alterar a versão de destino de projetos do C++, confira [Como modificar a estrutura de destino e o conjunto de ferramentas da plataforma](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset).

1. No **Gerenciador de Soluções**, abra o menu de contexto do projeto que você deseja alterar e, em seguida, escolha **Propriedades**.

1. Na coluna à esquerda da janela **Propriedades** , escolha a guia **aplicativo** .

   ![Guia Aplicativo das propriedades do projeto](../ide/media/vs_slnexplorer_properties_applicationtab.png)

   > [!NOTE]
   > Depois de criar um aplicativo UWP, você não poderá alterar a versão de destino do Windows ou do .NET.

1. Na lista **Estrutura de Destino**, escolha a versão desejada.

1. Na caixa de diálogo de verificação exibida, escolha o botão **Sim**.

   O projeto é descarregado. Quando ele é recarregado, ele é direcionado à versão do .NET recém-escolhida.

> [!NOTE]
> Se o código contiver referências a outra versão do .NET que não seja a que você o direcionou, poderão ser exibidas mensagens de erro quando você compilar ou executar o código. Para resolver esses erros, modifique as referências. Confira [Solução de problemas de erros de direcionamento do .NET](../msbuild/troubleshooting-dotnet-framework-targeting-errors.md).

> [!TIP]
> Dependendo da estrutura de destino, ele pode ser representado das seguintes maneiras no arquivo de projeto:
>
> - Para um aplicativo .NET Core: `<TargetFramework>netcoreapp2.1</TargetFramework>`
> - Para um aplicativo .NET Standard: `<TargetFramework>netstandard2.0</TargetFramework>`
> - Para um aplicativo .NET Framework: `<TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>`

## <a name="resolve-system-and-user-assembly-references"></a>Resolver referências de assembly do sistema e do usuário

Para definir uma versão do .NET como destino, é necessário primeiro instalar as referências de assembly apropriadas. Baixe pacotes de desenvolvedor para diferentes versões do .NET na página de [downloads do .NET](https://www.microsoft.com/net/download/windows).

Para projetos .NET Framework, a caixa de diálogo **Adicionar Referência** desabilita os assemblies do sistema que não pertencem à versão do .NET Framework de destino, de modo que eles não possam ser adicionados a um projeto acidentalmente. (Os assemblies do sistema são arquivos *. dll* incluídos em uma versão do .NET Framework.) As referências que pertencem a uma versão de estrutura superior à versão de destino não serão resolvidas e os controles que dependem dessa referência não poderão ser adicionados. Se você desejar habilitar essa referência, redefina o destino do .NET Framework do projeto para um que inclua a referência.

Para obter mais informações sobre referências de assembly, consulte [Resolver assemblies em tempo de design](../msbuild/resolving-assemblies-at-design-time.md).

## <a name="enable-linq"></a>Habilitar LINQ

Ao direcionar ao .NET Framework 3.5 ou posterior, uma referência ao **System.Core** e uma importação no nível do projeto para <xref:System.Linq> (somente no Visual Basic) são adicionadas automaticamente. Se você desejar usar recursos do LINQ, também precisará ativar `Option Infer` (somente no Visual Basic). A referência e a importação serão removidas automaticamente se você alterar o destino para uma versão anterior do .NET Framework. Para obter mais informações, consulte [Trabalhar com o LINQ](/dotnet/csharp/tutorials/working-with-linq).

## <a name="see-also"></a>Confira também

- [Estruturas de destino](/dotnet/standard/frameworks)
- [Multiplataforma (MSBuild)](../msbuild/msbuild-multitargeting-overview.md)
- [Como modificar o Framework de destino e o conjunto de ferramentas de plataforma (C++)](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset)
