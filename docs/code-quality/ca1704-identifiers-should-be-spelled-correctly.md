---
title: 'CA1704: os identificadores do recurso devem ter a ortografia correta'
ms.date: 03/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
helpviewer_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
ms.assetid: f2c7a44d-1690-44ca-9cd0-681b04b12b2a
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 710e18f4ce8199c76c34683c510d3a64160544e6
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31916887"
---
# <a name="ca1704-identifiers-should-be-spelled-correctly"></a>CA1704: os identificadores do recurso devem ter a ortografia correta

|||
|-|-|
|NomeDoTipo|IdentifiersShouldBeSpelledCorrectly|
|CheckId|CA1704|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

O nome de um identificador contém uma ou mais palavras que não são reconhecidas pela biblioteca do verificador ortográfico do Microsoft. Esta regra não Verifique construtores ou membros denominado especial, como get e definir acessadores de propriedade.

## <a name="rule-description"></a>Descrição da regra

Esta regra analisa o identificador em tokens e verifica a ortografia de cada token. O algoritmo de análise executa as transformações a seguir:

- Letras maiusculas iniciar um novo token. Por exemplo, MyNameIsJoe cria tokens "Meu", "Name", "É", "Joe".

- Para várias letras maiusculas, a última letra maiuscula inicia um novo token. Por exemplo, GUIEditor cria tokens para "GUI", "Editor".

- À esquerda e à direita apóstrofos são removidos. Por exemplo, 'remetente' cria tokens para "sender".

- Sublinhados significam o final de um token em são removidos. Por exemplo, Hello_world cria tokens para "Hello", "world".

- E comercial inseridos é removidos. Por exemplo, para & mat cria tokens para "Formatar".

## <a name="language"></a>Idioma

O verificador ortográfico verifica atualmente apenas em dicionários de cultura baseada em inglês. Você pode alterar a cultura do seu projeto no arquivo de projeto, adicionando o **CodeAnalysisCulture** elemento.

Por exemplo:

```xml
<Project ...>
  <PropertyGroup>
    <CodeAnalysisCulture>en-AU</CodeAnalysisCulture>
```

> [!IMPORTANT]
> Se você definir a cultura para algo diferente de uma cultura baseada em inglês, esta regra de análise de código silenciosamente está desabilitada.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação desta regra, corrija a ortografia da palavra ou adicionar a palavra ao dicionário personalizado.

### <a name="to-add-words-to-a-custom-dictionary"></a>Para adicionar palavras a um dicionário personalizado

Nomeie o arquivo XML de dicionário personalizado *CustomDictionary.xml*. Coloque o dicionário no diretório de instalação da ferramenta, o diretório do projeto, ou no diretório que está associado com a ferramenta de perfil do usuário (*%USERPROFILE%\Application\\...* ). Para aprender a adicionar dicionário personalizado a um projeto no Visual Studio, consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md).

- Adicione palavras que não devem causar uma violação no caminho palavras/dicionário/reconhecido.

- Adicione palavras que poderiam causar uma violação no caminho de dicionário/palavras/não reconhecida.

- Adicione palavras que devem ser sinalizadas como obsoletos no caminho palavras/dicionário/preterido. Consulte o tópico relacionado regra [CA1726: usar termos preferenciais](../code-quality/ca1726-use-preferred-terms.md) para obter mais informações.

- Adicione exceções às regras de maiusculas e minúsculas acrônimo para o caminho de acrônimos/dicionário/CasingExceptions.

Este é um exemplo da estrutura de um arquivo de dicionário personalizado:

```xml
<Dictionary>
   <Words>
      <Unrecognized>
         <Word>cb</Word>
      </Unrecognized>
      <Recognized>
         <Word>stylesheet</Word>
         <Word>GotDotNet</Word>
      </Recognized>
      <Deprecated>
         <Term PreferredAlternate="EnterpriseServices">ComPlus</Term>
      </Deprecated>
   </Words>
   <Acronyms>
      <CasingExceptions>
         <Acronym>CJK</Acronym>
         <Acronym>Pi</Acronym>
      </CasingExceptions>
   </Acronyms>
</Dictionary>
```

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprima um aviso dessa regra somente se a palavra é intencionalmente incorreta e o word aplica-se a um conjunto limitado de biblioteca. Corretamente palavras reduzem a curva de aprendizado que é necessária para novas bibliotecas de software.

## <a name="related-rules"></a>Regras relacionadas

- [CA2204: os literais devem ter a ortografia correta](../code-quality/ca2204-literals-should-be-spelled-correctly.md)
- [CA1703: as cadeias de caracteres do recurso devem ter a ortografia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
- [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
- [CA1707: os identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)
- [CA1726: usar termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)

## <a name="see-also"></a>Consulte também

- [Como personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)
