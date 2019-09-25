---
title: 'CA1704: Identificadores devem ser escritos corretamente'
ms.date: 03/28/2018
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa04ca237134c1947b5c58b921f87f32a1ecfb16
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234302"
---
# <a name="ca1704-identifiers-should-be-spelled-correctly"></a>CA1704: Identificadores devem ser escritos corretamente

|||
|-|-|
|NomeDoTipo|IdentifiersShouldBeSpelledCorrectly|
|CheckId|CA1704|
|Categoria|Microsoft.Naming|
|Alteração significativa|Quebra|

## <a name="cause"></a>Causa

O nome de um identificador contém uma ou mais palavras que não são reconhecidas pela biblioteca do verificador ortográfico da Microsoft. Essa regra não verifica construtores ou membros com nomes especiais, como acessadores get e Set Property.

## <a name="rule-description"></a>Descrição da regra

Essa regra analisa o identificador em tokens e verifica a ortografia de cada token. O algoritmo de análise executa as seguintes transformações:

- Letras maiúsculas iniciam um novo token. Por exemplo, MyNameIsJoe cria tokens para "My", "Name", "is", "Joe".

- Para várias letras maiúsculas, a última letra maiúscula inicia um novo token. Por exemplo, GUIEditor cria tokens para "GUI", "Editor".

- Apóstrofos à esquerda e à direita são removidos. Por exemplo, ' Sender ' cria tokens para "Sender".

- Sublinhados significam o final de um token e são removidos. Por exemplo, Hello_world cria tokens para "Olá", "mundo".

- Os e comercial inseridos são removidos. Por exemplo, para & passe-partout cria tokens para "Format".

## <a name="language"></a>Idioma

Atualmente, o verificador ortográfico verifica apenas os dicionários de cultura baseados em inglês. Você pode alterar a cultura do seu projeto no arquivo de projeto, adicionando o elemento **CodeAnalysisCulture** .

Por exemplo:

```xml
<Project ...>
  <PropertyGroup>
    <CodeAnalysisCulture>en-AU</CodeAnalysisCulture>
```

> [!IMPORTANT]
> Se você definir a cultura como algo diferente de uma cultura baseada em inglês, essa regra de análise de código será silenciosamente desabilitada.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, corrija a grafia da palavra ou adicione a palavra a um dicionário personalizado.

### <a name="to-add-words-to-a-custom-dictionary"></a>Para adicionar palavras a um dicionário personalizado

Nomeie o arquivo XML do dicionário personalizado *CustomDictionary. xml*. Coloque o dicionário no diretório de instalação da ferramenta, no diretório do projeto ou no diretório que está associado à ferramenta sob o perfil do usuário ( *%UserProfile%\Application Data\\...* ). Para saber como adicionar o dicionário personalizado a um projeto no Visual Studio, consulte [como: Personalize o dicionário](../code-quality/how-to-customize-the-code-analysis-dictionary.md)de análise de código.

- Adicione palavras que não devem causar uma violação sob o dicionário/palavras/caminho reconhecido.

- Adicione palavras que devem causar uma violação sob o caminho/palavras/caminhos não reconhecidos.

- Adicione palavras que devem ser sinalizadas como obsoletas sob o caminho de dicionário/palavras/preterido. Consulte o tópico [de regra relacionada CA1726: Use os termos](../code-quality/ca1726-use-preferred-terms.md) preferenciais para obter mais informações.

- Adicione exceções às regras de maiúsculas e minúsculas do acrônimo ao caminho Dictionary/acrônimos/CasingExceptions.

Veja a seguir um exemplo da estrutura de um arquivo de dicionário personalizado:

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

Suprimir um aviso dessa regra somente se a palavra for intencionalmente digitada incorretamente e a palavra se aplicar a um conjunto limitado da biblioteca. Palavras escritas corretamente reduzem a curva de aprendizado necessária para novas bibliotecas de software.

## <a name="related-rules"></a>Regras relacionadas

- [CA2204: Os literais devem ser escritos corretamente](../code-quality/ca2204-literals-should-be-spelled-correctly.md)
- [CA1703: As cadeias de caracteres de recurso devem ser digitadas corretamente](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
- [CA1709: Os identificadores devem estar em maiúsculas e minúsculas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708: Os identificadores devem ser diferentes em mais do que caso](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
- [CA1707: Identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)
- [CA1726: Usar termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)

## <a name="see-also"></a>Consulte também

- [Como: personalizar o dicionário da Análise de Código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)
