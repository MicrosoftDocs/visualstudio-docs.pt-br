---
title: Associar controles a dados
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data, displaying
- data sources, displaying data
- Data Sources window
- dislaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: c4e27f5ce9536e7128330ebe932709a9be408b7e
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305257"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>Associar controles a dados no Visual Studio

É possível exibir dados para usuários do aplicativo associando-se dados a controles. Você pode criar esses controles ligados a dados arrastando itens dos **fontes de dados** window em uma superfície de design ou controles em uma superfície no Visual Studio.

Este tópico descreve as fontes de dados que você pode usar para criar controles associados a dados. Ele também descreve algumas das tarefas básicas envolvidas na associação de dados. Para obter detalhes mais específicos sobre como criar controles associados a dados, consulte [controles de ligar o Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) e [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md).

## <a name="data-sources"></a>Fontes de dados

No contexto de associação de dados, uma fonte de dados representa os dados na memória que pode ser associado a sua interface do usuário. Em termos práticos, uma fonte de dados pode ser uma classe do Entity Framework, um conjunto de dados, um ponto de extremidade de serviço que é encapsulado em um objeto de proxy do .NET, uma classe LINQ to SQL, ou qualquer objeto do .NET ou coleção. Algumas fontes de dados permitem criar controles associados a dados arrastando itens dos **fontes de dados** janela, enquanto outras fontes de dados não. A tabela a seguir mostra quais fontes de dados têm suporte.

| Fonte de dados | Suporte a arrastar e soltar no **o Designer de formulários do Windows** | Suporte a arrastar e soltar no **o WPF Designer** | Suporte a arrastar e soltar no **Silverlight Designer** |
| - | - | - | - |
| Conjunto de dados | Sim | Sim | Não |
| Modelo de Dados de Entidade | Sim<sup>1</sup> | Sim | Sim |
| Classes do LINQ to SQL | Não<sup>2</sup> | Não<sup>2</sup> | Não<sup>2</sup> |
| Serviços (incluindo [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)], WCF services e web services) | Sim | Sim | Sim |
| Objeto | Sim | Sim | Sim |
| SharePoint | Sim | Sim | Sim |

1. Gerar o modelo usando o **modelo de dados de entidade** assistente, em seguida, arrastar esses objetos para o designer.

2. Classes LINQ to SQL não aparecem na **fontes de dados** janela. No entanto, você pode adicionar uma nova fonte de dados de objeto com base no LINQ para classes SQL e, em seguida, arrastar esses objetos para o designer para criar controles associados a dados. Para obter mais informações, consulte [instruções passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md).

## <a name="data-sources-window"></a>janela Fontes de Dados

Fontes de dados estão disponíveis para seu projeto como itens na **fontes de dados** janela. Esta janela está visível quando uma superfície de design do formulário é a janela ativa no seu projeto, ou ela poderá ser aberta (quando um projeto é aberto), escolhendo **modo de exibição** > **Other Windows**  >   **Fontes de dados**. Você pode arrastar itens dessa janela para criar controles associados aos dados subjacentes, e você também pode configurar as fontes de dados clicando com o.

![janela Fontes de Dados](../data-tools/media/raddata-data-sources-window.png)

Para cada tipo de dados que aparece na **fontes de dados** janela, um controle padrão é criado quando você arrasta o item para o designer. Antes de arrastar um item a partir de **fontes de dados** janela, você pode alterar o controle que é criado. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

## <a name="tasks-involved-in-binding-controls-to-data"></a>Tarefas envolvidas na associação de controles a dados

A tabela a seguir lista algumas das tarefas mais comuns que você executa para associar controles a dados.

|Tarefa|Mais informações|
|----------| - |
|Abra o **fontes de dados** janela.|Abra uma superfície de design no editor e escolha **modo de exibição** > **fontes de dados**.|
|Adicione uma fonte de dados ao seu projeto.|[Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)|
|Definir o controle que é criado quando você arrasta um item do **fontes de dados** janela no Designer.|[Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|
|Modificar a lista de controles que estão associadas a itens do **fontes de dados** janela.|[Adicionar controles personalizados à janela Fontes de Dados](../data-tools/add-custom-controls-to-the-data-sources-window.md)|
|Crie controles associados a dados.|[Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)|
|Associe a um objeto ou coleção.|[Associar objetos no Visual Studio](../data-tools/bind-objects-in-visual-studio.md)|
|Filtre dados que aparecem na interface do usuário.|[Filtrar e classificar dados em um Aplicativo do Windows Forms](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|
|Personalize legendas para controles.|[Personalizar o modo como o Visual Studio cria legendas para controles associados a dados](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|

## <a name="see-also"></a>Consulte também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Associação de dados do Windows Forms](/dotnet/framework/winforms/windows-forms-data-binding)