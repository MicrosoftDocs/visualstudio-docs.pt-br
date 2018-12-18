---
title: Criar tabelas de pesquisa em aplicativos do WPF
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 56a1fbff-c7e8-4187-a1c1-ffd17024bc1b
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: c76f769234d8b8c14ccd44d8c2cf4c669bf48ffd
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305475"
---
# <a name="create-lookup-tables-in-wpf-applications"></a>Criar tabelas de pesquisa em aplicativos do WPF

O termo *tabela de pesquisa* (às vezes chamado de um *vinculação de pesquisa*) descreve um controle que exibe informações de uma tabela de dados com base no valor de um campo de chave estrangeira em outra tabela. Você pode criar uma tabela de pesquisa, arrastando o nó principal de uma tabela pai ou objeto de **fontes de dados** window para um controle que já está associado a uma coluna ou propriedade em uma tabela filho relacionada.

Por exemplo, considere uma tabela de `Orders` em um banco de dados de vendas. Cada registro a `Orders` tabela inclui uma `CustomerID` que indica qual cliente fez o pedido. O `CustomerID` é uma chave estrangeira que aponta para um registro de cliente no `Customers` tabela. Quando você exibe uma lista de pedidos do `Orders` tabela, você talvez queira exibir o nome do cliente real, em vez do `CustomerID`. Porque o nome do cliente está no `Customers` tabela, você precisa criar uma tabela de pesquisa para exibir o nome do cliente. A tabela de pesquisa usa o `CustomerID` valor no `Orders` registre para navegar pela relação e retornar o nome do cliente.

## <a name="to-create-a-lookup-table"></a>Criar uma tabela de pesquisa

1.  Adicione um dos seguintes tipos de fontes de dados com dados relacionados ao seu projeto:

    -   Conjunto de dados ou modelo de dados de entidade.

    -   WCF Data Service, serviço WCF ou serviço web. Para obter mais informações, consulte [como: conectar-se aos dados em um serviço](../data-tools/how-to-connect-to-data-in-a-service.md).

    -   Objetos. Para obter mais informações, consulte [associar a objetos no Visual Studio](bind-objects-in-visual-studio.md).

    > [!NOTE]
    > Antes de criar uma tabela de pesquisa, duas tabelas relacionadas ou objetos devem existir como uma fonte de dados para o projeto.

2.  Abra o **WPF Designer**e certifique-se de que o designer contém um contêiner que é um destino de soltar válido para itens na **fontes de dados** janela.

     Para obter mais informações sobre destinos depósitos válidos, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md).

3.  Sobre o **dados** menu, clique em **Mostrar fontes de dados** para abrir o **fontes de dados** janela.

4.  Expanda os nós na **fontes de dados** janela, até que você possa ver a tabela pai ou objeto e a tabela filho relacionada ou objeto.

    > [!NOTE]
    > A tabela filho relacionada ou o objeto é o nó que aparece como um nó filho expansível sob a tabela pai ou o objeto.

5.  Clique no menu suspenso para o nó filho e selecione **detalhes**.

6.  Expanda o nó filho.

7.  Sob o nó filho, clique no menu suspenso para o item que está relacionado os dados pai e filho. (No exemplo anterior, isso é o **CustomerID** nó.) Selecione um dos seguintes tipos de controles que dão suporte à vinculação de pesquisa:

    -   **ComboBox**

    -   **ListBox**

    -   **ListView**

        > [!NOTE]
        > Se o **ListBox** ou **ListView** controle não aparecer na lista, você pode adicionar esses controles à lista. Para obter informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

    -   Qualquer controle personalizado que deriva de <xref:System.Windows.Controls.Primitives.Selector>.

        > [!NOTE]
        > Para obter informações sobre como adicionar personalizado controles à lista de controles que você podem selecionar para itens na **fontes de dados** janela, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

8.  Arraste o nó filho do **fontes de dados** window para um contêiner no WPF designer. (No exemplo anterior, o nó filho é o **pedidos** nó.)

     O Visual Studio gera XAML que cria novos controles de associação de dados para cada um dos itens que você arrasta. O XAML também adiciona um novo <xref:System.Windows.Data.CollectionViewSource> para a tabela filho ou o objeto para os recursos de destino de soltar. Para algumas fontes de dados, o Visual Studio também gera código para carregar dados na tabela ou objeto. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md).

9. Arraste o nó pai de **fontes de dados** janela para o controle de associação de pesquisa que você criou anteriormente. (No exemplo anterior, o nó pai é o **clientes** nó).

     O Visual Studio define algumas propriedades no controle para configurar a associação de pesquisa. A tabela a seguir lista as propriedades que o Visual Studio modifica. Se necessário, você pode alterar essas propriedades no XAML ou nos **propriedades** janela.

    |Propriedade|Explicação da configuração|
    |--------------| - |
    |<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>|Esta propriedade especifica a coleção ou associação que é usada para obter os dados que são exibidos no controle. Visual Studio define essa propriedade para o <xref:System.Windows.Data.CollectionViewSource> para os dados pai que você arrastou para o controle.|
    |<xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A>|Essa propriedade especifica o caminho do item de dados que é exibido no controle. Visual Studio define essa propriedade para a primeira coluna ou propriedade nos dados do pai, após a chave primária, que tem um tipo de dados de cadeia de caracteres.<br /><br /> Se você quiser exibir uma coluna ou propriedade diferente dos dados pai, altere essa propriedade para o caminho de uma propriedade diferente.|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A>|Visual Studio é associado a essa propriedade como a coluna ou a propriedade dos dados filho que você arrastou para o designer. Isso é a chave estrangeira para os dados pai.|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValuePath%2A>|Visual Studio define essa propriedade ao caminho da coluna ou a propriedade dos dados filho que é a chave estrangeira para os dados pai.|

## <a name="see-also"></a>Consulte também

- [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [Exibir dados relacionados em aplicativos WPF](../data-tools/display-related-data-in-wpf-applications.md)
- [Passo a passo: exibindo dados relacionados em um aplicativo WPF](../data-tools/display-related-data-in-wpf-applications.md)