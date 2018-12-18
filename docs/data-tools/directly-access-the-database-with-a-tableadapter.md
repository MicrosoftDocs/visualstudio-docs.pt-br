---
title: Acessar o banco de dados diretamente com um TableAdapter
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 22a2580809394ba1b41e7923f4f2df458d995a93
ms.sourcegitcommit: 1df0ae74af03bcf0244129a29fd6bd605efc9f61
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50750952"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>Acessar o banco de dados diretamente com um TableAdapter

Além de `InsertCommand`, `UpdateCommand`, e `DeleteCommand`, TableAdapters são criados com métodos que podem ser executados diretamente no banco de dados. Você pode chamar esses métodos (`TableAdapter.Insert`, `TableAdapter.Update`, e `TableAdapter.Delete`) para manipular os dados diretamente no banco de dados.

Se você não quiser criar esses métodos diretos, defina o TableAdapter `GenerateDbDirectMethods` propriedade para `false` na **propriedades** janela. Se todas as consultas forem adicionadas a um TableAdapter, além da consulta principal do TableAdapter, eles são consultas autônomas que não gerá-los `DbDirect` métodos.

## <a name="send-commands-directly-to-a-database"></a>Enviar comandos diretamente para um banco de dados

Chame o TableAdapter `DbDirect` método que executa a tarefa que você está tentando realizar.

### <a name="to-insert-new-records-directly-into-a-database"></a>Para inserir novos registros diretamente em um banco de dados

-   Chame o TableAdapter `Insert` método, passando os valores para cada coluna como parâmetros. O procedimento a seguir usa o `Region` tabela no banco de dados Northwind como um exemplo.

    > [!NOTE]
    > Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

     [!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_1.vb)]
     [!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_1.cs)]

### <a name="to-update-records-directly-in-a-database"></a>Para atualizar registros diretamente em um banco de dados

-   Chame o TableAdapter `Update` método, passando os valores novos e originais para cada coluna como parâmetros.

    > [!NOTE]
    > Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

     [!code-vb[VbRaddataSaving#18](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_2.vb)]
     [!code-csharp[VbRaddataSaving#18](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_2.cs)]

### <a name="to-delete-records-directly-from-a-database"></a>Para excluir registros diretamente de um banco de dados

-   Chame o TableAdapter `Delete` método, passando os valores para cada coluna como parâmetros do `Delete` método. O procedimento a seguir usa o `Region` tabela no banco de dados Northwind como um exemplo.

    > [!NOTE]
    > Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

     [!code-vb[VbRaddataSaving#21](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_3.vb)]
     [!code-csharp[VbRaddataSaving#21](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_3.cs)]

## <a name="see-also"></a>Consulte também

- [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)