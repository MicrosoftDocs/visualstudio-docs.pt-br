---
title: 'Como: iniciar o Assistente de configuração do TableAdapter | Microsoft Docs'
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
- TableAdapters, Configuration Wizard
- TableAdapter Configuration Wizard
ms.assetid: 301f2dcd-ed72-4229-80ef-3b59cb062d5d
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 7f603789014239762f564c3b2391b99865d8f620
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49261880"
---
# <a name="how-to-start-the-tableadapter-configuration-wizard"></a>Como iniciar o assistente de configuração TableAdapter
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **Assistente de configuração TableAdapter** cria e edita TableAdapters em conjuntos de dados com rigidez de tipos. O assistente cria TableAdapters baseados em instruções SQL que você insere no assistente ou em procedimentos armazenados existentes no banco de dados. O assistente também pode criar novos procedimentos armazenados no banco de dados com base em instruções SQL inseridas no assistente.  
  
### <a name="to-start-the-tableadapter-configuration-wizard-to-create-a-new-tableadapter"></a>Para iniciar o Assistente de Configuração do TableAdapter para criar um novo TableAdapter  
  
1.  Abra o dataset na **Dataset Designer**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
    > [!NOTE]
    >  Se você não tiver um conjunto de dados em seu projeto, consulte [criar e configurar conjuntos de dados](../data-tools/create-and-configure-datasets-in-visual-studio.md).  
  
2.  Se você estiver criando um novo TableAdapter, arraste um **TableAdapter** do objeto da **conjunto de dados** guia da **caixa de ferramentas** até o **Dataset Designer**.  
  
3.  Sobre o **escolha sua Conexão de dados** página, selecione uma conexão de dados na lista de conexões atualmente disponíveis ou selecione **nova Conexão** para criar uma nova conexão.  
  
### <a name="to-start-the-tableadapter-configuration-wizard-to-edit-an-existing-tableadapter"></a>Para iniciar o Assistente de Configuração do TableAdapter para editar um TableAdapter  
  
1.  Abra o dataset na **Dataset Designer**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Clique com botão direito no TableAdapter na **Dataset Designer** e escolha **configurar**. O assistente abre o **gerar as instruções SQL** página ou o **ligar comandos aos procedimentos armazenados existentes** página, dependendo de como o TableAdapter foi originalmente configurado.  
  
3.  Conclua o assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Criar e editar Datasets tipados](../data-tools/creating-and-editing-typed-datasets.md)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Como conectar-se a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Como: Classificar e filtrar dados ADO.NET com o componente BindingSource dos Windows Forms](http://msdn.microsoft.com/library/6c206daf-d706-4602-9dbe-435343052063)   
 [Como: criar uma tabela de pesquisa com o componente BindingSource dos Windows Forms](http://msdn.microsoft.com/library/622fce80-879d-44be-abbf-8350ec22ca2b)   
 [Passo a passo: exibindo dados em um Windows Form](../data-tools/walkthrough-displaying-data-on-a-windows-form.md)