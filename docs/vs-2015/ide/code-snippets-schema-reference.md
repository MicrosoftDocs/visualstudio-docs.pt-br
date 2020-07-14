---
title: Referência de esquema de snippets de código | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- schema reference [Visual Studio]
- snippets [Visual Studio], schema reference
- code snippets [Visual Studio], schema reference
- IntelliSense Code Snippets, XML Schema
ms.assetid: 58a60621-725f-4763-93b7-62ea5424ef88
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 67bc1a18b4e4cbfdf69fe917c0d0fdff09832983
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545022"
---
# <a name="code-snippets-schema-reference"></a>Referência de esquema dos snippets de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os Snippets de Código IntelliSense são partes de código pré-criadas que estão prontas para serem inseridas no seu aplicativo com o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Você pode aumentar a produtividade fornecendo snippets de código que reduzem a quantidade de tempo gasto digitando código repetitivo ou procurando exemplos. É possível usar o esquema XML do Snippet de Código IntelliSense para criar seus próprios snippets de código e adicioná-los aos snippets de código que o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] já contém.

## <a name="intellisense-code-snippets-schema-elements"></a>Elementos do esquema de Snippets de Código IntelliSense

|Elemento|Elemento|Elemento|
|-|-|-|
|[Elemento Assembly](../ide/code-snippets-schema-reference.md#assembly)|[Elemento HelpUrl](../ide/code-snippets-schema-reference.md#helpurl)|[Elemento References](../ide/code-snippets-schema-reference.md#references)|
|[Elemento Author](../ide/code-snippets-schema-reference.md#author)|[Elemento ID](../ide/code-snippets-schema-reference.md#id)|[Elemento Shortcut](../ide/code-snippets-schema-reference.md#shortcut)|
|[Elemento de código](../ide/code-snippets-schema-reference.md#code)|[Importar elemento](../ide/code-snippets-schema-reference.md#import)|[Elemento Snippet](../ide/code-snippets-schema-reference.md#snippet)|
|[Elemento CodeSnippet](../ide/code-snippets-schema-reference.md#codesnippet)|[Elemento Imports](../ide/code-snippets-schema-reference.md#imports)|[Elemento SnippetType](../ide/code-snippets-schema-reference.md#snippettype)|
|[Elemento CodeSnippets](../ide/code-snippets-schema-reference.md#codesnippets)|[Elemento keyword](../ide/code-snippets-schema-reference.md#keyword)|[Elemento trechos](../ide/code-snippets-schema-reference.md#snippettypes)|
|[Elemento Declarations](../ide/code-snippets-schema-reference.md#declarations)|[Elemento Keywords](../ide/code-snippets-schema-reference.md#keywords)|[Elemento title](../ide/code-snippets-schema-reference.md#title)|
|[Elemento Default](../ide/code-snippets-schema-reference.md#default)|[Elemento Literal](../ide/code-snippets-schema-reference.md#literal)|[Elemento ToolTip](../ide/code-snippets-schema-reference.md#tooltip)|
|[Elemento Description](../ide/code-snippets-schema-reference.md#description)|[Elemento Namespace](../ide/code-snippets-schema-reference.md#namespace)|[Elemento Type](../ide/code-snippets-schema-reference.md#type)|
|[Elemento Function](../ide/code-snippets-schema-reference.md#function)|[Elemento Object](../ide/code-snippets-schema-reference.md#object)|[Elemento URL](../ide/code-snippets-schema-reference.md#url)|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|[Elemento Reference](../ide/code-snippets-schema-reference.md#reference)||

## <a name="assembly-element"></a><a name="assembly"></a>Elemento assembly
 Especifica o nome do assembly referenciado pelo snippet de código.

> [!NOTE]
> O elemento `Assembly` tem suporte apenas de snippets de código Visual Basic.

 O valor de texto do elemento **Assembly** é o nome de texto amigável do assembly, como `System.dll`, ou seu nome forte, como `System,Version=1.0.0.1,Culture=neutral,PublicKeyToken=9b35aa323c18d4fb1`.

```xml
<Assembly>
    AssemblyName
</Assembly>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Reference](../ide/code-snippets-schema-reference.md#reference)|Contém informações sobre referências de assembly exigidas pelo snippet de código.|

 Um valor de texto é obrigatório. Esse texto especifica o assembly ao qual o snippet de código faz referência.

## <a name="author-element"></a><a name="author"></a> Elemento Author
 Especifica o nome do autor do snippet. O **Gerenciador de Snippets de Código** exibe o nome armazenado no elemento `Author` do snippet de código.

```xml
<Author>
   Code Snippet Author
</Author>

```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Contém informações gerais sobre o snippet de código.|

 Um valor de texto é obrigatório. Esse texto especifica o autor do snippet de código.

## <a name="code-element"></a>Elemento de código <a name="code"></a>
 Fornece um contêiner para blocos de códigos curtos.

 Duas palavras reservadas estão disponíveis para uso no texto do elemento `Code`: `$end$` e `$selected$`. `$end$` marca o local para colocar o cursor depois que o snippet de código é inserido. `$selected$` representa o texto selecionado no documento que deve ser inserido no snippet quando ele é invocado. Por exemplo, dado um snippet que inclui:

```xml
$selected$ is a great color.
```

 Se a palavra "Blue" for selecionada, quando o usuário invoca o modelo, o resultado é:

```xml
Blue is a great color.
```

 Você não pode usar o `$end$` ou `$selected$` mais de uma vez em um snippet de código. Nesse caso, apenas a segunda instância é reconhecida. Dado um snippet que inclui:

```
$selected$ is a great color. I love $selected$.
```

 Se a palavra "Blue" for selecionada, o resultado é:

```
is a great color. I love Blue.
```

 O espaço inicial aparece porque há um espaço entre `$selected$` e `is`.

 Todas as outras palavras-chave `$` são dinamicamente definidas nas marcas `<Literal>` e `<Object>`.

```xml
<Code Language="Language"
    Kind="method body/method decl/type decl/page/file/any"
    Delimiter="Delimiter">
    Code to insert
</Code>
```

|Atributo|Descrição|
|---------------|-----------------|
|`Delimiter`|Atributo opcional. Especifica o delimitador usado para descrever os literais e os objetos no código. Por padrão, o delimitador é `$`.|
|`Kind`|Atributo opcional. Especifica o tipo de código que o snippet contém e o local em que um snippet de código deve ser inserido para compilação. Os valores disponíveis são `method body`, `method decl`, `type decl`, `file` e `any`.|
|`Language`|Atributo obrigatório. Especifica a linguagem do snippet de código.|

|Valor do atributo do tipo|Descrição|
|--------------------------|-----------------|
|`method body`|Especifica que o snippet de código é um corpo de método e, portanto, deve ser inserido em uma declaração de método.|
|`method decl`|Especifica que o snippet de código é um método e, portanto, deve ser inserido em uma classe ou um módulo.|
|`type decl`|Especifica que o snippet de código é um tipo e, portanto, deve ser inserido em uma classe, um módulo ou um namespace.|
|`file`|Especifica que o snippet é um arquivo de código completo. Esses snippets de código podem ser inseridos sozinhos em um arquivo de código ou dentro de um namespace.|
|`any`|Especifica que o snippet pode ser inserido em qualquer lugar. Essa marca é usada para snippets de código que não dependem de contexto, como os comentários.|

|Valor do atributo da linguagem|Descrição|
|------------------------------|-----------------|
|`VB`|Identifica um snippet de código Visual Basic.|
|`CSharp`|Identifica um snippet de código C#.|
|`CPP`|Identifica um snippet de código C++.|
|`XML`|Identifica um snippet de código XML.|
|`JavaScript`|Identifica um snippet de código JavaScript.|
|`SQL`|Identifica um snippet de código SQL.|
|`HTML`|Identifica um snippet de código HTML.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Snippet](../ide/code-snippets-schema-reference.md#snippet)|Contém as referências, as importações, as declarações e o código do snippet de código.|

 Um valor de texto é obrigatório. Esse texto especifica o código, juntamente como os literais e objetos, que você pode usar quando esse snippet de código é inserido em um projeto.

## <a name="codesnippet-element"></a><a name="codesnippet"></a>Elemento CodeSnippet
 Permite que você especifique um título e vários Snippets de Código IntelliSense, que podem ser inseridos em arquivos de código do Visual Studio.

```xml
<CodeSnippet Format="x.x.x">
    <Header>... </Header>
    <Snippet>... </Snippet>
</CodeSnippet>

```

|Atributo|Descrição|
|---------------|-----------------|
|`Format`|Atributo obrigatório. Especifica a versão do esquema do snippet de código. O atributo Format deve ser uma cadeia de caracteres na sintaxe x.x.x, em que cada "x" representa um valor numérico do número da versão. O Visual Studio vai ignorar snippets de código com atributos `Format` que ele não entende.|

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Elemento necessário. Contém informações gerais sobre o snippet de código. Deve haver exatamente um elemento `Header` em um snippet de código.|
|[Elemento Snippet](../ide/code-snippets-schema-reference.md#snippet)|Elemento necessário. Contém o código que será inserido pelo Visual Studio. Deve haver exatamente um elemento `Snippet` em um snippet de código.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento CodeSnippets](../ide/code-snippets-schema-reference.md#codesnippets)|Elemento raiz do esquema XML do snippet de código.|

## <a name="codesnippets-element"></a><a name="codesnippets"></a>Elemento trechos
 Agrupa elementos [CodeSnippet Element](../ide/code-snippets-schema-reference.md#codesnippet). O elemento `CodeSnippets` é o elemento raiz do esquema XML do snippet de código.

```xml
<CodeSnippets>
    <CodeSnippet>... </CodeSnippet>
</CodeSnippets>

```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento CodeSnippet](../ide/code-snippets-schema-reference.md#codesnippet)|Elemento opcional. Elemento pai de todos os dados do snippet de código. Pode ser que não haja nenhum ou mais de um elemento `CodeSnippet` em um elemento `CodeSnippets`.|

## <a name="declarations-element"></a><a name="declarations"></a>Elemento Declarations
 Especifica os literais e os objetos que compõem as partes de um snippet de código que você pode editar.

```xml
<Declarations>
    <Literal>... </Literal>
    <Object>... </Object>
</Declarations>

```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Literal](../ide/code-snippets-schema-reference.md#literal)|Elemento opcional. Define os literais do snippet de código que você pode editar. Pode ser que não haja nenhum ou mais de um elemento `Literal` em um elemento `Declarations`.|
|[Elemento Object](../ide/code-snippets-schema-reference.md#object)|Elemento opcional. Define os objetos do snippet de código que você pode editar. Pode ser que não haja nenhum ou mais de um elemento `Object` em um elemento `Declarations`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Snippet](../ide/code-snippets-schema-reference.md#snippet)|Contém as referências, as importações, as declarações e o código do snippet de código.|

## <a name="default-element"></a><a name="default"></a>Elemento padrão
 Especifica o valor padrão do literal ou do objeto para um Snippet de Código IntelliSense.

```xml
<Default>
    Default value
</Default>

```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Literal](../ide/code-snippets-schema-reference.md#literal)|Define os campos de literal do snippet de código que você pode editar.|
|[Elemento Object](../ide/code-snippets-schema-reference.md#object)|Define os campos de objeto do snippet de código que você pode editar.|

 Um valor de texto é obrigatório. Esse texto especifica o valor padrão do literal ou do objeto que preenche os campos do snippet de código que você pode editar.

## <a name="description-element"></a><a name="description"></a>Elemento Description
 Especifica as informações descritivas sobre o conteúdo de um Snippet de Código IntelliSense.

```xml
<Description>
    Code Snippet Description
</Description>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Contém informações gerais sobre o snippet de código.|

 Um valor de texto é obrigatório. Esse texto descreve o snippet de código.

## <a name="function-element"></a><a name="function"></a>Elemento Function
 Especifica uma função a ser executada quando o literal ou o objeto receber foco no Visual Studio.

> [!NOTE]
> O elemento `Function` tem suporte somente em snippets de código Visual C#.

```xml
<Function>
    FunctionName
</Function>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Literal](../ide/code-snippets-schema-reference.md#literal)|Define os campos de literal do snippet de código que você pode editar.|
|[Elemento Object](../ide/code-snippets-schema-reference.md#object)|Define os campos de objeto do snippet de código que você pode editar.|

 Um valor de texto é obrigatório. Esse texto especifica uma função a ser executada quando o campo de literal ou objeto recebe foco no Visual Studio.

## <a name="header-element"></a><a name="header"></a>Elemento Header
 Especifica informações gerais sobre o Snippet de Código IntelliSense.

```xml
<Header>
    <Title>... </Title>
    <Author>... </Author>
    <Description>... </Description>
    <HelpUrl>... </HelpUrl>
    <SnippetTypes>... </SnippetTypes>
    <Keywords>... </Keywords>
    <Shortcut>... </Shortcut>
</Header>

```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Author](../ide/code-snippets-schema-reference.md#author)|Elemento opcional. O nome da pessoa ou da empresa que criou o snippet de código. Pode ser que não haja nenhum ou um elemento `Author` em um elemento `Header`.|
|[Elemento Description](../ide/code-snippets-schema-reference.md#description)|Elemento opcional. Uma descrição do snippet de código. Pode ser que não haja nenhum ou um elemento `Description` em um elemento `Header`.|
|[Elemento HelpUrl](../ide/code-snippets-schema-reference.md#helpurl)|Elemento opcional. Uma URL que contém mais informações sobre o snippet de código. Pode ser que não haja nenhum ou um elemento `HelpURL` em um elemento Header. **Observação:** o Visual Studio não usa o elemento `HelpUrl`. O elemento faz parte do esquema XML do Snippet de Código IntelliSense e qualquer snippet de código que contenha o elemento será válido, mas o valor do elemento nunca será usado.|
|[Elemento Keywords](../ide/code-snippets-schema-reference.md#keywords)|Elemento opcional. Agrupa elementos `Keyword`. Pode ser que não haja nenhum ou um elemento `Keywords` em um elemento `Header`.|
|[Elemento Shortcut](../ide/code-snippets-schema-reference.md#shortcut)|Elemento opcional. Especifica o texto de atalho que pode ser usado para inserir o snippet. Pode ser que não haja nenhum ou um elemento `Shortcut` em um elemento `Header`.|
|[Elemento trechos](../ide/code-snippets-schema-reference.md#snippettypes)|Elemento opcional. Agrupa elementos `SnippetType`. Pode ser que não haja nenhum ou um elemento `SnippetTypes` em um elemento `Header`. Se não houver nenhum elemento `SnippetTypes`, o snippet de código sempre será válido.|
|[Elemento title](../ide/code-snippets-schema-reference.md#title)|Elemento necessário. O nome amigável do snippet de código. Deve haver exatamente um elemento `Title` em um elemento `Header`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento CodeSnippet](../ide/code-snippets-schema-reference.md#codesnippet)|Elemento pai de todos os dados do snippet de código.|

## <a name="helpurl-element"></a><a name="helpurl"></a>Elemento HelpUrl
 Especifica uma URL que fornece mais informações sobre um snippet de código.

> [!NOTE]
> O Visual Studio não usa o elemento `HelpUrl`. O elemento faz parte do esquema XML do Snippet de Código IntelliSense e qualquer snippet de código que contenha o elemento será válido, mas o valor do elemento nunca será usado.

```xml
<HelpUrl>
    www.microsoft.com
</HelpUrl>

```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Contém informações gerais sobre o snippet de código.|

 Um valor de texto é opcional. Esse texto especifica a URL a ser visitada para obter mais informações sobre um snippet de código.

## <a name="id-element"></a><a name="id"></a>Elemento ID
 Especifica um identificador exclusivo para um elemento `Literal` ou `Object`. Dois literais ou objetos no mesmo snippet de código não podem ter o mesmo valor de texto em seus elementos `ID`. Literais e objetos não podem conter um elemento `ID` com um valor de fim. O valor `$end$` é reservado e usado para marcar o local onde colocar o cursor depois que o snippet de código é inserido.

```xml
<ID>
    Unique Identifier
</ID>

```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Literal](../ide/code-snippets-schema-reference.md#literal)|Define os campos de literal do snippet de código que você pode editar.|
|[Elemento Object](../ide/code-snippets-schema-reference.md#object)|Define os campos de objeto do snippet de código que você pode editar.|

 Um valor de texto é obrigatório. Esse texto especifica o identificador exclusivo do objeto ou literal.

## <a name="import-element"></a><a name="import"></a>Importar elemento
 Especifica os namespaces importados usados por um Snippet de Código IntelliSense.

> [!NOTE]
> O elemento `Import` tem suporte apenas em projetos do Visual Basic.

```xml
<Import>
    <Namespace>... </Namespace>
</Import>

```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Namespace](../ide/code-snippets-schema-reference.md#namespace)|Elemento necessário. Especifica o namespace usado pelo snippet de código. Deve haver exatamente um elemento `Namespace` em um elemento `Import`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Imports](../ide/code-snippets-schema-reference.md#imports)|Elemento de agrupamento para elementos **Import**.|

## <a name="imports-element"></a><a name="imports"></a>Elemento Imports
 Agrupa elementos `Import` individuais.

> [!NOTE]
> O elemento `Imports` tem suporte apenas em projetos do Visual Basic.

```xml
<Imports>
    <Import>... </Import>
<Imports>
```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Importar elemento](../ide/code-snippets-schema-reference.md#import)|Elemento opcional. Contém os namespaces importados para o snippet de código. Pode ser haver zero ou mais elementos **Import** em um elemento `Imports`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Snippet](../ide/code-snippets-schema-reference.md#snippet)|Contém as referências, as importações, as declarações e o código do snippet de código.|

## <a name="keyword-element"></a><a name="keyword"></a> Elemento Keyword
 Especifica uma palavra-chave personalizada para o snippet de código. As palavras-chave de snippet de código são usadas pelo Visual Studio e representam uma maneira padronizada de os provedores de conteúdo online adicionarem palavras-chave personalizadas para pesquisa ou categorização.

```xml
<Keyword>
    Code Snippet Keyword
</Keyword>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Keywords](../ide/code-snippets-schema-reference.md#keywords)|Agrupa elementos `Keyword` individuais.|

 Um valor de texto é obrigatório. A palavra-chave para o snippet de código.

## <a name="keywords-element"></a><a name="keywords"></a>Elemento de palavras-chave
 Agrupa elementos `Keyword` individuais. As palavras-chave de snippet de código são usadas pelo Visual Studio e representam uma maneira padronizada de os provedores de conteúdo online adicionarem palavras-chave personalizadas para pesquisa ou categorização

```xml
<Keywords>
    <Keyword>... </Keyword>
    <Keyword>... </Keyword>
<Keywords>
```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento keyword](../ide/code-snippets-schema-reference.md#keyword)|Elemento opcional. Contém palavras-chave individuais para o snippet de código. Pode ser que não haja nenhum ou mais de um elemento `Keyword` em um elemento `Keywords`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Contém informações gerais sobre o snippet de código.|

## <a name="literal-element"></a><a name="literal"></a>Elemento literal
 Define os literais do snippet de código que você pode editar. O elemento `Literal` é usado para identificar um substituto para uma parte de código totalmente contido no snippet, mas que provavelmente será personalizado depois de inserido no código. Por exemplo, cadeias de caracteres literais, valores numéricos e alguns nomes de variáveis devem ser declarados como literais.

 Os literais e objetos não podem conter um elemento **ID** com um valor de selecionado ou fim. O valor `$selected$` representa o texto selecionado no documento que deve ser inserido no snippet quando ele é invocado. `$end$` marca o local para colocar o cursor depois que o snippet de código é inserido.

```xml
<Literal Editable="true/false">
   <ID>... </ID>
   <ToolTip>... </ToolTip>
   <Default>... </Default>
   <Function>... </Function>
</Literal>
```

|Atributo|Descrição|
|---------------|-----------------|
|`Editable`|Atributo `Boolean` opcional. Especifica se você pode editar ou não o literal depois de inserido o snippet de código. O valor padrão desse atributo é `true`.|

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Default](../ide/code-snippets-schema-reference.md#default)|Elemento necessário. Especifica o valor padrão do literal quando você insere o snippet de código. Deve haver exatamente um elemento `Default` em um elemento `Literal`.|
|[Elemento Function](../ide/code-snippets-schema-reference.md#function)|Elemento opcional. Especifica uma função a ser executada quando o literal recebe foco no Visual Studio. Pode ser que não haja nenhum ou um elemento `Function` em um elemento `Literal`.|
|[Elemento ID](../ide/code-snippets-schema-reference.md#id)|Elemento necessário. Especifica um identificador exclusivo para o literal. Deve haver exatamente um elemento `ID` em um elemento `Literal`.|
|[Elemento ToolTip](../ide/code-snippets-schema-reference.md#tooltip)|Elemento opcional. Descreve o valor esperado e o uso do literal. Pode haver zero ou um elemento **Tooltip** em um elemento `Literal`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Declarations](../ide/code-snippets-schema-reference.md#declarations)|Contém os literais e objetos de um snippet de código que você pode editar.|

## <a name="namespace-element"></a><a name="namespace"></a>Elemento namespace
 Especifica o namespace que deve ser importado para compilação e execução do snippet de código. O namespace especificado no elemento `Namespace` é adicionado automaticamente a uma instrução `Imports` no início do código, se ele ainda não existir.

> [!NOTE]
> O elemento `Namespace` tem suporte apenas em projetos do Visual Basic.

```xml
<Namespace>
    Namespace
</Namespace>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Importar elemento](../ide/code-snippets-schema-reference.md#import)|Importa o namespace especificado.|

 Um valor de texto é obrigatório. Esse texto especifica um namespace que o snippet de código supõe que seja importado.

## <a name="object-element"></a><a name="object"></a>Elemento Object
 Define os objetos do snippet de código que você pode editar. O elemento `Object` é usado para identificar um item que é exigido pelo snippet de código, mas que provavelmente será definido fora do snippet em si. Por exemplo, os controles do Windows Forms, os controles do ASP.NET, as instâncias do objeto e as instâncias do tipo devem ser declarados como objetos. As declarações de objeto exigem que um tipo seja especificado, o que é feito com o elemento `Type`.

```xml
<Object Editable="true/false">
    <ID>... </ID>
    <Type>... </Type>
    <ToolTip>... </ToolTip>
    <Default>... </Default>
    <Function>... </Function>
</Object>
```

|Atributo|Descrição|
|---------------|-----------------|
|`Editable`|Atributo `Boolean` opcional. Especifica se você pode editar ou não o literal depois de inserido o snippet de código. O valor padrão desse atributo é `true`.|

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Default](../ide/code-snippets-schema-reference.md#default)|Elemento necessário. Especifica o valor padrão do literal quando você insere o snippet de código. Deve haver exatamente um elemento `Default` em um elemento `Literal`.|
|[Elemento Function](../ide/code-snippets-schema-reference.md#function)|Elemento opcional. Especifica uma função a ser executada quando o literal recebe foco no Visual Studio. Pode ser que não haja nenhum ou um elemento `Function` em um elemento `Literal`.|
|[Elemento ID](../ide/code-snippets-schema-reference.md#id)|Elemento necessário. Especifica um identificador exclusivo para o literal. Deve haver exatamente um elemento `ID` em um elemento `Literal`.|
|[Elemento ToolTip](../ide/code-snippets-schema-reference.md#tooltip)|Elemento opcional. Descreve o valor esperado e o uso do literal. Pode haver zero ou um elemento **Tooltip** em um elemento `Literal`.|
|[Elemento Type](../ide/code-snippets-schema-reference.md#type)|Elemento necessário. Especifica o tipo do objeto. Deve haver exatamente um elemento `Type` em um elemento `Object`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Declarations](../ide/code-snippets-schema-reference.md#declarations)|Contém os literais e objetos de um snippet de código que você pode editar.|

## <a name="reference-element"></a><a name="reference"></a> Elemento Reference
 Especifica informações sobre as referências de assembly exigidas pelo snippet de código.

> [!NOTE]
> O elemento `Reference` tem suporte apenas em projetos do Visual Basic.

```xml
<Reference>
    <Assembly>... </Assembly>
    <Url>... </Url>
</Reference>
```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Assembly](../ide/code-snippets-schema-reference.md#assembly)|Elemento necessário. Contém o nome do assembly referenciado pelo snippet de código. Deve haver exatamente um elemento `Assembly` em um elemento `Reference`.|
|[Elemento URL](../ide/code-snippets-schema-reference.md#url)|Elemento opcional. Contém uma URL que fornece mais informações sobre o assembly referenciado. Pode ser que não haja nenhum ou um elemento `Url` em um elemento `Reference`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento References](../ide/code-snippets-schema-reference.md#references)|Elemento de agrupamento de elementos `Reference`.|

## <a name="references-element"></a><a name="references"></a>Elemento References
 Agrupa elementos `Reference` individuais.

> [!NOTE]
> O elemento `References` tem suporte apenas em projetos do Visual Basic.

```xml
<References>
    <Reference>... </Reference>
</References>
```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento Reference](../ide/code-snippets-schema-reference.md#reference)|Elemento opcional. Contém informações sobre referências de assembly para o snippet de código. Pode ser que não haja nenhum ou mais de um elemento `Reference` em um elemento `References`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Snippet](../ide/code-snippets-schema-reference.md#snippet)|Contém as referências, as importações, as declarações e o código do snippet de código.|

## <a name="shortcut-element"></a><a name="shortcut"></a>Elemento Shortcut
 Especifica o texto do atalho usado para inserir o snippet. O valor de texto de um elemento `Shortcut` pode conter apenas caracteres alfanuméricos, hifens ( - ) e sublinhados ( _ ).

> [!CAUTION]
> _ e – não são caracteres com suporte nos atalhos de snippet do C++.

```xml
<Shortcut>
    Shortcut Text
</Shortcut>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Contém informações gerais sobre o snippet de código.|

 Um valor de texto é opcional. Esse texto é usado como um atalho para inserção do snippet de código.

## <a name="snippet-element"></a><a name="snippet"></a> Elemento Snippet
 Especifica as referências, as importações, as declarações e o código do snippet de código.

```xml
<Snippet>
    <References>... </References>
    <Imports>... </Imports>
    <Declarations>... </Declarations>
    <Code>... </Code>
</Snippet>

```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento de código](../ide/code-snippets-schema-reference.md#code)|Elemento necessário. Especifica o código que você deseja inserir em um arquivo de documentação. Deve haver exatamente um elemento `Code` em um elemento `Snippet`.|
|[Elemento Declarations](../ide/code-snippets-schema-reference.md#declarations)|Elemento opcional. Especifica os literais e os objetos que compõem as partes de um snippet de código que você pode editar. Pode ser que não haja nenhum ou um elemento `Declarations` em um elemento `Snippet`.|
|[Elemento Imports](../ide/code-snippets-schema-reference.md#imports)|Elemento opcional. Agrupa elementos `Import` individuais. Pode ser que não haja nenhum ou um elemento `Imports` em um elemento `Snippet`.|
||Elemento opcional. Agrupa elementos `Reference` individuais. Pode ser que não haja nenhum ou um elemento `References` em um elemento `Snippet`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento CodeSnippet](../ide/code-snippets-schema-reference.md#codesnippet)|Permite que você especifique um título e vários Snippets de Código IntelliSense, que podem ser inseridos em arquivos de código do Visual Studio.|

## <a name="snippettype-element"></a><a name="snippettype"></a>Elemento SnippetType
 Especifica como o Visual Studio insere o snippet de código.

```xml
<SnippetType>
    SurroundsWith/Expansion
<SnippetType>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento trechos](../ide/code-snippets-schema-reference.md#snippettypes)|Agrupa elementos `SnippetType`.|

 O valor de texto deve ser um dos seguintes valores:

- `SurroundsWith`: permite que o snippet de código seja colocado em torno de uma parte do código selecionada.

- `Expansion`: permite que o snippet de código seja inserido onde está o cursor.

- `Refactoring`: especifica que o snippet de código é usado durante refatoração do Visual C#. `Refactoring` não pode ser usado em snippets de código personalizados.

## <a name="snippettypes-element"></a><a name="snippettypes"></a> Elemento SnippetTypes
 Agrupa elementos `SnippetType` individuais. Se o elemento `SnippetTypes` não estiver presente, o snippet de código poderá ser inserido em qualquer lugar no código.

```xml
<SnippetTypes>
    <SnippetType>... </SnippetType>
    <SnippetType>... </SnippetType>
<SnippetTypes>
```

|Elemento filho|Descrição|
|-------------------|-----------------|
|[Elemento SnippetType](../ide/code-snippets-schema-reference.md#snippettype)|Elemento opcional. Especifica como o Visual Studio insere o snippet de código no código. Pode ser que não haja nenhum ou mais de um elemento `SnippetType` em um elemento `SnippetTypes`.|

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Especifica informações gerais sobre o snippet de código.|

## <a name="title-element"></a><a name="title"></a> Elemento Title
 Especifica o título do snippet de código. O título armazenado no elemento `Title` do snippet de código aparece no **Selecionador de Snippets de Código** e na descrição do snippet de código no **Gerenciador de Snippets de Código**.

```xml
<Title>
    Code Snippet Title
<Title>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Header](../ide/code-snippets-schema-reference.md#header)|Especifica informações gerais sobre o snippet de código.|

 Um valor de texto é obrigatório. Esse texto especifica o título do snippet de código.

## <a name="tooltip-element"></a><a name="tooltip"></a> Elemento ToolTip
 Descreve o valor esperado e o uso de um literal ou um objeto em um snippet de código, que o Visual Studio exibe em uma Dica de Ferramenta quando inserir o snippet de código em um projeto. O texto Dica de Ferramenta é exibido quando o mouse passa sobre o literal ou objeto depois que o snippet de código foi inserido.

```xml
<ToolTip>
    ToolTip description
</ToolTip>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Literal](../ide/code-snippets-schema-reference.md#literal)|Define os campos de literal do snippet de código que você pode editar.|
|[Elemento Object](../ide/code-snippets-schema-reference.md#object)|Define os campos de objeto do snippet de código que você pode editar.|

 Um valor de texto é obrigatório. Esse texto especifica a descrição da Dica de Ferramenta a ser associada ao objeto ou literal no snippet de código.

## <a name="type-element"></a><a name="type"></a>Elemento Type
 Especifica o tipo do objeto. O elemento `Object` é usado para identificar um item que é exigido pelo snippet de código, mas que provavelmente será definido fora do snippet em si. Por exemplo, os controles do Windows Forms, os controles do ASP.NET, as instâncias do objeto e as instâncias do tipo devem ser declarados como objetos. As declarações de objeto exigem que um tipo seja especificado, o que é feito com o elemento `Type`.

```xml
<Type>
    Type
</Type>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Object](../ide/code-snippets-schema-reference.md#object)|Define os campos de objeto do snippet de código que você pode editar.|

 Um valor de texto é obrigatório. Esse texto especifica o tipo do objeto.

## <a name="url-element"></a><a name="url"></a>Elemento URL
 Especifica uma URL que fornece mais informações sobre o assembly referenciado.

> [!NOTE]
> O elemento `Url` tem suporte apenas em projetos do Visual Basic.

```xml
<Url>
    www.microsoft.com
</Url>
```

|Elemento pai|Descrição|
|--------------------|-----------------|
|[Elemento Reference](../ide/code-snippets-schema-reference.md#reference)|Especifica as referências de assembly exigidas pelo snippet de código.|

 Um valor de texto é obrigatório. Esse texto especifica uma URL com mais informações sobre o assembly referenciado. Essa URL é exibida quando a referência não pode ser adicionada ao projeto.

## <a name="see-also"></a>Consulte Também
 Explicação de [trechos de código](../ide/code-snippets.md) [: Criando um trecho de código](../ide/walkthrough-creating-a-code-snippet.md)
