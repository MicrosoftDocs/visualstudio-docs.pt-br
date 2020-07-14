---
title: 'CA1709: os identificadores devem estar em maiúsculas e minúsculas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldBeCasedCorrectly
- CA1709
helpviewer_keywords:
- CA1709
- IdentifiersShouldBeCasedCorrectly
ms.assetid: f633d1a7-4ca4-40ae-b207-ec571c5fb083
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 14c50ed94f05401cc5575af9f8b98472c35b261d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543995"
---
# <a name="ca1709-identifiers-should-be-cased-correctly"></a>CA1709: Identificadores devem ter maiúsculas e minúsculas corretas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente sobre o Visual Studio, consulte [CA1709: os identificadores devem estar em maiúsculas e minúsculas](/visualstudio/code-quality/ca1709-identifiers-should-be-cased-correctly).

|Item|Valor|
|-|-|
|TypeName|IdentifiersShouldBeCasedCorrectly|
|CheckId|CA1709|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra-quando gerado em assemblies, namespaces, tipos, membros e parâmetros.<br /><br /> Não separável-quando acionado em parâmetros de tipo genérico.|

## <a name="cause"></a>Causa
 O nome de um identificador não está em maiúsculas corretamente.

 \- ou –

 O nome de um identificador contém um acrônimo de duas letras e a segunda letra é minúscula.

 \- ou –

 O nome de um identificador contém um acrônimo de três ou mais letras maiúsculas.

## <a name="rule-description"></a>Descrição da Regra
 As convenções de nomenclatura fornecem uma aparência comum para as bibliotecas direcionadas ao Common Language Runtime. Isso reduz a curva de aprendizado necessária para novas bibliotecas de software e aumenta a confiança do cliente de que a biblioteca foi desenvolvida por alguém que tenha experiência no desenvolvimento de código gerenciado.

 Por convenção, os nomes de parâmetro usam a capitalização de Camel; namespace, tipo e nomes de membro usam maiúsculas e minúsculas do Pascal. Em um nome de camel case, a primeira letra é minúscula e a primeira letra de qualquer palavra restante no nome está em letras maiúsculas. Exemplos de nomes de camel case são "packetSniffer", "ioFile" e "fatalErrorCode". Em um nome em Pascal, a primeira letra é maiúscula e a primeira letra das palavras restantes no nome está em letras maiúsculas. Exemplos de nomes de Pascal-case são "PacketSniffer", "IOFile" e "FatalErrorCode".

 Essa regra divide o nome em palavras com base na capitalização e verifica quaisquer palavras de duas letras em uma lista de palavras de duas letras comuns, como "in" ou "My". Se uma correspondência não for encontrada, presume-se que a palavra seja um acrônimo. Além disso, essa regra pressupõe que ela encontrou um acrônimo quando o nome contém quatro letras maiúsculas em uma linha ou três letras maiúsculas em uma linha no final do nome.

 Por convenção, os acrônimos de duas letras usam todas as letras maiúsculas e os acrônimos de três ou mais caracteres usam a capitalização de Pascal. Os exemplos a seguir usam essa Convenção de nomenclatura: ' DB ', ' CR ', ' contador ' e ' ECMA '. Os exemplos a seguir violam a Convenção: ' Io ', ' XML ' e ' DoD ' e para nomes de não parâmetros, ' XP ' e ' CPL '.

 ' ID ' é especial para causar uma violação dessa regra. ' ID ' não é um acrônimo, mas é uma abreviação para ' identificação '.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Altere o nome para que ele esteja em maiúsculas e minúsculas.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir esse aviso se você tiver suas próprias convenções de nomenclatura ou se o identificador representar um nome adequado, por exemplo, o nome de uma empresa ou uma tecnologia.

 Você também pode adicionar termos, abreviações e acrônimos específicos a um dicionário personalizado de análise de código. Os termos especificados no dicionário personalizado não causarão violações dessa regra. Para obter mais informações, consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)

## <a name="related-rules"></a>Regras relacionadas
 [CA1708: Identificadores devem ser diferentes em algo além das maiúsculas e minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
