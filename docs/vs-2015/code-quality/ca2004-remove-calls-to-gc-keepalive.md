---
title: 'CA2004: Remover chamadas para GC. KeepAlive | Microsoft Docs'
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
- RemoveCallsToGCKeepAlive
- CA2004
helpviewer_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
ms.assetid: bc543b5b-23eb-4b45-abc2-9325cd254ac2
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 944862f742e96ef061c3c425bb28c0addcb4fb4e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49829060"
---
# <a name="ca2004-remove-calls-to-gckeepalive"></a>CA2004: remover chamadas para GC.KeepAlive
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|RemoveCallsToGCKeepAlive|
|CheckId|CA2004|
|Categoria|Microsoft.Reliability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Classes usam `SafeHandle` , mas ainda contém chamadas para `GC.KeepAlive`.

## <a name="rule-description"></a>Descrição da Regra
 Se você estiver convertendo em `SafeHandle` uso, remova todas as chamadas para `GC.KeepAlive` (objeto). Nesse caso, as classes não deve chamar `GC.KeepAlive`, supondo que eles não têm um finalizador, mas dependem `SafeHandle` para concluir o identificador de sistema operacional para eles.  Embora o custo de deixar em uma chamada para `GC.KeepAlive` pode ser insignificante, conforme medido pelo desempenho, a percepção de que uma chamada para `GC.KeepAlive` é necessária ou suficiente para resolver um problema que talvez não exista mais torna mais difícil para o código de tempo de vida Manter.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Remover chamadas para `GC.KeepAlive`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você pode suprimir esse aviso somente se ele não é tecnicamente certo converter em `SafeHandle` uso na sua classe.



