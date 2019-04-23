---
title: Atualizar dados usando um TableAdapter | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 585dfa357082fbb46794ab5f6dcc7b0e141fc9b7
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59653743"
---
# <a name="update-data-by-using-a-tableadapter"></a>Atualizar dados usando um TableAdapter
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depois que os dados no conjunto de dados foi modificados e validados, você pode enviar os dados atualizados para uma chamada de databaseby o `Update` método de um TableAdapter. O `Update` método atualiza uma única tabela de dados e executa o comando correto (INSERT, UPDATE ou DELETE) com base no <xref:System.Data.DataRow.RowState%2A> de cada linha de dados na tabela. Quando um conjunto de dados tiver tabelas relacionadas, o Visual Studio gera uma classe de TableAdapterManager que você usa para fazer as atualizações. A classe TableAdapterManager garante que as atualizações são feitas na ordem correta com base nas restrições de chave estrangeira são definidas no banco de dados. Quando você usa controles ligados a dados, a arquitetura de vinculação de dados cria uma variável de membro da classe TableAdapterManager chamada tableAdapterManager. Para obter mais informações, consulte [visão geral de atualização hierárquica](http://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6).  
  
> [!NOTE]
>  Quando você tenta atualizar uma fonte de dados com o conteúdo de um conjunto de dados, você poderá obter erros. Para evitar erros, recomendamos autilização coloque o código que chama o adaptador `Update` método dentro de uma `try` / `catch` bloco.  
  
 O procedimento exato para atualizar uma fonte de dados pode variar, dependendo das necessidades de negócios, mas inclui as seguintes etapas:  
  
1.  Chame o adaptador `Update` método em um `try` / `catch` bloco.  
  
2.  Se uma exceção é detectada, localize a linha de dados que causou o erro. Para obter mais informações, confira [Como: Localizar linhas que têm erros](http://msdn.microsoft.com/library/1fa907c5-fe66-4f29-a253-2b97b900050c).  
  
3.  Reconciliar o problema nos dados de linha (por meio de programação, se possível, ou apresentando a linha inválida para o usuário para modificação) e, em seguida, tente atualizar novamente (<xref:System.Data.DataRow.HasErrors%2A>, <xref:System.Data.DataTable.GetErrors%2A>).  
  
## <a name="savedata-to-a-database"></a>SaveData para um banco de dados  
 Chamar o `Update` método de um TableAdapter. Passe o nome da tabela de dados que contém os valores a serem gravados no banco de dados.  
  
#### <a name="to-update-a-database-by-using-a-tableadapter"></a>Para atualizar um banco de dados usando um TableAdapter  
  
-   Coloque o TableAdapter`Update` método em um `try` / `catch` bloco. O exemplo a seguir mostra como atualizar o conteúdo a `Customers` na tabela `NorthwindDataSet` de dentro um `try` / `catch` bloco.  
  
     [!code-csharp[VbRaddataSaving#9](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#9)]
     [!code-vb[VbRaddataSaving#9](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#9)]  
  
## <a name="see-also"></a>Consulte também  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
