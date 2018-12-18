---
title: 'CA1809: Evitar locais excessivos | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA1809
- AvoidExcessiveLocals
helpviewer_keywords:
- AvoidExcessiveLocals
- CA1809
ms.assetid: 5c81ea43-cb49-448f-980f-a1dd9764043c
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 57a0c520dfa610acf247cad62ea2daf690aad05f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853292"
---
# <a name="ca1809-avoid-excessive-locals"></a>CA1809: evitar locais excessivos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidExcessiveLocals|
|CheckId|CA1809|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um membro contiver mais de 64 variáveis locais, algumas das quais podem ser gerado pelo compilador.

## <a name="rule-description"></a>Descrição da Regra
 Uma otimização de desempenho comum é armazenar um valor em um registro do processador, em vez de na memória, que é conhecido como *registro* o valor. O common language runtime considera até 64 variáveis locais para enregistration. Variáveis que não seja cancelado são colocadas na pilha e devem ser movidas para um registro antes de manipulação. Para permitir que a chance de que todas as variáveis locais obter cancelado, limite o número de variáveis locais a 64.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, Refatore a implementação para usar não mais do que 64 variáveis locais.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro para suprimir um aviso nessa regra, ou para desabilitar a regra, se o desempenho não for um problema.

## <a name="related-rules"></a>Regras relacionadas
 [CA1804: remover locais não usados](../code-quality/ca1804-remove-unused-locals.md)



