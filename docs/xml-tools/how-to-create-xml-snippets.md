---
title: 'Como: Crie snippets XML'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d8556dd7-1382-4af7-ba80-3e873c9416be
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b86962221dcdeff59b1152baf7b7cddcc55293e
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815390"
---
# <a name="how-to-create-xml-snippets"></a>Como: criar trechos XML

O editor de XML pode ser usado para criar novos trechos de código XML. O editor inclui um snippet XML, chamado “Snippets”, que é um snippet de texto constante para criar novos snippets XML.

## <a name="to-create-a-new-xml-snippet"></a>Para criar um novo snippet XML

Para criar um novo trecho de código XML, crie um novo arquivo XML e use o recurso **Inserir trecho** .

1. No menu **arquivo** , clique em **novo** e em **arquivo**.

2. Clique em **arquivo XML** e em **abrir**.

3. Clique com o botão direito do mouse no painel do editor e selecione **Inserir trecho de código**.

4. Selecione **trecho** na lista e pressione **Enter**.

5. Faça as alterações para o novo snippet.

6. No menu **arquivo** , selecione **salvar XMLFile.xml**.

     A caixa de diálogo **salvar arquivo como** é exibida.

7. Insira o nome para o novo trecho e selecione **arquivos de trecho** na janela suspensa **salvar como tipo** .

8. Use a lista suspensa **salvar na** para alterar o local do arquivo para a pasta *Meus Documentos\Visual Studio 2005 \ código Snippets\XML\My XML Snippets* e, em seguida, pressione **salvar**.

## <a name="snippet-description"></a>Descrição do trecho

Esta seção descreve alguns dos elementos-chave no snippet de texto constante. Para obter mais informações sobre elementos de esquema usados pelos trechos XML, consulte [referência de esquema de trechos de código](../ide/code-snippets-schema-reference.md).

### <a name="snippettype-element"></a>Elemento SnippetType

Suporte do editor dois tipos de snippet:

```xml
<SnippetTypes>
  <SnippetType>SurroundsWith</SnippetType>
  <SnippetType>Expansion</SnippetType>
</SnippetTypes>
```

O `Expansion` tipo determina se o trecho de código aparece quando você invoca o comando **Insert Snippet** . O `SurroundsWith` tipo determina se o trecho de código é exibido quando você invoca o comando **Circundar com** .

### <a name="code-element"></a>Elemento de código

O elemento de `Code` define o texto XML que será inserido quando o snippet é chamado.

> [!NOTE]
> O texto de snippet XML deve ser incluído em uma seção de `<![CDATA[...]]>` .

O seguinte é o elemento de `Code` que é criado pelo snippet de texto constante.

```xml
<Code Language="XML">
  <![CDATA[<test>
  <name>$name$</name>
  $selected$ $end$</test>]]>
</Code>
```

O elemento de `Code` inclui três variáveis.

- $name$ variável é definido pelo usuário. Cria um elemento de `name` , que tem um valor editável que usa padrão “para nomear”. As variáveis definidas pelo usuário são definidos usando o elemento de `Literal` .

- $selected$ é uma variável predefinido. Ele representa o texto que foi selecionado no editor de XML antes de invocar o trecho de código. O posicionamento dessa variável determina onde o texto selecionado aparece no snippet de código que circunda a seleção.

- $end$ é uma variável predefinido. Quando o usuário pressiona **Enter** para concluir a edição dos campos de trecho de código, essa variável determina para onde o cursor (^) é movido.

  O elemento acima de `Code` insira o seguinte texto XML:

```xml
<test>
  <name>name</name>
</test>
```

O valor do elemento de nome é marcado como uma região editável.

### <a name="literal-element"></a>Elemento Literal

O elemento de `Literal` é usado para identificar o texto de substituição que pode ser personalizada depois que é inserido no arquivo. Por exemplo, cadeias de caracteres literais, os valores numéricos, e alguns nomes de variável podem ser declarados como literais. Você pode definir qualquer número do snippet em literais XML e você pode referir-lhes várias vezes dentro de snippet. O código a seguir é um exemplo de um elemento de `Literal` que define um variável de $name$ cujo valor padrão é “nome”.

```xml
<Literal>
  <ID>name</ID>
  <Default>name</Default>
</Literal
```

Literais também podem se referir funções. O editor de XML inclui uma função chamada **LookupPrefix**. A função **LookupPrefix** pesquisa o URI de namespace fornecido do local no documento XML para o qual esse trecho é invocado e retorna o prefixo de namespace definido para esse namespace, se houver, e inclui os dois-pontos (:) nesse nome. Veja a seguir um exemplo de um `Literal` elemento que usa a função **LookupPrefix** .

```xml
<Literal Editable="false">
   <ID>prefix</ID>
   <Function>LookupPrefix("namespaceURI")</Function>
</Literal>
```

A variável de $prefix$ pode então ser usado em qualquer lugar no seu snippet XML.

## <a name="see-also"></a>Veja também

- [Snippets XML](../xml-tools/xml-snippets.md)
- [Como: usar trechos XML](../xml-tools/how-to-use-xml-snippets.md)
- [Como gerar um trecho XML a partir de um esquema XML](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)
