---
title: Adicionar código a TableAdapters em aplicativos de n camadas
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3ea451ac60de971677ee2f7910b28b334c67dff3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283093"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>Adicionar código a TableAdapters em aplicativos de n camadas
Você pode estender a funcionalidade de um TableAdapter criando um arquivo de classe parcial para o TableAdapter e adicionando código a ele (em vez de adicionar código ao arquivo *DataSetName. DataSet. designer* ). As classes parciais permitem que o código de uma classe específica seja dividido entre vários arquivos físicos. Para obter mais informações, consulte [parcial](/dotnet/visual-basic/language-reference/modifiers/partial) ou [parcial (tipo)](/dotnet/csharp/language-reference/keywords/partial-type).

O código que define um TableAdapter é gerado sempre que são feitas alterações no TableAdapter no conjunto de data. Esse código também é gerado quando são feitas alterações durante a execução de qualquer assistente que modifica a configuração do TableAdapter. Para impedir que seu código seja excluído durante a regeneração de um TableAdapter, adicione o código ao arquivo de classe parcial do TableAdapter.

Por padrão, depois de separar o DataSet e o código do TableAdapter, o resultado é um arquivo de classe discreto em cada projeto. O projeto original tem um arquivo chamado *DataSetName. designer. vb* (ou *DataSetName.designer.cs*) que contém o código do TableAdapter. O projeto designado na Propriedade Project do **conjunto** de conteúdo tem um arquivo chamado *DataSetName. DataSet. designer. vb* (ou *DataSetName.DataSet.designer.cs*) que contém o código do conjunto de conteúdo.

> [!NOTE]
> Quando você separa os conjuntos de dados e os TableAdapters (configurando a propriedade **Projeto de Conjunto de Dados**), as classes dos conjuntos de dados parciais existentes no projeto não são movidas automaticamente. As classes parciais de DataSet existentes devem ser movidas manualmente para o projeto DataSet.

> [!NOTE]
> O conjunto de recursos fornece a funcionalidade de geração <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> manipuladores de eventos quando a validação é necessária. Para obter mais informações, consulte [Adicionar validação a um conjunto](../data-tools/add-validation-to-an-n-tier-dataset.md)de dados de n camadas.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>Para adicionar código de usuário a um TableAdapter em um aplicativo de n camadas

1. Localize o projeto que contém o arquivo *. xsd* .

2. Clique duas vezes no arquivo *. xsd* para abrir o **Designer de conjunto de dados**.

3. Clique com o botão direito do mouse no TableAdapter ao qual você deseja adicionar o código e selecione **Exibir código**.

     Uma classe parcial é criada e aberta no editor de código.

4. Adicione o código dentro da declaração de classe parcial.

5. O exemplo a seguir mostra onde adicionar código ao `CustomersTableAdapter` no `NorthwindDataSet` :

    ```vb
    Partial Public Class CustomersTableAdapter
        ' Add code here to add functionality
        ' to the CustomersTableAdapter.
    End Class
    ```

    ```csharp
    public partial class CustomersTableAdapter
    {
        // Add code here to add functionality
        // to the CustomersTableAdapter.
    }
    ```

## <a name="see-also"></a>Veja também

- [Visão geral de aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)
- [Como adicionar código a conjuntos de dados em aplicativos de N camadas](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [Criar e configurar TableAdapters](create-and-configure-tableadapters.md)
- [Visão geral de atualização hierárquica](hierarchical-update.md)
