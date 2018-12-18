---
title: Os objetos que você está adicionando ao designer usam uma conexão de dados diferente que o designer está usando atualmente | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c86b40a79cc91f1a778d6c98be0865dc4a161840
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49260917"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer-is-currently-using"></a>Os objetos você estiver adicionando ao uso de designer uma conexão de dados diferente do designer está usando atualmente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Os objetos que você está adicionando ao designer usam uma conexão de dados diferente da que o designer está usando no momento. Deseja substituir a conexão usada pelo designer?  
  
 Quando você adiciona itens para o [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]), todos os itens usam uma conexão de dados compartilhada. (A superfície de design representa <xref:System.Data.Linq.DataContext>, que usa uma única conexão para todos os objetos na superfície.) Se você adicionar um objeto para o designer que usa uma conexão de dados que seja diferente de conexão de dados atualmente sendo usada pelo designer, esta mensagem aparece. Para resolver esse erro, você pode escolher para manter a conexão existente. Se você fizer essa opção, o objeto selecionado não será adicionado. Como alternativa, você pode optar por adicionar o objeto e redefinir o <xref:System.Data.Linq.DataContext> conexão para a nova conexão.  
  
> [!NOTE]
>  Se você clicar **Sim**, classes de entidade todas no [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] são mapeados para a nova conexão.  
  
### <a name="to-replace-the-existing-connection-with-the-connection-used-by-the-selected-object"></a>Para substituir a conexão existente com a conexão usada pelo objeto selecionado  
  
-   Clique em **Sim**.  
  
     O objeto selecionado é adicionado a [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)], e o DataContext.Connection é definido para a nova conexão.  
  
### <a name="to-continue-to-use-the-existing-connection-and-cancel-adding-the-selected-object"></a>Para continuar a usar a conexão e cancelar existentes que adicionam o objeto selecionado  
  
-   Clique em **Não**.  
  
     A ação é cancelada. O DataContext.Connection de definidas para a conexão existente.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)

