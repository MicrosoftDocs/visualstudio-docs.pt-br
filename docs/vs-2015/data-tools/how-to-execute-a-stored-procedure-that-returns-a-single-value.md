---
title: 'Como: executar um procedimento armazenado que retorna um único valor | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CommandType.StoredProcedure
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- ExecuteReader method example [Visual Basic]
- stored procedures, examples
- stored procedures, executing
ms.assetid: ecf8c262-58ca-4a69-a82c-916c0c061422
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 2c27c8e0fca1393e097f1244a01988052911f73a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49281002"
---
# <a name="how-to-execute-a-stored-procedure-that-returns-a-single-value"></a>Como executar um procedimento armazenado que retorna um único valor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para executar um procedimento armazenado que retorna um único valor, você pode executar a consulta do TableAdapter que está configurada para executar um procedimento armazenado (por exemplo, `CustomersTableAdapter.CustomerCount()`).  
  
 Se seu aplicativo não usar TableAdapters, chame o `ExecuteScalar` método em um objeto de comando, definindo seu `CommandType` propriedade <xref:System.Data.CommandType>. ("Objeto de comando" refere-se ao comando específico para o [.NET Framework Data Provider](http://msdn.microsoft.com/library/03a9fc62-2d24-491a-9fe6-d6bdb6dcb131) seu aplicativo está usando. Por exemplo, se seu aplicativo estiver usando o .NET Framework Data Provider para SQL Server, o objeto de comando seria <xref:System.Data.SqlClient.SqlCommand>.)  
  
 Os exemplos a seguir mostram como executar procedimentos armazenados que retornam valores únicos de um banco de dados usando o TableAdapters ou objetos de comando. Para obter mais informações sobre como consultar com TableAdapters e comandos, consulte [preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md).  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="executing-stored-procedures-that-return-single-values-using-a-tableadapter"></a>Executar procedimentos armazenados que retornam valores únicos usando um TableAdapter  
 Este exemplo mostra como criar uma consulta TableAdapter usando o [editando TableAdapters](../data-tools/editing-tableadapters.md), e, em seguida, ele fornece informações sobre como declarar uma instância do TableAdapter e executar a consulta.  
  
#### <a name="to-execute-a-stored-procedure-that-returns-a-single-value-using-a-tableadapter"></a>Para executar um procedimento armazenado que retorna um único valor usando um TableAdapter  
  
1.  Abrir em um conjunto de dados do **Dataset Designer**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Se você não tiver uma, crie um TableAdapter. Para obter mais informações sobre como criar TableAdapters, consulte [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).  
  
3.  Se você já tiver uma consulta no seu TableAdapter que usa um procedimento armazenado para retornar um único valor, vá para o próximo procedimento, "para"declarar uma instância do TableAdapter e executar a consulta. Caso contrário, continue com a etapa 4 para criar uma nova consulta que retorna um valor único.  
  
4.  Clique com botão direito do TableAdapter que você deseja e use o menu de atalho para adicionar uma consulta.  
  
     O **Assistente de configuração de consulta do TableAdapter** é aberta.  
  
5.  Selecione **usar o procedimento armazenado existente**e, em seguida, clique em **próxima**.  
  
6.  Selecione um procedimento armazenado na lista suspensa e, em seguida, clique em **próxima**.  
  
7.  Selecione a opção para retornar **um único valor**e, em seguida, clique em **próxima**.  
  
8.  Forneça um nome para a consulta.  
  
9. Clique em **próxima** ou **concluir** para concluir o assistente; a consulta é adicionada ao TableAdapter.  
  
10. Criar o projeto.  
  
#### <a name="to-declare-an-instance-of-the-tableadapter-and-execute-the-query"></a>Para declarar uma instância do TableAdapter e executar a consulta  
  
1.  Declare uma instância do TableAdapter que contém a consulta que você deseja executar.  
  
    -   Para criar uma instância usando as ferramentas de tempo de design, arraste o TableAdapter que você deseja do **caixa de ferramentas**. (Os componentes no seu projeto agora aparecem na **caixa de ferramentas** sob um título que corresponda ao nome do projeto.) Se o TableAdapter não aparecer na **caixa de ferramentas**, talvez seja necessário compilar seu projeto.  
  
         -ou-  
  
    -   Para criar uma instância no código, substitua o código a seguir com os nomes dos seus <xref:System.Data.DataSet> e TableAdapter.  
  
         `Dim tableAdapter As New DataSetTableAdapters.TableAdapter`  
  
        > [!NOTE]
        >  TableAdapters não são realmente estão localizadas dentro de suas classes de conjunto de dados associado. Cada conjunto de dados tem uma coleção correspondente de TableAdapters em seu próprio namespace. Por exemplo, se você tiver um conjunto de dados denominado `SalesDataSet`, deve haver um `SalesDataSetTableAdapters` namespace que contém seus TableAdapters.  
  
2.  Chame sua consulta, como você poderia chamar qualquer outro método no código. Sua consulta é um método no TableAdapter. Substitua o código a seguir com os nomes de seu TableAdapter e a consulta. Você também precisará passar os parâmetros necessários para sua consulta. Se você não tiver certeza se sua consulta exigir parâmetros, ou que parâmetros requer, em seguida, verifique o IntelliSense para a assinatura necessária da consulta. Dependendo se sua consulta usa parâmetros ou não, o código seria semelhante a um dos exemplos a seguir:  
  
     `TableAdapter.Query()`  
  
     `TableAdapter.Query(Parameters)`  
  
     O código completo para declarar uma instância do TableAdapter e executar a consulta deve ser semelhante ao seguinte:  
  
     [!code-csharp[VbRaddataFillingAndExecuting#9](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form2.cs#9)]
     [!code-vb[VbRaddataFillingAndExecuting#9](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form2.vb#9)]  
  
## <a name="executing-stored-procedures-that-return-single-values-using-a-command-object"></a>Executar procedimentos armazenados que retornam valores únicos usando um objeto de comando  
 O exemplo a seguir mostra como criar um comando e executar um procedimento armazenado que retorna um valor único. Para obter informações sobre como definir e obter valores de parâmetro para um comando, consulte [como: definir e obter parâmetros para objetos de comando](http://msdn.microsoft.com/library/10110ecc-d2ed-4796-bb8f-74f2ecd40787).  
  
 Este exemplo usa o <xref:System.Data.SqlClient.SqlCommand> do objeto e requer:  
  
-   Referências para o <xref:System>, <xref:System.Data>, e <xref:System.Xml> namespaces.  
  
-   Uma conexão de dados denominado `SqlConnection1`.  
  
-   Uma tabela denominada `Customers` na fonte de dados que `SqlConnection1` se conecta ao. (Caso contrário, você precisa de uma instrução SQL válida para sua fonte de dados).  
  
#### <a name="to-execute-a-stored-procedure-that-returns-a-single-value-using-a-datacommand"></a>Para executar um procedimento armazenado que retorna um único valor usando um DataCommand  
  
-   Adicione o seguinte código para um método que você deseja executar o código. Retornar valores únicos chamando o `ExecuteScalar` método de um comando (por exemplo, <xref:System.Data.SqlClient.SqlCommand.ExecuteScalar%2A>). Os dados são retornados em um `object`.  
  
     [!code-csharp[VbRaddataFillingAndExecuting#14](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form2.cs#14)]
     [!code-vb[VbRaddataFillingAndExecuting#14](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form2.vb#14)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Data.SqlClient.SqlCommand.ExecuteScalar%2A?displayProperty=fullName>   
 <xref:System.Data.OleDb.OleDbCommand.ExecuteScalar%2A?displayProperty=fullName>   
 <xref:System.Data.Odbc.OdbcCommand.ExecuteScalar%2A?displayProperty=fullName>   
 <xref:System.Data.OracleClient.OracleCommand.ExecuteScalar%2A?displayProperty=fullName>   
 [Como: criar consultas TableAdapter](../data-tools/how-to-create-tableadapter-queries.md)   
 [Como: editar consultas TableAdapter](../data-tools/how-to-edit-tableadapter-queries.md)   
 [Como: preencher um conjunto de dados com dados](../data-tools/how-to-fill-a-dataset-with-data.md)   
 [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)   
 [Como: definir e obter parâmetros para objetos de comando](http://msdn.microsoft.com/library/10110ecc-d2ed-4796-bb8f-74f2ecd40787)