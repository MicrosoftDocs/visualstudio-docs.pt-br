---
title: 'CA1707: Os identificadores não devem conter sublinhados | Microsoft Docs'
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
- IdentifiersShouldNotContainUnderscores
- CA1707
helpviewer_keywords:
- CA1707
- IdentifiersShouldNotContainUnderscores
ms.assetid: 5fb539ef-c304-4323-90c0-b14386da9774
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0aeea5c113ebebe33d4c371fed1a5c46da4e735e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49211062"
---
# <a name="ca1707-identifiers-should-not-contain-underscores"></a>CA1707: os identificadores não devem conter sublinhados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA1707: os identificadores não devem conter sublinhados](https://docs.microsoft.com/visualstudio/code-quality/ca1707-identifiers-should-not-contain-underscores) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|IdentifiersShouldNotContainUnderscores|  
|CheckId|CA1707|  
|Categoria|Microsoft.Naming|  
|Alteração Significativa|Recentes – quando gerado em assemblies<br /><br /> Separação de não - quando gerado em parâmetros de tipo|  
  
## <a name="cause"></a>Causa  
 O nome de um identificador contém o caractere de sublinhado (_).  
  
## <a name="rule-description"></a>Descrição da Regra  
 Por convenção, os nomes de identificador não contêm o caractere de sublinhado (_). A regra verifica namespaces, tipos, membros e parâmetros.  
  
 Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Remova todos os caracteres de sublinhado do nome.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima um aviso nessa regra.  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)  
  
 [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

