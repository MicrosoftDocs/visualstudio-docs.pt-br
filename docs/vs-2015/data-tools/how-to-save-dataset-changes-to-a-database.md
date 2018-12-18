---
title: 'Como: salvar as alterações do conjunto de dados em um banco de dados | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- DbDataAdapter.Update
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], saving
- databases, updating
- updating datasets, writing changes to data source
ms.assetid: c9970150-b71b-4c9d-a355-5efb6b510dca
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 60bb855202cfb333820fe2292fedc0b31608c5c6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949013"
---
# <a name="how-to-save-dataset-changes-to-a-database"></a>Como salvar as alterações no conjunto de dados em um banco de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depois que os dados no conjunto de dados foi modificados e validados, você provavelmente desejará enviar os dados atualizados para um banco de dados. Para enviar os dados modificados para um banco de dados, você chama o `Update` método de um [TableAdapter](../data-tools/tableadapter-overview.md) ou adaptador de dados. O adaptador `Update` método atualiza uma única tabela de dados e executa o comando correto (INSERT, UPDATE ou DELETE) com base no <xref:System.Data.DataRow.RowState%2A> de cada linha de dados na tabela.  
  
 Ao salvar dados em tabelas relacionadas, o Visual Studio fornece um componente do TableAdapterManager que auxilia a salva na ordem correta com base nas restrições de chave estrangeira definidas no banco de dados. Para obter mais informações, consulte [visão geral de atualização hierárquica](http://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6).  
  
> [!NOTE]
>  Como a tentativa de atualizar uma fonte de dados com o conteúdo de um conjunto de dados pode resultar em erros, você deve colocar o código que chama o adaptador `Update` método dentro de uma `try` / `catch` bloco.  
  
 O procedimento exato para atualizar uma fonte de dados pode variar dependendo de suas necessidades de negócios, mas seu aplicativo deve incluir as seguintes etapas:  
  
1.  Executar o código que tenta enviar atualizações para o banco de dados dentro de um `try` / `catch` bloco.  
  
2.  Se uma exceção é detectada, localize a linha de dados que causou o erro. Para obter mais informações, consulte [como: localizar linhas que têm os erros](http://msdn.microsoft.com/library/1fa907c5-fe66-4f29-a253-2b97b900050c).  
  
3.  Reconciliar o problema nos dados de linha (por meio de programação, se possível, ou apresentando a linha inválida para o usuário para modificação) e, em seguida, tente novamente a atualização (<xref:System.Data.DataRow.HasErrors%2A> propriedade, <xref:System.Data.DataTable.GetErrors%2A> método).  
  
## <a name="saving-data-to-a-database"></a>Salvando dados em um banco de dados  
 Chamar o `Update` método de um TableAdapter ou adaptador de dados, passando o nome da tabela de dados que contém os valores a serem gravados no banco de dados. Para obter mais informações sobre como salvar dados de uma única tabela de dados para um banco de dados, consulte [instruções passo a passo: salvando dados para um banco de dados (tabela única)](http://msdn.microsoft.com/library/68befa96-7463-43e8-abcf-dc2f42ccd53d).  
  
#### <a name="to-update-a-database-with-a-dataset-using-a-tableadapter"></a>Para atualizar um banco de dados com um conjunto de dados usando um TableAdapter  
  
-   Coloque o `TableAdapter.Update` método dentro de uma `try` / `catch` bloco. O exemplo a seguir mostra como tentar uma atualização com o conteúdo do `Customers` na tabela a `NorthwindDataSet`.  
  
     [!code-csharp[VbRaddataSaving#9](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#9)]
     [!code-vb[VbRaddataSaving#9](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#9)]  
  
#### <a name="to-update-a-database-with-a-dataset-using-a-data-adapter"></a>Para atualizar um banco de dados com um conjunto de dados usando um adaptador de dados  
  
-   Coloque o `DataAdapter.Update` método dentro de uma `try` / `catch` bloco. O exemplo a seguir mostra como tentar uma atualização para uma fonte de dados com o conteúdo do `Table1` em `DataSet1`.  
  
     [!code-csharp[VbRaddataSaving#26](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#26)]
     [!code-vb[VbRaddataSaving#26](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#26)]  
  
## <a name="updating-two-related-tables-in-a-dataset"></a>Atualizando duas tabelas relacionadas em um conjunto de dados  
 Ao atualizar as tabelas relacionadas em um conjunto de dados, é importante atualizar na sequência apropriada para reduzir a chance de violar as restrições de integridade referencial. A ordem de execução do comando também seguirá os índices do <xref:System.Data.DataRowCollection> no conjunto de dados. Para evitar que erros de integridade de dados que está sendo gerado, a prática recomendada é atualizar o banco de dados na sequência a seguir:  
  
1. Tabela filho: excluir registros.  
  
2. Tabela pai: Inserir, atualizar e excluir registros.  
  
3. Tabela filho: inserir e atualizar registros.  
  
   Para obter informações detalhadas sobre como salvar dados de várias tabelas, consulte [salvar dados em um banco de dados (várias tabelas)](../data-tools/save-data-to-a-database-multiple-tables.md).  
  
   Se você estiver atualizando dois ou mais tabelas relacionadas, você deve incluir toda a lógica de atualização dentro de uma transação. Uma transação é um processo que garante que todas as alterações a um banco de dados são bem-sucedidas antes de aplicar qualquer alteração. Para obter mais informações, consulte [transações e simultaneidade](http://msdn.microsoft.com/library/f46570de-9e50-4fe6-8710-a8c31fa8569b).  
  
#### <a name="to-update-two-related-tables-using-a-tableadapter"></a>Para atualizar duas tabelas relacionadas usando um TableAdapter  
  
1.  Criar três temporário <xref:System.Data.DataTable>s para armazenar os registros distintos.  
  
2.  Chame o `Update` método para cada subconjunto de linhas de dentro um `try` / `catch` bloco. Se ocorrerem erros de atualização, o curso de ação sugerido é ramificar e resolvê-los.  
  
3.  Confirme as alterações do conjunto de dados para o banco de dados.  
  
4.  Descarte as tabelas de dados temporários para liberar os recursos.  
  
     [!code-csharp[VbRaddataSaving#27](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#27)]
     [!code-vb[VbRaddataSaving#27](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#27)]  
  
#### <a name="to-update-two-related-tables-using-a-data-adapter"></a>Para atualizar duas tabelas relacionadas usando um adaptador de dados  
  
-   Chamar o `Update` método de cada adaptador de dados.  
  
     O exemplo a seguir mostra como atualizar uma fonte de dados com um conjunto de dados contiver tabelas relacionadas. Para seguir a sequência acima, três temporário <xref:System.Data.DataTable>s será criada para armazenar os registros distintos. Em seguida, a `Update` método será chamado para cada subconjunto de linhas de dentro um `try` / `catch` bloco. Se ocorrerem erros de atualização, o curso de ação sugerido é ramificar e resolvê-los. Em seguida, o conjunto de dados confirma as alterações. Finalmente, descarte as tabelas de dados temporários para liberar os recursos.  
  
     [!code-csharp[VbRaddataSaving#28](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#28)]
     [!code-vb[VbRaddataSaving#28](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#28)]  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)