---
title: Filtrar e classificar dados em um aplicativo Windows Forms | Microsoft Docs
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
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d1ea216e20045cd7b8cfba3c70a3126a673519be
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49175585"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>Filtrar e classificar dados em um aplicativo do Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Filtrar dados, definindo o <xref:System.Windows.Forms.BindingSource.Filter%2A> propriedade a uma expressão de cadeia de caracteres que retorna os registros desejados.  
  
 Classificar dados, definindo a <xref:System.Windows.Forms.BindingSource.Sort%2A> propriedade para o nome da coluna que você deseja classificar; acrescentar `DESC` para classificar em ordem decrescente, ou anexar `ASC` para classificar em ordem crescente.  
  
> [!NOTE]
>  Se seu aplicativo não usar <xref:System.Windows.Forms.BindingSource> componentes, você pode filtrar e classificar dados usando <xref:System.Data.DataView> objetos. Para obter mais informações, consulte [DataViews](http://msdn.microsoft.com/library/0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b).  
  
## <a name="to-filter-data-by-using-a-bindingsource-component"></a>Para filtrar dados usando um componente BindingSource  
  
-   Defina o <xref:System.Windows.Forms.BindingSource.Filter%2A> propriedade para a expressão que você deseja retornar. Por exemplo, o código a seguir retorna clientes com um `CompanyName` que começa com "B":  
  
     [!code-csharp[VbRaddataDisplaying#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#6)]
     [!code-vb[VbRaddataDisplaying#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#6)]  
  
## <a name="to-sort-data-by-using-a-bindingsource-component"></a>Para classificar dados usando um componente BindingSource  
  
-   Defina o <xref:System.Windows.Forms.BindingSource.Sort%2A> propriedade para a coluna que você deseja classificar. Por exemplo, o código a seguir classifica os clientes sobre o `CompanyName` coluna em ordem decrescente:  
  
     [!code-csharp[VbRaddataDisplaying#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#7)]
     [!code-vb[VbRaddataDisplaying#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#7)]  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)

