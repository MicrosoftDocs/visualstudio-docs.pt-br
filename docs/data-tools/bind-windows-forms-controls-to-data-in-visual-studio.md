---
title: Associar controles do Windows Forms a dados
ms.date: 11/03/2017
ms.topic: how-to
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b6a1d240c865ecc6abddd399c94122a757ee0983
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283002"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>Associar controles do Windows Forms a dados no Visual Studio

Você pode exibir dados para os usuários do seu aplicativo ligando dados a Windows Forms. Para criar esses controles associados a dados, arraste os itens da janela **fontes de dados** para o designer de formulários do Windows no Visual Studio.

![Operação de arrastar da fonte de dados](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> Se a janela **fontes de dados** não estiver visível, você poderá abri-la escolhendo **Exibir**  >  **outras**  >  **fontes de dados**do Windows ou pressionando **Shift** + **ALT** + **D**. Você deve ter um projeto aberto no Visual Studio para ver a janela **fontes de dados** .

Antes de arrastar itens, você pode definir o tipo de controle ao qual deseja associar. Valores diferentes aparecem dependendo se você escolher a própria tabela ou uma coluna individual.  Você também pode definir valores personalizados. Para uma tabela, **detalhes** significa que cada coluna está associada a um controle separado.

![Associar fonte de dados ao DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>Controles BindingSource e BindingNavigator

O <xref:System.Windows.Forms.BindingSource> componente atende a duas finalidades. Primeiro, ele fornece uma camada de abstração ao ligar os controles aos dados. Os controles no formulário são vinculados ao <xref:System.Windows.Forms.BindingSource> componente em vez de diretamente a uma fonte de dados. Em segundo lugar, ele pode gerenciar uma coleção de objetos. Adicionar um tipo ao <xref:System.Windows.Forms.BindingSource> cria uma lista desse tipo.

Para obter mais informações sobre o <xref:System.Windows.Forms.BindingSource> componente, consulte:

- [Componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component)

- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [Arquitetura do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

O [controle BindingNavigator](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms) fornece uma interface do usuário para navegar pelos dados exibidos por um aplicativo do Windows.

## <a name="bind-to-data-in-a-datagridview-control"></a>Associar a dados em um controle DataGridView

Para um [controle DataGridView](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms), a tabela inteira é associada a esse controle único. Quando você arrasta um **DataGridView** para o formulário, uma faixa de ferramenta para os registros de navegação ( <xref:System.Windows.Forms.BindingNavigator> ) também é exibida. Um [DataSet](../data-tools/dataset-tools-in-visual-studio.md), o [TableAdapter](../data-tools/create-and-configure-tableadapters.md), <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> aparece na bandeja do componente. Na ilustração a seguir, um [TableAdapterManager](https://msdn.microsoft.com/library/bb384426.aspx) também é adicionado porque a tabela Customers tem uma relação com a tabela Orders. Essas variáveis são todas declaradas no código gerado automaticamente como membros privados na classe Form. O código gerado automaticamente para preencher o **DataGridView** está localizado no manipulador de `Form_Load` eventos. O código para salvar os dados para atualizar o banco de dado está localizado no `Save` manipulador de eventos do **BindingNavigator**. Você pode mover ou modificar esse código conforme necessário.

![GridView com BindingNavigator](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

Você pode personalizar o comportamento do **DataGridView** e do **BindingNavigator** clicando na marca inteligente no canto superior direito de cada um:

![DataGridView e marcas inteligentes do navegador de associação](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

Se os controles de que seu aplicativo precisa não estiverem disponíveis na janela **fontes de dados** , você poderá adicionar controles. Para obter mais informações, consulte [Adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

Você também pode arrastar itens da janela **fontes de dados** para controles que já estão em um formulário para associar o controle aos dados. Um controle que já está associado a dados tem suas associações de dados redefinidas para o item arrastado mais recentemente para ele. Para serem destinos de destino válidos, os controles devem ser capazes de exibir o tipo de dados subjacente do item arrastado para ele na janela **fontes de dados** . Por exemplo, não é válido arrastar um item que tenha um tipo de dados <xref:System.DateTime> para um <xref:System.Windows.Forms.CheckBox> , porque o <xref:System.Windows.Forms.CheckBox> não é capaz de exibir uma data.

## <a name="bind-to-data-in-individual-controls"></a>Associar a dados em controles individuais

Quando você associa uma fonte de dados a **detalhes**, cada coluna no conjunto é associada a um controle separado.

![Associar fonte de dados a detalhes](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> Observe que, na ilustração anterior, você arrasta da propriedade Orders da tabela Customers, não da tabela Orders. Ligando-se à `Customer.Orders` propriedade, os comandos de navegação feitos no **DataGridView** são refletidos imediatamente nos controles de detalhes. Se você arrastou da tabela Orders, os controles ainda seriam associados ao conjunto de um, mas não seriam sincronizados com o **DataGridView**.

A ilustração a seguir mostra os controles associados a dados padrão que são adicionados ao formulário depois que a propriedade Orders na tabela Customers é associada a **detalhes** na janela **Data Sources** .

![Tabela de pedidos associada a detalhes](../data-tools/media/raddata-orders-table-bound-to-details.png)

Observe também que cada controle tem uma marca inteligente. Essa marca permite personalizações que se aplicam somente ao controle.

## <a name="see-also"></a>Veja também

- [Associando controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Associação de dados em Windows Forms (.NET Framework)](/dotnet/framework/winforms/windows-forms-data-binding)
