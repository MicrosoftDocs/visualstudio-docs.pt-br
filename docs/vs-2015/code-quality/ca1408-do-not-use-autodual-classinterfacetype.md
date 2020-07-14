---
title: 'CA1408: não usar AutoDual ClassInterfaceType | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotUseAutoDualClassInterfaceType
- CA1408
helpviewer_keywords:
- CA1408
- DoNotUseAutoDualClassInterfaceType
ms.assetid: 60ca5e02-3c51-42dd-942b-4f950eecfa0f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b953a97d557e28cce50f554acc03797d4be38220
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534869"
---
# <a name="ca1408-do-not-use-autodual-classinterfacetype"></a>CA1408: Não usar AutoDual ClassInterfaceType
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo de Component Object Model (COM) visível é marcado com o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo definido como o `AutoDual` valor de <xref:System.Runtime.InteropServices.ClassInterfaceType> .

## <a name="rule-description"></a>Descrição da Regra
 Tipos que usam uma interface dupla permitem que clientes sejam associados a um layout de interface específico. Todas as alterações feitas em uma versão futura do layout do tipo ou de qualquer tipo de base interromperão clientes COM associados à interface. Por padrão, se o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo não for especificado, uma interface somente de expedição será usada.

 A menos que marcado de outra forma, todos os tipos públicos não genéricos são visíveis para COM; todos os tipos não públicos e genéricos são invisíveis para COM.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o valor do <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo para o `None` valor de <xref:System.Runtime.InteropServices.ClassInterfaceType> e defina explicitamente a interface.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso dessa regra, a menos que tenha certeza de que o layout do tipo e seus tipos base não serão alterados em uma versão futura.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe que viola a regra e uma redeclaração da classe para usar uma interface explícita.

 [!code-csharp[FxCop.Interoperability.AutoDual#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/cs/FxCop.Interoperability.AutoDual.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoDual#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/vb/FxCop.Interoperability.AutoDual.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1403: Tipos de layout automático não devem ser visíveis no COM](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

 [CA1412: Marcar interfaces ComSource como IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## <a name="see-also"></a>Consulte Também
 [Introdução à interface de classe](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024) [qualificando tipos .net para interoperação](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd) [interoperabilidade com código não-gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
