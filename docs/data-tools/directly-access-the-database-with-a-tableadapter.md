---
title: Acessar o banco de dados diretamente com um TableAdapter
description: Acesse diretamente um banco de dados com um TableAdapter, usando métodos como INSERT, Update e Delete para manipular dados diretamente no banco de dado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Visual Basic], accessing with a TableAdapter
- DBDirect methods
- datasets [Visual Basic], adding to projects
- data [Visual Studio], saving
- TableAdapter.Delete method
- GenerateDbDirectMethods property
- TableAdapter.Insert method
- TableAdapter.GenerateDBDirectMethods property
- TableAdapter.Update method
- saving data
- TableAdapters
ms.assetid: 012c5924-91f7-4790-b2a6-f51402b7014b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 30248632eacde07cfcc94213aeeb75ecac8dcf70
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215910"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>Acessar o banco de dados diretamente com um TableAdapter

Além dos `InsertCommand` `UpdateCommand` `DeleteCommand` TableAdapters, e, são criados com métodos que podem ser executados diretamente no banco de dados. Você pode chamar esses métodos ( `TableAdapter.Insert` , `TableAdapter.Update` e `TableAdapter.Delete` ) para manipular dados diretamente no banco de dado.

Se você não quiser criar esses métodos diretos, defina a propriedade do TableAdapter `GenerateDbDirectMethods` como `false` na janela **Propriedades** . Se qualquer consulta for adicionada a um TableAdapter além da consulta principal do TableAdapter, elas serão consultas autônomas que não geram esses `DbDirect` métodos.

## <a name="send-commands-directly-to-a-database"></a>Enviar comandos diretamente para um banco de dados

Chame o `DbDirect` método TableAdapter que executa a tarefa que você está tentando realizar.

### <a name="to-insert-new-records-directly-into-a-database"></a>Para inserir novos registros diretamente em um banco de dados

- Chame o método do TableAdapter `Insert` , passando os valores para cada coluna como parâmetros. O procedimento a seguir usa a `Region` tabela no banco de dados Northwind como um exemplo.

    > [!NOTE]
    > Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

### <a name="to-update-records-directly-in-a-database"></a>Para atualizar registros diretamente em um banco de dados

- Chame o método do TableAdapter `Update` , passando os valores novos e originais para cada coluna como parâmetros.

    > [!NOTE]
    > Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet18":::

### <a name="to-delete-records-directly-from-a-database"></a>Para excluir registros diretamente de um banco de dados

- Chame o método do TableAdapter `Delete` , passando os valores de cada coluna como parâmetros do `Delete` método. O procedimento a seguir usa a `Region` tabela no banco de dados Northwind como um exemplo.

    > [!NOTE]
    > Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet21":::

## <a name="see-also"></a>Confira também

- [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)
