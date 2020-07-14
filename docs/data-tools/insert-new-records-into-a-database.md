---
title: Inserir novos registros em um banco de dados
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, inserting new records into
- data [Visual Studio], saving
- databases, inserting new records into
- records, inserting
- saving data
ms.assetid: ea118fff-69b1-4675-b79a-e33374377f04
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b703d3ccc6ffbd5e2449a1768071b930f606f37f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281988"
---
# <a name="insert-new-records-into-a-database"></a>Inserir novos registros em um banco de dados

Para inserir novos registros em um banco de dados, você pode usar o `TableAdapter.Update` método ou um dos métodos DBDirect do TableAdapter (especificamente o `TableAdapter.Insert` método). Para obter mais informações, consulte [TableAdapter](../data-tools/create-and-configure-tableadapters.md).

Se seu aplicativo não usar TableAdapters, você poderá usar objetos de comando (por exemplo, <xref:System.Data.SqlClient.SqlCommand> ) para inserir novos registros em seu banco de dados.

Se o seu aplicativo usa conjuntos de dados para armazenar, use o `TableAdapter.Update` método. O `Update` método envia todas as alterações (atualizações, inserções e exclusões) para o banco de dados.

Se seu aplicativo usar objetos para armazenar dados, ou se você quiser um controle mais preciso sobre a criação de novos registros no banco de dado, use o `TableAdapter.Insert` método.

Se o TableAdapter não tiver um `Insert` método, significa que o TableAdapter está configurado para usar procedimentos armazenados ou sua `GenerateDBDirectMethods` propriedade é definida como `false` . Tente definir a propriedade do TableAdapter `GenerateDBDirectMethods` para `true` de dentro do **Designer de conjunto de dados**e salve o conjunto de os. Isso irá regenerar o TableAdapter. Se o TableAdapter ainda não tiver um `Insert` método, a tabela provavelmente não fornecerá informações de esquema suficientes para distinguir entre linhas individuais (por exemplo, pode não haver nenhuma chave primária definida na tabela).

## <a name="insert-new-records-by-using-tableadapters"></a>Inserir novos registros usando TableAdapters

Os TableAdapters fornecem maneiras diferentes de inserir novos registros em um banco de dados, dependendo dos requisitos do seu aplicativo.

Se o seu aplicativo usa conjuntos de dados para armazenar, você pode simplesmente adicionar novos registros ao desejado <xref:System.Data.DataTable> no DataSet e, em seguida, chamar o `TableAdapter.Update` método. O `TableAdapter.Update` método envia quaisquer alterações no <xref:System.Data.DataTable> banco de dados (incluindo registros modificados e excluídos).

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>Para inserir novos registros em um banco de dados usando o método TableAdapter. Update

1. Adicione novos registros ao desejado <xref:System.Data.DataTable> criando um novo <xref:System.Data.DataRow> e adicionando-o à <xref:System.Data.DataTable.Rows%2A> coleção.

2. Depois que as novas linhas forem adicionadas ao <xref:System.Data.DataTable> , chame o `TableAdapter.Update` método. Você pode controlar a quantidade de dados a serem atualizados passando um inteiro <xref:System.Data.DataSet> , um <xref:System.Data.DataTable> , uma matriz de <xref:System.Data.DataRow> s ou um único <xref:System.Data.DataRow> .

   O código a seguir mostra como adicionar um novo registro a um <xref:System.Data.DataTable> e, em seguida, chamar o `TableAdapter.Update` método para salvar a nova linha no banco de dados. (Este exemplo usa a `Region` tabela no banco de dados Northwind.)

   [!code-vb[VbRaddataSaving#14](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_1.vb)]
   [!code-csharp[VbRaddataSaving#14](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_1.cs)]

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>Para inserir novos registros em um banco de dados usando o método TableAdapter. Insert

Se seu aplicativo usa objetos para armazenar dados, você pode usar o `TableAdapter.Insert` método para criar novas linhas diretamente no banco de dado. O `Insert` método aceita os valores individuais para cada coluna como parâmetros. Chamar o método insere um novo registro no banco de dados com os valores de parâmetro passados.

- Chame o método do TableAdapter `Insert` , passando os valores para cada coluna como parâmetros.

O procedimento a seguir demonstra como usar o `TableAdapter.Insert` método para inserir linhas. Este exemplo insere dados na `Region` tabela no banco de dado Northwind.

> [!NOTE]
> Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

[!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_2.vb)]
[!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_2.cs)]

## <a name="insert-new-records-by-using-command-objects"></a>Inserir novos registros usando objetos de comando

Você pode inserir novos registros diretamente em um banco de dados usando objetos de comando.

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>Para inserir novos registros em um banco de dados usando objetos de comando

- Crie um novo objeto de comando e, em seguida, defina suas `Connection` `CommandType` Propriedades, e `CommandText` .

O exemplo a seguir demonstra a inserção de registros em um banco de dados usando o objeto Command. Ele insere dados na `Region` tabela no banco de dado Northwind.

[!code-vb[VbRaddataSaving#16](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_3.vb)]
[!code-csharp[VbRaddataSaving#16](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_3.cs)]

## <a name="net-security"></a>Segurança do .NET

Você deve ter acesso ao banco de dados ao qual está tentando se conectar, bem como permissão para executar inserções na tabela desejada.

## <a name="see-also"></a>Veja também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
