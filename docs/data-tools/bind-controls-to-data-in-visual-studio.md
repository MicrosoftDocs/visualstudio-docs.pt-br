---
title: Associar controles a dados
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data, displaying
- data sources, displaying data
- Data Sources window
- displaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3d812316de46caf7480146003f7ba1950ae3b9e2
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283028"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>Associar controles a dados no Visual Studio

É possível exibir dados para usuários do aplicativo associando-se dados a controles. Você pode criar esses controles associados a dados arrastando itens da janela **fontes de dados** para uma superfície de design ou controles em uma superfície no Visual Studio.

Este tópico descreve as fontes de dados que você pode usar para criar controles vinculados a dados. Ele também descreve algumas das tarefas gerais envolvidas na vinculação de dados. Para obter detalhes mais específicos sobre como criar controles vinculados a dados, consulte [associar controles de Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) e [associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md).

## <a name="data-sources"></a>Fontes de dados

No contexto de vinculação de dados, uma fonte de dados representa os dados na memória que podem ser associados à sua interface do usuário. Em termos práticos, uma fonte de dados pode ser uma classe Entity Framework, um conjunto de ponto de extremidade de serviço que é encapsulado em um objeto de proxy .NET, uma classe LINQ to SQL ou qualquer objeto ou coleção .NET. Algumas fontes de dados permitem que você crie controles vinculados a dados arrastando itens da janela **fontes de dados** , enquanto outras fontes de dados não. A tabela a seguir mostra quais fontes de dados têm suporte.

| Fonte de dados | Suporte a arrastar e soltar no **Designer de formulários do Windows** | Suporte a arrastar e soltar no **designer do WPF** | Suporte a arrastar e soltar no **designer do Silverlight** |
| - | - | - | - |
| Dataset | Sim | Sim | Não |
| Modelo de Dados de Entidade | Sim<sup>1</sup> | Sim | Sim |
| Classes do LINQ to SQL | Não<sup>2</sup> | Não<sup>2</sup> | Não<sup>2</sup> |
| Serviços (incluindo serviços [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] WCF e serviços Web) | Sim | Sim | Sim |
| Objeto | Sim | Sim | Sim |
| SharePoint | Sim | Sim | Sim |

1. Gere o modelo usando o assistente de **modelo de dados de entidade** e, em seguida, arraste esses objetos para o designer.

2. LINQ to SQL classes não aparecem na janela **fontes de dados** . No entanto, você pode adicionar uma nova fonte de dados de objeto com base em classes de LINQ to SQL e, em seguida, arrastar esses objetos para o designer a fim de criar controles vinculados a dados. Para obter mais informações, consulte [Walkthrough: Creating LINQ to SQL classes (O-R Designer)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md).

## <a name="data-sources-window"></a>janela Fontes de Dados

As fontes de dados estão disponíveis para seu projeto como itens na janela **fontes de dados** . Essa janela fica visível quando uma superfície de design de formulário é a janela ativa em seu projeto, ou você pode abri-la (quando um projeto estiver aberto) escolhendo **Exibir**  >  **outras**  >  **fontes de dados**do Windows. Você pode arrastar itens desta janela para criar controles associados aos dados subjacentes e também pode configurar as fontes de dados clicando com o botão direito do mouse.

![janela Fontes de Dados](../data-tools/media/raddata-data-sources-window.png)

Para cada tipo de dados que aparece na janela **fontes de dados** , um controle padrão é criado quando você arrasta o item para o designer. Antes de arrastar um item da janela **fontes de dados** , você pode alterar o controle criado. Para obter mais informações, consulte [definir o controle a ser criado ao arrastar da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

## <a name="tasks-involved-in-binding-controls-to-data"></a>Tarefas envolvidas na associação de controles aos dados

A tabela a seguir lista algumas das tarefas mais comuns que você executa para associar controles a dados.

|Tarefa|Mais informações|
|----------| - |
|Abra a janela **fontes de dados** .|Abra uma superfície de design no editor e escolha **Exibir**  >  **fontes de dados**.|
|Adicione uma fonte de dados ao seu projeto.|[Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)|
|Defina o controle que é criado quando você arrasta um item da janela **fontes de dados** para o designer.|[Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|
|Modifique a lista de controles que estão associados aos itens na janela **fontes de dados** .|[Adicionar controles personalizados à janela Fontes de Dados](../data-tools/add-custom-controls-to-the-data-sources-window.md)|
|Criar controles vinculados a dados.|[Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)|
|Associar a um objeto ou uma coleção.|[Associar objetos no Visual Studio](../data-tools/bind-objects-in-visual-studio.md)|
|Filtre os dados que aparecem na interface do usuário.|[Filtrar e classificar dados em um Aplicativo do Windows Forms](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|
|Personalizar legendas para controles.|[Personalizar o modo como o Visual Studio cria legendas para controles associados a dados](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|

## <a name="see-also"></a>Veja também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Windows Forms Associação de dados](/dotnet/framework/winforms/windows-forms-data-binding)
