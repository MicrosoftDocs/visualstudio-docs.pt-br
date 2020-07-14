---
title: 'CA1704: os identificadores devem ser escritos corretamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
helpviewer_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
ms.assetid: f2c7a44d-1690-44ca-9cd0-681b04b12b2a
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b5e078fc1bb7fe247d541e7695e98c2de76c2466
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544060"
---
# <a name="ca1704-identifiers-should-be-spelled-correctly"></a>CA1704: Identificadores devem ser escritos corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|IdentifiersShouldBeSpelledCorrectly|
|CheckId|CA1704|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um identificador contém uma ou mais palavras que não são reconhecidas pela biblioteca do verificador ortográfico da Microsoft. Essa regra não verifica construtores ou membros com nomes especiais, como acessadores get e Set Property.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra analisa o identificador em tokens e verifica a ortografia de cada token. O algoritmo de análise executa as seguintes transformações:

- Letras maiúsculas iniciam um novo token. Por exemplo, MyNameIsJoe cria tokens para "My", "Name", "is", "Joe".

- Para várias letras maiúsculas, a última letra maiúscula inicia um novo token. Por exemplo, GUIEditor cria tokens para "GUI", "Editor".

- Apóstrofos à esquerda e à direita são removidos. Por exemplo, ' Sender ' cria tokens para "Sender".

- Sublinhados significam o final de um token e são removidos. Por exemplo, Hello_world cria tokens para "Olá", "mundo".

- Os e comercial inseridos são removidos. Por exemplo, para&passe-partout cria tokens para "Format".

  Por padrão, a versão em inglês (EN) do verificador ortográfico é usada. Nenhum outro dicionário de idiomas está disponível no momento.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, corrija a ortografia da palavra ou adicione a palavra a um dicionário personalizado chamado CustomDictionary.xml. Coloque o dicionário no diretório de instalação da ferramenta, no diretório do projeto ou no diretório que está associado à ferramenta sob o perfil do usuário (%USERPROFILE%\Application Data \\ ...). Para saber como adicionar o dicionário personalizado a um projeto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)

- Adicione palavras que não devem causar uma violação sob o dicionário/palavras/caminho reconhecido.

- Adicione palavras que devem causar uma violação sob o caminho/palavras/caminhos não reconhecidos.

- Adicione palavras que devem ser sinalizadas como obsoletas sob o caminho de dicionário/palavras/preterido. Consulte o tópico de regra relacionada [CA1726: usar os termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)para obter mais informações.

- Adicione exceções às regras de maiúsculas e minúsculas do acrônimo ao caminho Dictionary/acrônimos/CasingExceptions.

  Veja a seguir um exemplo da estrutura de um arquivo de dicionário personalizado.

```
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

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra somente se a palavra for intencionalmente digitada incorretamente e a palavra se aplicar a um conjunto limitado da biblioteca. Palavras escritas corretamente reduzem a curva de aprendizado necessária para novas bibliotecas de software.

## <a name="related-rules"></a>Regras relacionadas
 [CA2204: Literais devem ser escritos corretamente](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

 [CA1703: Cadeias de caracteres de recurso devem ser escritas corretamente](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

 [CA1709: Identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708: Identificadores devem ser diferentes em algo além das maiúsculas e minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707: Identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1726: Usar termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)

## <a name="see-also"></a>Consulte Também
 [Como personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)
