---
title: 'CA2133: os delegados devem ser associados a métodos com transparência consistente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2133
ms.assetid: a09672e2-63cb-4abd-9e8f-dff515e101ce
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 12132622900d5698a6b78a1914c687a369d7dc03
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547726"
---
# <a name="ca2133-delegates-must-bind-to-methods-with-consistent-transparency"></a>CA2133: Representantes devem ser associados a métodos com transparência consistente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DelegatesMustBindWithConsistentTransparency|
|CheckId|CA2133|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

> [!NOTE]
> Esse aviso é aplicado somente ao código que está executando o CoreCLR (a versão do CLR que é específica para aplicativos Web do Silverlight).

## <a name="cause"></a>Causa
 Esse aviso é acionado em um método que associa um delegado que é marcado com o <xref:System.Security.SecurityCriticalAttribute> para um método que é transparente ou que está marcado com <xref:System.Security.SecuritySafeCriticalAttribute> . O aviso também é acionado em um método que associa um representante transparente ou de segurança crítica a um método crítico.

## <a name="rule-description"></a>Descrição da Regra
 Tipos delegados e os métodos aos quais eles se associam devem ter transparência consistente. Delegados transparentes e com segurança crítica só podem ser associados a outros métodos transparentes ou de segurança crítica. Da mesma forma, os delegados críticos só podem ser associados a métodos críticos. Essas regras de associação garantem que o único código que pode invocar um método por meio de um delegado também poderia chamar o mesmo método diretamente. Por exemplo, as regras de associação impedem que o código Transparent chame código Critical diretamente por meio de um delegado transparente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação desse aviso, altere a transparência do delegado ou do método associado para que a transparência dos dois seja equivalente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Security.CA2133.DelegatesMustBindWithConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2133.delegatesmustbindwithconsistenttransparency/cs/ca2133 - delegatesmustbindwithconsistenttransparency.cs#1)]
