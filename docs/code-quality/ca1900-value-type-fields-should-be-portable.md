---
title: 'CA1900: os campos de tipo de valor devem ser móveis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1900
- ValueTypeFieldsShouldBePortable
helpviewer_keywords:
- ValueTypeFieldsShouldBePortable
- CA1900
ms.assetid: 1787d371-389f-4d39-b305-12b53bc0dfb9
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fbf54493d4abb455649558a82126f09b7becc605
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844625"
---
# <a name="ca1900-value-type-fields-should-be-portable"></a>CA1900: os campos de tipo de valor devem ser móveis

|||
|-|-|
|NomeDoTipo|ValueTypeFieldsShouldBePortable|
|CheckId|CA1900|
|Categoria|Microsoft.Portability|
|Alteração Significativa|Quebrando - se o campo pode ser visto de fora do assembly.<br /><br /> Sem quebra - se o campo não está visível fora do assembly.|

## <a name="cause"></a>Causa
 Esta regra verifica que estruturas que são declaradas com layout explícito serão corretamente alinhados quando passa por marshaling para código não gerenciado em sistemas operacionais de 64 bits. IA-64 não permite que os acessos à memória desalinhada e o processo falhará se essa violação não for corrigida.

## <a name="rule-description"></a>Descrição da regra
 Estruturas com layout explícito contendo campos desalinhados podem causar quedas em sistemas operacionais de 64 bits.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Todos os campos que são menores do que 8 bytes devem ter os deslocamentos são um múltiplo de seu tamanho e os campos que são 8 bytes ou mais devem ter os deslocamentos são um múltiplo de 8. Outra solução é usar `LayoutKind.Sequential` em vez de `LayoutKind.Explicit`, se razoável.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Esse aviso deve ser suprimido somente se ele ocorrer no erro.