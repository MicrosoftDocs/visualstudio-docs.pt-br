---
title: Conjunto de regras mínimas gerenciado para código gerenciado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f67b9e28069a1717ad500b7e8895a363db715fda
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49251051"
---
# <a name="managed-minimun-rules-rule-set-for-managed-code"></a>Conjunto de regras mínimas gerenciado para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As regras mínimas gerenciado enfocam os problemas mais críticos do código, inclusive falhas potenciais de segurança, falhas do aplicativo e outros erros importantes de lógica e design. Você deve incluir este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos.  
  
|Regra|Descrição|  
|----------|-----------------|  
|[CA1001](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|Tipos que possuem campos descartáveis devem ser descartáveis|  
|[CA1821](../code-quality/ca1821-remove-empty-finalizers.md)|Remova finalizadores vazios|  
|[CA2213](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|Campos descartáveis devem ser descartados|  
|[CA2231](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|Sobrecarregar operador equals ao substituir ValueType.Equals&lt;2}&lt;1}|



