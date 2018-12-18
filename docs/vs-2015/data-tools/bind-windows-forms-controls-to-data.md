---
title: Associar controles dos Windows Forms a dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- displaying data, Windows Forms controls
- Windows Forms, displaying data
- data sources, displaying
- data [Windows Forms], displaying
ms.assetid: 0163a34a-38cb-40b9-8f38-3058a90caf21
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d1d8710ef98339c0cf4b44ddd3fa41cca8676570
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49237465"
---
# <a name="bind-windows-forms-controls-to-data"></a>Associar controles do Windows Forms a dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode associar a fontes de dados a controles arrastando objetos do **fontes de dados** janela para um formulário do Windows ou para um controle existente em um formulário. Antes de você arrasta itens, você pode definir o tipo de controle que você deseja associar. Valores diferentes são exibidos, dependendo se você escolher a tabela a mesmo ou para uma coluna individual.  Você também pode definir valores personalizados. Para uma tabela "Detalhes" significa que cada coluna é associada a um controle separado.  
  
 ![Associar a fonte de dados a DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png "fonte de dados de ligação raddata DataGridView")  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="bind-to--data-in-a-datagridview-control"></a>Associar a dados em um controle DataGridView  
 Para DataGridView, a tabela inteira é associada a esse controle único. Quando você arrasta uma DataGridView no formulário, uma ferramenta da faixa para navegação em registros (<xref:System.Windows.Forms.BindingNavigator>) também é exibida. Um [DataSet](../data-tools/dataset-tools-in-visual-studio.md), [TableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes. Na ilustração a seguir, um TableAdapterManager também é adicionado como a tabela de clientes tem uma relação à tabela Orders. Essas variáveis todos são declaradas no código gerado automaticamente como membros particulares na classe de formulário. O código gerado automaticamente para preencher o DataGridView está localizado no manipulador de eventos form_load. O código para salvar os dados para atualizar o banco de dados está localizado no manipulador de eventos de salvamento para o BindingNavigator. Você pode mover ou modificar este código conforme necessário.  
  
 ![GridView com BindingNavigator](../data-tools/media/raddata-gridview-with-bindingnavigator.png "raddata GridView com o BindingNavigator")  
  
 Você pode personalizar o comportamento do DataGridView e o BindingNavigator clicando na marca inteligente no canto superior direito de cada um:  
  
 ![Marcas inteligentes do DataGridView e associação Navigator](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png "raddata DataGridView e associação Navigator marcas inteligentes")  
  
 Se os controles de seu aplicativo precisa não está disponível de dentro de **fontes de dados** janela, você pode adicionar controles. Para obter mais informações, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).  
  
 Você também pode arrastar itens dos **fontes de dados** window para controles já em um formulário para associar o controle aos dados. Um controle que já está associado a dados tem seus dados associações redefinidas para o item mais recentemente arrastado para ele. Para destinos depósitos válidos, os controles devem ser capazes de exibir o tipo de dados subjacentes do item arrastado para ele da **fontes de dados** janela. Por exemplo, não é válido para arrastar um item que tem um tipo de dados <xref:System.DateTime> em um <xref:System.Windows.Forms.CheckBox>, porque o <xref:System.Windows.Forms.CheckBox> não é capaz de exibir uma data.  
  
## <a name="bind-to--data-in-individual-controls"></a>Associar a dados em controles individuais  
 Quando você associa uma fonte de dados para "Detalhes", cada coluna no conjunto de dados é associada a um controle separado.  
  
 ![Associar a fonte de dados para obter detalhes](../data-tools/media/raddata-bind-data-source-to-details.png "raddata fonte de dados de ligação para obter detalhes")  
  
> [!IMPORTANT]
>  Observe que, na ilustração anterior, você arrasta da propriedade Orders de tabela de clientes, não da tabela Orders. Fazendo a ligação com a propriedade Orders, feitos no DataGridView de comandos de navegação são refletidos imediatamente nos controles de detalhes. Se você arrastou da tabela Pedidos, os controles ainda poderá estar associados ao conjunto de dados, mas não eles não seriam ser sincronizados com o DataGridView.  
  
 A ilustração a seguir mostra o padrão controles ligados a dados que são adicionados ao formulário depois que a propriedade de pedidos na tabela Customers é associada a "Detalhes" a **fontes de dados** janela.  
  
 ![Tabela de pedidos associada aos detalhes](../data-tools/media/raddata-orders-table-bound-to-details.png "raddata pedidos tabela vinculada detalhes")  
  
 Observe também que cada controle tem uma marca inteligente. Essa marca permite que as personalizações que se aplicam a esse controle somente.  
  
## <a name="see-also"></a>Consulte também  
 [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

