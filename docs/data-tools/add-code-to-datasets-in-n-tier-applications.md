---
title: Adicionar código aos conjuntos de dados em aplicativos de n camadas
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, extending DataSets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a57a05ddb8317ea31b852ded369ad7ef69d40bd0
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283080"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>Adicionar código aos conjuntos de dados em aplicativos de n camadas

Você pode estender a funcionalidade de um conjunto de um DataSet criando um arquivo de classe parcial para o conjunto de recursos e adicionando código a ele (em vez de adicionar código ao *DataSetName*. Arquivo DataSet. Designer). As classes parciais permitem que o código de uma classe específica seja dividido entre vários arquivos físicos. Para obter mais informações, consulte [classes e métodos](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods) [parciais](/dotnet/visual-basic/language-reference/modifiers/partial) ou parciais.

O código que define um conjunto de um DataSet é gerado toda vez que são feitas alterações na definição do conjunto de código (no dataset tipado). Esse código também é gerado quando você faz alterações durante a execução de qualquer assistente que modifica a configuração de um conjunto de uma. Para impedir que seu código seja excluído durante a regeneração de um conjunto de um DataSet, adicione o código ao arquivo de classe parcial do conjunto de um.

Por padrão, depois de separar o DataSet e o código do TableAdapter, o resultado é um arquivo de classe discreto em cada projeto. O projeto original tem um arquivo chamado *DataSetName. designer. vb* (ou *DataSetName.designer.cs*) que contém o código do TableAdapter. O projeto designado na Propriedade Project de **DataSet** tem um arquivo chamado *DataSetName. DataSet. designer. vb* (ou *DataSetName.DataSet.designer.cs*). Esse arquivo contém o código do conjunto de conteúdo.

> [!NOTE]
> Quando você separa DataSets e TableAdapters (definindo a propriedade de **projeto DataSet** ), as classes parciais DataSet existentes no projeto não serão movidas automaticamente. As classes parciais de DataSet existentes devem ser movidas manualmente para o projeto do conjunto de um.

> [!NOTE]
> Quando o código de validação precisa ser adicionado, o dataset tipado fornece a funcionalidade de geração <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> manipuladores de eventos. Para obter mais informações, consulte [Adicionar validação a um conjunto](../data-tools/add-validation-to-an-n-tier-dataset.md)de dados de n camadas.

## <a name="to-add-code-to-datasets-in-n-tier-applications"></a>Para adicionar código a conjuntos de valores em aplicativos de n camadas

1. Localize o projeto que contém o arquivo *. xsd* .

2. Selecione o arquivo **. xsd** para abrir o conjunto de um.

3. Clique com o botão direito do mouse na tabela de dados à qual você deseja adicionar o código (o nome da tabela na barra de título) e, em seguida, selecione **Exibir código**.

     Uma classe parcial é criada e aberta no editor de código.

4. Adicione o código dentro da declaração de classe parcial.

     O exemplo a seguir mostra onde adicionar código ao CustomersDataTable no NorthwindDataSet:

    ```vb
    Partial Public Class CustomersDataTable
        ' Add code here to add functionality
        ' to the CustomersDataTable.
    End Class
    ```

    ```csharp
    partial class CustomersDataTable
    {
        // Add code here to add functionality
        // to the CustomersDataTable.
    }
    ```

## <a name="see-also"></a>Veja também

- [Visão geral de aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)
- [Adicionar código a TableAdapters em aplicativos de N camadas](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [Criar e configurar TableAdapters](create-and-configure-tableadapters.md)
- [Visão geral de atualização hierárquica](hierarchical-update.md)
- [Ferramentas de DataSet no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
