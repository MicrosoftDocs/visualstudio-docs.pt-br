---
title: Entity Framework Tools
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 14a0e5b6b746356e38dfc71c26f53ced5a470e34
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066790"
---
# <a name="entity-framework-tools-in-visual-studio"></a>Ferramentas do Entity Framework no Visual Studio

Entity Framework é uma tecnologia de mapeamento relacional de objeto que permite aos desenvolvedores de .NET trabalhar com dados relacionais usando objetos específicos de domínio. Elimina a necessidade da maioria do código de acesso a dados que os desenvolvedores geralmente precisam gravar. O Entity Framework é o mapeamento relacional de objeto recomendado (ORM) tecnologia para novos aplicativos do .NET de modelagem.

Ferramentas do Entity Framework são projetadas para ajudá-lo a criar aplicativos do Entity Framework (EF). A documentação completa do Entity Framework está aqui: [EF Core e EF 6](/ef/).

Com ferramentas do Entity Framework, você pode criar uma *modelo conceitual* de uma já existente de banco de dados e, em seguida, graficamente visualizar e editar seu modelo conceitual. Ou, você pode criar graficamente um modelo conceitual primeiro e, em seguida, gerar um banco de dados que dá suporte a seu modelo. Em ambos os casos, você pode atualizar automaticamente seu modelo quando subjacente alterações de banco de dados e gerar automaticamente o código da camada de objeto para o seu aplicativo. Geração de banco de dados e geração de código da camada de objeto são personalizáveis.

As ferramentas do Entity Framework são instaladas como parte dos **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio. Você também pode instalá-los como um componente individual sob o **SDKs, bibliotecas e estruturas** categoria.

Estas são as ferramentas específicas que constituem ferramentas do Entity Framework no Visual Studio:

- Você pode usar o [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)]  **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] Designer** (**Entity Designer**) para criar visualmente e modificar entidades, associações, mapeamentos e relações de herança. O **Entity Designer** também gera [!INCLUDE[TLA#tla_cshrp](../data-tools/includes/tlasharptla_cshrp_md.md)] ou [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] código da camada de objeto.

- Você pode usar o  **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] assistente** para gerar um modelo conceitual de um banco de dados existente e adicionar informações de conexão de banco de dados ao seu aplicativo.

- Você pode usar o **Assistente para criação de banco de dados** para criar um modelo conceitual primeiro e, em seguida, criar um banco de dados que oferece suporte ao modelo.

- Você pode usar o **Assistente de atualização de modelo** para atualizar seu modelo conceitual, o modelo de armazenamento e a mapeamentos de quando foram feitas alterações no banco de dados subjacente.

  > [!NOTE]
  > Iniciando com o Visual Studio 2010, as ferramentas do Entity Framework não dá suporte ao [!INCLUDE[ss2k](../data-tools/includes/ss2k_md.md)].

As ferramentas de gerar ou modificar uma *. edmx* arquivo. Isso *. edmx* arquivo contém informações que descrevem o modelo conceitual, o modelo de armazenamento e os mapeamentos entre eles. Para obter mais informações, consulte [EDMX](https://docs.microsoft.com/ef/ef6/).

[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EntityFrameworkPowerToolsBeta4) ajudá-lo a criar aplicativos que usam o modelo de dados de entidade. O power tools pode gerar um modelo conceitual, validar um modelo existente, produzir arquivos de código-fonte que contêm classes de objeto com base no modelo conceitual e produzem arquivos de código-fonte que contêm modos de exibição que gera o modelo. Para obter informações detalhadas, consulte [modos de exibição de mapeamento Pre-Generated](https://docs.microsoft.com/ef/ef6/fundamentals/performance/pre-generated-views).

## <a name="related-topics"></a>Tópicos relacionados

| Título | Descrição |
| - | - |
| [Entity Framework do ADO.NET](/dotnet/framework/data/adonet/ef/index) | Descreve como usar [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] ferramentas, que [!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)] fornece para criar aplicativos. |
| [Modelo de Dados de Entidade](/dotnet/framework/data/adonet/entity-data-model) | Fornece links e informações sobre como trabalhar com dados que são usados por aplicativos criados no [!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)]. |
| [Documentação do Entity Framework (EF))](https://docs.microsoft.com/ef/ef6/get-started) | Fornece um índice de vídeos, tutoriais e documentação do advanced para ajudá-lo a tirar o máximo proveito do Entity Framework. |
| [O ASP.NET 5 aplicativo para o novo banco de dados](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html) | Descreve como criar um novo aplicativo ASP.NET 5 usando o Entity Framework 7. |

## <a name="see-also"></a>Consulte também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)