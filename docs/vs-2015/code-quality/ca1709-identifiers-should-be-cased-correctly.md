---
title: 'CA1709: Os identificadores devem ter maiusculas e minúsculas corretamente | Microsoft Docs'
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
- IdentifiersShouldBeCasedCorrectly
- CA1709
helpviewer_keywords:
- CA1709
- IdentifiersShouldBeCasedCorrectly
ms.assetid: f633d1a7-4ca4-40ae-b207-ec571c5fb083
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 795bf9c307862195cd9ec70bb2de1f89ca4d1e17
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49199544"
---
# <a name="ca1709-identifiers-should-be-cased-correctly"></a>CA1709: os identificadores do recurso devem ter maiúsculas e minúsculas corretas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA1709: os identificadores devem ter maiusculas e minúsculas corretamente](https://docs.microsoft.com/visualstudio/code-quality/ca1709-identifiers-should-be-cased-correctly) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|IdentifiersShouldBeCasedCorrectly|  
|CheckId|CA1709|  
|Categoria|Microsoft.Naming|  
|Alteração Significativa|Quebrando - quando gerado em assemblies, namespaces, tipos, membros e parâmetros.<br /><br /> Sem quebra - quando disparado em parâmetros de tipo genérico.|  
  
## <a name="cause"></a>Causa  
 O nome de um identificador não é maiusculas e minúsculas corretas.  
  
 \- ou -  
  
 O nome de um identificador contém um acrônimo de duas letras e a segunda letra é minúscula.  
  
 \- ou -  
  
 O nome de um identificador contém um acrônimo de três ou mais letras maiusculas.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.  
  
 Por convenção, nomes de parâmetro usam o camel casing; nomes de namespace, tipo e membro usar Pascal casing. Em um nome em camel case, a primeira letra é minúscula e a primeira letra de qualquer palavras restantes no nome está em letras maiusculas. Exemplos de nomes em camel case são "packetSniffer", "ioFile" e "fatalErrorCode". Em um nome padrão Pascal-case, a primeira letra é maiuscula e a primeira letra de qualquer palavras restantes no nome está em letras maiusculas. Exemplos de nomes padrão Pascal-case são "PacketSniffer", "IOFile" e "FatalErrorCode".  
  
 Essa regra divide o nome em palavras com base nas maiusculas e minúsculas e verifica todas as palavras duas letras em relação a uma lista de palavras comuns de duas letras, como "In" ou "My". Se uma correspondência não for encontrada, a palavra é considerada um acrônimo. Além disso, esta regra pressupõe que ele encontrou um acrônimo quando o nome contém quatro letras maiusculas em uma linha ou três letras maiusculas em uma linha no final do nome.  
  
 Por convenção, os acrônimos de duas letras usam todas as letras maiusculas e acrônimos de três ou mais caracteres Pascal casing. Os exemplos a seguir usam esta convenção de nomenclatura: 'DB', 'CR', 'Cpa' e 'Ecma'. Os exemplos a seguir violam a convenção: ' E/s', 'XML' e 'DoD' e para nomes de nonparameter, 'xp' e 'cpl'.  
  
 'ID' é de maiusculas e minúsculas especiais para causar uma violação dessa regra. 'Id' não é um acrônimo, mas é uma abreviação para 'identificação'.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Altere o nome, de modo que ele é maiusculas e minúsculas corretas.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 É seguro suprimir este aviso se você tiver suas próprias convenções de nomenclatura, ou se o identificador representa um nome apropriado, por exemplo, o nome de uma empresa ou uma tecnologia.  
  
 Você também pode adicionar termos específicos, as abreviações e acrônimos que a um dicionário personalizado de análise de código. Termos especificados no dicionário personalizado não fará com que as violações dessa regra. Para obter mais informações, consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

