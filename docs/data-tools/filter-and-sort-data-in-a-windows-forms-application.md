---
title: Filtrar e classificar dados em um aplicativo do Windows Forms
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.workload:
- data-storage
ms.openlocfilehash: 6da584d4966d61a873ca43477930084c4f9a464b
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53890005"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>Filtrar e classificar dados em um aplicativo do Windows Forms

Filtrar dados, definindo o <xref:System.Windows.Forms.BindingSource.Filter%2A> propriedade a uma expressão de cadeia de caracteres que retorna os registros desejados.

Classificar dados, definindo a <xref:System.Windows.Forms.BindingSource.Sort%2A> propriedade para o nome da coluna na qual você deseja classificar; acrescentar `DESC` para classificar em ordem decrescente, ou anexar `ASC` para classificar em ordem crescente.

> [!NOTE]
> Se seu aplicativo não usar <xref:System.Windows.Forms.BindingSource> componentes, você pode filtrar e classificar dados usando <xref:System.Data.DataView> objetos. Para obter mais informações, consulte [DataViews](/dotnet/framework/data/adonet/dataset-datatable-dataview/dataviews).

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>Para filtrar dados usando um componente BindingSource

-   Defina o <xref:System.Windows.Forms.BindingSource.Filter%2A> propriedade para a expressão que você deseja retornar. Por exemplo, o código a seguir retorna clientes com um `CompanyName` que começa com "B":

     [!code-csharp[VbRaddataDisplaying#6](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_1.cs)]
     [!code-vb[VbRaddataDisplaying#6](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_1.vb)]

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>Para classificar dados usando um componente BindingSource

-   Defina o <xref:System.Windows.Forms.BindingSource.Sort%2A> propriedade para a coluna que você deseja classificar. Por exemplo, o código a seguir classifica os clientes sobre o `CompanyName` coluna em ordem decrescente:

     [!code-csharp[VbRaddataDisplaying#7](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_2.cs)]
     [!code-vb[VbRaddataDisplaying#7](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_2.vb)]

## <a name="see-also"></a>Consulte também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)