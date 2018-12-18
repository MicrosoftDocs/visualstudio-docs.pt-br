---
title: 'Como: atualizar registros em um banco de dados | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- records, updating
- data [Visual Studio], saving
- records, editing
- databases, updating
- TableAdapter.Update method
ms.assetid: cdc8a8e4-a5fa-40dd-9221-97b8571d802a
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: b62dc86425dcbebb225c66eecd51505f674e20ec
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949026"
---
# <a name="how-to-update-records-in-a-database"></a>Como atualizar registros em um banco de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o `TableAdapter.Update` método para atualizar (Editar) registros em um banco de dados. O `TableAdapter.Update` método fornece várias sobrecargas que executam operações diferentes dependendo dos parâmetros passados. É importante entender os resultados da chamada essas assinaturas de método diferente.  
  
> [!NOTE]
>  Se seu aplicativo não usa TableAdapters e, em seguida, você pode usar objetos de comando para atualizar registros no banco de dados (por exemplo, <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>). Para obter mais informações sobre como atualizar dados com objetos de comando, consulte "Atualizar registros usando objetos de comando" abaixo.  
  
 A tabela a seguir descreve o comportamento dos vários `TableAdapter.Update` métodos:  
  
|Método|Descrição|  
|------------|-----------------|  
|`TableAdapter.Update(DataTable)`|Tenta salvar todas as alterações no <xref:System.Data.DataTable> no banco de dados. (Isso inclui remover quaisquer linhas excluídas da tabela, adicionar linhas inseridas na tabela e atualizar quaisquer linhas na tabela que foram alteradas.)|  
|`TableAdapter.Update(DataSet)`|Embora o parâmetro aceita um conjunto de dados, o TableAdapter tenta salvar todas as alterações no TableAdapter associado do <xref:System.Data.DataTable> no banco de dados. (Isso inclui remover quaisquer linhas excluídas da tabela, adicionar linhas inseridas na tabela e atualizar quaisquer linhas na tabela que foram alteradas.) **Observação:** associada de um TableAdapter <xref:System.Data.DataTable> é o <xref:System.Data.DataTable> criada quando o TableAdapter foi originalmente configurado.|  
|`TableAdapter.Update(DataRow)`|Tenta salvar as alterações no indicado <xref:System.Data.DataRow> ao banco de dados.|  
|`TableAdapter.Update(DataRows())`|Tenta salvar as alterações em qualquer linha na matriz de <xref:System.Data.DataRow>s para o banco de dados.|  
|`TableAdapter.Update("new column values", "original column values")`|Tenta salvar as alterações em uma única linha que é identificada pelos valores da coluna original.|  
  
 Normalmente, você usa o `TableAdapter.Update` método que usa um <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, ou <xref:System.Data.DataRow>(s) quando seu aplicativo usa conjuntos de dados exclusivamente para armazenar dados.  
  
 Normalmente, você usa o `TableAdapter.Update` método que usa valores de coluna quando o aplicativo usa objetos para armazenar dados.  
  
 Se seu TableAdapter não tem um `Update` método que usa valores de coluna, em seguida, ele significa que o ou o TableAdapter está configurado para usar procedimentos armazenados ou seus `GenerateDBDirectMethods` estiver definida como `false`. Tente definir o TableAdapter `GenerateDBDirectMethods` propriedade para `true` de dentro de [Dataset Designer](../data-tools/creating-and-editing-typed-datasets.md) e, em seguida, salve o conjunto de dados para regenerar o TableAdapter. Se o TableAdapter ainda não tiver um `Update` método que usa valores de coluna e, em seguida, a tabela provavelmente não fornece informações de esquema suficientes para distinguir entre linhas individuais (por exemplo, nenhuma chave primária é definida na tabela).  
  
## <a name="update-existing-records-using-tableadapters"></a>Atualizar registros existentes usando TableAdapters  
 TableAdapters fornecem maneiras diferentes para atualizar registros em um banco de dados, dependendo dos requisitos do seu aplicativo.  
  
 Se seu aplicativo usa conjuntos de dados para armazenar dados, você poderá simplesmente atualizar os registros no desejado <xref:System.Data.DataTable> e, em seguida, chamar o `TableAdapter.Update` método e passar a <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, <xref:System.Data.DataRow>, ou uma matriz de <xref:System.Data.DataRow>s. A tabela acima descreve os diferentes `Update` métodos.  
  
#### <a name="to-update-records-in-a-database-with-the-tableadapterupdate-method-that-takes-dataset-datatable-datarow-or-datarows"></a>Para atualizar registros em um banco de dados com o método do TableAdapter que usa o DataSet, DataTable, DataRow ou DataRows)  
  
1. Editar registros em desejado <xref:System.Data.DataTable> editando diretamente o <xref:System.Data.DataRow> no <xref:System.Data.DataTable>. Para obter mais informações, consulte [como: editar as linhas em uma DataTable](http://msdn.microsoft.com/library/d5eea200-9bfa-4956-bf7c-08dd6fb6663c).  
  
2. Depois que as linhas são editadas na <xref:System.Data.DataTable>, chame o `TableAdapter.Update` método. Você pode controlar a quantidade de dados para atualizar, passando um inteiro <xref:System.Data.DataSet>, um <xref:System.Data.DataTable>, uma matriz de <xref:System.Data.DataRow>s ou um único <xref:System.Data.DataRow>.  
  
    O código a seguir mostra como editar um registro em uma <xref:System.Data.DataTable> e, em seguida, chamar o `TableAdapter.Update` método para salvar as alterações no banco de dados. (Este exemplo usa a tabela de região do banco de dados Northwind.)  
  
    [!code-csharp[VbRaddataSaving#17](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs#17)]
    [!code-vb[VbRaddataSaving#17](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb#17)]  
  
   Se seu aplicativo usa objetos para armazenar os dados em seu aplicativo, você pode usar o TableAdapter `DBDirect` métodos para enviar dados de seus objetos diretamente para o banco de dados. Esses métodos permitem que você passe valores individuais para cada coluna como parâmetros de método. Chamar esse método atualiza um registro existente no banco de dados com os valores de coluna passados para o método.  
  
   O procedimento a seguir usa o Northwind `Region` tabela como um exemplo.  
  
#### <a name="to-update-records-in-a-database-using-the-tableadapterupdate-method-that-takes-column-values"></a>Para atualizar registros em um banco de dados usando o método do TableAdapter que recebe valores de coluna  
  
-   Chame o TableAdapter `Update` método, passando os valores novos e originais para cada coluna como parâmetros.  
  
    > [!NOTE]
    >  Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.  
  
     [!code-csharp[VbRaddataSaving#18](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#18)]
     [!code-vb[VbRaddataSaving#18](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#18)]  
  
## <a name="update-records-using-command-objects"></a>Atualizar registros usando objetos de comando  
 O exemplo a seguir atualiza os registros existentes diretamente em um banco de dados usando objetos de comando. Para obter mais informações sobre como usar objetos de comando para executar comandos e procedimentos armazenados, consulte [buscando dados em seu aplicativo](../data-tools/fetching-data-into-your-application.md).  
  
 O procedimento a seguir usa o Northwind `Region` tabela como um exemplo.  
  
#### <a name="to-update-existing-records-in-a-database-using-command-objects"></a>Para atualizar registros existentes em um banco de dados usando objetos de comando  
  
-   Criar um novo objeto de comando; Defina suas `Connection`, `CommandType`, e `CommandText` propriedades; e, em seguida, abra uma conexão e execute o comando.  
  
     [!code-csharp[VbRaddataSaving#19](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#19)]
     [!code-vb[VbRaddataSaving#19](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#19)]  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Você deve ter acesso ao banco de dados que você está tentando se conectar ao, bem como permissão para atualizar registros na tabela desejada.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Como: excluir registros em um banco de dados](../data-tools/how-to-delete-records-in-a-database.md)   
 [Inserir novos registros em um banco de dados](../data-tools/insert-new-records-into-a-database.md)   
 [Salvar dados de um objeto em um banco de dados](../data-tools/save-data-from-an-object-to-a-database.md)   
 [Visão geral de aplicativos de dados no Visual Studio](../data-tools/overview-of-data-applications-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)