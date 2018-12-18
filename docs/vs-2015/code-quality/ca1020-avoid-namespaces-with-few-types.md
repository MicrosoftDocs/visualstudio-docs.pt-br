---
title: 'CA1020: Evitar namespaces com poucos tipos | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA1020
- AvoidNamespacesWithFewTypes
helpviewer_keywords:
- CA1020
- AvoidNamespacesWithFewTypes
ms.assetid: 9cb272f6-a3ff-45af-b35d-70dea620b074
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6663660319791f1e81d0ed89f171c929c3e50725
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906176"
---
# <a name="ca1020-avoid-namespaces-with-few-types"></a>CA1020: evitar namespaces com poucos tipos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidNamespacesWithFewTypes|
|CheckId|CA1020|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um namespace diferente do namespace global contém menos de cinco tipos.

## <a name="rule-description"></a>Descrição da Regra
 Certifique-se de que cada um dos namespaces tem uma organização lógica e a existência de um motivo válido para colocar tipos em um namespace populado de modo disperso. Namespaces deve conter tipos que são usados juntos na maioria dos cenários. Quando seus aplicativos são mutuamente exclusivos, tipos deverá estar localizados em namespaces separados. Por exemplo, o <xref:System.Web.UI> namespace contém tipos que são usados em aplicativos Web, e o <xref:System.Windows.Forms> namespace contém tipos que são usados em [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)]-com base em aplicativos. Embora ambos os namespaces têm tipos que controlam aspectos da interface do usuário, esses tipos não são projetados para uso no mesmo aplicativo. Portanto, eles estão localizados em namespaces separados. Namespace cuidado organização também pode ser útil, pois ele aumenta a detectabilidade de um recurso. Examinando a hierarquia de namespace, os clientes de biblioteca devem ser capazes de localizar os tipos que implementam um recurso.

> [!NOTE]
>  Permissões e tipos de tempo de design não devem ser mescladas em outros namespaces em conformidade com essa diretriz. Esses tipos pertencem a seus próprios namespaces abaixo seu namespace principal, e deve terminar com os namespaces `.Design` e `.Permissions`, respectivamente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, tente combinar os namespaces que contêm apenas alguns tipos em um único namespace.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, quando o namespace não contém tipos que são usados com os tipos de seus outros namespaces.



