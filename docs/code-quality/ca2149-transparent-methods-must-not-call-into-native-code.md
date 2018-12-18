---
title: 'CA2149: os métodos transparentes não devem chamar código nativo'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2149
ms.assetid: 28951bd7-f3db-4871-99aa-bad68d1ead80
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 53e41a6faa5885fd598810224abfeef0d017f05a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908880"
---
# <a name="ca2149-transparent-methods-must-not-call-into-native-code"></a>CA2149: os métodos transparentes não devem chamar código nativo

|||
|-|-|
|NomeDoTipo|TransparentMethodsMustNotCallNativeCode|
|CheckId|CA2149|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método chama uma função nativa por meio de um stub de método, como a P/Invoke.

## <a name="rule-description"></a>Descrição da regra
 Essa regra é acionada em qualquer método transparente chamado diretamente no código nativo, por exemplo, por meio de um P/Invoke. As violações dessa regra resultam em uma <xref:System.MethodAccessException> no modelo de transparência de nível 2 e uma demanda completa para <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> no modelo de transparência de nível 1.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, marque o método que chama o código nativo com o <xref:System.Security.SecurityCriticalAttribute> ou <xref:System.Security.SecuritySafeCriticalAttribute> atributo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 [!code-csharp[FxCop.Security.CA2149.TransparentMethodsMustNotCallNativeCode#1](../code-quality/codesnippet/CSharp/ca2149-transparent-methods-must-not-call-into-native-code_1.cs)]