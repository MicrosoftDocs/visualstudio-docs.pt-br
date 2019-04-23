---
title: 'Como: Personalizar o dicionário de análise de código | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis dictionary
- custom dictionary, code analysis
- dictionary, code analysis
ms.assetid: 667e3b4e-beff-48be-b3d1-376e1716a895
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 26a9d65ed21eed00820a7968617c610e4b11c153
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60055672"
---
# <a name="how-to-customize-the-code-analysis-dictionary"></a>Como: Personalizar o dicionário de análise de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Análise de código usa um dicionário interno para verificar identificadores em seu código para erros de ortografia, caso gramatical e outras convenções de nomenclatura do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] diretrizes. Você pode criar um arquivo Xml de dicionário personalizado para adicionar, remover ou modificar os termos e abreviações acrônimos ao dicionário interno.  
  
 Por exemplo, suponha que seu código continha uma classe chamada **DoorKnokker**. Análise de código deve identificar o nome como um composto de duas palavras: **porta** e **knokker**. Ele gera um aviso que **knokker** não foi digitado corretamente. Para forçar a reconhecer a ortografia da análise de código, você pode adicionar o termo **knokker** ao dicionário personalizado.  
  
## <a name="to-create-a-custom-dictionary"></a>Para criar um dicionário personalizado  
 Crie um arquivo chamado **Customdictionary**.  
  
 Defina suas palavras personalizadas, usando a seguinte estrutura XML:  
  
```  
<Dictionary>  
      <Words>  
         <Unrecognized>  
            <Word>knokker</Word>  
         </Unrecognized>  
         <Recognized>  
            <Word></Word>  
         </Recognized>  
         <Deprecated>  
            <Term PreferredAlternate=""></Term>  
         </Deprecated>  
         <Compound>  
            <Term CompoundAlternate=""></Term>  
         </Compound>  
         <DiscreteExceptions>  
            <Term></Term>  
         </DiscreteExceptions>  
      </Words>  
      <Acronyms>  
         <CasingExceptions>  
            <Acronym></Acronym>  
         </CasingExceptions>  
      </Acronyms>  
   </Dictionary>  
```  
  
## <a name="custom-dictionary-elements"></a>Elementos do dicionário personalizado  
 Você pode modificar o comportamento do dicionário de análise de código, adicionando os termos de como o texto interno dos seguintes elementos no dicionário personalizado:  
  
- [Dictionary/Words/Recognized/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsRecognizedWord)  
  
- [Dictionary/Words/Unrecognized/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsUnrecognizedWord)  
  
- [Dictionary/Words/Deprecated/Term[@PreferredAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDeprecatedTermPreferredAlternate)  
  
- [Dictionary/Words/Compound/Term[@CompoundAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsCompoundTermCompoundAlternate)  
  
- [Dictionary/Words/DiscreteExceptions/Term](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDiscreteExceptionsTerm)  
  
- [Dictionary/Acronyms/CasingExceptions/Acronym](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryAcronymsCasingExceptionsAcronym)  
  
### <a name="BKMK_DictionaryWordsRecognizedWord"></a> Dicionário e palavras/reconhecido/de palavras  
 Para incluir um termo na lista de termos que identifica a análise de código como escrito corretamente, adicione o termo como o texto interno de um elemento do dicionário e palavras/reconhecido/de palavras. Termos de elementos do dicionário e palavras/reconhecido/de palavras não diferenciam maiusculas de minúsculas.  
  
 **Exemplo**  
  
```  
<Dictionary>  
      <Words>  
         <Recognized>  
            <Word>knokker</Word>  
            ...  
         </Recognized>  
         ...  
      </Words>  
      ...  
</Dictionary>  
  
```  
  
 Termos de dicionário/palavras/reconhecido nós são aplicados as seguintes regras de análise de código:  
  
- [CA1701: Palavras compostas da cadeia de caracteres de recurso devem ter maiusculas e minúsculas corretamente](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)  
  
- [CA1702: Palavras compostas devem ter maiusculas e minúsculas corretamente](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)  
  
- [CA1703: Cadeias de caracteres de recurso devem ter grafia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)  
  
- [CA1704: Identificadores devem ter grafia correta](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)  
  
- [CA1709: Identificadores devem ter maiusculas e minúsculas corretamente](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)  
  
- [CA1726: Use termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)  
  
- [CA2204: Literais devem ter grafia correta](../code-quality/ca2204-literals-should-be-spelled-correctly.md)  
  
### <a name="BKMK_DictionaryWordsUnrecognizedWord"></a> Dicionário e palavras/não reconhecida/de palavras  
 Para excluir um termo da lista de termos que identifica a análise de código como escrito corretamente, adicione o termo a ser excluído como o texto interno de um elemento do dicionário e palavras/não reconhecida/de palavras. Termos de elementos do dicionário e palavras/não reconhecida/de palavras não diferenciam maiusculas de minúsculas.  
  
 **Exemplo**  
  
```  
<Dictionary>  
      <Words>  
         <Unrecognized>  
            <Word>meth</Word>  
            ...  
         </Unrecognized>  
         ...  
      </Words>  
      ...  
</Dictionary>  
  
```  
  
 Termos no nó de dicionário/palavras/não reconhecida são aplicados as seguintes regras de análise de código:  
  
- [CA1701: Palavras compostas da cadeia de caracteres de recurso devem ter maiusculas e minúsculas corretamente](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)  
  
- [CA1702: Palavras compostas devem ter maiusculas e minúsculas corretamente](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)  
  
- [CA1703: Cadeias de caracteres de recurso devem ter grafia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)  
  
- [CA1704: Identificadores devem ter grafia correta](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)  
  
- [CA1709: Identificadores devem ter maiusculas e minúsculas corretamente](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)  
  
- [CA1726: Use termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)  
  
- [CA2204: Literais devem ter grafia correta](../code-quality/ca2204-literals-should-be-spelled-correctly.md)  
  
### <a name="BKMK_DictionaryWordsDeprecatedTermPreferredAlternate"></a> Dictionary/Words/Deprecated/Term[@PreferredAlternate]  
 Para incluir um termo na lista de termos que a análise de código identifica como preterido, adicione o termo como o texto interno de um elemento de dicionário/palavras/preterido/termo. Um termo reprovado é uma palavra que está escrita corretamente, mas não deve ser usada.  
  
 Para incluir um termo alternativo sugerido no aviso, especifique a alternativa no atributo PreferredAlternate do elemento de termo. Você pode deixar o valor do atributo vazio se não desejar sugerir uma alternativa.  
  
- O termo reprovado em palavras do dicionário/elemento obsoleto/termo não diferencia maiusculas de minúsculas.  
  
- O valor do atributo PreferredAlternate diferencia maiusculas de minúsculas. Use Pascal case para alternativas compostas.  
  
  **Exemplo**  
  
```  
<Dictionary>  
      <Words>  
         <Deprecated>  
            <Term PreferredAlternate="LogOn">login</Term>  
            ...  
         </Deprecated>  
         ...  
      </Words>  
      ...  
</Dictionary>  
  
```  
  
 Termos no nó de palavras/dicionário/preteridos são aplicados as seguintes regras de análise de código:  
  
- [CA1701: Palavras compostas da cadeia de caracteres de recurso devem ter maiusculas e minúsculas corretamente](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)  
  
- [CA1702: Palavras compostas devem ter maiusculas e minúsculas corretamente](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)  
  
- [CA1703: Cadeias de caracteres de recurso devem ter grafia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)  
  
- [CA1704: Identificadores devem ter grafia correta](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)  
  
- [CA1726: Use termos preferenciais](../code-quality/ca1726-use-preferred-terms.md)  
  
### <a name="BKMK_DictionaryWordsCompoundTermCompoundAlternate"></a> Dicionário/palavras/composta/termo [@CompoundAlternate]  
 O dicionário interno identifica alguns termos como termos simples e discretos, em vez de um termo composto. Para incluir um termo na lista de termos que a análise de código identifica como uma palavra composta e para especificar as maiusculas e minúsculas corretas do termo, adicione o termo como o texto interno de um elemento de dicionário/palavras/composta/termo. No atributo do elemento de termo CompoundAlternate, especifique as palavras individuais que compõem o termo composto, usando maiusculas para a primeira letra de palavras individuais (caso Pascal). Observe que o termo especificado no texto interno é automaticamente adicionado à lista de palavras/dicionário/DiscreteExceptions.  
  
- O termo reprovado em palavras do dicionário/elemento obsoleto/termo não diferencia maiusculas de minúsculas.  
  
- O valor do atributo PreferredAlternate diferencia maiusculas de minúsculas. Use Pascal case para alternativas compostas.  
  
  **Exemplo**  
  
```  
<Dictionary>  
      <Words>  
         <Compound>  
            <Term CompoundAlternate="CheckBox">checkbox</Term>  
            ...  
         </Compound>  
         ...  
      </Words>  
      ...  
</Dictionary>  
  
```  
  
 Termos no nó de palavras/dicionário/compostos são aplicados as seguintes regras de análise de código:  
  
- [CA1701: Palavras compostas da cadeia de caracteres de recurso devem ter maiusculas e minúsculas corretamente](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)  
  
- [CA1702: Palavras compostas devem ter maiusculas e minúsculas corretamente](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)  
  
- [CA1703: Cadeias de caracteres de recurso devem ter grafia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)  
  
- [CA1704: Identificadores devem ter grafia correta](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)  
  
### <a name="BKMK_DictionaryWordsDiscreteExceptionsTerm"></a> Dicionário/palavras/DiscreteExceptions/termo  
 Para excluir um termo na lista de termos que identifica de análise de código como um único, o word discreto quando o termo estiver marcado, as regras de maiusculas e minúsculas de palavras compostas, adicionar o termo como o texto interno de um elemento de dicionário/palavras/DiscreteExceptions/termo. O termo no elemento de dicionário/palavras/DiscreteExceptions/termo não diferencia maiusculas de minúsculas.  
  
 **Exemplo**  
  
```  
<Dictionary>  
      <Words>  
         <DiscreteExceptions>  
            <Term>checkbox</Term>  
            ...  
         </DiscreteExceptions>  
         ...  
      </Words>  
      ...  
</Dictionary>  
  
```  
  
 Termos no nó de palavras/dicionário/DiscreteExceptions são aplicados as seguintes regras de análise de código:  
  
- [CA1701: Palavras compostas da cadeia de caracteres de recurso devem ter maiusculas e minúsculas corretamente](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)  
  
- [CA1702: Palavras compostas devem ter maiusculas e minúsculas corretamente](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)  
  
### <a name="BKMK_DictionaryAcronymsCasingExceptionsAcronym"></a> Dicionário/acrônimos/CasingExceptions/acrônimo  
 Para incluir um acrônimo na lista de termos que a análise de código identifica como digitada corretamente e para indicar como o acrônimo quando o termo é marcado por maiusculas e minúsculas de regras para palavras compostas, adicionar o termo como o texto interno do dicionário/acrônimos/CasingExceptions / Elemento ACRONYM. O acrônimo entre o elemento de dicionário/acrônimos/CasingExceptions/acrônimo diferencia maiusculas de minúsculas.  
  
 **Exemplo**  
  
```  
<Dictionary>  
      <Acronyms>  
         <CasingExceptions>  
            <Acronym>NESW</Acronym>   <!-- North East South West -->  
            ...  
         </CasingExceptions>  
         ...  
      </Acronyms>  
      ...  
</Dictionary>  
  
```  
  
 Termos no nó de dicionário/acrônimos/CasingExceptions são aplicados as seguintes regras de análise de código:  
  
- [CA1709: Identificadores devem ter maiusculas e minúsculas corretamente](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)  
  
## <a name="BKMK_ToApplyACustomDictionaryToAProject"></a> Para aplicar um dicionário personalizado a um projeto  
  
1. Na **Gerenciador de soluções**, use um dos procedimentos a seguir:  
  
2. Para adicionar um dicionário para um único projeto, clique com botão direito no nome do projeto e, em seguida, clique em **Add Existing Item**. Especifique o arquivo na **Add Existing Item** caixa de diálogo.  
  
3. Para adicionar um dicionário que é compartilhado entre dois ou mais projetos, localize o arquivo para compartilhar na **Adicionar Item existente** caixa de diálogo, clique na seta para baixo na **Add** botão e, em seguida, clique em **adicionar como vínculo** .  
  
4. Na **Gerenciador de soluções**, clique com botão direito do **Customdictionary** nome de arquivo e clique em **propriedades**.  
  
5. Dos **ação de compilação** lista, selecione **CodeAnalysisDictionary**.  
  
6. Dos **Copy to Output Directory** lista, selecione **não copiar**.
