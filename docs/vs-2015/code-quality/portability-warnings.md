---
title: Avisos de portabilidade | Microsoft Docs
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
- vs.codeanalysis.PortabilityRules
helpviewer_keywords:
- portability warnings
- managed code analysis warnings, portability warnings
- warnings, portability
ms.assetid: 902e859a-2153-4970-baaa-8a5b4a11806f
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3b7c38f8380fc8e52707b9c4817880b1ce86b4b9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49173065"
---
# <a name="portability-warnings"></a>Avisos de portabilidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Avisos de portabilidade dão suporte a portabilidade entre diferentes sistemas operacionais.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Regra|Descrição|  
|----------|-----------------|  
|[CA1900: os campos de tipo de valor devem ser móveis](../code-quality/ca1900-value-type-fields-should-be-portable.md)|Esta regra verifica que estruturas que são declaradas usando um atributo de layout explícito serão corretamente alinhados quando passa por marshaling para código não gerenciado em sistemas operacionais de 64 bits.|  
|[CA1901: as declarações P/Invoke devem ser portáteis](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|Essa regra avalia o tamanho de cada parâmetro e o valor retornado de um P/Invoke e verifica se o seu tamanho é correto durante a realização de marshaling para código não gerenciado em sistemas operacionais de 32 bits e 64 bits.|  
|[CA1903: usar apenas a API da estrutura de destino](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|Um membro ou um tipo está usando um membro ou um tipo que foi introduzido em um service pack não incluído com a estrutura de destino do projeto.|



