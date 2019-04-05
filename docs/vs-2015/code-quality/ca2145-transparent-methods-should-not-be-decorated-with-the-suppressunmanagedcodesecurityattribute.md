---
title: 'CA2145: Métodos transparentes não devem ser decorados com o SuppressUnmanagedCodeSecurityAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2145
ms.assetid: 81970700-b438-4b3b-9239-16887e16f7b7
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b6a7c1b5684181098ef0bec1cde430f401ba1136
ms.sourcegitcommit: c496a77add807ba4a29ee6a424b44a5de89025ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "58923155"
---
# <a name="ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute"></a>CA2145: Métodos transparentes não devem ser decorados com o SuppressUnmanagedCodeSecurityAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity|
|CheckId|CA2145|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método transparente, um método marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> método ou um tipo que contém um método é marcado com o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> atributo.

## <a name="rule-description"></a>Descrição da Regra
 Os métodos decorados com o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> atributo têm um LinkDemand implícito colocado em qualquer método que o chama. Este LinkDemand requer que o código de chamada seja crítico de segurança. A marcação do método que usa SuppressUnmanagedCodeSecurity com o <xref:System.Security.SecurityCriticalAttribute> atributo torna esse requisito mais óbvio para chamadores do método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, marque o método ou tipo com o <xref:System.Security.SecurityCriticalAttribute> atributo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Security.CA2145.TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2145.transparentmethodsshouldnotusesuppressunmanagedcodesecurity/cs/ca2145.cs#1)]

### <a name="comments"></a>Comentários
