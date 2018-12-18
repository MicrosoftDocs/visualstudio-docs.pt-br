---
title: 'CA1702: Palavras compostas devem ter maiusculas e minúsculas corretamente | Microsoft Docs'
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
- CA1702
- CompoundWordsShouldBeCasedCorrectly
helpviewer_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
ms.assetid: 05481245-7ad8-48c3-a456-3aa44b6160a6
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: cfc723e94b8be2f427be7b42d676218b0d9aa68d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49201117"
---
# <a name="ca1702-compound-words-should-be-cased-correctly"></a>CA1702: palavras compostas devem ter maiúsculas e minúsculas corretas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA1702: palavras compostas devem ter maiusculas e minúsculas corretamente](https://docs.microsoft.com/visualstudio/code-quality/ca1702-compound-words-should-be-cased-correctly) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|CompoundWordsShouldBeCasedCorrectly|  
|CheckId|CA1702|  
|Categoria|Microsoft.Naming|  
|Alteração Significativa|Quebra quando acionado em assemblies.<br /><br /> Sem quebra - quando disparado em parâmetros de tipo.|  
  
## <a name="cause"></a>Causa  
 O nome de um identificador contém várias palavras e pelo menos uma das palavras parece ser uma palavra composta que não é maiusculas e minúsculas corretas.  
  
## <a name="rule-description"></a>Descrição da Regra  
 O nome do identificador é dividido em palavras que são baseadas em maiusculas. Cada combinação de duas palavras contígua é verificada pela biblioteca do verificador ortográfico da Microsoft. Se ele for reconhecido, o identificador produz uma violação da regra. São exemplos de palavras compostas que fazem com que uma violação "CheckSum" e "MultiPart", que deve ter maiusculas e minúsculas como "Checksum" e "Multipart", respectivamente. Devido ao uso anterior de comuns, várias exceções são incorporadas a regra e várias palavras únicas são sinalizadas, como "Ferramentas" e "Filename", que deve ter a grafia duas palavras distintas (nesse caso, "Ferramentas" e "FileName").  
  
 Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Altere o nome, de modo que ele é maiusculas e minúsculas corretas.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 É seguro suprimir um aviso nessa regra, se ambas as partes da palavra composta são reconhecidas pelo dicionário de ortografia e a intenção é usar duas palavras.  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA1701: as palavras compostas da cadeia de caracteres de recurso devem ter maiúsculas e minúsculas corretas](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)  
  
 [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)  
  
 [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)  
  
## <a name="see-also"></a>Consulte também  
 [Diretrizes de nomenclatura](http://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)   
 [Convenções de maiúsculas e minúsculas](http://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)

