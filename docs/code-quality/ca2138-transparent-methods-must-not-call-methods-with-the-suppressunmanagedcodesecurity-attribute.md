---
title: 'CA2138: os métodos transparentes não devem chamar métodos com o atributo SuppressUnmanagedCodeSecurity'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 3ba7a1c25387349ba78b198a37b709d6bdd10b64
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49948623"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138: os métodos transparentes não devem chamar métodos com o atributo SuppressUnmanagedCodeSecurity

|||
|-|-|
|NomeDoTipo|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método de segurança transparente chama um método que é marcado com o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> atributo.

## <a name="rule-description"></a>Descrição da regra
 Essa regra é acionada em qualquer método transparente chamado diretamente no código nativo, por exemplo, usando P/Invoke (invocação de plataforma) chamar. Métodos de interoperabilidade P/Invoke e COM que são marcados com o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> resultam em um LinkDemand que está sendo feito em relação ao método de chamada do atributo. Porque o código transparente de segurança não é possível atender a LinkDemands, o código também não é possível chamar métodos que são marcados com o atributo SuppressUnmanagedCodeSecurity ou métodos da classe que é marcado com o atributo SuppressUnmanagedCodeSecurity. O método irá falhar ou a demanda será convertida em uma demanda completa.

 As violações dessa regra resultam em uma <xref:System.MethodAccessException> no modelo de transparência de segurança de nível 2 e uma demanda completa para <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> no modelo de transparência de nível 1.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, remova os <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> de atributos e marcar o método com o <xref:System.Security.SecurityCriticalAttribute> ou o <xref:System.Security.SecuritySafeCriticalAttribute> atributo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 [!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../code-quality/codesnippet/CSharp/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute_1.cs)]