---
title: 'Como: criar consultas TableAdapter | Microsoft Docs'
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
- TableAdapters, creating queries
- queries [Visual Studio], creating
- data [Visual Studio], TableAdapter queries
- queries [Visual Studio], TableAdapters
ms.assetid: df0cf4a5-e9cc-4de6-8b94-ce74fb7b2452
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: c4b800bcb70e41e1d80bf9a0a37d72f08f78c7a6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49195540"
---
# <a name="how-to-create-tableadapter-queries"></a>Como criar consultas TableAdapter
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Consultas TableAdapter são instruções SQL ou procedimentos armazenados que seu aplicativo pode ser executada em um banco de dados.  
  
 Adicione tantas consultas a um TableAdapter requer que seu aplicativo. Consultas TableAdapter aparecem como métodos em um TableAdapter. Quando você cria uma consulta chamada `FillByCity` que leva um parâmetro que representa o valor de cidade, a consulta é adicionada ao TableAdapter. Ele é adicionado como um método tipado que tem o tipo correto do parâmetro como um argumento — nesse caso, uma cadeia de caracteres que representa o valor de cidade. Você pode chamar a consulta do TableAdapter como qualquer método em qualquer objeto. Por exemplo, o código a seguir executa o `FillByCity` preenchimentos e consulta o `Customers` tabela com todos os clientes com um valor de cidade de `Seattle`:  
  
 [!code-csharp[VbRaddataTableAdapters#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Form1.cs#1)]
 [!code-vb[VbRaddataTableAdapters#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Form1.vb#1)]  
  
 Consultas TableAdapter podem preencher uma tabela de dados (`Fill` e `FillBy` consultas) ou retornar novas tabelas de dados preenchidas com os dados retornados pela consulta (`GetData` e `GetDataBy` consultas).  
  
 Você pode adicionar consultas a TableAdapters existentes executando o [editando TableAdapters](../data-tools/editing-tableadapters.md). (Qualquer TableAdapter com o botão direito e escolha **Add Query**.)  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="create-a-query-in-the-dataset-designer"></a>Criar uma consulta no Designer de conjunto de dados  
  
#### <a name="to-add-a-query-to-a-tableadapter-in-the-dataset-designer"></a>Para adicionar uma consulta a um TableAdapter no Designer de conjunto de dados  
  
1.  Abrir em um conjunto de dados do **Dataset Designer**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Clique com botão direito no TableAdapter desejado e selecione **Add Query**.  
  
     -ou-  
  
3.  Arraste uma **consulta** da **conjunto de dados** guia da **caixa de ferramentas** em uma tabela no designer.  
  
     O **Assistente de configuração de consulta do TableAdapter** é aberta.  
  
4.  Conclua o Assistente; a consulta é adicionada ao TableAdapter.  
  
## <a name="create-a-query-directly-on-a-form-in-your-windows-application"></a>Criar uma consulta diretamente em um formulário em seu aplicativo do Windows  
 Se você tiver uma instância de um TableAdapter em seu formulário você pode adicionar uma consulta usando o [caixa de diálogo do construtor de critérios de pesquisa](http://msdn.microsoft.com/library/0b306b92-f35e-45ef-a4be-3f653cd00c3d), que adiciona um <xref:System.Windows.Forms.ToolStrip> controle ao formulário que aceita qualquer entrada de parâmetros necessários para a consulta, bem como um botão para executar a consulta.  
  
#### <a name="to-add-a-query-to-a-tableadapter-using-the-search-criteria-dialog-box"></a>Para adicionar uma consulta a um TableAdapter usando a caixa de diálogo critérios de pesquisa  
  
1.  Selecione um TableAdapter na bandeja de componentes.  
  
2.  Clique em marca inteligente do TableAdapter e escolha **Add Query**.  
  
3.  Preencha a caixa de diálogo e a consulta é adicionada ao TableAdapter. Para obter mais informações, consulte [caixa de diálogo do construtor de critérios de pesquisa](http://msdn.microsoft.com/library/0b306b92-f35e-45ef-a4be-3f653cd00c3d).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Como: editar consultas TableAdapter](../data-tools/how-to-edit-tableadapter-queries.md)   
 [Criar e editar Datasets tipados](../data-tools/creating-and-editing-typed-datasets.md)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Como conectar-se a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Como: navegar em dados com o controle BindingNavigator dos Windows Forms](http://msdn.microsoft.com/library/0e5d4f34-bc9b-47cf-9b8d-93acbb1f1dbb)   
 [Passo a passo: Exibindo dados em um formulário do Windows](../data-tools/walkthrough-displaying-data-on-a-windows-form.md)   
 [Passo a passo: criando um TableAdapter com várias consultas](../data-tools/walkthrough-creating-a-tableadapter-with-multiple-queries.md)