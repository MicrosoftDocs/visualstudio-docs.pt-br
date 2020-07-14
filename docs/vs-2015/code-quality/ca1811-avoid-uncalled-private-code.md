---
title: 'CA1811: evitar código particular não chamado | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUncalledPrivateCode
- CA1811
helpviewer_keywords:
- CA1811
- AvoidUncalledPrivateCode
ms.assetid: aadbba74-7821-475f-8980-34d17c0a0a8b
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 223b2ff9aa25ddd94a3c62eb9e641127a1cace4e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543813"
---
# <a name="ca1811-avoid-uncalled-private-code"></a>CA1811: Evitar código particular não chamado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidUncalledPrivateCode|
|CheckId|CA1811|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um membro privado ou interno (no nível do assembly) não tem chamadores no assembly, não é invocado pelo Common Language Runtime e não é invocado por um delegado. Os seguintes membros não são verificados por esta regra:

- Membros de interface explícitos.

- Construtores estáticos.

- Construtores de serialização.

- Métodos marcados com <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> ou <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> .

- Membros que são substituições.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra pode relatar falsos positivos se ocorrerem pontos de entrada que não estão identificados atualmente pela lógica da regra. Além disso, um compilador pode emitir código não chamável em um assembly.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o código não chamável ou adicione o código que o chama.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1812: Evitar classes internas sem instâncias](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801: Examinar parâmetros não utilizados](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804: Remover locais não utilizados](../code-quality/ca1804-remove-unused-locals.md)
