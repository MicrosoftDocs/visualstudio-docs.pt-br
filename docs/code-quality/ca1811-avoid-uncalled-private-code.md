---
title: 'CA1811: evitar código privado não chamado'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUncalledPrivateCode
- CA1811
helpviewer_keywords:
- CA1811
- AvoidUncalledPrivateCode
ms.assetid: aadbba74-7821-475f-8980-34d17c0a0a8b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3b8c71c7dc549c980be8ae7a2241629774f32150
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49822963"
---
# <a name="ca1811-avoid-uncalled-private-code"></a>CA1811: evitar código privado não chamado

|||
|-|-|
|NomeDoTipo|AvoidUncalledPrivateCode|
|CheckId|CA1811|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Membro privado ou interno (nível de assembly) não tem chamadores no assembly, não é invocado pelo common language runtime e não é invocado por um delegado. Os seguintes membros não são verificados por essa regra:

- Membros de interface explícita.

- Construtores estáticos.

- Construtores de serialização.

- Métodos marcados com <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> ou <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>.

- Membros que são substituições.

## <a name="rule-description"></a>Descrição da regra
 Essa regra pode relatar falsos positivos se houver pontos de entrada que não são identificados no momento pela lógica de regra. Além disso, um compilador pode emitir código noncallable em um assembly.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, remova o código noncallable ou adicionar código que o chama.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1812: evitar classes internas sem instâncias](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801: examinar parâmetros não usados](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804: remover locais não usados](../code-quality/ca1804-remove-unused-locals.md)