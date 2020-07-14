---
title: 'CA1900: os campos de tipo de valor devem ser portáteis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1900
- ValueTypeFieldsShouldBePortable
helpviewer_keywords:
- ValueTypeFieldsShouldBePortable
- CA1900
ms.assetid: 1787d371-389f-4d39-b305-12b53bc0dfb9
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2ece4788a277bfc4d16568d4014f9eae2ed4de33
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545269"
---
# <a name="ca1900-value-type-fields-should-be-portable"></a>CA1900: Campos de tipo de valor devem ser portáteis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente sobre o Visual Studio, consulte [CA1900: os campos de tipo de valor devem ser portáteis](/visualstudio/code-quality/ca1900-value-type-fields-should-be-portable).

|Item|Valor|
|-|-|
|TypeName|ValueTypeFieldsShouldBePortable|
|CheckId|CA1900|
|Categoria|Microsoft. portabilidade|
|Alteração Significativa|Quebra-se o campo pode ser visto fora do assembly.<br /><br /> Não separável – se o campo não estiver visível fora do assembly.|

## <a name="cause"></a>Causa
 Essa regra verifica se as estruturas declaradas com layout explícito serão alinhadas corretamente quando marshaled para código não gerenciado em sistemas operacionais de 64 bits. IA-64 não permite acessos de memória não alinhados e o processo falhará se essa violação não for corrigida.

## <a name="rule-description"></a>Descrição da Regra
 Estruturas com layout explícito que contém campos desalinhados causam falhas em sistemas operacionais de 64 bits.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Todos os campos menores que 8 bytes devem ter deslocamentos que são múltiplos de seu tamanho e os campos que têm 8 bytes ou mais devem ter deslocamentos que sejam múltiplos de 8. Outra solução é usar `LayoutKind.Sequential` em vez de `LayoutKind.Explicit` , se for razoável.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Esse aviso deve ser suprimido somente se ocorrer um erro.
