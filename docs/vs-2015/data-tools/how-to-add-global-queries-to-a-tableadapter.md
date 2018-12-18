---
title: 'Como: adicionar consultas globais a um TableAdapter | Microsoft Docs'
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
- global functions, datasets
- scalar functions, datasets
- TableAdapters, global queries
- data [Visual Studio], TableAdapters
- datasets [Visual Basic], scalar functions
- TableAdapter Query Configuration Wizard
- datasets [Visual Basic], global functions
- TableAdapter queries
- queries [Visual Studio], TableAdapters
ms.assetid: 4abffd6b-2e9f-4ef3-99b2-6e9ae4ad4679
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: fd185c9a6803a5e66b1fdaac0f040815328ddb82
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49193889"
---
# <a name="how-to-add-global-queries-to-a-tableadapter"></a>Como: adicionar consultas globais a um TableAdapter
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*Consultas globais* são consultas SQL que retornam um valor único (escalar) ou nenhum valor. Normalmente, funções globais executam operações de banco de dados como inserções, atualizações, exclusões e a agregação de informações, como retornar uma contagem de clientes em uma tabela ou o total das taxas para todos os itens em uma ordem específica.  
  
 Adicionar consultas globais, executando o **Assistente de configuração de consulta do TableAdapter** de dentro de **Dataset Designer**.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-add-a-global-query-to-a-dataset"></a>Para adicionar uma consulta global a um conjunto de dados  
  
1.  Abrir em um conjunto de dados do **Dataset Designer**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Arraste uma **consulta** da **conjunto de dados** guia da **caixa de ferramentas** em uma área vazia do **Dataset Designer**.  
  
     O [editando TableAdapters](../data-tools/editing-tableadapters.md) é aberta.  
  
3.  Escolha uma conexão para a consulta a ser usada. Você pode escolher um na lista ou crie uma nova conexão. Se você criar uma nova conexão, você terá a opção para salvá-lo para o arquivo de configuração do aplicativo. Para obter mais informações, consulte [como: salvar e editar cadeias de caracteres de Conexão](~/E:/Repos/visualstudio-docs-pr/docs/data-tools/how-to-save-and-edit-connection-strings.md).  
  
4.  Escolha se deseja usar instruções SQL ou procedimentos armazenados.  
  
5.  Escolha o procedimento armazenado para usar ou, nos **escolher um tipo de consulta** página do assistente, escolha o tipo de consulta você deseja e, em seguida, clique em **próxima**.  
  
6.  Forneça uma consulta que realiza a tarefa desejada, por exemplo, `SELECT COUNT(*) AS CustomerCount FROM Customers`.  
  
    > [!NOTE]
    >  Arrastar uma consulta diretamente para o **Dataset Designer** cria um método que só retornará um valor escalar (único). Enquanto a consulta ou procedimento armazenado que você selecionar pode retornar mais de um único valor, o método criado pelo assistente retornará apenas um único valor. Por exemplo, a consulta pode retornar a primeira coluna da primeira linha dos dados retornados.  
  
7.  Conclua o Assistente; a consulta é adicionada para o **Dataset Designer**. Para obter informações sobre como executar a consulta, consulte [como: executar consultas do TableAdapter](http://msdn.microsoft.com/library/c7518855-f896-41c1-b3de-1a8116280593).  
  
## <a name="see-also"></a>Consulte também  
 [Criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md)   
 [Como: criar consultas TableAdapter](../data-tools/how-to-create-tableadapter-queries.md)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Criar e editar Datasets tipados](../data-tools/creating-and-editing-typed-datasets.md)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Como conectar-se a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Como: navegar em dados com o controle BindingNavigator dos Windows Forms](http://msdn.microsoft.com/library/0e5d4f34-bc9b-47cf-9b8d-93acbb1f1dbb)   
 [Passo a passo: exibindo dados em um Windows Form](../data-tools/walkthrough-displaying-data-on-a-windows-form.md)