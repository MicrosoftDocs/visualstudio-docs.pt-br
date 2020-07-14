---
title: 'CA2149: os métodos Transparent não devem chamar o código nativo | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2149
ms.assetid: 28951bd7-f3db-4871-99aa-bad68d1ead80
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5c1e254ae7912efbb6773155ed834e54a1db1832
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546322"
---
# <a name="ca2149-transparent-methods-must-not-call-into-native-code"></a>CA2149: Métodos transparentes não devem chamar código nativo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TransparentMethodsMustNotCallNativeCode|
|CheckId|CA2149|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método chama uma função nativa por meio de um stub de método, como P/Invoke.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra é acionada em qualquer método transparente chamado diretamente no código nativo, por exemplo, por meio de um P/Invoke. As violações dessa regra levam a um <xref:System.MethodAccessException> no modelo de transparência de nível 2 e uma demanda completa para <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> o modelo de transparência de nível 1.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, marque o método que chama o código nativo com o <xref:System.Security.SecurityCriticalAttribute> atributo ou <xref:System.Security.SecuritySafeCriticalAttribute> .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 [!code-csharp[FxCop.Security.CA2149.TransparentMethodsMustNotCallNativeCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2149.transparentmethodsmustnotcallnativecode/cs/ca2149 - transparentmethodsmustnotcallnativecode.cs#1)]
