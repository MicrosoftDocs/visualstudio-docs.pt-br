---
title: 'Como: editar consultas TableAdapter | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vbData.Microsoft.VSDesigner.DataSource.DbSource
- vbdata.Microsoft.VSDesigner.DataSource.DbSource
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- queries [Visual Basic], editing
- TableAdapters, editing queries
- data [Visual Studio], TableAdapters
- editing queries
ms.assetid: aac7b7b4-bd91-4225-95d4-a07643568c43
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 687336b979ef7e6d46ea6deb4a5682f3aec065be
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49287892"
---
# <a name="how-to-edit-tableadapter-queries"></a>Como editar consultas TableAdapter
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Editar consultas TableAdapter com o [editando TableAdapters](../data-tools/editing-tableadapters.md) na **Dataset Designer**. Quando ele não é mais adequada às necessidades do seu aplicativo, você deve modificar uma consulta do TableAdapter. (Como alternativa, você pode criar consultas adicionais no TableAdapter. Para obter mais informações sobre como adicionar novas consultas, consulte [como: criar consultas do TableAdapter](../data-tools/how-to-create-tableadapter-queries.md).)  
  
> [!NOTE]
>  Se o [Assistente de configuração TableAdapter](http://msdn.microsoft.com/library/3a373dd9-7b34-4d3c-a48b-69414512bac8) é aberta em vez da **Assistente de configuração de consulta do TableAdapter**, talvez você tenha selecionado principal do TableAdapter `Fill` consulta e não uma da Consultas de adicionais do TableAdapter. Para obter informações sobre como editar o TableAdapter principais do `Fill` da consulta, consulte [como: editar TableAdapters](http://msdn.microsoft.com/library/ca178745-e35a-45f1-a395-23cddfd8f855).  
  
 ![TableAdapter com várias consultas](../data-tools/media/tableadapter.gif "TableAdapter")  
  
### <a name="to-edit-a-tableadapter-query"></a>Para editar uma consulta do TableAdapter  
  
1.  Abra o conjunto de dados do **Dataset Designer**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Selecione a consulta do TableAdapter que você deseja editar.  
  
3.  A consulta do TableAdapter com o botão direito e selecione **configurar**.  
  
     O **Assistente de configuração de consulta do TableAdapter** abre, pronto para você modificar a consulta ou procedimento armazenado para a consulta.  
  
4.  Conclua o **Assistente de configuração de consulta do TableAdapter** com as alterações que você deseja. Para obter mais informações, consulte [editando TableAdapters](../data-tools/editing-tableadapters.md).  
  
## <a name="see-also"></a>Consulte também  
 [TableAdapters](http://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)