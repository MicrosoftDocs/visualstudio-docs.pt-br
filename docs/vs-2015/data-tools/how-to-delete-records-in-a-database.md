---
title: 'Como: excluir registros em um banco de dados | Microsoft Docs'
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
- data [Visual Studio], saving
- records, deleting
- TableAdapter.Delete method
- databases, deleting records
- deleting data
- TableAdapter.Update method
- saving data
ms.assetid: d74d2130-9732-4648-abea-241059c4a372
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 87ab5ccde2c1100fbd0efc5f4272efe27803b717
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49938611"
---
# <a name="how-to-delete-records-in-a-database"></a>Como excluir registros em um banco de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para excluir registros de um banco de dados, use o `TableAdapter.Update` método ou o `TableAdapter.Delete` método. Ou, se seu aplicativo não usar TableAdapters, você pode usar objetos de comando para excluir registros de um banco de dados (por exemplo, <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>).  
  
 O `TableAdapter.Update` método normalmente é usado quando o aplicativo usa conjuntos de dados para armazenar dados, enquanto o `TableAdapter.Delete` método normalmente é usado quando seu aplicativo usa objetos para armazenar dados.  
  
 Se seu TableAdapter não tem um `Delete` método, ele significa ou o TableAdapter está configurado para usar procedimentos armazenados, ou seus `GenerateDBDirectMethods` estiver definida como `false`. Tente definir o TableAdapter `GenerateDBDirectMethods` propriedade para `true` de dentro de [Dataset Designer](../data-tools/creating-and-editing-typed-datasets.md) e, em seguida, salve o conjunto de dados para regenerar o TableAdapter. Se o TableAdapter ainda não tiver um `Delete` método e, em seguida, a tabela provavelmente não fornece informações de esquema suficientes para distinguir entre linhas individuais (por exemplo, nenhuma chave primária é definida na tabela).  
  
## <a name="delete-records-using-tableadapters"></a>Excluir registros usando TableAdapters  
 TableAdapters fornecem maneiras diferentes para excluir registros de um banco de dados, dependendo dos requisitos do seu aplicativo.  
  
 Se seu aplicativo usa conjuntos de dados para armazenar dados você pode simplesmente excluir registros de desejado <xref:System.Data.DataTable> no <xref:System.Data.DataSet>e, em seguida, chamar o `TableAdapter.Update` método. O `TableAdapter.Update` método obtém as alterações na tabela de dados e envia essas alterações para o banco de dados (incluindo registros inseridos, atualizados e excluídos).  
  
#### <a name="to-delete-records-from-a-database-using-the-tableadapterupdate-method"></a>Para excluir registros de um banco de dados usando o método do TableAdapter.  
  
- Excluir registros de desejado <xref:System.Data.DataTable> excluindo <xref:System.Data.DataRow> objetos da tabela. Para obter mais informações, consulte [como: excluir linhas em uma DataTable](http://msdn.microsoft.com/library/add481e5-08c7-4923-9276-f036ae29d31e). Após as linhas são excluídas do <xref:System.Data.DataTable>, chame o `TableAdapter.Update` método. Você pode controlar a quantidade de dados para atualizar, passando em um todo <xref:System.Data.DataSet>, um <xref:System.Data.DataTable>, uma matriz de <xref:System.Data.DataRow>s ou um único <xref:System.Data.DataRow>. O código a seguir mostra como excluir um registro de um <xref:System.Data.DataTable> e, em seguida, chamar o `TableAdapter.Update` método para comunicar as alterações e excluir a linha do banco de dados. (Este exemplo usa o banco de dados de Northwind `Region` tabela.)  
  
   [!code-csharp[VbRaddataSaving#20](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs#20)]
   [!code-vb[VbRaddataSaving#20](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb#20)]  
  
  Se seu aplicativo usa objetos para armazenar os dados em seu aplicativo, você pode usar os métodos DBDirect do TableAdapter para excluir dados diretamente do banco de dados. Chamar o `Delete` método remove registros do banco de dados com base nos valores de parâmetro passados.  
  
#### <a name="to-delete-records-from-a-database-using-the-tableadapterdelete-method"></a>Para excluir registros de um banco de dados usando o método TableAdapter.  
  
-   Chame o TableAdapter `Delete` método, passando os valores para cada coluna como parâmetros do `Delete` método. (Este exemplo usa o banco de dados de Northwind `Region` tabela.)  
  
    > [!NOTE]
    >  Se você não tiver uma instância disponível, crie uma instância do TableAdapter que você deseja usar.  
  
     [!code-csharp[VbRaddataSaving#21](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#21)]
     [!code-vb[VbRaddataSaving#21](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#21)]  
  
## <a name="delete-records-using-command-objects"></a>Excluir registros usando objetos de comando  
 O exemplo a seguir exclui registros diretamente de um banco de dados usando objetos de comando. Para obter mais informações sobre como usar objetos de comando para executar comandos e procedimentos armazenados, consulte [buscando dados em seu aplicativo](../data-tools/fetching-data-into-your-application.md).  
  
#### <a name="to-delete-records-from-a-database-using-command-objects"></a>Para excluir registros de um banco de dados usando objetos de comando  
  
-   Criar um novo objeto de comando, defina suas `Connection`, `CommandType`, e `CommandText` propriedades. (Este exemplo usa o banco de dados de Northwind `Region` tabela.)  
  
     [!code-csharp[VbRaddataSaving#22](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#22)]
     [!code-vb[VbRaddataSaving#22](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#22)]  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Você deve ter acesso ao banco de dados que você está tentando se conectar ao, bem como permissão para excluir registros da tabela desejada.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Inserir novos registros em um banco de dados](../data-tools/insert-new-records-into-a-database.md)   
 [Como: atualizar registros em um banco de dados](../data-tools/how-to-update-records-in-a-database.md)   
 [Salvar dados de um objeto em um banco de dados](../data-tools/save-data-from-an-object-to-a-database.md)   
 [Visão geral de aplicativos de dados no Visual Studio](../data-tools/overview-of-data-applications-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)