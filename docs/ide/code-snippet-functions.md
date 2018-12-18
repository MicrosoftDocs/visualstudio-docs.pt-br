---
title: Funções de trecho de código
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- code snippets [Visual Studio], functions
- snippets [Visual Studio], functions
- IntelliSense code snippets, functions
ms.assetid: c0a2bf21-8fa5-4457-9281-f599beb53e7d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f3362bae41b540ee097e1109848680a11d37a272
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39512129"
---
# <a name="code-snippet-functions"></a>Funções de trecho de código

Há três funções disponíveis para uso com os trechos de código de C#. As funções são especificadas no elemento [Function](../ide/code-snippets-schema-reference.md#function-element) do trecho de código. Para obter informações sobre como criar trechos de código, consulte [Trechos de código](../ide/code-snippets.md).

## <a name="functions"></a>Funções

A tabela a seguir descreve as funções disponíveis para uso com o elemento `Function` em trechos de código.

|Função|Descrição|Idioma|
|--------------|-----------------|--------------|
|`GenerateSwitchCases(``EnumerationLiteral``)`|Gera uma instrução de opção e um conjunto de instruções de maiúsculas e minúsculas para os membros da enumeração especificada pelo parâmetro `EnumerationLiteral`. O parâmetro `EnumerationLiteral` deve ser uma referência a uma literal de enumeração ou a um tipo de enumeração.|C#|
|`ClassName()`|Retorna o nome da classe que contém o trecho inserido.|C#|
|`SimpleTypeName(``TypeName``)`|Reduz o parâmetro *TypeName* para sua forma mais simples no contexto em que o trecho foi invocado.|C#|

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como usar a função `GenerateSwitchCases`. Quando este trecho for inserido e uma enumeração for inserida no literal `$switch_on$`, o literal `$cases$` gerará uma instrução `case` para cada valor na enumeração.

```xml
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title>switch</Title>
            <Shortcut>switch</Shortcut>
            <Description>Code snippet for switch statement</Description>
            <Author>Microsoft Corporation</Author>
            <SnippetTypes>
                <SnippetType>Expansion</SnippetType>
            </SnippetTypes>
        </Header>
        <Snippet>
            <Declarations>
                <Literal>
                    <ID>expression</ID>
                    <ToolTip>Expression to switch on</ToolTip>
                    <Default>switch_on</Default>
                </Literal>
                <Literal Editable="false">
                    <ID>cases</ID>
                    <Function>GenerateSwitchCases($expression$)</Function>
                    <Default>default:</Default>
                </Literal>
            </Declarations>
            <Code Language="csharp">
                <![CDATA[
                    switch ($expression$)
                    {
                        $cases$
                    }
                ]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como usar a função `ClassName`. Quando este trecho for inserido, o literal `$classname$` será substituído pelo nome da classe delimitadora nesse local no arquivo de código.

```xml
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title>Common constructor pattern</Title>
            <Shortcut>ctor</Shortcut>
            <Description>Code Snippet for a constructor</Description>
            <Author>Microsoft Corporation</Author>
            <SnippetTypes>
                <SnippetType>Expansion</SnippetType>
            </SnippetTypes>
        </Header>
        <Snippet>
            <Declarations>
                <Literal>
                    <ID>type</ID>
                    <Default>int</Default>
                </Literal>
                <Literal>
                    <ID>name</ID>
                    <Default>field</Default>
                </Literal>
                <Literal default="true" Editable="false">
                    <ID>classname</ID>
                    <ToolTip>Class name</ToolTip>
                    <Function>ClassName()</Function>
                    <Default>ClassNamePlaceholder</Default>
                </Literal>
            </Declarations>
            <Code Language="csharp" Format="CData">
                <![CDATA[
                    public $classname$ ($type$ $name$)
                    {
                        this._$name$ = $name$;
                    }
                    private $type$ _$name$;
                ]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

## <a name="example"></a>Exemplo

Este exemplo mostra como usar a função `SimpleTypeName`. Quando este trecho for inserido em um arquivo de código, o literal `$SystemConsole$` será substituído pela forma mais simples do tipo <xref:System.Console> no contexto em que o trecho foi invocado.

```xml
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title>Console_WriteLine</Title>
            <Shortcut>cw</Shortcut>
            <Description>Code snippet for Console.WriteLine</Description>
            <Author>Microsoft Corporation</Author>
            <SnippetTypes>
                <SnippetType>Expansion</SnippetType>
            </SnippetTypes>
        </Header>
        <Snippet>
            <Declarations>
                <Literal Editable="false">
                    <ID>SystemConsole</ID>
                    <Function>SimpleTypeName(global::System.Console)</Function>
                </Literal>
            </Declarations>
            <Code Language="csharp">
                <![CDATA[
                    $SystemConsole$.WriteLine();
                ]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

## <a name="see-also"></a>Consulte também

- [Elemento Function](../ide/code-snippets-schema-reference.md#function-element)
- [Referência de esquema dos trechos de código](../ide/code-snippets-schema-reference.md)
