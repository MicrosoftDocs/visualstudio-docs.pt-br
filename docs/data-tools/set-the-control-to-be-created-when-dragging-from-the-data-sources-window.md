---
title: Definir o controle para criar ao arrastar da janela fontes de dados
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Data Sources Window, select controls
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- data [Visual Studio], Data Sources window
ms.assetid: 20597ff8-0c98-43ec-8fb1-05376804ba48
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 8f5a3cf2d1f34ca9a3d0c2918a8f3f0a3e05260f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281533"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>Definir o controle a ser criado quando arrastado da janela Fontes de Dados

Você pode criar controles vinculados a dados arrastando itens da janela **fontes de dados** para o designer WPF ou Windows Forms Designer. Cada item na janela **Data Sources** tem um controle padrão que é criado quando você o arrasta para o designer. No entanto, você pode optar por criar um controle diferente.

## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>Definir os controles a serem criados para tabelas de dados ou objetos

Antes de arrastar itens que representam tabelas de dados ou objetos da janela **fontes de dados** , você pode optar por exibir todos os dados em um controle ou exibir cada coluna ou propriedade em um controle separado.

Nesse contexto, o termo *objeto* refere-se a um objeto comercial personalizado, uma entidade (em um modelo de dados de entidade) ou um objeto retornado por um serviço.

### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>Para definir os controles a serem criados para tabelas de dados ou objetos

1. Verifique se o designer do **WPF** ou o designer de **Windows Forms** está aberto.

2. Na janela **fontes de dados** , selecione o item que representa a tabela de dados ou o objeto que você deseja definir.

   > [!TIP]
   > Se a janela **fontes de dados** não estiver aberta, você poderá abri-la selecionando **Exibir**  >  **outras**  >  **fontes de dados**do Windows.

3. Clique no menu suspenso do item e, em seguida, clique em um dos seguintes itens no menu:

    - Para exibir cada campo de dados em um controle separado, clique em **detalhes**. Quando você arrasta o item de dados para o designer, essa ação criará um controle associado a dados diferente para cada coluna ou propriedade da tabela ou objeto de dados pai, juntamente com os rótulos para cada controle.

    - Para exibir todos os dados em um único controle, selecione um controle diferente na lista, como **DataGrid** ou **list** em um aplicativo WPF, ou **DataGridView** em um aplicativo Windows Forms.

    A lista de controles disponíveis depende de qual designer você abriu, qual versão do .NET seu projeto tem como destino e se você adicionou controles personalizados que dão suporte à ligação de dados com a **caixa de ferramentas**. Se o controle que você deseja criar não estiver na lista de controles disponíveis, você poderá adicionar o controle à lista. Para obter mais informações, consulte [Adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

    Para saber como criar um controle de Windows Forms personalizado que pode ser adicionado à lista de controles para tabelas de dados ou objetos na janela **fontes de dados** , consulte [criar um controle de usuário Windows Forms que dá suporte à ligação de dados complexa](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).

## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>Definir os controles a serem criados para colunas de dados ou propriedades

Antes de arrastar um item que representa uma coluna ou uma propriedade de um objeto da janela **fontes de dados** para o designer, você pode definir o controle a ser criado.

### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>Para definir os controles a serem criados para colunas ou propriedades

1. Verifique se o designer do **WPF** ou o designer de **Windows Forms** está aberto.

2. Na janela **fontes de dados** , expanda a tabela ou o objeto desejado para exibir suas colunas ou propriedades.

3. Selecione cada coluna ou propriedade para a qual você deseja definir o controle a ser criado.

4. Clique no menu suspenso da coluna ou da propriedade e, em seguida, selecione o controle que você deseja criar quando o item for arrastado para o designer.

     A lista de controles disponíveis depende de qual designer você abriu, qual versão do .NET seu projeto tem como destino e quais controles personalizados oferecem suporte à ligação de dados que você adicionou à **caixa de ferramentas**. Se o controle que você deseja criar estiver na lista de controles disponíveis, você poderá adicionar o controle à lista. Para obter mais informações, consulte [Adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

     Para saber como criar um controle personalizado que pode ser adicionado à lista de controles para colunas de dados ou propriedades na janela **fontes de dados** , consulte [criar um Windows Forms controle de usuário que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).

     Se você não quiser criar um controle para a coluna ou propriedade, selecione **nenhum** no menu suspenso. Isso será útil se você quiser arrastar a tabela ou o objeto pai para o designer, mas não desejar incluir a coluna ou propriedade específica.

## <a name="see-also"></a>Veja também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
