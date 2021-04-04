---
title: Filtrar e classificar dados em um aplicativo do Windows Forms
description: Filtrar e classificar dados em um aplicativo Windows Forms. Defina a propriedade de filtro para uma expressão de cadeia de caracteres que retorne os registros desejados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 045da0ade1ce60e2a8d21c24238c8e2b061e8612
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215819"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>Filtrar e classificar dados em um aplicativo do Windows Forms

Você filtra os dados definindo a <xref:System.Windows.Forms.BindingSource.Filter%2A> propriedade como uma expressão de cadeia de caracteres que retorna os registros desejados.

Você classifica os dados definindo a <xref:System.Windows.Forms.BindingSource.Sort%2A> propriedade como o nome da coluna na qual você deseja classificar; acrescentar `DESC` para classificar em ordem decrescente ou acrescentar `ASC` para classificar em ordem crescente.

> [!NOTE]
> Se o seu aplicativo não usar <xref:System.Windows.Forms.BindingSource> componentes, você poderá filtrar e classificar dados usando <xref:System.Data.DataView> objetos. Para obter mais informações, consulte [DataViews](/dotnet/framework/data/adonet/dataset-datatable-dataview/dataviews).

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>Para filtrar dados usando um componente BindingSource

- Defina a <xref:System.Windows.Forms.BindingSource.Filter%2A> propriedade para a expressão que você deseja retornar. Por exemplo, o código a seguir retorna clientes com um `CompanyName` que começa com "B":

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb" id="Snippet6":::

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>Para classificar dados usando um componente BindingSource

- Defina a <xref:System.Windows.Forms.BindingSource.Sort%2A> propriedade para a coluna que você deseja classificar. Por exemplo, o código a seguir classifica os clientes na `CompanyName` coluna em ordem decrescente:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb" id="Snippet7":::

## <a name="see-also"></a>Confira também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
