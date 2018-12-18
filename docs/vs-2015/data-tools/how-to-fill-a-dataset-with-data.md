---
title: 'Como: preencher um conjunto de dados com dados | Microsoft Docs'
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
- TableAdapter.GetData
- TableAdapter.Fill
- datasets [Visual Basic], filling
- DataTable objects, loading
- data [Visual Basic], loading into datasets
ms.assetid: 7ab436d4-54ba-4621-902f-3f193279e18c
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: f36aa2dac656f6fd27b656d0ddfb58a758eb6487
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49295991"
---
# <a name="how-to-fill-a-dataset-with-data"></a>Como: preencher um conjunto de dados com dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A frase "preenchendo um dataset com dados" se refere a carregar dados para o indivíduo <xref:System.Data.DataTable> objetos que compõem o conjunto de dados. Você preenche as tabelas de dados, executando consultas TableAdapter ou executando o adaptador de dados (por exemplo, <xref:System.Data.SqlClient.SqlDataAdapter>) comandos.  
  
 Se você deve usar TableAdapters ou adaptadores de dados depende de como você criou o conjunto de dados. Se você tiver usado as ferramentas de design no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], como o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f), seu conjunto de dados contém TableAdapters. Para obter mais informações sobre TableAdapters, consulte [visão geral de TableAdapter](../data-tools/tableadapter-overview.md). Se você tiver criado seu conjunto de dados por meio de programação, geralmente você precisará criar adaptadores de dados para carregar dados nas tabelas de dados.  
  
> [!NOTE]
>  Ao arrastar itens dos [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) para um formulário, o código para preencher a tabela de dados com dados é adicionado automaticamente para o `Form_Load` manipulador de eventos. Abra o formulário no editor de código para ver a sintaxe exata para preencher as tabelas específicas. Se você não deseja preencher a tabela quando o formulário é carregado, você pode mover esse código para algum outro método ou remova-o inteiramente.  
  
## <a name="filling-a-dataset-using-a-tableadapter"></a>Preenchendo um Dataset usando um TableAdapter  
 Você pode chamar uma consulta no TableAdapter para carregar dados em tabelas de dados em um conjunto de dados. Passar o <xref:System.Data.DataTable> você deseja preencher para a consulta do TableAdapter. Se sua consulta usa parâmetros, passe-os para o método também. Se o conjunto de dados contiver várias tabelas, você deve ter TableAdapters separados para cada tabela e, portanto, deve preencher cada tabela separadamente.  
  
> [!NOTE]
>  Por padrão, toda vez que executar uma consulta do TableAdapter, os dados na tabela são desmarcados antes dos resultados da consulta que está sendo carregada na tabela. Você pode manter os dados existentes na tabela e acrescentar os resultados, definindo o TableAdapter `ClearBeforeFill` propriedade para `false`.  
  
#### <a name="to-fill-a-dataset-with-data-using-a-tableadapter"></a>Para preencher um conjunto de dados com dados usando um TableAdapter  
  
1.  Abra seu formulário ou componente na **Editor de códigos**.  
  
2.  Adicione o código em qualquer lugar em seu aplicativo em que você precisa carregar uma tabela de dados com dados. Se sua consulta não aceita parâmetros, passe o <xref:System.Data.DataTable> você deseja preencher. O código deve ser semelhante ao seguinte:  
  
     [!code-csharp[VbRaddataFillingAndExecuting#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form2.cs#4)]
     [!code-vb[VbRaddataFillingAndExecuting#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form2.vb#4)]  
  
3.  Se sua consulta usa parâmetros, passe o <xref:System.Data.DataTable> você deseja preencher e os parâmetros esperados pela consulta. Dependendo dos parâmetros reais em sua consulta, o código seria semelhante aos exemplos a seguir:  
  
     [!code-csharp[VbRaddataFillingAndExecuting#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form2.cs#5)]
     [!code-vb[VbRaddataFillingAndExecuting#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form2.vb#5)]  
  
## <a name="filling-a-dataset-using-a-dataadapter"></a>Preenchendo um Dataset usando um DataAdapter  
 Você chama o adaptador de dados `Fill` método. Isso faz com que o adaptador executar a instrução SQL ou procedimento armazenado referenciado em seu `SelectCommand` propriedade e coloca os resultados em uma tabela no conjunto de dados. Se o conjunto de dados contiver várias tabelas, você deve ter adaptadores de dados separado para cada tabela e, portanto, deve preencher cada tabela separadamente.  
  
#### <a name="to-fill-a-dataset-with-data-using-a-dataadapter"></a>Para preencher um conjunto de dados com dados usando um DataAdapter  
  
-   Chame o <xref:System.Data.Common.DataAdapter.Fill%2A> método da <xref:System.Data.Common.DataAdapter>, passando o <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> para carregar os dados. Por exemplo:  
  
     [!code-csharp[VbRaddataFillingAndExecuting#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form2.cs#6)]
     [!code-vb[VbRaddataFillingAndExecuting#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form2.vb#6)]  
  
     Geralmente, você deve fornecer o nome da <xref:System.Data.DataTable> para carregar os dados. Se você passar o nome de um <xref:System.Data.DataSet> em vez de uma tabela de dados específico, um <xref:System.Data.DataTable> denominado `Table1` é adicionado ao conjunto de dados e carregada com os resultados do banco de dados (em vez de carregar os dados em um existente <xref:System.Data.DataTable> no conjunto de dados). Para obter mais informações, consulte [populando um DataSet a partir de um DataAdapter](http://msdn.microsoft.com/library/3fa0ac7d-e266-4954-bfac-3fbe2f913153).  
  
## <a name="see-also"></a>Consulte também  
 [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)