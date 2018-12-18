---
title: Adicionar código a TableAdapters em aplicativos de n camadas
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: e5a9aad4aaecb629f5860fadf56e35a55455be63
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38783084"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>Adicionar código a TableAdapters em aplicativos de n camadas
Você pode estender a funcionalidade de um TableAdapter, criando um arquivo de classe parcial para o TableAdapter e adicionando código a ele (em vez de adicionar código para o *DatasetName.DataSet.Designer* arquivo). Classes parciais permitem codificar uma classe específica a ser dividido entre vários arquivos físicos. Para obter mais informações, consulte [parcial](/dotnet/visual-basic/language-reference/modifiers/partial) ou [partial (tipo)](/dotnet/csharp/language-reference/keywords/partial-type).

O código que define um TableAdapter é gerado sempre que forem feitas alterações no TableAdapter no conjunto de dados. Esse código também é gerado quando as alterações são feitas durante a execução de qualquer assistente que modifica a configuração do TableAdapter. Para impedir que seu código seja excluído durante a regeneração de um TableAdapter, adicione código ao arquivo de classe parcial do TableAdapter.

Por padrão, após você separar o conjunto de dados e o código TableAdapter, o resultado é um arquivo de classe distintas em cada projeto. O projeto original tem um arquivo chamado *DatasetName.Designer.vb* (ou *DatasetName.Designer.cs*) que contém o código do TableAdapter. O projeto que é designado na **projeto Dataset** propriedade tem um arquivo chamado *DatasetName.DataSet.Designer.vb* (ou *DatasetName.DataSet.Designer.cs*) que contém o código do conjunto de dados.

> [!NOTE]
>  Quando você separa os conjuntos de dados e TableAdapters (Configurando o **projeto DataSet** propriedade), classes parciais do conjunto de dados existentes no projeto não serão movidas automaticamente. As classes parciais do conjunto de dados existentes devem ser movidas manualmente para o projeto de conjunto de dados.

> [!NOTE]
> O conjunto de dados fornece funcionalidade para gerar <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> manipuladores de eventos quando a validação é necessária. Para obter mais informações, consulte [adicionar validação a um conjunto de dados de n camadas](../data-tools/add-validation-to-an-n-tier-dataset.md).

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>Para adicionar o código do usuário a um TableAdapter em um aplicativo de n camadas

1.  Localize o projeto que contém o *. xsd* arquivo.

2.  Clique duas vezes o *. xsd* arquivo para abrir o **Dataset Designer**.

3.  Clique com botão direito no TableAdapter que você deseja adicionar código para e, em seguida, selecione **Exibir código**.

     Uma classe parcial é criada e é aberto no Editor de códigos.

4.  Adicione o código dentro da declaração de classe parcial.

5.  O exemplo a seguir mostra onde adicionar código para o `CustomersTableAdapter` no `NorthwindDataSet`:

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

## <a name="see-also"></a>Consulte também

- [Visão geral dos aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)
- [Como adicionar código a conjuntos de dados em aplicativos de N camadas](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [Criar e configurar TableAdapters](create-and-configure-tableadapters.md)
- [Visão geral de atualização hierárquica](hierarchical-update.md)
