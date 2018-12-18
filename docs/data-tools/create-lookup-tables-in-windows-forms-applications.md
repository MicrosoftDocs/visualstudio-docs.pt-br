---
title: Criar tabelas de pesquisa em aplicativos do Windows Forms
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- lookup tables
- lookup tables, creating
ms.assetid: 0edd5385-c381-4b17-9096-74e2778db9d5
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: c52e5f157dcbc6dcfeacf72df465bd3d8d9d172e
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304904"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>Criar tabelas de pesquisa em aplicativos do Windows Forms

O termo *tabela de pesquisa* descreve controles que estão associados às tabelas de dois dados relacionados. Esses controles de pesquisa exibem dados da primeira tabela com base em um valor selecionado na segunda tabela.

Você pode criar tabelas de pesquisa, arrastando o nó principal de uma tabela pai (da [janela Data Sources](add-new-data-sources.md#data-sources-window)) para um controle em seu formulário que já está associado à coluna na tabela filho relacionada.

Por exemplo, considere uma tabela de `Orders` em um banco de dados de vendas. Cada registro a `Orders` tabela inclui um `CustomerID`, indicando qual cliente fez o pedido. O `CustomerID` é uma chave estrangeira apontando para um registro de cliente no `Customers` tabela. Nesse cenário, você expandirá a `Orders` na tabela o **fontes de dados** janela e defina o nó principal como **detalhes**. Em seguida, defina a `CustomerID` coluna para usar um <xref:System.Windows.Forms.ComboBox> (ou qualquer outro controle que dá suporte à vinculação de pesquisa) e arraste o `Orders` nó para seu formulário. Por fim, arraste o `Customers` nó para o controle que está associado à coluna relacionada — nesse caso, o <xref:System.Windows.Forms.ComboBox> associado para o `CustomerID` coluna.

## <a name="to-databind-a-lookup-control"></a>Vincular dados de um controle de pesquisa

1.  Com o projeto aberto, abra o **fontes de dados** janela escolhendo **exibição** > **Other Windows** > **defontesdedados**.

    > [!NOTE]
    > Tabelas de pesquisa requerem que as duas tabelas relacionadas ou objetos estejam disponíveis na **fontes de dados** janela. Para obter mais informações, consulte [relacionamentos em conjuntos de dados](relationships-in-datasets.md).

2.  Expanda os nós na **fontes de dados** janela até que você possa ver a tabela pai e todas as suas colunas e a tabela filho relacionada e todas as suas colunas.

    > [!NOTE]
    > O nó da tabela filho é o nó que aparece como um nó filho expansível na tabela pai.

3.  Altere o tipo subjacente da tabela filho para **detalhes** selecionando **detalhes** na lista de controle no nó da tabela filho. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

4.  Localize o nó que relaciona as duas tabelas (o `CustomerID` nó no exemplo anterior). Altere seu tipo subjacente para um <xref:System.Windows.Forms.ComboBox> , selecionando **ComboBox** na lista de controle.

5.  Arraste o nó da tabela filho principal dos **fontes de dados** window para seu formulário.

     Controles de ligação de dados (com rótulos descritivos) e uma ferramenta da faixa (<xref:System.Windows.Forms.BindingNavigator>) aparecem no formulário. Um [DataSet](../data-tools/dataset-tools-in-visual-studio.md), [TableAdapter](../data-tools/create-and-configure-tableadapters.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.

6.  Agora, arraste o nó da tabela pai principal do **fontes de dados** janela diretamente para o controle de pesquisa (o <xref:System.Windows.Forms.ComboBox>).

     As associações de pesquisa agora são estabelecidas. Consulte a tabela a seguir para as propriedades específicas que foram definidas no controle.

    |Propriedade|Explicação da configuração|
    |--------------| - |
    |DataSource|O Visual Studio define esta propriedade para o <xref:System.Windows.Forms.BindingSource> criado para a tabela que você arrasta para o controle (em oposição ao <xref:System.Windows.Forms.BindingSource> criado quando o controle foi criado).<br /><br /> Se você precisar fazer um ajuste, defina isso como o <xref:System.Windows.Forms.BindingSource> da tabela com a coluna que você deseja exibir.|
    |DisplayMember|O Visual Studio define essa propriedade para a primeira coluna após a chave primária que tem um tipo de dado de cadeia da tabela que você arrasta para o controle.<br /><br /> Se você precisar fazer um ajuste, defina isso para o nome da coluna que deseja exibir.|
    |ValueMember|O Visual Studio define essa propriedade para a primeira coluna participante da chave primária, ou a primeira coluna na tabela, se nenhuma chave for definida.<br /><br /> Se você precisar fazer um ajuste, defina isso para a chave primária na tabela com a coluna que você deseja exibir.|
    |SelectedValue|Visual Studio define essa propriedade como a coluna original descartada dos **fontes de dados** janela.<br /><br /> Se você precisar fazer um ajuste, defina isso para a coluna de chave estrangeira na tabela relacionada.|

## <a name="see-also"></a>Consulte também

- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)