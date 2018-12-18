---
title: Caixa de diálogo Editor de coleção de tipo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: c33049c264041495041798ab98c4223ebe0ed6f7
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49298554"
---
# <a name="type-collection-editor-dialog-box"></a>Digite a caixa de diálogo Editor de Coleção
O **Editor de coleção do tipo** caixa de diálogo é usada para adicionar tipos conhecidos para o **enviar** e **Receive** atividades. Essa caixa de diálogo também é usada para adicionar argumentos de tipo genérico para o **InvokeMethod** atividade. Quando usado para o **envie** e **Receive** atividades para adicionar tipos conhecidos, o **Editor de coleção do tipo** caixa de diálogo requer as adições do tipo ser exclusivos. Se um tipo duplicado é adicionado e a alteração é confirmada clicando **Okey**, uma mensagem de erro é retornada. Quando usado para o **InvokeMethod** atividade para adicionar argumentos de tipo genérico, o **Editor de coleção do tipo** caixa de diálogo permite a adição de tipos duplicados.  
  
> [!NOTE]
>  [!INCLUDE[crabout](../includes/crabout-md.md)] tipos conhecidos, consulte [tipos conhecidos de contrato de dados](http://msdn.microsoft.com/library/1a0baea1-27b7-470d-9136-5bbad86c4337).  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **tipo de coleção** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Lista de Tipos**|Uma lista de tipos que foram adicionados ou removidos.|  
  
## <a name="to-bring-up-the-type-collection-editor"></a>Para transferir anterior o Editor de Coleção do tipo  
  
#### <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>Para transferir anterior o Editor de Coleção do tipo para o enviar e receber atividades  
  
1.  Selecione o **envie** ou **Receive** atividade na exibição design.  
  
2.  Pressione **F4** para abrir o **propriedades** janela.  
  
3.  No **propriedades** , clique no botão de reticências ao lado de **KnownTypes** propriedade.  
  
#### <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>Para transferir anterior o Editor de Coleção do tipo para atividades de InvokeMethod  
  
1.  Selecione o **InvokeMethod** atividade na exibição design.  
  
2.  Pressione **F4** para abrir o **propriedades** janela.  
  
3.  No **propriedades** , clique no botão de reticências ao lado de **GenericTypeArguments** propriedade.