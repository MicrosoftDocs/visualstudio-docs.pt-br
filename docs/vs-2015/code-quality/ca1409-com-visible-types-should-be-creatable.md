---
title: 'CA1409: os tipos visíveis com devem ser creatable | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
helpviewer_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
ms.assetid: 9f59569b-de15-4a38-b7cb-cff152972243
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: feb50f576fbff656acaa10b70bb4d8adbca1d6c3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72602387"
---
# <a name="ca1409-com-visible-types-should-be-creatable"></a>CA1409: os tipos visíveis Com devem ser criáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ComVisibleTypesShouldBeCreatable|
|CheckId|CA1409|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo de referência que é marcado especificamente como visível para Component Object Model (COM) contém um construtor público com parâmetros, mas não contém um construtor público padrão (sem parâmetros).

## <a name="rule-description"></a>Descrição da Regra
 Um tipo sem um construtor padrão público não pode ser criado por clientes COM. No entanto, o tipo ainda pode ser acessado por clientes COM, se outro meio estiver disponível para criar o tipo e passá-lo para o cliente (por exemplo, por meio do valor de retorno de uma chamada de método).

 A regra ignora os tipos derivados de <xref:System.Delegate?displayProperty=fullName>.

 Por padrão, os itens a seguir são visíveis para COM: assemblies, tipos públicos, membros de instância pública em tipos públicos e todos os membros de tipos de valor público.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione um construtor padrão público ou remova o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> do tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se outras maneiras forem fornecidas para criar e passar o objeto para o cliente COM.

## <a name="related-rules"></a>Regras relacionadas
 [CA1017: marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>Consulte também
 [Qualificando tipos .net para interoperação](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd) [interoperabilidade com código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
