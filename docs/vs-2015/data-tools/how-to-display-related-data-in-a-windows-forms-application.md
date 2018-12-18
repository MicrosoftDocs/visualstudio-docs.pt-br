---
title: 'Como: Exibir relacionados a dados em um Windows Forms Application | Microsoft Docs'
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
- Windows Forms, displaying data
- displaying data, related data
- related data, displaying
- displaying tables, related data
- data [Windows Forms], displaying
- displaying table data
- data [Windows Forms], related
- displaying data on forms, related data
- displaying table information
ms.assetid: 60b1f1ec-6257-42ab-83f0-06d54ed364fd
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 3fd7a29e1de66a5b5fd57dab1adbcf99128001ac
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49215456"
---
# <a name="how-to-display-related-data-in-a-windows-forms-application"></a>Como exibir dados relacionados em um Aplicativo do Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode exibir dados relacionados, arrastando os itens que compartilham o mesmo nó da tabela principal dos [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) para seu formulário. Por exemplo, se você tiver um dados de origem que tem um `Customers` tabela e um relacionado `Orders` tabela, você vê ambas as tabelas como nós de nível superior (na exibição de árvore) a **fontes de dados** janela. Expanda o `Customers` nó para que você possa ver as colunas, e você observará que a última coluna na lista é um nó expansível que representa o `Orders` tabela. Este nó representa os pedidos relacionados para um cliente. Isso significa que, se você quiser criar um formulário que permite que você selecione um cliente e, em seguida, exibir uma lista de pedidos desse cliente, você arrastaria os itens que você deseja exibir dessa hierarquia única.  
  
 ![Janela de fontes de dados que mostra a relação](../data-tools/media/datasources2.gif "DataSources2")  
Criando controles ligados a dados que exibem registros relacionados  
  
 ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo") para uma versão em vídeo deste tópico, consulte [How do i: atualizar de tabelas relacionadas](http://go.microsoft.com/fwlink/?LinkId=143527).  
  
### <a name="to-create-controls-that-display-related-records"></a>Para criar controles que exibem registros relacionados  
  
1.  Abra o formulário na [Designer de formulários do Windows](http://msdn.microsoft.com/en-us/3c3d61f8-f36c-4d41-b9c3-398376fabb15).  
  
2.  Abra o **fontes de dados** janela. Para obter mais informações, consulte [como: abrir a janela de fontes de dados](../data-tools/how-to-open-the-data-sources-window.md).  
  
3.  Expanda o nó que representa a tabela pai na relação. (A tabela pai é a tabela no lado "um" de uma relação um-para-muitos.)  
  
4.  Arraste os itens que você deseja exibir da tabela pai da relação dos **fontes de dados** window para seu formulário.  
  
5.  Tabelas filho relacionados aparecem como nós expansíveis na parte inferior da lista de colunas da tabela pai. Arraste os itens que você deseja exibir em um nó relacionado para seu formulário.  
  
    > [!NOTE]
    >  Arrastar um item de um nó de nível superior cria um separado não relacionado [componente BindingSource](http://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9) que facilita a navegação pelos registros relacionados. Para vincular dados relacionados, você deve selecionar as tabelas do mesmo nó hierárquico.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Passo a passo: Exibindo dados em um formulário do Windows](../data-tools/walkthrough-displaying-data-on-a-windows-form.md)   
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Criar e editar Datasets tipados](../data-tools/creating-and-editing-typed-datasets.md)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Como conectar-se a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Como navegar em dados com o controle BindingNavigator dos Windows Forms](http://msdn.microsoft.com/library/0e5d4f34-bc9b-47cf-9b8d-93acbb1f1dbb)