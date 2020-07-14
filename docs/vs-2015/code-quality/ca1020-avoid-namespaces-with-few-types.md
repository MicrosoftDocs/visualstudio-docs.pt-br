---
title: 'CA1020: evitar namespaces com poucos tipos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1020
- AvoidNamespacesWithFewTypes
helpviewer_keywords:
- CA1020
- AvoidNamespacesWithFewTypes
ms.assetid: 9cb272f6-a3ff-45af-b35d-70dea620b074
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ddd69c62eb4d6b818410a588967c1e23f164f9a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546725"
---
# <a name="ca1020-avoid-namespaces-with-few-types"></a>CA1020: Evitar namespaces com poucos tipos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidNamespacesWithFewTypes|
|CheckId|CA1020|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um namespace diferente do namespace global contém menos de cinco tipos.

## <a name="rule-description"></a>Descrição da Regra
 Certifique-se de que cada um dos seus namespaces tem uma organização lógica, e que existe uma razão válida para colocar os tipos em um namespace populamente preenchido. Os namespaces devem conter tipos que são usados juntos na maioria dos cenários. Quando seus aplicativos são mutuamente exclusivos, os tipos devem estar localizados em namespaces separados. Por exemplo, o <xref:System.Web.UI> namespace contém tipos que são usados em aplicativos Web e o <xref:System.Windows.Forms> namespace contém tipos que são usados em [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] aplicativos baseados em. Embora os namespaces tenham tipos que controlam aspectos da interface do usuário, esses tipos não são projetados para uso no mesmo aplicativo. Portanto, eles estão localizados em namespaces separados. A organização de namespace cuidadosa também pode ser útil porque aumenta a capacidade de descoberta de um recurso. Examinando a hierarquia de namespace, os consumidores de biblioteca devem ser capazes de localizar os tipos que implementam um recurso.

> [!NOTE]
> Os tipos de tempo de design e as permissões não devem ser mesclados em outros namespaces para obedecer a essa diretriz. Esses tipos pertencem a seus próprios namespaces abaixo do namespace principal, e os namespaces devem terminar em `.Design` e `.Permissions` , respectivamente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, tente combinar namespaces que contenham apenas alguns tipos em um único namespace.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando o namespace não contém tipos que são usados com os tipos em seus outros namespaces.
