---
title: Inserir novos registros em um banco de dados
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: aae5ec2197ff2a899f27df20e7199fdeb7a02d31
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949195"
---
# <a name="insert-new-records-into-a-database"></a>Inserir novos registros em um banco de dados

Para inserir novos registros em um banco de dados, você pode usar o `TableAdapter.Update` método, ou um dos métodos DBDirect do TableAdapter (especificamente o `TableAdapter.Insert` método). Para obter mais informações, consulte [TableAdapter](../data-tools/create-and-configure-tableadapters.md).

Se seu aplicativo não usar TableAdapters, você pode usar objetos de comando (por exemplo, <xref:System.Data.SqlClient.SqlCommand>) para inserir novos registros no banco de dados.

Se seu aplicativo usa conjuntos de dados para armazenar dados, use o `TableAdapter.Update` método. O `Update` método envia todas as alterações (atualizações, inserções e exclusões) para o banco de dados.

Se seu aplicativo usa objetos para armazenar dados, ou se você quiser ter maior controle sobre a criação de novos registros no banco de dados, use o `TableAdapter.Insert` método.

Se seu TableAdapter não tem um `Insert` método, ele significa que o ou o TableAdapter está configurado para usar procedimentos armazenados ou seus `GenerateDBDirectMethods` estiver definida como `false`. Tente definir o TableAdapter `GenerateDBDirectMethods` propriedade para `true` de dentro de **Dataset Designer**e, em seguida, salve o conjunto de dados. Isso irá regenerar o TableAdapter. Se o TableAdapter ainda não tiver um `Insert` método, a tabela provavelmente não fornece informações de esquema suficientes para distinguir entre linhas individuais (por exemplo, não pode haver nenhum conjunto de chaves primário na tabela).

## <a name="insert-new-records-by-using-tableadapters"></a>Inserir novos registros usando TableAdapters

TableAdapters fornecem maneiras diferentes para inserir novos registros em um banco de dados, dependendo dos requisitos do seu aplicativo.

Se seu aplicativo usa conjuntos de dados para armazenar dados, você pode simplesmente adicionar novos registros para o estado desejado <xref:System.Data.DataTable> no conjunto de dados e, em seguida, chame o `TableAdapter.Update` método. O `TableAdapter.Update` método envia todas as alterações <xref:System.Data.DataTable> no banco de dados (incluindo registros excluídos e modificados).

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>Para inserir novos registros em um banco de dados usando o método TableAdapter.

1. Adicionar novos registros para o estado desejado <xref:System.Data.DataTable> criando um novo <xref:System.Data.DataRow> e adicioná-lo para o <xref:System.Data.DataTable.Rows%2A> coleção.

2. Depois que as novas linhas são adicionadas para o <xref:System.Data.DataTable>, chame o `TableAdapter.Update` método. Você pode controlar a quantidade de dados para atualizar, passando um inteiro <xref:System.Data.DataSet>, um <xref:System.Data.DataTable>, uma matriz de <xref:System.Data.DataRow>s ou um único <xref:System.Data.DataRow>.

   O código a seguir mostra como adicionar um novo registro para um <xref:System.Data.DataTable> e, em seguida, chamar o `TableAdapter.Update` método para salvar a nova linha no banco de dados. (Este exemplo usa o `Region` tabela no banco de dados Northwind.)

   [!code-vb[VbRaddataSaving#14](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_1.vb)]
   [!code-csharp[VbRaddataSaving#14](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_1.cs)]

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>Para inserir novos registros em um banco de dados usando o método TableAdapter.

Se seu aplicativo usa objetos para armazenar dados, você pode usar o `TableAdapter.Insert` método para criar novas linhas diretamente no banco de dados. O `Insert` método aceita os valores individuais para cada coluna como parâmetros. Chamar o método insere um novo registro no banco de dados com os valores de parâmetro passados.

- Chame o TableAdapter `Insert` método, passando os valores para cada coluna como parâmetros.

O procedimento a seguir demonstra como usar o `TableAdapter.Insert` método para inserir linhas. Este exemplo insere dados no `Region` tabela no banco de dados Northwind.

> [!NOTE]
> Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.

[!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_2.vb)]
[!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_2.cs)]

## <a name="insert-new-records-by-using-command-objects"></a>Inserir novos registros por meio de objetos de comando

Você pode inserir novos registros diretamente em um banco de dados usando objetos de comando.

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>Para inserir novos registros em um banco de dados usando objetos de comando

- Criar um novo objeto de comando e, em seguida, defina suas `Connection`, `CommandType`, e `CommandText` propriedades.

O exemplo a seguir demonstra a inserção de registros em um banco de dados usando o objeto de comando. Ele insere dados no `Region` tabela no banco de dados Northwind.

[!code-vb[VbRaddataSaving#16](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_3.vb)]
[!code-csharp[VbRaddataSaving#16](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_3.cs)]

## <a name="net-framework-security"></a>Segurança do .NET Framework

Você deve ter acesso ao banco de dados que você está tentando se conectar ao, bem como permissão para executar inserções na tabela desejada.

## <a name="see-also"></a>Consulte também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)