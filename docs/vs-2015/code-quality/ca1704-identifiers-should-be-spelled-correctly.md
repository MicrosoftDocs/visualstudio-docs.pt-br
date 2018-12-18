---
title: 'CA1704: Os identificadores devem ter grafia correta | Microsoft Docs'
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
- CA1704
- IdentifiersShouldBeSpelledCorrectly
helpviewer_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
ms.assetid: f2c7a44d-1690-44ca-9cd0-681b04b12b2a
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c1e31917356e3d55a7db38ba7aabc9258af1deb0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49827518"
---
# <a name="ca1704-identifiers-should-be-spelled-correctly"></a>CA1704: os identificadores do recurso devem ter a ortografia correta
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|IdentifiersShouldBeSpelledCorrectly|
|CheckId|CA1704|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um identificador contém uma ou mais palavras não reconhecidas pela biblioteca do verificador ortográfico da Microsoft. Essa regra não Verifique construtores ou membros de chamada em especial, como obter e definir acessadores de propriedade.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra analisa o identificador em tokens e verifica a ortografia de cada token. O algoritmo de análise executa as seguintes transformações:

- Letras maiusculas iniciar um novo token. Por exemplo, MyNameIsJoe cria tokens "Meu", "Name", "Is", "Joe".

- Para várias letras maiusculas, a última letra maiuscula inicia um novo token. Por exemplo, GUIEditor cria tokens para "GUI", "Editor".

- À esquerda e à direita apóstrofos são removidos. Por exemplo, 'remetente' cria tokens para "sender".

- Sublinhados significam o final de um token em são removidos. Por exemplo, Hello_world cria tokens para "Hello", "world".

- E comercial inseridos é removidos. Por exemplo, para & mat cria tokens para "formato".

  Por padrão, a versão em inglês (en) do verificador ortográfico é usada. Não há outros dicionários de idioma estão disponíveis atualmente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, corrija a grafia da palavra ou adicionar a palavra a um dicionário personalizado chamado Customdictionary. Coloque o dicionário no diretório de instalação da ferramenta, o diretório do projeto, ou no diretório que está associado com a ferramenta sob o perfil do usuário (%USERPROFILE%\Application dados\\...). Para saber como adicionar um dicionário personalizado a um projeto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)

- Adicione palavras que não devem causar uma violação no caminho de dicionário/palavras/reconhecido.

- Adicione palavras que devem causar uma violação no caminho de dicionário/palavras/não reconhecida.

- Adicione palavras que devem ser sinalizadas como obsoletas no caminho de dicionário/palavras/preterido. Consulte o tópico relacionado regra [CA1726: usar termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)para obter mais informações.

- Adicione exceções às regras de maiusculas e minúsculas acrônimo para o caminho de dicionário/acrônimos/CasingExceptions.

  O exemplo a seguir é um exemplo da estrutura de um arquivo de dicionário personalizado.

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
 Suprima um aviso nessa regra somente se a palavra está intencionalmente incorreta e o word aplica-se a um conjunto limitado de biblioteca. Corretamente as palavras escritas de reduzem a curva de aprendizado que é necessária para novas bibliotecas de software.

## <a name="related-rules"></a>Regras relacionadas
 [CA2204: os literais devem ter a ortografia correta](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

 [CA1703: as cadeias de caracteres do recurso devem ter a ortografia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

 [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707: os identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1726: usar termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)

## <a name="see-also"></a>Consulte também
 [Como personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md)



