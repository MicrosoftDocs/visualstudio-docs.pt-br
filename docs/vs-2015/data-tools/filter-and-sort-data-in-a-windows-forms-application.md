---
title: Filtrar e classificar dados em um aplicativo de Windows Forms | Microsoft Docs
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
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 24c623efc141ff84c2585f967596271d1efbc502
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671642"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>Filtrar e classificar dados em um aplicativo do Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você filtra os dados definindo a propriedade <xref:System.Windows.Forms.BindingSource.Filter%2A> como uma expressão de cadeia de caracteres que retorna os registros desejados.

 Você classifica os dados definindo a propriedade <xref:System.Windows.Forms.BindingSource.Sort%2A> como o nome da coluna que você deseja classificar; Acrescente `DESC` para classificar em ordem decrescente ou acrescentar `ASC` para classificar em ordem crescente.

> [!NOTE]
> Se o seu aplicativo não usar <xref:System.Windows.Forms.BindingSource> componentes, você poderá filtrar e classificar dados usando <xref:System.Data.DataView> objetos. Para obter mais informações, consulte [DataViews](https://msdn.microsoft.com/library/0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b).

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>Para filtrar dados usando um componente BindingSource

- Defina a propriedade <xref:System.Windows.Forms.BindingSource.Filter%2A> como a expressão que você deseja retornar. Por exemplo, o código a seguir retorna aos clientes um `CompanyName` que começa com "B":

     [!code-csharp[VbRaddataDisplaying#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#6)]
     [!code-vb[VbRaddataDisplaying#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#6)]

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>Para classificar dados usando um componente BindingSource

- Defina a propriedade <xref:System.Windows.Forms.BindingSource.Sort%2A> como a coluna que você deseja classificar. Por exemplo, o código a seguir classifica os clientes na coluna `CompanyName` em ordem decrescente:

     [!code-csharp[VbRaddataDisplaying#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#7)]
     [!code-vb[VbRaddataDisplaying#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#7)]

## <a name="see-also"></a>Consulte também
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
