---
title: 'CA1724: Nomes de tipo não devem corresponder a Namespaces | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
helpviewer_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
ms.assetid: 329af3b5-5600-4101-831d-531ab3eb7060
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 7fe95e08d2265baf06c6da265996ffcd579f0d1f
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58925402"
---
# <a name="ca1724-type-names-should-not-match-namespaces"></a>CA1724: Nomes de tipos não devem corresponder a namespaces
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TypeNamesShouldNotMatchNamespaces|
|CheckId|CA1724|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um nome de tipo corresponde a um [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] nomes de namespace em uma comparação que diferencia maiusculas de minúsculas.

## <a name="rule-description"></a>Descrição da Regra
 Os nomes de tipo não devem corresponder aos nomes de namespaces definidos na biblioteca de classes do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. A violação dessa regra pode reduzir a usabilidade da biblioteca.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Selecione um nome de tipo que não coincide com o nome de um [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] namespace da biblioteca de classe.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para novos desenvolvimentos, nenhum conhecidos ocorrem de cenários em que você deve suprimir um aviso nessa regra. Antes de você suprime o aviso, considere cuidadosamente como os usuários da sua biblioteca talvez estejam confusos pelas nome correspondente. Para o envio de bibliotecas, talvez você precise suprimir um aviso nessa regra.
