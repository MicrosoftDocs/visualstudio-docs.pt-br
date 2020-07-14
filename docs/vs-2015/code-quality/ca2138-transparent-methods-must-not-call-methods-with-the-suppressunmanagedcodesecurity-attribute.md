---
title: 'CA2138: métodos Transparent não devem chamar métodos com o atributo SuppressUnmanagedCodeSecurity | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 35cc152998b15a2fd4c4ff02e4730cdfae5366cb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546491"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138: Métodos transparentes não devem chamar métodos com o atributo SuppressUnmanagedCodeSecurity
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método transparente de segurança chama um método que é marcado com o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> atributo.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra é acionada em qualquer método transparente que chama diretamente em código nativo, por exemplo, usando uma chamada P/Invoke (Platform Invoke). Os métodos de interoperabilidade P/Invoke e COM que são marcados com o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> atributo resultam em um LinkDemand sendo feito em relação ao método de chamada. Como o código Transparent Security não pode satisfazer LinkDemands, o código também não pode chamar métodos que são marcados com o atributo SuppressUnmanagedCodeSecurity ou métodos de classe que são marcados com o atributo SuppressUnmanagedCodeSecurity. O método falhará ou a demanda será convertida em uma demanda completa.

 As violações dessa regra levam a um <xref:System.MethodAccessException> no modelo de transparência de segurança de nível 2 e uma demanda completa pelo <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> modelo de transparência de nível 1.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> atributo e marque o método com o <xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute> atributo ou.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 [!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2138.transparentmethodsmustnotcallsuppressunmanagedcodesecuritymethods/cs/ca2138.cs#1)]
