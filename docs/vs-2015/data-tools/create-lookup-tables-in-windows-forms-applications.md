---
title: Criar tabelas de pesquisa em aplicativos do Windows Forms | Microsoft Docs
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
- lookup tables
- lookup tables, creating
ms.assetid: 0edd5385-c381-4b17-9096-74e2778db9d5
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 334acba1e70545f1f8be758e34c8fc4843878406
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49223881"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>Criar tabelas de pesquisa em aplicativos do Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O termo *tabela de pesquisa* descreve controles que estão associados às tabelas de dois dados relacionados. Esses controles de pesquisa exibem dados da primeira tabela com base em um valor selecionado na segunda tabela.  
  
 Você pode criar tabelas de pesquisa, arrastando o nó principal de uma tabela pai (da [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)) para um controle em seu formulário que já está associado à coluna na tabela filho relacionada.  
  
 Por exemplo, considere uma tabela de `Orders` em um banco de dados de vendas. Cada registro a `Orders` tabela inclui um `CustomerID`, indicando qual cliente fez o pedido. O `CustomerID` é uma chave estrangeira apontando para um registro de cliente no `Customers` tabela. Nesse cenário, você expandirá a `Orders` na tabela o **fontes de dados** janela e defina o nó principal como **detalhes**. Em seguida, defina a `CustomerID` coluna para usar um <xref:System.Windows.Forms.ComboBox> (ou qualquer outro controle que dá suporte à vinculação de pesquisa) e arraste o `Orders` nó para seu formulário. Por fim, arraste o `Customers` nó para o controle que está associado à coluna relacionada — nesse caso, o <xref:System.Windows.Forms.ComboBox> associado para o `CustomerID` coluna.  
  
## <a name="to-databind-a-lookup-control"></a>Vincular dados de um controle de pesquisa  
  
1.  Abra o **fontes de dados** janela.  
  
    > [!NOTE]
    >  Tabelas de pesquisa requerem que as duas tabelas relacionadas ou objetos estejam disponíveis na **fontes de dados** janela. Para obter mais informações, consulte [Como exibir dados relacionados em um aplicativo dos Windows Forms](../data-tools/how-to-display-related-data-in-a-windows-forms-application.md).  
  
2.  Expanda os nós na **fontes de dados** janela até que você possa ver a tabela pai e todas as suas colunas e a tabela filho relacionada e todas as suas colunas.  
  
    > [!NOTE]
    >  O nó da tabela filho é o nó que aparece como um nó filho expansível na tabela pai.  
  
3.  Altere o tipo subjacente da tabela filho para **detalhes** selecionando **detalhes** na lista de controle no nó da tabela filho. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
4.  Localize o nó que relaciona as duas tabelas (o `CustomerID` nó no exemplo anterior). Altere seu tipo subjacente para um <xref:System.Windows.Forms.ComboBox> , selecionando **ComboBox** na lista de controle.  
  
5.  Arraste o nó da tabela filho principal dos **fontes de dados** window para seu formulário.  
  
     Controles de ligação de dados (com rótulos descritivos) e uma ferramenta da faixa (<xref:System.Windows.Forms.BindingNavigator>) aparecem no formulário. Um [DataSet](../data-tools/dataset-tools-in-visual-studio.md), [TableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
6.  Agora, arraste o nó da tabela pai principal do **fontes de dados** janela diretamente para o controle de pesquisa (o <xref:System.Windows.Forms.ComboBox>).  
  
     As associações de pesquisa agora são estabelecidas. Consulte a tabela abaixo para as propriedades específicas que foram definidas no controle.  
  
    |Propriedade|Explicação da configuração|  
    |--------------|----------------------------|  
    |**Fonte de dados**|O Visual Studio define esta propriedade para o <xref:System.Windows.Forms.BindingSource> criado para a tabela que você arrasta para o controle (em oposição ao <xref:System.Windows.Forms.BindingSource> criado quando o controle foi criado).<br /><br /> Se você precisar fazer um ajuste, defina isso como o <xref:System.Windows.Forms.BindingSource> da tabela com a coluna que você deseja exibir.|  
    |**DisplayMember**|O Visual Studio define essa propriedade para a primeira coluna após a chave primária que tem um tipo de dado de cadeia da tabela que você arrasta para o controle.<br /><br /> Se você precisar fazer um ajuste, defina isso para o nome da coluna que deseja exibir.|  
    |**ValueMember**|O Visual Studio define essa propriedade para a primeira coluna participante da chave primária, ou a primeira coluna na tabela, se nenhuma chave for definida.<br /><br /> Se você precisar fazer um ajuste, defina isso para a chave primária na tabela com a coluna que você deseja exibir.|  
    |**SelectedValue**|Visual Studio define essa propriedade como a coluna original descartada dos **fontes de dados** janela.<br /><br /> Se você precisar fazer um ajuste, defina isso para a coluna de chave estrangeira na tabela relacionada.|  
  
## <a name="see-also"></a>Consulte também  
 [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

