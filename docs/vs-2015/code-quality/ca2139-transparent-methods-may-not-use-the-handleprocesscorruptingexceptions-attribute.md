---
title: 'CA2139: métodos transparentes não podem usar o atributo HandleProcessCorruptingExceptions | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2139
ms.assetid: 45a0328a-add7-40f9-8934-dff59beb02b3
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 233e4366befd2a5a0d5690b14198ac13e2fcc957
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546478"
---
# <a name="ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute"></a>CA2139: Métodos transparentes podem não usar o atributo HandleProcessCorruptingExceptions
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TransparentMethodsMustNotHandleProcessCorruptingExceptions|
|CheckId|CA2139|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método transparente é marcado com o <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> atributo.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra dispara qualquer método que é transparente e tenta manipular um processo que corrompe a exceção usando o <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> atributo. Uma exceção de corrompimento de processo é uma classificação de exceção do CLR versão 4,0 de exceções, como <xref:System.AccessViolationException> . O atributo HandleProcessCorruptedStateExceptionsAttribute só pode ser usado por métodos de segurança crítica e será ignorado se for aplicado a um método transparente. Para lidar com exceções que corrompem o processo, esse método deve se tornar crítico de segurança ou de segurança.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> atributo ou marque o método com o <xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute> atributo ou.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 Neste exemplo, um método transparente é marcado com o <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> atributo e falhará na regra. O método também deve ser marcado com o <xref:System.Security.SecurityCriticalAttribute> atributo ou <xref:System.Security.SecuritySafeCriticalAttribute> .

 [!code-csharp[FxCop.Security.CA2139#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2139/cs/ca2139.cs#1)]
