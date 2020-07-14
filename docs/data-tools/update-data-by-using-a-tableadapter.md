---
title: Atualizar dados usando um TableAdapter
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: f7ecca8c28ff355952907f1f0c49485117a25456
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281195"
---
# <a name="update-data-by-using-a-tableadapter"></a>Atualizar dados usando um TableAdapter

Depois que os dados em seu DataSet forem modificados e validados, você poderá enviar os dados atualizados de volta para um banco de dado chamando o `Update` método de um [TableAdapter](../data-tools/create-and-configure-tableadapters.md). O `Update` método atualiza uma única tabela de dados e executa o comando correto (INSERT, Update ou Delete) com base em <xref:System.Data.DataRow.RowState%2A> cada linha de dados na tabela. Quando um conjunto de um DataSet tem tabelas relacionadas, o Visual Studio gera uma classe TableAdaptermanager que você usa para fazer as atualizações. A classe TableAdaptermanager garante que as atualizações sejam feitas na ordem correta com base nas restrições de chave estrangeira definidas no banco de dados. Quando você usa controles vinculados a dados, a arquitetura DataBinding cria uma variável de membro da classe TableAdaptermanager chamada tableAdaptermanager.

> [!NOTE]
> Quando você tenta atualizar uma fonte de dados com o conteúdo de um conjunto, você pode obter erros. Para evitar erros, recomendamos que você coloque o código que chama o método do adaptador `Update` dentro de um `try` / `catch` bloco.

O procedimento exato para atualizar uma fonte de dados pode variar dependendo das necessidades dos negócios, mas inclui as seguintes etapas:

1. Chame o método do adaptador `Update` em um `try` / `catch` bloco.

2. Se uma exceção for detectada, localize a linha de dados que causou o erro.

3. Reconcilie o problema na linha de dados (programaticamente se você puder, ou apresentando a linha inválida para o usuário para modificação) e tente a atualização novamente ( <xref:System.Data.DataRow.HasErrors%2A> , <xref:System.Data.DataTable.GetErrors%2A> ).

## <a name="save-data-to-a-database"></a>Salvar dados em um banco de dado

Chame o `Update` método de um TableAdapter. Passe o nome da tabela de dados que contém os valores a serem gravados no banco de dado.

### <a name="to-update-a-database-by-using-a-tableadapter"></a>Para atualizar um banco de dados usando um TableAdapter

- Coloque o método do TableAdapter `Update` em um `try` / `catch` bloco. O exemplo a seguir mostra como atualizar o conteúdo da `Customers` tabela no `NorthwindDataSet` de dentro de um `try` / `catch` bloco.

     [!code-csharp[VbRaddataSaving#9](../data-tools/codesnippet/CSharp/update-data-by-using-a-tableadapter_1.cs)]
     [!code-vb[VbRaddataSaving#9](../data-tools/codesnippet/VisualBasic/update-data-by-using-a-tableadapter_1.vb)]

## <a name="see-also"></a>Veja também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
