---
title: Adicionar controles personalizados à janela Fontes de Dados
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
author: ghogen
ms.author: ghogen
manager: jillfra
ms.openlocfilehash: 39ff272581793be9b456bbc404119a488850b3c4
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283067"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>Adicionar controles personalizados à janela Fontes de Dados

Quando você arrasta um item da janela fontes de dados para uma superfície de design para criar um controle vinculado a dados, você pode selecionar o tipo de controle que você criar. Cada item na janela tem uma lista suspensa que exibe os controles dos quais você pode escolher. O conjunto de controles associados a cada item é determinado pelo tipo de dados do item. Se o controle que você deseja criar não aparecer na lista, você poderá seguir as instruções neste tópico para adicionar o controle à lista.

Para obter mais informações sobre como selecionar controles vinculados a dados para criar itens na janela fontes de dados, consulte [definir o controle a ser criado ao arrastar da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

## <a name="customize-the-bindable-controls-list"></a>Personalizar a lista de controles vinculáveis

Para adicionar ou remover controles da lista de controles disponíveis para itens na janela fontes de dados que têm um tipo de dados específico, execute as etapas a seguir.

### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>Para selecionar os controles a serem listados para um tipo de dados

1. Verifique se o designer do WPF ou o Designer de Formulários do Windows está aberto.

2. Na janela **fontes de dados** , clique em um item que faz parte de uma fonte de dados que você adicionou à janela e, em seguida, clique no menu suspenso do item.

   > [!TIP]
   > Se a janela fontes de dados não estiver aberta, abra-a selecionando **Exibir**  >  **outras**  >  **fontes de dados**do Windows.

3. No menu suspenso, clique em **Personalizar**. Uma das seguintes caixas de diálogo é aberta:

    - Se o **Designer de formulários do Windows** estiver aberto, a página **personalização da interface do usuário de dados** da caixa de diálogo **Opções** será aberta. Para obter mais informações, consulte [caixa de diálogo opções de personalização de interface do usuário de dados](../ide/reference/options-windows-forms-designer-data-ui-customization.md).

    - Se o **designer do WPF** estiver aberto, a caixa de diálogo **Personalizar vinculação de controle** será aberta.

4. Na caixa de diálogo, selecione um tipo de dados na lista suspensa **tipo de dados** .

    - Para personalizar a lista de controles de uma tabela ou objeto, selecione **[lista]**.

    - Para personalizar a lista de controles de uma coluna de uma tabela ou de uma propriedade de um objeto, selecione o tipo de dados da coluna ou propriedade no armazenamento de dados subjacente.

    - Para personalizar a lista de controles para exibir objetos de dados que têm formas definidas pelo usuário, selecione **[outros]**. Por exemplo, selecione **[outros]** se seu aplicativo tiver um controle personalizado que exibe dados de mais de uma propriedade de um objeto específico.

5. Na caixa **controles associados** , selecione cada controle que você deseja disponibilizar para o tipo de dados selecionado ou desmarque a seleção de todos os controles que deseja remover da lista.

    > [!NOTE]
    > Se o controle que você deseja selecionar não aparecer na caixa **controles associados** , você deverá adicionar o controle à lista. Para obter mais informações, consulte [Adicionar controles associados](#add-associated-controls).

6. Clique em **OK**.

7. Na janela **fontes de dados** , clique em um item do tipo de dados ao qual você acabou de associar um ou mais controles e, em seguida, clique no menu suspenso do item.

     Os controles selecionados na caixa **controles associados** agora aparecem no menu suspenso do item.

## <a name="add-associated-controls"></a>Adicionar controles associados

Se você quiser associar um controle a um tipo de dados, mas o controle não aparecer na caixa **controles associados** , você deverá adicionar o controle à lista. O controle deve estar localizado na solução atual ou em um assembly referenciado. Ele também deve estar disponível na **caixa de ferramentas** e ter um atributo que especifica o comportamento de vinculação de dados do controle.

Para adicionar controles à lista de controles associados:

1. Adicione o controle desejado à caixa de **ferramentas** clicando com o botão direito do mouse na **caixa de ferramentas** e selecionando **escolher itens**.

     O controle deve ter um dos seguintes atributos:

    |Atributo|Descrição|
    |---------------|-----------------|
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|Implemente esse atributo em controles simples que exibem uma única coluna (ou Propriedade) de dados, como um <xref:System.Windows.Forms.TextBox> .|
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|Implemente esse atributo em controles que exibem listas (ou tabelas) de dados, como um <xref:System.Windows.Forms.DataGridView> .|
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|Implemente esse atributo em controles que exibem listas (ou tabelas) de dados, mas também precisam apresentar uma única coluna ou propriedade, como um <xref:System.Windows.Forms.ComboBox> .|

2. Para Windows Forms, na caixa de diálogo **Opções** , abra a página **personalização da interface do usuário de dados** . Ou, para o WPF, abra a caixa de diálogo **Personalizar Associação de controle** . Para obter mais informações, consulte [Personalizar a lista de controles vinculáveis para um tipo de dados](#customize-the-bindable-controls-list).

3. Na caixa **controles associados** , o controle que você acabou de adicionar à **Toolbox** agora deve aparecer.

    > [!NOTE]
    > Somente os controles localizados na solução atual ou em um assembly referenciado podem ser adicionados à lista de controles associados. (Os controles também devem implementar um dos atributos de vinculação de dados na tabela anterior.) Para associar dados a um controle personalizado que não está disponível na janela fontes de dados, arraste o controle da **caixa de ferramentas** para a superfície de design e, em seguida, arraste o item para associar da janela **fontes de dados** para o controle.

## <a name="see-also"></a>Veja também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Caixa de diálogo opções de personalização da interface do usuário de dados](../ide/reference/options-windows-forms-designer-data-ui-customization.md)
