---
title: Associar controles do Windows Forms a dados
ms.date: 11/03/2017
ms.topic: conceptual
helpviewer_keywords:
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 596475ed3a5e1cac535ca0cdf43980af44bd4bf1
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304630"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>Associar controles do Windows Forms a dados no Visual Studio

Você pode exibir dados para usuários do seu aplicativo pela associação de dados ao Windows Forms. Para criar esses controles ligados a dados, arraste itens dos **fontes de dados** janela para o Designer de formulários do Windows no Visual Studio.

![Operação de arrastar do código-fonte de dados](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> Se o **fontes de dados** janela não estiver visível, você pode abri-lo escolhendo **exibição** > **Other Windows** > **fontes de dados** , ou pressionando **Shift**+**Alt**+**1!d**. Você deve ter um projeto aberto no Visual Studio para ver os **fontes de dados** janela.

Antes de você arrasta itens, você pode definir o tipo de controle que você deseja associar. Valores diferentes são exibidos, dependendo se você escolher a tabela a mesmo ou para uma coluna individual.  Você também pode definir valores personalizados. Para uma tabela **detalhes** significa que cada coluna é associada a um controle separado.

![Associar a fonte de dados a DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>Controles BindingSource e BindingNavigator

O <xref:System.Windows.Forms.BindingSource> componente tem duas finalidades. Primeiro, ele fornece uma camada de abstração ao associar os controles a dados. Controles no formulário são vinculados para o <xref:System.Windows.Forms.BindingSource> componente, em vez de diretamente para uma fonte de dados. Em segundo lugar, ele pode gerenciar uma coleção de objetos. Adição de um tipo para o <xref:System.Windows.Forms.BindingSource> cria uma lista desse tipo.

Para obter mais informações sobre o <xref:System.Windows.Forms.BindingSource> componente, consulte:

- [Componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component)

- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [Arquitetura do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

O [controle BindingNavigator](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms) fornece uma interface de usuário para navegar pelos dados exibidos por um aplicativo do Windows.

## <a name="bind-to-data-in-a-datagridview-control"></a>Associar a dados em um controle DataGridView

Para um [controle DataGridView](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms), a tabela inteira está associada a esse controle único. Quando você arrasta uma **DataGridView** ao formulário, uma ferramenta da faixa para navegação em registros (<xref:System.Windows.Forms.BindingNavigator>) também é exibida. Um [DataSet](../data-tools/dataset-tools-in-visual-studio.md), [TableAdapter](../data-tools/create-and-configure-tableadapters.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes. Na ilustração a seguir, uma [TableAdapterManager](https://msdn.microsoft.com/library/bb384426.aspx) também é adicionada como a tabela de clientes tem uma relação à tabela Orders. Essas variáveis todos são declaradas no código gerado automaticamente como membros particulares na classe de formulário. O código gerado automaticamente para preencher a **DataGridView** está localizado no `Form_Load` manipulador de eventos. O código para salvar os dados para atualizar o banco de dados está localizado na `Save` manipulador de eventos para o **BindingNavigator**. Você pode mover ou modificar este código conforme necessário.

![GridView com o BindingNavigator](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

Você pode personalizar o comportamento do **DataGridView** e o **BindingNavigator** clicando na marca inteligente no canto superior direito de cada um:

![DataGridView e associação Navigator marcas inteligentes](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

Se os controles de seu aplicativo precisa não está disponível de dentro de **fontes de dados** janela, você pode adicionar controles. Para obter mais informações, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

Você também pode arrastar itens dos **fontes de dados** window para controles já em um formulário para associar o controle aos dados. Um controle que já está associado a dados tem seus dados associações redefinidas para o item mais recentemente arrastado para ele. Para destinos depósitos válidos, os controles devem ser capazes de exibir o tipo de dados subjacentes do item arrastado para ele da **fontes de dados** janela. Por exemplo, não é válido para arrastar um item que tem um tipo de dados <xref:System.DateTime> em um <xref:System.Windows.Forms.CheckBox>, porque o <xref:System.Windows.Forms.CheckBox> não é capaz de exibir uma data.

## <a name="bind-to-data-in-individual-controls"></a>Associar a dados em controles individuais

Quando você associa uma fonte de dados para **detalhes**, cada coluna no conjunto de dados é associada a um controle separado.

![Associar a fonte de dados para obter detalhes](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> Observe que, na ilustração anterior, você arrasta da propriedade Orders de tabela de clientes, não da tabela Orders. Fazendo a ligação com o `Customer.Orders` comandos de navegação de propriedade, feita na **DataGridView** são refletidas imediatamente nos controles de detalhes. Se você arrastou da tabela Pedidos, os controles ainda poderá estar associados ao conjunto de dados, mas não eles não seriam possível sincronizar com o **DataGridView**.

A ilustração a seguir mostra o padrão de controles ligados a dados que são adicionados ao formulário depois que a propriedade de pedidos na tabela Customers é associada a **detalhes** na **fontes de dados** janela.

![Tabela de pedidos associada para obter detalhes](../data-tools/media/raddata-orders-table-bound-to-details.png)

Observe também que cada controle tem uma marca inteligente. Essa marca permite que as personalizações que se aplicam a esse controle somente.

## <a name="see-also"></a>Consulte também

- [Associando controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Associação de dados no Windows Forms (.NET Framework)](/dotnet/framework/winforms/windows-forms-data-binding)