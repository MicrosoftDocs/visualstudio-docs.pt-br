---
title: Definir o controle a ser criado quando arrastado da janela Fontes de Dados
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Data Sources Window, select controls
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- data [Visual Studio], Data Sources window
ms.assetid: 20597ff8-0c98-43ec-8fb1-05376804ba48
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: daceedd2709de7882ecff5b29a657f706c96175d
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305462"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>Definir o controle a ser criado quando arrastado da janela Fontes de Dados

Você pode criar controles associados a dados arrastando itens dos **fontes de dados** janela para o WPF designer ou o designer de formulários do Windows. Cada item na **fontes de dados** janela tem um controle padrão que é criado quando você arrastá-lo para o designer. No entanto, você pode optar por criar um controle diferente.

## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>Defina os controles a serem criados para tabelas de dados ou objetos

Antes de arrastar itens que representam as tabelas de dados ou objetos a partir de **fontes de dados** janela, você pode escolher para exibir todos os dados em um controle, ou para exibir cada coluna ou propriedade em um controle separado.

Nesse contexto, o termo *objeto* refere-se a um objeto comercial personalizado, uma entidade (em um modelo de dados de entidade) ou um objeto retornado por um serviço.

### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>Para definir os controles a serem criados para tabelas de dados ou objetos

1. Certifique-se a **WPF** designer ou o **Windows Forms** designer é aberto.

2. No **fontes de dados** janela, selecione o item que representa a tabela de dados ou objeto que você deseja definir.

   > [!TIP]
   > Se o **fontes de dados** janela não estiver aberta, você pode abri-lo selecionando **exibição** > **Other Windows** > **defontesdedados**.

3. Clique no menu suspenso para o item e, em seguida, clique em um dos seguintes itens no menu:

    - Para exibir cada campo de dados em um controle separado, clique em **detalhes**. Quando você arrasta o item de dados para o designer, essa ação criará um controle de associação de dados diferente para cada coluna ou propriedade do objeto, juntamente com os rótulos para cada controle ou tabela de dados pai.

    - Para exibir todos os dados em um único controle, selecione um controle diferente na lista, como **DataGrid** ou **lista** em um aplicativo WPF, ou **DataGridView** em um Windows Forms aplicativo.

    A lista de controles disponíveis depende, em que o designer você abriu, qual versão do .NET Framework o projeto está destinado e se você tiver adicionado personalizado controla esses suporte à vinculação de dados para o **caixa de ferramentas**. Se o controle que você deseja criar não estiver na lista de controles disponíveis, você pode adicionar o controle à lista. Para obter mais informações, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

    Para saber como criar um controle personalizado do Windows Forms que pode ser adicionado à lista de controles para tabelas de dados ou objetos na **fontes de dados** janela, consulte [criar um controle de usuário do Windows Forms que dá suporte a dados complexos associação](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).

## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>Defina os controles a serem criados para colunas de dados ou propriedades

Antes de arrastar um item que representa uma coluna ou uma propriedade de um objeto a partir de **fontes de dados** janela no Designer, você pode definir o controle a ser criado.

### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>Para definir os controles a serem criados para colunas ou propriedades

1. Certifique-se a **WPF** designer ou o **Windows Forms** designer é aberto.

2. No **fontes de dados** janela, expanda a tabela desejada ou para exibir suas colunas ou propriedades do objeto.

3. Selecione cada coluna ou propriedade para o qual você deseja definir o controle a ser criado.

4. Clique no menu suspenso para a coluna ou propriedade e, em seguida, selecione o controle que você deseja criar quando o item é arrastado para o designer.

     A lista de controles disponíveis depende, em que o designer você abriu, qual versão do .NET Framework o projeto está destinado e quais personalizado controles que suportam dados de associação que você adicionou à **caixa de ferramentas**. Se o controle que você deseja criar estiver na lista de controles disponíveis, você pode adicionar o controle à lista. Para obter mais informações, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

     Para saber como criar um controle personalizado que pode ser adicionado à lista de controles para colunas de dados ou as propriedades na **fontes de dados** janela, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).

     Se você não quiser criar um controle para a propriedade ou coluna, selecione **None** no menu suspenso. Isso é útil se você deseja arrastar a tabela pai ou o objeto para o designer, mas você não deseja incluir a propriedade ou coluna específica.

## <a name="see-also"></a>Consulte também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)