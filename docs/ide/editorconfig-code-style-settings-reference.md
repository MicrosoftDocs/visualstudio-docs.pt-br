---
title: Configurações de convenção de codificação do .NET para o EditorConfig
ms.date: 06/14/2018
ms.topic: reference
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- coding conventions [EditorConfig]
- EditorConfig coding conventions
- language code style rules [EditorConfig]
- formatting conventions [EditorConfig]
author: kuhlenh
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: a54a3d6b967e7652c25e24922d7bd3b49141cc17
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769746"
---
# <a name="net-coding-convention-settings-for-editorconfig"></a>Configurações de convenção de codificação do .NET para o EditorConfig

No Visual Studio 2017, você pode definir e manter um estilo de código consistente em sua base de código usando um arquivo [EditorConfig](../ide/create-portable-custom-editor-options.md). O EditorConfig inclui várias propriedades de formatação de núcleo, como `indent_style` e `indent_size`. No Visual Studio, as definições de convenções de codificação do .NET também podem ser configuradas usando um arquivo EditorConfig. Os arquivos EditorConfig permitem habilitar ou desabilitar convenções individuais de codificação do .NET e configurar o grau de imposição da convenção por meio de um nível de gravidade. Para saber mais sobre como usar o EditorConfig para impor a consistência em sua base de código, leia [Criar opções portáteis de editor personalizado](../ide/create-portable-custom-editor-options.md).

Confira o final deste artigo para obter um [exemplo do arquivo .editorconfig](#example-editorconfig-file).

## <a name="convention-categories"></a>Categorias de convenção

Há três categorias de convenção de codificação .NET com suporte:

- [Estilos de código da linguagem](#language-code-styles)

   Regras referentes à linguagem C# ou Visual Basic. Por exemplo, você pode especificar regras sobre o uso de `var` ou tipos explícitos ao definir variáveis ou dar preferência a membros aptos para expressão.

- [Convenções de formatação](#formatting-conventions)

   Regras sobre o layout e a estrutura do seu código para facilitar a leitura. Por exemplo, você pode especificar regras em relação a chaves Allman ou dar preferência a espaços em blocos de controle.

- [Convenções de nomenclatura](../ide/editorconfig-naming-conventions.md)

   Regras relacionadas a nomenclatura dos elementos de código. Por exemplo, você pode especificar que os métodos `async` devem terminar com "Async".

## <a name="language-code-styles"></a>Estilos de código da linguagem

As regras para o estilos de código da linguagem têm o seguinte formato:

`options_name = false|true : none|silent|suggestion|warning|error`

Para cada regra de estilo de linguagem, é necessário especificar **true** (dê preferência a esse estilo) ou **false** (não dê preferência a esse estilo) e uma **gravidade**. A gravidade especifica o nível de imposição para aquele estilo.

A tabela a seguir lista os valores possíveis de gravidade e seus efeitos:

Severidade | Efeito
:------- | ------
`none` | Não mostra nada para o usuário quando esta regra é violada. No entanto, os recursos de geração de código geram código neste estilo. As regras com a severidade `none` nunca são exibidas no menu **Ações Rápidas e Refatorações**. Na maioria dos casos, isso é considerado "desabilitado" ou "ignorado".
`silent` (também `refactoring` no Visual Studio 2017 versão 15.8) | Não mostra nada para o usuário quando esta regra é violada. No entanto, os recursos de geração de código geram código neste estilo. As regras com severidade `silent` participam da limpeza e também aparecem no menu **Ações Rápidas e Refatorações**.
`suggestion` | Quando esta regra de estilo for violada, deverá ser mostrada ao usuário como uma sugestão. As sugestões são exibidas como três pontos cinza sob os dois primeiros caracteres.
`warning` | Quando esta regra de estilo for violada, deverá ser exibido um aviso do compilador.
`error` | Quando esta regra de estilo for violada, deverá ser exibido um erro do compilador.

A lista a seguir mostra as configurações de estilo de código da linguagem permitidas:

- Configurações de estilo de código do .NET
    - [Qualificadores "This." e "Me."](#this_and_me)
        - dotnet\_style\_qualification\_for_field
        - dotnet\_style\_qualification\_for_property
        - dotnet\_style\_qualification\_for_method
        - dotnet\_style\_qualification\_for_event
    - [Palavras-chave de linguagem em vez de nomes de tipos de estrutura para referências de tipo](#language_keywords)
        - dotnet\_style\_predefined\_type\_for\_locals\_parameters_members
        - dotnet\_style\_predefined\_type\_for\_member_access
    - [Preferências do modificador](#normalize_modifiers)
        - dotnet\_style\_require\_accessibility_modifiers
        - csharp\_preferred\_modifier_order
        - visual\_basic\_preferred\_modifier_order
        - dotnet\_style\_readonly\_field
    - [Preferências de parênteses](#parentheses)
        - dotnet\_style\_parentheses\_in\_arithmetic\_binary\_operators
        - dotnet\_style\_parentheses\_in\_other\_binary\_operators
        - dotnet\_style\_parentheses\_in\_other\_operators
        - dotnet\_style\_parentheses\_in\_relational\_binary\_operators
    - [Preferências de nível de expressão](#expression_level)
        - dotnet\_style\_object_initializer
        - dotnet\_style\_collection_initializer
        - dotnet\_style\_explicit\_tuple_names
        - dotnet\_style\_prefer\_inferred\_tuple_names
        - dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names
        - dotnet\_style\_prefer\_auto\_properties
        - dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method
        - dotnet\_style\_prefer\_conditional\_expression\_over\_assignment
        - dotnet\_style\_prefer\_conditional\_expression\_over\_return
    - [Preferências da verificação de "null"](#null_checking)
        - dotnet\_style\_coalesce_expression
        - dotnet\_style\_null_propagation
- Configurações de estilo de código de C#
    - [Tipos implícitos e explícitos](#implicit-and-explicit-types)
        - csharp\_style\_var\_for\_built\_in_types
        - csharp\_style\_var\_when\_type\_is_apparent
        - csharp\_style\_var_elsewhere
    - [Membros de expressão incorporada](#expression_bodied_members)
        - csharp\_style\_expression\_bodied_methods
        - csharp\_style\_expression\_bodied_constructors
        - csharp\_style\_expression\_bodied_operators
        - csharp\_style\_expression\_bodied_properties
        - csharp\_style\_expression\_bodied_indexers
        - csharp\_style\_expression\_bodied_accessors
    - [Correspondência de padrões](#pattern_matching)
        - csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check
        - csharp\_style\_pattern\_matching\_over\_as\_with\_null_check
    - [Declarações de variável embutida](#inlined_variable_declarations)
        - csharp\_style\_inlined\_variable_declaration
    - [Preferências de nível de expressão](#expression_level_csharp)
        - csharp\_prefer\_simple\_default_expression
        - csharp\_style\_deconstructed\_variable_declaration
        - csharp\_style\_pattern\_local\_over\_anonymous_function
    - [Preferências da verificação de "null"](#null_checking_csharp)
        - csharp\_style\_throw_expression
        - csharp\_style\_conditional\_delegate_call
    - [Preferências de bloco de código](#code_block)
        - csharp\_prefer_braces

### <a name="net-code-style-settings"></a>Configurações de estilo de código do .NET

As regras de estilo nesta seção são aplicáveis tanto para C# quanto para Visual Basic. Para ver exemplos de código na sua linguagem de programação preferida, escolha no menu suspenso **Linguagem**, no canto superior direito da janela do navegador.

#### <a name="this_and_me"></a>Qualificadores "Este." e "Eu.

Essa regra de estilo (IDs de regra IDE0003 e IDE0009) pode ser aplicada a campos, propriedades, métodos ou eventos. Um valor **true** significa a preferência pelo símbolo de código ser precedido de `this.` em C# ou `Me.` no Visual Basic. Um valor **false** significa a preferência pelo elemento de código _não_ ser precedido de `this.` ou `Me.`.

A tabela a seguir mostra os nomes das regras, as linguagens de programação aplicáveis e os valores padrão:

| Nome da regra | Linguagens aplicáveis | Valor padrão do Visual Studio |
| ----------- | -------------------- | ----------------------|
| dotnet_style_qualification_for_field | C# e Visual Basic | false:none |
| dotnet_style_qualification_for_property | C# e Visual Basic | false:none |
| dotnet_style_qualification_for_method | C# e Visual Basic | false:none |
| dotnet_style_qualification_for_event | C# e Visual Basic | false:none |

**dotnet\_style\_qualification\_for_field**

- Quando essa regra é definida como **true**, prefira que campos sejam precedidos com `this.` em C# ou `Me.` no Visual Basic.
- Quando essa regra é definida como **false**, prefira que os campos _não_ sejam precedidos com `this.` ou `Me.`.

Exemplos de código:

```csharp
// dotnet_style_qualification_for_field = true
this.capacity = 0;

// dotnet_style_qualification_for_field = false
capacity = 0;
```

```vb
' dotnet_style_qualification_for_field = true
Me.capacity = 0

' dotnet_style_qualification_for_field = false
capacity = 0
```

**dotnet\_style\_qualification\_for_property**

- Quando essa regra é definida como **true**, prefira que as propriedades sejam precedidas com `this.` em C# ou `Me.` no Visual Basic.
- Quando essa regra é definida como **false**, prefira que as propriedades _não_ sejam precedidas com `this.` ou `Me.`.

Exemplos de código:

```csharp
// dotnet_style_qualification_for_property = true
this.ID = 0;

// dotnet_style_qualification_for_property = false
ID = 0;
```

```vb
' dotnet_style_qualification_for_property = true
Me.ID = 0

' dotnet_style_qualification_for_property = false
ID = 0
```

**dotnet\_style\_qualification\_for_method**

- Quando essa regra é definida como **true**, prefira que os métodos sejam precedidos com `this.` em C# ou `Me.` no Visual Basic.
- Quando essa regra é definida como **false**, prefira que os métodos _não_ sejam precedidos com `this.` ou `Me.`.

Exemplos de código:

```csharp
// dotnet_style_qualification_for_method = true
this.Display();

// dotnet_style_qualification_for_method = false
Display();
```

```vb
' dotnet_style_qualification_for_method = true
Me.Display()

' dotnet_style_qualification_for_method = false
Display()
```

**dotnet\_style\_qualification\_for_event**

- Quando essa regra é definida como **true**, prefira que os eventos sejam precedidos com `this.` em C# ou `Me.` no Visual Basic.
- Quando essa regra é definida como **false**, prefira que os eventos _não_ sejam precedidos com `this.` ou `Me.`.

Exemplos de código:

```csharp
// dotnet_style_qualification_for_event = true
this.Elapsed += Handler;

// dotnet_style_qualification_for_event = false
Elapsed += Handler;
```

```vb
' dotnet_style_qualification_for_event = true
AddHandler Me.Elapsed, AddressOf Handler

' dotnet_style_qualification_for_event = false
AddHandler Elapsed, AddressOf Handler
```

Essas regras podem aparecer em um arquivo *.editorconfig*, assim como mostrado a seguir:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion
```

#### <a name="language_keywords"></a>Palavras-chave de linguagem em vez de nomes de tipos de estrutura para referências de tipo

Essa regra de estilo pode ser aplicada a variáveis locais, parâmetros de método e membros de classe ou como uma regra separada para expressões de acesso a membro de tipo. Um valor **true** significa preferência pela palavra-chave de linguagem (por exemplo, `int` ou `Integer`) em vez do nome do tipo (por exemplo, `Int32`) para tipos que têm uma palavra-chave para representá-los. Um valor **false** significa preferência pelo nome do tipo em vez da palavra-chave de linguagem.

A tabela a seguir mostra os nomes das regras, IDs de regras, as linguagens de programação aplicáveis e os valores padrão:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio |
| --------- | ------- | -------------------- | ----------------------|
| dotnet_style_predefined_type_for_locals_parameters_members | IDE0012 e IDE0014 | C# e Visual Basic | true:none |
| dotnet_style_predefined_type_for_member_access | IDE0013 e IDE0015 | C# e Visual Basic | true:none |

**dotnet\_style\_predefined\_type\_for\_locals\_parameters_members**

- Quando essa regra é definida como **true**, prefira a palavra-chave de linguagem para variáveis locais, parâmetros de método e membros de classe, em vez do nome de tipo, para tipos que têm uma palavra-chave para representá-los.
- Quando essa regra é definida como **false**, prefira o nome do tipo para variáveis locais, parâmetros de método e membros de classe, em vez da palavra-chave de linguagem.

Exemplos de código:

```csharp
// dotnet_style_predefined_type_for_locals_parameters_members = true
private int _member;

// dotnet_style_predefined_type_for_locals_parameters_members = false
private Int32 _member;
```

```vb
' dotnet_style_predefined_type_for_locals_parameters_members = true
Private _member As Integer

' dotnet_style_predefined_type_for_locals_parameters_members = false
Private _member As Int32
```

**dotnet\_style\_predefined\_type\_for\_member_access**

- Quando essa regra é definida como **true**, prefira a palavra-chave de linguagem para expressões de acesso a membro, em vez do nome de tipo, para tipos que têm uma palavra-chave para representá-los.
- Quando essa regra é definida como **false**, prefira o nome do tipo para expressões de acesso a membro, em vez da palavra-chave de linguagem.

Exemplos de código:

```csharp
// dotnet_style_predefined_type_for_member_access = true
var local = int.MaxValue;

// dotnet_style_predefined_type_for_member_access = false
var local = Int32.MaxValue;
```

```vb
' dotnet_style_predefined_type_for_member_access = true
Dim local = Integer.MaxValue

' dotnet_style_predefined_type_for_member_access = false
Dim local = Int32.MaxValue
```

Essas regras podem aparecer em um arquivo *.editorconfig*, assim como mostrado a seguir:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion
```

#### <a name="normalize_modifiers"></a>Preferências do modificador

As regras de estilo desta seção dizem respeito às preferências do modificador, incluindo a exigência de modificadores de acessibilidade, a especificação da ordem de classificação de modificador desejada e a exigência do modificador somente leitura.

A tabela a seguir mostra os nomes das regras, as IDs de regra, as linguagens de programação aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| --------- | ------- | -------------------- | ----------------------| ---------------- |
| dotnet_style_require_accessibility_modifiers | IDE0040 | C# e Visual Basic | for_non_interface_members:none | 15.5 |
| csharp_preferred_modifier_order | IDE0036 | C# | público, privado, protegido, interno, estático, externo, novo, virtual, abstrato, selado, substituído, somente leitura, não seguro, volátil, assíncrono:nenhum | 15.5 |
| visual_basic_preferred_modifier_order | IDE0036 | Visual Basic | Parcial, Padrão, Privado, Protegido, Público, Amigo, NotOverridable Substituível, MustOverride, Sobrecargas, Substituições, MustInherit, NotInheritable, Estático, Compartilhado, Sombras, Somente Leitura, Somente Gravação, Esmaecer, Const, WithEvents, Expandindo, Reduzindo, Personalizado, Assíncrono:nenhum | 15.5 |
| dotnet_style_readonly_field | IDE0044 | C# e Visual Basic | true:suggestion | 15.7 |

**dotnet\_style\_require\_accessibility_modifiers**

Essa regra não aceita um valor **true** ou **false**; em vez disso, ela aceita um valor da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| always | Preferir que modificadores de acessibilidade sejam especificados |
| for\_non\_interface_members | Preferir que modificadores de acessibilidade sejam declarados, exceto os membros de interface pública. Isso é o mesmo que **always** e foi adicionado para durabilidade, caso o C# adicione métodos de interface padrão. |
| never | Não preferir que modificadores de acessibilidade sejam especificados |

Exemplos de código:

```csharp
// dotnet_style_require_accessibility_modifiers = always
// dotnet_style_require_accessibility_modifiers = for_non_interface_members
class MyClass
{
    private const string thisFieldIsConst = "constant";
}

// dotnet_style_require_accessibility_modifiers = never
class MyClass
{
    const string thisFieldIsConst = "constant";
}
```

**csharp_preferred_modifier_order**

- Quando esta regra for definida como uma lista de modificadores, prefira a ordenação especificada.
- Quando esta regra for omitida do arquivo, não prefira uma ordem de modificador.

Exemplos de código:

```csharp
// csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async
class MyClass
{
    private static readonly int _daysInYear = 365;
}
```

**visual_basic_preferred_modifier_order**

- Quando esta regra for definida como uma lista de modificadores, prefira a ordenação especificada.
- Quando esta regra for omitida do arquivo, não prefira uma ordem de modificador.

Exemplos de código:

```vb
' visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async
Public Class MyClass
    Private Shared ReadOnly daysInYear As Int = 365
End Class
```

**dotnet_style_readonly_field**

- Quando essa regra é definida como **true**, prefira que os campos sejam marcados com `readonly` (C#) ou `ReadOnly` (Visual Basic), caso sejam somente atribuídos de maneira embutida ou dentro de um construtor.
- Quando essa regra é definida como **false**, não especifique nenhuma preferência sobre se os campos devem ser marcados com `readonly` (C#) ou `ReadOnly` (Visual Basic).

Exemplos de código:

```csharp
// dotnet_style_readonly_field = true
class MyClass
{
    private readonly int _daysInYear = 365;
}
```

```vb
' dotnet_style_readonly_field = true
Public Class MyClass
    Private ReadOnly daysInYear As Int = 365
End Class
```

Essas regras podem aparecer em um arquivo *.editorconfig*, assim como mostrado a seguir:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_require_accessibility_modifiers = always:suggestion
dotnet_style_readonly_field = true:warning

# CSharp code style settings:
[*.cs]
csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async:suggestion

# Visual Basic code style settings:
[*.vb]
visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async:suggestion
```

#### <a name="parentheses"></a>Preferências de parênteses

As regras de estilo nesta seção referem-se às preferências de parênteses, incluindo o uso de parênteses para operadores aritméticos, relacionais e outros operadores binários.

A tabela a seguir mostra os nomes das regras, as IDs de regra, as linguagens de programação aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| --------- | ------- | -------------------- | ----------------------| ---- |
| dotnet_style_parentheses_in_arithmetic_binary_operators | IDE0047 | C# e Visual Basic | always_for_clarity:none | 15.8 |
| dotnet_style_parentheses_in_relational_binary_operators | IDE0047 | C# e Visual Basic | always_for_clarity:none | 15.8 |
| dotnet_style_parentheses_in_other_binary_operators | IDE0047 | C# e Visual Basic | always_for_clarity:none | 15.8 |
| dotnet_style_parentheses_in_other_operators | IDE0047 | C# e Visual Basic | never_if_unnecessary:none | 15.8 |

**dotnet\_style\_parentheses\_in\_arithmetic\_binary_operators**

- Quando essa regra for definida como **always_for_clarity**, prefira usar parênteses para esclarecer a precedência do operador aritmético (`*`, `/`, `%`, `+`, `-`, `<<`, `>>`, `&`, `^`, `|`).
- Quando essa regra for definida como **never_if_unnecessary**, prefira não usar parênteses quando a precedência do operador aritmético (`*`, `/`, `%`, `+`, `-`, `<<`, `>>`, `&`, `^`, `|`) for óbvia.

Exemplos de código:

```csharp
// dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity
var v = a + (b * c);

// dotnet_style_parentheses_in_arithmetic_binary_operators = never_if_unnecessary
var v = a + b * c;
```

```vb
' dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity
Dim v = a + (b * c)

' dotnet_style_parentheses_in_arithmetic_binary_operators = never_if_unnecessary
Dim v = a + b * c
```

**dotnet\_style\_parentheses\_in\_relational\_binary_operators**

- Quando essa regra for definida como **always_for_clarity**, prefira usar parênteses para esclarecer a precedência do operador relacional (`>`, `<`, `<=`, `>=`, `is`, `as`, `==`, `!=`).
- Quando essa regra for definida como **never_if_unnecessary**, prefira não usar parênteses quando a precedência do operador relacional (`>`, `<`, `<=`, `>=`, `is`, `as`, `==`, `!=`) for óbvia.

Exemplos de código:

```csharp
// dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity
var v = (a < b) == (c > d);

// dotnet_style_parentheses_in_relational_binary_operators = never_if_unnecessary
var v = a < b == c > d;
```

```vb
' dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity
Dim v = (a < b) = (c > d)

' dotnet_style_parentheses_in_relational_binary_operators = never_if_unnecessary
Dim v = a < b = c > d
```

**dotnet\_style\_parentheses\_in\_other\_binary_operators**

- Quando essa regra for definida como **always_for_clarity**, prefira usar parênteses para esclarecer a precedência do outro operador binário (`&&`, `||`, `??`).
- Quando essa regra for definida como **never_if_unnecessary**, prefira não usar parênteses quando a precedência do outro operador binário (`&&`, `||`, `??`) for óbvia.

Exemplos de código:

```csharp
// dotnet_style_parentheses_in_other_binary_operators = always_for_clarity
var v = a || (b && c);

// dotnet_style_parentheses_in_other_binary_operators = never_if_unnecessary
var v = a || b && c;
```

```vb
' dotnet_style_parentheses_in_other_binary_operators = always_for_clarity
Dim v = a OrElse (b AndAlso c)

' dotnet_style_parentheses_in_other_binary_operators = never_if_unnecessary
Dim v = a OrElse b AndAlso c
```

**dotnet\_style\_parentheses\_in\_other_operators**

- Quando essa regra for definida como **always_for_clarity**, prefira usar parênteses para esclarecer a precedência do operador.
- Quando essa regra for definida como **never_if_unnecessary**, prefira não usar parênteses quando a precedência do operador for óbvia.

Exemplos de código:

```csharp
// dotnet_style_parentheses_in_other_operators = always_for_clarity
var v = (a.b).Length;

// dotnet_style_parentheses_in_other_operators = never_if_unnecessary
var v = a.b.Length;
```

```vb
' dotnet_style_parentheses_in_other_operators = always_for_clarity
Dim v = (a.b).Length

' dotnet_style_parentheses_in_other_operators = never_if_unnecessary
Dim v = a.b.Length
```

Essas regras podem aparecer em um arquivo *.editorconfig*, assim como mostrado a seguir:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity:none
dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity:none
dotnet_style_parentheses_in_other_binary_operators = always_for_clarity:none
dotnet_style_parentheses_in_other_operators = never_if_unnecessary:none
```

#### <a name="expression_level"></a>Preferências de nível de expressão

As regras de estilo nesta seção referem-se às preferências no nível da expressão, incluindo o uso de inicializadores de objeto, inicializadores de coleção, nomes de tupla explícitos ou inferidos e tipos anônimos inferidos.

A tabela a seguir mostra os nomes das regras, as IDs de regra, as linguagens de programação aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| --------- | ------- | -------------------- | ----------------------| ---- |
| dotnet_style_object_initializer | IDE0017 | C# e Visual Basic | true:suggestion | Primeira versão |
| dotnet_style_collection_initializer | IDE0028 | C# e Visual Basic | true:suggestion | Primeira versão |
| dotnet_style_explicit_tuple_names | IDE0033 | C# 7.0+ e Visual Basic 15+ | true:suggestion | Primeira versão |
| dotnet_style_prefer_inferred_tuple_names | IDE0037 | C# 7.1+ e Visual Basic 15+ | true:suggestion | 15.6 |
| dotnet_style_prefer_inferred_anonymous_type_member_names | IDE0037 | C# e Visual Basic | true:suggestion | 15.6 |
| dotnet_style_prefer_auto_properties | IDE0032 | C# e Visual Basic | true:none | 15.7 |
| dotnet_style_prefer_is_null_check_over_reference_equality_method | IDE0041 | C# e Visual Basic | true:suggestion | 15.7 |
| dotnet_style_prefer_conditional_expression_over_assignment | IDE0045 | C# e Visual Basic | true:none | 15.8 |
| dotnet_style_prefer_conditional_expression_over_return | IDE0046 | C# e Visual Basic | true:none | 15.8 |

**dotnet\_style\_object_initializer**

- Quando essa regra é definida como **true**, prefira que objetos sejam inicializados usando inicializadores de objeto quando possível.
- Quando essa regra é definida como **false**, prefira que objetos *não* sejam inicializados usando inicializadores de objeto.

Exemplos de código:

```csharp
// dotnet_style_object_initializer = true
var c = new Customer() { Age = 21 };

// dotnet_style_object_initializer = false
var c = new Customer();
c.Age = 21;
```

```vb
' dotnet_style_object_initializer = true
Dim c = New Customer() With {.Age = 21}

' dotnet_style_object_initializer = false
Dim c = New Customer()
c.Age = 21
```

**dotnet\_style\_collection_initializer**

- Quando essa regra é definida como **true**, prefira que coleções sejam inicializadas usando inicializadores de coleção quando possível.
- Quando essa regra é definida como **false**, prefira que as coleções *não* sejam inicializadas usando inicializadores de coleção.

Exemplos de código:

```csharp
// dotnet_style_collection_initializer = true
var list = new List<int> { 1, 2, 3 };

// dotnet_style_collection_initializer = false
var list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);
```

```vb
' dotnet_style_collection_initializer = true
Dim list = New List(Of Integer) From {1, 2, 3}

' dotnet_style_collection_initializer = false
Dim list = New List(Of Integer)
list.Add(1)
list.Add(2)
list.Add(3)
```

**dotnet\_style\_explicit\_tuple_names**

- Quando essa regra é definida como **true**, prefira nomes de tupla a propriedades ItemX.
- Quando essa regra é definida como **false**, prefira propriedades ItemX a nomes de tupla.

Exemplos de código:

```csharp
// dotnet_style_explicit_tuple_names = true
(string name, int age) customer = GetCustomer();
var name = customer.name;

// dotnet_style_explicit_tuple_names = false
(string name, int age) customer = GetCustomer();
var name = customer.Item1;
```

```vb
 ' dotnet_style_explicit_tuple_names = true
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.name

' dotnet_style_explicit_tuple_names = false
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.Item1
```

**dotnet\_style\_prefer\_inferred\_tuple_names**

- Quando essa regra for definida como **true**, prefira nomes de elemento de tupla inferidos.
- Quando essa regra for definida como **false**, prefira nomes de elemento de tupla explícitos.

Exemplos de código:

```csharp
// dotnet_style_prefer_inferred_tuple_names = true
var tuple = (age, name);

// dotnet_style_prefer_inferred_tuple_names = false
var tuple = (age: age, name: name);
```

```vb
' dotnet_style_prefer_inferred_tuple_names = true
Dim tuple = (name, age)

' dotnet_style_prefer_inferred_tuple_names = false
Dim tuple = (name:=name, age:=age)
```

**dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names**

- Quando essa regra for definida como **true**, prefira nomes de membro de tipo anônimo inferidos.
- Quando essa regra for definida como **false**, prefira nomes de membro de tipo anônimo explícitos.

Exemplos de código:

```csharp
// dotnet_style_prefer_inferred_anonymous_type_member_names = true
var anon = new { age, name };

// dotnet_style_prefer_inferred_anonymous_type_member_names = false
var anon = new { age = age, name = name };
```

```vb
' dotnet_style_prefer_inferred_anonymous_type_member_names = true
Dim anon = New With {name, age}

' dotnet_style_prefer_inferred_anonymous_type_member_names = false
Dim anon = New With {.name = name, .age = age}
```

**dotnet\_style\_prefer\_auto\_properties**

- Quando essa regra está definida como **true**, dá preferência a propriedades automáticas em vez de propriedades com campos de suporte particulares.
- Quando essa regra está definida como **false**, dá preferência a propriedades com campos de suporte particulares em vez de propriedades automáticas.

Exemplos de código:

```csharp
// dotnet_style_prefer_auto_properties = true
private int Age { get; }

// dotnet_style_prefer_auto_properties = false
private int age;

public int Age
{
    get
    {
        return age;
    }
}
```

```vb
' dotnet_style_prefer_auto_properties = true
Public ReadOnly Property Age As Integer

' dotnet_style_prefer_auto_properties = false
Private _age As Integer

Public ReadOnly Property Age As Integer
    Get
        return _age
    End Get
End Property
```

**dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method**

- Quando essa regra é definida como **true**, ela dá preferência ao uso de uma verificação nula com correspondência de padrões, em vez de object.ReferenceEquals.
- Quando essa regra é definida como **false**, ela dá preferência a object.ReferenceEquals, em vez de uma verificação nula com correspondência de padrões.

Exemplos de código:

```csharp
// dotnet_style_prefer_is_null_check_over_reference_equality_method = true
if (value is null)
    return;

// dotnet_style_prefer_is_null_check_over_reference_equality_method = false
if (object.ReferenceEquals(value, null))
    return;
```

```vb
' dotnet_style_prefer_is_null_check_over_reference_equality_method = true
If value Is Nothing
    Return
End If

' dotnet_style_prefer_is_null_check_over_reference_equality_method = false
If Object.ReferenceEquals(value, Nothing)
    Return
End If
```



**dotnet\_style\_prefer\_conditional\_expression\_over_assignment**

- Quando essa regra for definida como **true**, prefira atribuições com uma condicional ternária em vez de uma instrução if-else.
- Quando essa regra for definida como **false**, prefira atribuições com uma instrução if-else em vez de uma condicional ternária.

Exemplos de código:

```csharp
// dotnet_style_prefer_conditional_expression_over_assignment = true
string s = expr ? "hello" : "world";

// dotnet_style_prefer_conditional_expression_over_assignment = false
string s;
if (expr)
{
    s = "hello";
}
else
{
    s = "world";
}
```

```vb
' dotnet_style_prefer_conditional_expression_over_assignment = true
Dim s As String = If(expr, "hello", "world")

' dotnet_style_prefer_conditional_expression_over_assignment = false
Dim s As String
If expr Then
    s = "hello"
Else
    s = "world"
End If
```

**dotnet\_style\_prefer\_conditional\_expression\_over_return**

- Quando essa regra for definida como **true**, prefira que as instruções de retorno usem uma condicional ternária em vez de uma instrução if-else.
- Quando essa regra for definida como **false**, prefira que as instruções de retorno usem uma instrução if-else em vez de uma condicional ternária.

Exemplos de código:

```csharp
// dotnet_style_prefer_conditional_expression_over_return = true
return expr ? "hello" : "world"

// dotnet_style_prefer_conditional_expression_over_return = false
if (expr)
{
    return "hello";
}
else
{
    return "world";
}
```

```vb
' dotnet_style_prefer_conditional_expression_over_return = true
Return If(expr, "hello", "world")

' dotnet_style_prefer_conditional_expression_over_return = false
If expr Then
    Return "hello"
Else
    Return "world"
End If
```

Essas regras podem aparecer em um arquivo *.editorconfig*, assim como mostrado a seguir:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_prefer_inferred_tuple_names = true:suggestion
dotnet_style_prefer_inferred_anonymous_type_member_names = true:suggestion
dotnet_style_prefer_auto_properties = true:none
dotnet_style_prefer_conditional_expression_over_assignment = true:suggestion
dotnet_style_prefer_conditional_expression_over_return = true:suggestion
```

#### <a name="null_checking"></a>Preferências de verificação de nulo

As regras de estilo nesta seção referem-se às preferências de verificação de nulo.

A tabela a seguir mostra os nomes das regras, as IDs de regra, as linguagens de programação aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| --------- | ------- | -------------------- | ----------------------| ---- |
| dotnet_style_coalesce_expression | IDE0029 | C# e Visual Basic | true:suggestion | Primeira versão |
| dotnet_style_null_propagation | IDE0031 | C# 6.0+ e Visual Basic 14+ | true:suggestion | Primeira versão |

**dotnet\_style\_coalesce_expression**

- Quando essa regra é definida como **true**, prefira expressões de união nula a verificação do operador ternário.
- Quando essa regra é definida como **false**, prefira a verificação do operador ternário a expressões de união nula.

Exemplos de código:

```csharp
// dotnet_style_coalesce_expression = true
var v = x ?? y;

// dotnet_style_coalesce_expression = false
var v = x != null ? x : y; // or
var v = x == null ? y : x;
```

```vb
' dotnet_style_coalesce_expression = true
Dim v = If(x, y)

' dotnet_style_coalesce_expression = false
Dim v = If(x Is Nothing, y, x) ' or
Dim v = If(x IsNot Nothing, x, y)
```

**dotnet\_style\_null_propagation**

- Quando essa regra é definida como **true**, prefira usar o operador condicional nulo quando possível.
- Quando essa regra é definida como **false**, prefira o uso da verificação de ternário nulo sempre que possível.

Exemplos de código:

```csharp
// dotnet_style_null_propagation = true
var v = o?.ToString();

// dotnet_style_null_propagation = false
var v = o == null ? null : o.ToString(); // or
var v = o != null ? o.String() : null;
```

```vb
' dotnet_style_null_propagation = true
Dim v = o?.ToString()

' dotnet_style_null_propagation = false
Dim v = If(o Is Nothing, Nothing, o.ToString()) ' or
Dim v = If(o IsNot Nothing, o.ToString(), Nothing)
```

Essas regras podem aparecer em um arquivo *.editorconfig*, assim como mostrado a seguir:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion
```

### <a name="c-code-style-settings"></a>Configurações de estilo de código de C#

As regras de estilo nesta seção são aplicáveis somente á linguagem C#.

#### <a name="implicit-and-explicit-types"></a>Tipos implícitos e explícitos

As regras de estilo nesta seção (IDs de regra IDE0007 e IDE0008) referem-se ao uso da palavra-chave [var](/dotnet/csharp/language-reference/keywords/var) em vez de um tipo explícito em uma declaração de variável. Essa regra pode ser aplicada separadamente a tipos internos, quando o tipo é aparente e em qualquer outro local.

A tabela a seguir mostra os nomes das regras, as linguagens de programação aplicáveis e os valores padrão:

| Nome da regra | Linguagens aplicáveis | Padrão do Visual Studio |
| ----------- | -------------------- | ----------------------|
| csharp_style_var_for_built_in_types | C# | true:none |
| csharp_style_var_when_type_is_apparent | C# | true:none |
| csharp_style_var_elsewhere | C# | true:none |

**csharp\_style\_var\_for\_built\_in_types**

- Quando essa regra é definida como **true**, prefira que `var` seja usada para declarar variáveis com tipos de sistema internos, como `int`.
- Quando essa regra é definida como **false**, prefira tipo explícito em vez de `var` para declarar variáveis com tipos de sistema internos, como `int`.

Exemplos de código:

```csharp
// csharp_style_var_for_built_in_types = true
var x = 5;

// csharp_style_var_for_built_in_types = false
int x = 5;
```

**csharp\_style\_var\_when\_type\_is_apparent**

- Quando essa regra é definida como **true**, prefira `var` quando o tipo já tiver sido mencionado no lado direito de uma expressão de declaração.
- Quando essa regra é definida como **false**, prefira tipo explícito em vez de `var` quando o tipo já tiver sido mencionado no lado direito de uma expressão de declaração.

Exemplos de código:

```csharp
// csharp_style_var_when_type_is_apparent = true
var obj = new Customer();

// csharp_style_var_when_type_is_apparent = false
Customer obj = new Customer();
```

**csharp\_style\_var_elsewhere**

- Quando essa regra é definida como **true**, prefira `var` em vez de tipo explícito em todos os casos, a menos que a regra seja substituída por outra regra de estilo de código.
- Quando essa regra é definida como **false**, prefira tipo explícito em vez de `var` em todos os casos, a menos que a regra seja substituída por outra regra de estilo de código.

Exemplos de código:

```csharp
// csharp_style_var_elsewhere = true
var f = this.Init();

// csharp_style_var_elsewhere = false
bool f = this.Init();
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_var_for_built_in_types = true:suggestion
csharp_style_var_when_type_is_apparent = true:suggestion
csharp_style_var_elsewhere = true:suggestion
```

#### <a name="expression_bodied_members"></a>Membros aptos para expressão

As regras de estilo nesta seção envolvem o uso de [membros aptos para expressão](/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members) quando a lógica consiste em uma única expressão. Essa regra pode ser aplicada a métodos, construtores, operadores, propriedades, indexadores e acessadores.

A tabela a seguir mostra os nomes das regras, as IDs de regra, as versões de linguagem aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| --------- | ------- | -------------------- | ----------------------| ---------------- |
| csharp_style_expression_bodied_methods | IDE0022 | C# 6.0+ | false:none | 15.3 |
| csharp_style_expression_bodied_constructors | IDE0021 | C# 7.0+ | false:none | 15.3 |
| csharp_style_expression_bodied_operators | IDE0023 e IDE0024 | C# 7.0+ | false:none | 15.3 |
| csharp_style_expression_bodied_properties | IDE0025 | C# 7.0+ | true:none | 15.3 |
| csharp_style_expression_bodied_indexers | IDE0026 | C# 7.0+ | true:none | 15.3 |
| csharp_style_expression_bodied_accessors | IDE0027 | C# 7.0+ | true:none | 15.3 |

**csharp\_style\_expression\_bodied_methods**

Esta regra aceita valores da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| true | Preferir membros aptos para expressão para métodos |
| when_on_single_line | Preferir membros aptos para expressão para métodos quando eles forem uma única linha |
| false | Preferir corpos de bloco para métodos |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_methods = true
public int GetAge() => this.Age;

// csharp_style_expression_bodied_methods = false
public int GetAge() { return this.Age; }
```

**csharp\_style\_expression\_bodied_constructors**

Esta regra aceita valores da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| true | Preferir membros aptos para expressão para construtores |
| when_on_single_line | Preferir membros aptos para expressão para construtores quando eles forem uma única linha |
| false | Preferir blocos do corpo para construtores |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_constructors = true
public Customer(int age) => Age = age;

// csharp_style_expression_bodied_constructors = false
public Customer(int age) { Age = age; }
```

**csharp\_style\_expression\_bodied_operators**

Esta regra aceita valores da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| true | Prefira membros aptos para expressão para operadores |
| when_on_single_line | Preferir membros aptos para expressão para operadores quando eles forem uma única linha |
| false | Preferir blocos do corpo para operadores |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_operators = true
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
    => new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);

// csharp_style_expression_bodied_operators = false
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
{ return new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary); }
```

**csharp\_style\_expression\_bodied_properties**

Esta regra aceita valores da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| true | Prefira membros aptos para expressão para propriedades |
| when_on_single_line | Preferir membros aptos para expressão para propriedades quando elas forem uma única linha |
| false | Preferir blocos do corpo para propriedades |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_properties = true
public int Age => _age;

// csharp_style_expression_bodied_properties = false
public int Age { get { return _age; }}
```

**csharp\_style\_expression\_bodied_indexers**

Esta regra aceita valores da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| true | Preferir membros aptos para expressão para indexadores |
| when_on_single_line | Preferir membros aptos para expressão para indexadores quando eles forem uma única linha |
| false | Preferir blocos do corpo para indexadores |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_indexers = true
public T this[int i] => _values[i];

// csharp_style_expression_bodied_indexers = false
public T this[int i] { get { return _values[i]; } }
```

**csharp\_style\_expression\_bodied_accessors**

Esta regra aceita valores da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| true | Preferir membros aptos para expressão para acessadores |
| when_on_single_line | Preferir membros aptos para expressão para acessadores quando eles forem uma única linha |
| false | Preferir blocos do corpo para acessadores |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_accessors = true
public int Age { get => _age; set => _age = value; }

// csharp_style_expression_bodied_accessors = false
public int Age { get { return _age; } set { _age = value; } }
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_expression_bodied_methods = false:none
csharp_style_expression_bodied_constructors = false:none
csharp_style_expression_bodied_operators = false:none
csharp_style_expression_bodied_properties = true:suggestion
csharp_style_expression_bodied_indexers = true:suggestion
csharp_style_expression_bodied_accessors = true:suggestion
```

#### <a name="pattern_matching"></a>Correspondência de padrões

As regras de estilo nesta seção envolvem o uso de [correspondência de padrões](/dotnet/csharp/pattern-matching) em C#.

A tabela a seguir mostra os nomes das regras, IDs de regras, as versões de linguagens aplicáveis e os valores padrão:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio |
| --------- | ------- | -------------------- | ----------------------|
| csharp_style_pattern_matching_over_is_with_cast_check | IDE0020 | C# 7.0+ | true:suggestion |
| csharp_style_pattern_matching_over_as_with_null_check | IDE0019 | C# 7.0+ | true:suggestion |

**csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check**

- Quando essa regra é definida como **true**, prefira a correspondência de padrões em vez de expressões `is` com conversões de tipo.
- Quando essa regra é definida como **false**, prefira expressões `is` com conversões de tipo em vez de correspondência de padrões.

Exemplos de código:

```csharp
// csharp_style_pattern_matching_over_is_with_cast_check = true
if (o is int i) {...}

// csharp_style_pattern_matching_over_is_with_cast_check = false
if (o is int) {var i = (int)o; ... }
```

**csharp\_style\_pattern\_matching\_over\_as\_with\_null_check**

- Quando essa regra é definida como **true**, prefira correspondência de padrões em vez de expressões `as` com verificações nulas para determinar se algo é de um tipo específico.
- Quando essa regra é definida como **false**, prefira expressões `as` com verificações nula em vez de correspondência de padrões para determinar se algo é de um tipo específico.

Exemplos de código:

```csharp
// csharp_style_pattern_matching_over_as_with_null_check = true
if (o is string s) {...}

// csharp_style_pattern_matching_over_as_with_null_check = false
var s = o as string;
if (s != null) {...}
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
```

#### <a name="inlined_variable_declarations"></a>Declarações de variável embutida

Essa regra de estilo é relacionada a se as variáveis `out` são declaradas embutidas ou não. Após o C#7, você pode [declarar uma variável de saída na lista de argumentos de uma chamada de método](/dotnet/csharp/language-reference/keywords/out-parameter-modifier#calling-a-method-with-an-out-argument) em vez de declará-la em uma declaração de variável separada.

A tabela a seguir mostra o nome da regra, a ID da regra, as versões de linguagens aplicáveis e os valores padrão:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio |
| --------- | -------- | -------------------- | ----------------------|
| csharp_style_inlined_variable_declaration | IDE0018 | C# 7.0+ | true:suggestion |

**csharp\_style\_inlined\_variable_declaration**

- Quando essa regra é definida como **true**, prefira que as variáveis `out` sejam declaradas embutidas na lista de argumentos de uma chamada de método quando possível.
- Quando essa regra é definida como **false**, prefira que as variáveis `out` sejam declaradas antes da chamada de método.

Exemplos de código:

```csharp
// csharp_style_inlined_variable_declaration = true
if (int.TryParse(value, out int i) {...}

// csharp_style_inlined_variable_declaration = false
int i;
if (int.TryParse(value, out i) {...}
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_inlined_variable_declaration = true:suggestion
```

#### <a name="expression_level_csharp"></a>Preferências de nível de expressão

As regras de estilo nesta seção dizem respeito às preferências de nível de expressão, incluindo o uso de [expressões padrão](/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and-type-inference), variáveis desconstruídas e funções locais em vez de funções anônimas.

A tabela a seguir mostra o nome da regra, a ID da regra, as versões de linguagem aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| --------- | ------- | -------------------- | ----------------------| ---------------- |
| csharp_prefer_simple_default_expression | IDE0034 | C# 7.1+ | true:suggestion | 15.3 |
| csharp_style_deconstructed_variable_declaration | IDE0042 | C# 7.0+ | true:suggestion | 15.5 |
| csharp_style_pattern_local_over_anonymous_function | IDE0039 | C# 7.0+ | true:suggestion | 15.5 |

**csharp\_prefer\_simple\_default_expression**

Essa regra de estilo refere-se ao uso do [literal `default` para expressões de valor padrão](/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and-type-inference) quando o compilador pode inferir o tipo da expressão.

- Quando essa regra é definida como **true**, prefira `default` em vez de `default(T)`.
- Quando essa regra é definida como **false**, prefira `default(T)` em vez de `default`.

Exemplos de código:

```csharp
// csharp_prefer_simple_default_expression = true
void DoWork(CancellationToken cancellationToken = default) { ... }

// csharp_prefer_simple_default_expression = false
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }
```

**csharp\_style\_deconstructed\_variable_declaration**

- Quando essa regra for definida como **true**, prefira a declaração de variável desconstruída.
- Quando essa regra for definida como **false**, não prefira a desconstrução em declarações de variável.

Exemplos de código:

```csharp
// csharp_style_deconstructed_variable_declaration = true
var (name, age) = GetPersonTuple();
Console.WriteLine($"{name} {age}");

(int x, int y) = GetPointTuple();
Console.WriteLine($"{x} {y}");

// csharp_style_deconstructed_variable_declaration = false
var person = GetPersonTuple();
Console.WriteLine($"{person.name} {person.age}");

(int x, int y) point = GetPointTuple();
Console.WriteLine($"{point.x} {point.y}");
```

**csharp\_style\_pattern\_local\_over\_anonymous_function**

- Quando essa regra for definida como **true**, prefira funções locais a funções anônimas.
- Quando essa regra for definida como **false**, prefira funções anônimas a funções locais.

Exemplos de código:

```csharp
// csharp_style_pattern_local_over_anonymous_function = true
int fibonacci(int n)
{
    return n <= 1 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}

// csharp_style_pattern_local_over_anonymous_function = false
Func<int, int> fibonacci = null;
fibonacci = (int n) =>
{
    return n <= 1 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
};
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_prefer_simple_default_expression = true:suggestion
csharp_style_deconstructed_variable_declaration = true:suggestion
csharp_style_pattern_local_over_anonymous_function = true:suggestion
```

#### <a name="null_checking_csharp"></a>Preferências da verificação de "null"

Essas regras de estilo referem-se à sintaxe da verificação de `null`, incluindo o uso de expressões `throw` ou instruções `throw`, e se é desejável executar uma verificação nula ou usar o operador de união condicional (`?.`) ao invocar uma [expressão lambda](/dotnet/csharp/lambda-expressions).

A tabela a seguir mostra os nomes das regras, IDs de regras, as versões de linguagens aplicáveis e os valores padrão:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio |
| --------- | ------- | -------------------- | ----------------------|
| csharp_style_throw_expression | IDE0016 | C# 7.0+ | true:suggestion |
| csharp_style_conditional_delegate_call | IDE0041 | C# 6.0+ | true:suggestion |

**csharp\_style\_throw_expression**

- Quando essa regra é definida como **true**, prefira usar expressões `throw` em vez de instruções `throw`.
- Quando essa regra é definida como **false**, prefira usar instruções `throw` em vez de expressões `throw`.

Exemplos de código:

```csharp
// csharp_style_throw_expression = true
this.s = s ?? throw new ArgumentNullException(nameof(s));

// csharp_style_throw_expression = false
if (s == null) { throw new ArgumentNullException(nameof(s)); }
this.s = s;
```

**csharp\_style\_conditional\_delegate_call**

- Quando essa regra é definida como **true**, prefira usar o operador de união condicional (`?.`) ao invocar uma expressão lambda, em vez de realizar uma verificação nula.
- Quando essa regra é definida como **false**, prefira realizar uma verificação nula antes de invocar uma expressão lambda, em vez de usar o operador de união condicional (`?.`).

Exemplos de código:

```csharp
// csharp_style_conditional_delegate_call = true
func?.Invoke(args);

// csharp_style_conditional_delegate_call = false
if (func != null) { func(args); }
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = false:suggestion
```

#### <a name="code_block"></a>Preferências de bloco de código

Essa regra de estilo diz respeito ao uso de chaves `{ }` para cercar blocos de código.

A tabela a seguir mostra o nome da regra, a ID da regra, as versões de linguagem aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | ID da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| --------- | ------- | -------------------- | ----------------------| ---------------- |
| csharp_prefer_braces | IDE0011 | C# | true:none | 15.3 |

**csharp\_prefer\_braces**

- Quando essa regra é definida como **true**, prefira chaves, até mesmo para uma linha de código.
- Quando essa regra é definida como **false**, prefira não usar chaves, se permitido.

Exemplos de código:

```csharp
// csharp_prefer_braces = true
if (test) { this.Display(); }

// csharp_prefer_braces = false
if (test) this.Display();
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_prefer_braces = true:none
```

## <a name="formatting-conventions"></a>Convenções de formatação

A maioria das regras para as convenções de formatação tem o seguinte formato:

`rule_name = false|true`

Você especifica **true** (dê preferência a esse estilo) ou **false** (não dê preferência a esse estilo). Você não especifica uma gravidade. Para algumas regras, em vez de true ou false, você especifica outros valores para descrever quando e onde aplicar a regra.

A lista a seguir mostra as regras de convenção de formatação disponíveis no Visual Studio:

- Configurações de formatação do .NET
    - [Organizar usos](#usings)
        - dotnet_sort_system_directives_first
- Configurações de formatação de C#
    - [Opções de nova linha](#newline)
        - csharp_new_line_before_open_brace
        - csharp_new_line_before_else
        - csharp_new_line_before_catch
        - csharp_new_line_before_finally
        - csharp_new_line_before_members_in_object_initializers
        - csharp_new_line_before_members_in_anonymous_types
        - csharp_new_line_between_query_expression_clauses
    - [Opções de recuo](#indent)
        - csharp_indent_case_contents
        - csharp_indent_switch_labels
        - csharp_indent_labels
    - [Opções de espaçamento](#spacing)
        - csharp_space_after_cast
        - csharp_space_after_keywords_in_control_flow_statements
        - csharp_space_between_method_declaration_parameter_list_parentheses
        - csharp_space_between_method_call_parameter_list_parentheses
        - csharp_space_between_parentheses
        - csharp_space_before_colon_in_inheritance_clause
        - csharp_space_after_colon_in_inheritance_clause
        - csharp_space_around_binary_operators
        - csharp_space_between_method_declaration_empty_parameter_list_parentheses
        - csharp_space_between_method_call_name_and_opening_parenthesis
        - csharp_space_between_method_call_empty_parameter_list_parentheses
    - [Opções de encapsulamento](#wrapping)
        - csharp_preserve_single_line_statements
        - csharp_preserve_single_line_blocks

### <a name="net-formatting-settings"></a>Configurações de formatação do .NET

As regras de formatação nesta seção são aplicáveis ao C# e Visual Basic.

#### <a name="usings"></a>Organizar usos

Essa regra de formatação diz respeito ao posicionamento de diretivas using System.* em relação a outras diretivas using.

A tabela a seguir mostra o nome da regra, as linguagens aplicáveis, o valor padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| ----------- | -------------------- | ----------------------| ---------------- |
| dotnet_sort_system_directives_first | C# e Visual Basic | true | 15.3 |

**dotnet\_sort\_system\_directives_first**

- Quando essa regra é definida como **true**, classifique as diretivas using System.* em ordem alfabética e posicione-as antes de outras usings.
- Quando essa regra é definida como **false**, não posicione diretivas using System.* antes de outras diretivas using.

Exemplos de código:

```csharp
// dotnet_sort_system_directives_first = true
using System.Collections.Generic;
using System.Threading.Tasks;
using Octokit;

// dotnet_sort_system_directives_first = false
using System.Collections.Generic;
using Octokit;
using System.Threading.Tasks;
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# .NET formatting settings:
[*.{cs,vb}]
dotnet_sort_system_directives_first = true
```

### <a name="c-formatting-settings"></a>Configurações de formatação de C#

As regras de formatação nesta seção aplicam-se somente a código em C#.

#### <a name="newline"></a>Opções de nova linha

Essas regras de formatação envolvem o uso de novas linhas para formatar o código.

A tabela a seguir mostra os nomes das regras "nova linha", as linguagens aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| ----------- | -------------------- | ----------------------| ---------------- |
| csharp_new_line_before_open_brace | C# | all | 15.3 |
| csharp_new_line_before_else | C# | true | 15.3 |
| csharp_new_line_before_catch | C# | true | 15.3 |
| csharp_new_line_before_finally | C# | true | 15.3 |
| csharp_new_line_before_members_in_object_initializers | C# | true | 15.3 |
| csharp_new_line_before_members_in_anonymous_types | C# | true | 15.3 |
| csharp_new_line_between_query_expression_clauses | C# | true | 15.3 |

**csharp\_new\_line\_before\_open_brace**

Essa regra está relacionada a se uma chave de abertura `{` devem ser colocada na mesma linha que a do código anterior ou em uma nova linha. Para esta regra, você não especifica **true** ou **false**. Em vez disso, você especifica **all**, **none** ou um ou mais elementos de código, como **methods** ou **properties**, para definir quando essa regra deve ser aplicada. A lista completa de valores permitidos é mostrada na tabela a seguir:

| Valor | Descrição
| ------------- |:-------------|
| accessors, anonymous_methods, anonymous_types, control_blocks, events, indexers, lambdas, local_functions, methods, object_collection_array_initializers, properties, types.<br>(Para vários tipos, separe com ","). | Exigir que chaves estejam em uma nova linha para os elementos de código especificados (também conhecido como estilo "Allman") |
| all | Requer que as chaves estejam em uma nova linha para todas as expressões (estilo "Allman") |
| nenhum | Requer que as chaves estejam na mesma linha para todas as expressões ("K&R") |

Exemplos de código:

```csharp
// csharp_new_line_before_open_brace = all
void MyMethod()
{
    if (...)
    {
        ...
    }
}

// csharp_new_line_before_open_brace = none
void MyMethod() {
    if (...) {
        ...
    }
}
```

**csharp\_new\_line\_before_else**

- Quando essa regra é definida como **true**, posicione as instruções `else` em uma nova linha.
- Quando essa regra é definida como **false**, posicione as instruções `else` na mesma linha.

Exemplos de código:

```csharp
// csharp_new_line_before_else = true
if (...) {
    ...
}
else {
    ...
}

// csharp_new_line_before_else = false
if (...) {
    ...
} else {
    ...
}
```

**csharp\_new\_line\_before_catch**

- Quando essa regra é definida como **true**, posicione as instruções `catch` em uma nova linha.
- Quando essa regra é definida como **false**, posicione as instruções `catch` na mesma linha.

Exemplos de código:

```csharp
// csharp_new_line_before_catch = true
try {
    ...
}
catch (Exception e) {
    ...
}

// csharp_new_line_before_catch = false
try {
    ...
} catch (Exception e) {
    ...
}
```

**csharp\_new\_line\_before_finally**

- Quando essa regra é definida como **true**, exigir que as instruções `finally` estejam em uma nova linha após a chave de fechamento.
- Quando essa regra é definida como **false**, exigir que as instruções `finally` estejam na mesma linha que a chave de fechamento.

Exemplos de código:

```csharp
// csharp_new_line_before_finally = true
try {
    ...
}
catch (Exception e) {
    ...
}
finally {
    ...
}

// csharp_new_line_before_finally = false
try {
    ...
} catch (Exception e) {
    ...
} finally {
    ...
}
```

**csharp\_new\_line\_before\_members\_in\_object_initializers**

- Quando essa regra está definida como **true**, exige que membros dos inicializadores de objeto estejam em linhas separadas.
- Quando essa regra é definida como **false**, exigir que membros dos inicializadores de objeto estejam na mesma linha.

Exemplos de código:

```csharp
// csharp_new_line_before_members_in_object_initializers = true
var z = new B()
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_object_initializers = false
var z = new B()
{
    A = 3, B = 4
}
```

**csharp\_new\_line\_before\_members\_in\_anonymous_types**

- Quando essa regra é definida como **true**, exigir que membros dos tipos anônimos estejam em linhas separadas.
- Quando essa regra é definida como **false**, exigir que membros dos tipos anônimos estejam na mesma linha.

Exemplos de código:

```csharp
// csharp_new_line_before_members_in_anonymous_types = true
var z = new
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_anonymous_types = false
var z = new
{
    A = 3, B = 4
}
```

**csharp_new_line_between_query_expression_clauses**

- Quando essa regra é definida como **true**, exigir que elementos das cláusulas de expressão de consulta estejam em linhas separadas.
- Quando essa regra é definida como **false**, exigir que elementos das cláusulas de expressão de consulta estejam na mesma linha.

Exemplos de código:

```csharp
// csharp_new_line_between_query_expression_clauses = true
var q = from a in e
        from b in e
        select a * b;

// csharp_new_line_between_query_expression_clauses = false
var q = from a in e from b in e
        select a * b;
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_new_line_before_open_brace = methods, properties, control_blocks, types
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_between_query_expression_clauses = true
```

#### <a name="indent"></a>Opções de recuo

Essas regras de formatação envolvem o uso de recuo para formatar o código.

A tabela a seguir mostra os nomes das regras, as linguagens aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| ----------- | -------------------- | ----------------------| ---------------- |
| csharp_indent_case_contents | C# | true | 15.3 |
| csharp_indent_switch_labels | C# | true | 15.3 |
| csharp_indent_labels | C# | no_change | 15.3 |

**csharp\_indent\_case_contents**

- Quando essa regra é definida como **true**, recue os conteúdos de caso `switch`.
- Quando essa regra é definida como **false**, não recue os conteúdos de caso `switch`.

Exemplos de código:

```csharp
// csharp_indent_case_contents = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_case_contents = false
switch(c) {
    case Color.Red:
    Console.WriteLine("The color is red");
    break;
    case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
    default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

**csharp\_indent\_switch_labels**

- Quando essa regra é definida como **true**, recue os rótulos `switch`.
- Quando essa regra é definida como **false**, não recue os rótulos `switch`.

Exemplos de código:

```csharp
// csharp_indent_switch_labels = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_switch_labels = false
switch(c) {
case Color.Red:
    Console.WriteLine("The color is red");
    break;
case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

**csharp\_indent_labels**

Essa regra não aceita um valor **true** ou **false**; em vez disso, ela aceita um valor da tabela a seguir:

| Valor | Descrição |
| ----- |:----------- |
| flush_left | Os rótulos são posicionados na coluna mais à esquerda |
| one_less_than_current | Os rótulos são posicionados em um recuo a menos do que o contexto atual |
| no_change | Os rótulos são posicionados no mesmo recuo do contexto atual |

Exemplos de código:

```csharp
// csharp_indent_labels= flush_left
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
error:
        throw new Exception(...);
    }
}

// csharp_indent_labels = one_less_than_current
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
    error:
        throw new Exception(...);
    }
}

// csharp_indent_labels= no_change
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
        error:
        throw new Exception(...);
    }
}
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = flush_left
```

#### <a name="spacing"></a>Opções de espaçamento

Essas regras de formatação envolvem o uso de caracteres de espaço para formatar o código.

A tabela a seguir mostra os nomes das regras, as linguagens aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| ----------- | -------------------- | ----------------------| ---------------- |
| csharp_space_after_cast | C# | false | 15.3 |
| csharp_space_after_keywords_in_control_flow_statements | C# | true | 15.3 |
| csharp_space_between_method_declaration_parameter_list_parentheses | C# | false | 15.3 |
| csharp_space_between_method_call_parameter_list_parentheses | C# | false | 15.3 |
| csharp_space_between_parentheses | C# | false | 15.3 |
| csharp_space_before_colon_in_inheritance_clause | C# | true | 15.7 |
| csharp_space_after_colon_in_inheritance_clause | C# | true | 15.7 |
| csharp_space_around_binary_operators | C# | before_and_after | 15.7 |
| csharp_space_between_method_declaration_empty_parameter_list_parentheses | C# | false | 15.7 |
| csharp_space_between_method_call_name_and_opening_parenthesis | C# | false | 15.7 |
| csharp_space_between_method_call_empty_parameter_list_parentheses | C# | false | 15.7 |

**csharp\_space\_after_cast**

- Quando essa regra é definida como **true**, exigir um espaço entre uma conversão e o valor.
- Quando essa regra é definida como **false**, _não_ exigir espaço entre a conversão e o valor.

Exemplos de código:

```csharp
// csharp_space_after_cast = true
int y = (int) x;

// csharp_space_after_cast = false
int y = (int)x;
```

**csharp_space_after_keywords_in_control_flow_statements**

- Quando essa regra é definida como **true**, exigir um espaço depois de uma palavra-chave em uma instrução de fluxo de controle, como um `for` loop.
- Quando essa regra é definida como **false**, _não_ exigir um espaço depois de uma palavra-chave em uma instrução de fluxo de controle, como um loop `for`.

Exemplos de código:

```csharp
// csharp_space_after_keywords_in_control_flow_statements = true
for (int i;i<x;i++) { ... }

// csharp_space_after_keywords_in_control_flow_statements = false
for(int i;i<x;i++) { ... }
```

**csharp_space_between_method_declaration_parameter_list_parentheses**

- Quando essa regra é definida como **true**, posicionar um caractere de espaço após o parêntese de abertura e antes do parêntese de fechamento de uma lista de parâmetros de declaração de método.
- Quando essa regra é definida como **false**, não posicionar caracteres de espaço após o parêntese de abertura e antes do parêntese de fechamento de uma lista de parâmetros de declaração de método.

Exemplos de código:

```csharp
// csharp_space_between_method_declaration_parameter_list_parentheses = true
void Bark( int x ) { ... }

// csharp_space_between_method_declaration_parameter_list_parentheses = false
void Bark(int x) { ... }
```

**csharp_space_between_method_call_parameter_list_parentheses**

- Quando essa regra é definida como **true**, posicionar um caractere de espaço após o parêntese de abertura e antes do parêntese de fechamento de uma chamada de método.
- Quando essa regra é definida como **false**, não posicionar caracteres de espaço após o parêntese de abertura e antes do parêntese de fechamento de uma chamada de método.

Exemplos de código:

```csharp
// csharp_space_between_method_call_parameter_list_parentheses = true
MyMethod( argument );

// csharp_space_between_method_call_parameter_list_parentheses = false
MyMethod(argument);
```

**csharp_space_between_parentheses**

Essa regra aceita um ou mais valores da tabela a seguir:

| Valor | Descrição |
| ----- |:------------|
| control_flow_statements | Inserir espaço entre parênteses das instruções de fluxo de controle |
| expressões | Inserir espaço entre os parênteses das expressões |
| type_casts | Inserir espaço entre os parênteses nas conversões de tipo |

Se você omitir essa regra ou usar um valor diferente de `control_flow_statements`, `expressions` ou `type_casts`, a configuração não será aplicada.

Exemplos de código:

```csharp
// csharp_space_between_parentheses = control_flow_statements
for ( int i = 0; i < 10; i++ ) { }

// csharp_space_between_parentheses = expressions
var z = ( x * y ) - ( ( y - x ) * 3 );

// csharp_space_between_parentheses = type_casts
int y = ( int )x;
```

**csharp\_space\_before\_colon\_in\_inheritance_clause**

- Quando essa regra é definida como **true**, ela exige um espaço antes dos dois-pontos para bases ou interfaces em uma declaração de tipo.
- Quando essa regra é definida como **false**, ela não exige _nenhum_ espaço antes dos dois-pontos para bases ou interfaces em uma declaração de tipo.

Exemplos de código:

```csharp
// csharp_space_before_colon_in_inheritance_clause = true
interface I
{

}

class C : I
{

}

// csharp_space_before_colon_in_inheritance_clause = false
interface I
{

}

class C: I
{

}
```

**csharp\_space\_after\_colon\_in\_inheritance_clause**

- Quando essa regra é definida como **true**, ela exige um espaço após os dois-pontos para bases ou interfaces em uma declaração de tipo.
- Quando essa regra é definida como **false**, ela não exige _nenhum_ espaço após os dois-pontos para bases ou interfaces em uma declaração de tipo.

Exemplos de código:

```csharp
// csharp_space_after_colon_in_inheritance_clause = true
interface I
{

}

class C : I
{

}

// csharp_space_after_colon_in_inheritance_clause = false
interface I
{

}

class C :I
{

}
```

**csharp\_space\_around\_binary_operators**

Essa regra aceita um valor da seguinte tabela:

| Valor | Descrição |
| ----- |:------------|
| before_and_after | Inserir espaço antes e depois do operador binário |
| nenhum | Remover espaços antes e depois do operador binário |
| ignorar | Ignorar espaços em torno de operadores binários |

Se você omitir essa regra ou usar um valor diferente de `before_and_after`, `none` ou `ignore`, a configuração não será aplicada.

Exemplos de código:

```csharp
// csharp_space_around_binary_operators = before_and_after
return x * (x - y);

// csharp_space_around_binary_operators = none
return x*(x-y);

// csharp_space_around_binary_operators = ignore
return x  *  (x-y);
```

**csharp_space_between_method_declaration_empty_parameter_list_parentheses**

- Quando essa regra é definida como **true**, ela insere um espaço nos parênteses vazios da lista de parâmetros para uma declaração de método.
- Quando essa regra é definida como **false**, ela remove um espaço dos parênteses vazios da lista de parâmetros para uma declaração de método.

Exemplos de código:

```csharp
// csharp_space_between_method_declaration_empty_parameter_list_parentheses = true
void Goo( )
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}

// csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

**csharp_space_between_method_call_name_and_opening_parenthesis**

- Quando essa regra é definida como **true**, ela insere um espaço entre o nome da chamada de método e o parêntese de abertura.
- Quando essa regra é definida como **false**, ela remove um espaço entre o nome da chamada de método e o parêntese de abertura.

Exemplos de código:

```csharp
// csharp_space_between_method_call_name_and_opening_parenthesis = true
void Goo()
{
    Goo (1);
}

void Goo(int x)
{
    Goo ();
}

// csharp_space_between_method_call_name_and_opening_parenthesis = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

**csharp_space_between_method_call_empty_parameter_list_parentheses**

- Quando essa regra é definida como **true**, ela insere um espaço nos parênteses vazios da lista de argumentos.
- Quando essa regra é definida como **false**, ela remove um espaço dos parênteses vazios da lista de argumentos.

Exemplos de código:

```csharp
// csharp_space_between_method_call_empty_parameter_list_parentheses = true
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo( );
}

// csharp_space_between_method_call_empty_parameter_list_parentheses = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_space_after_cast = true
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_between_method_declaration_parameter_list_parentheses = true
csharp_space_between_method_call_parameter_list_parentheses = true
csharp_space_between_parentheses = control_flow_statements, type_casts
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_around_binary_operators = before_and_after
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_between_method_call_empty_parameter_list_parentheses = false
```

#### <a name="wrapping"></a>Opções de encapsulamento

Essas regras de formatação referem-se ao uso de linhas únicas em comparação com linhas separadas para instruções e blocos de código.

A tabela a seguir mostra os nomes das regras, as linguagens aplicáveis, os valores padrão e a primeira versão compatível do Visual Studio:

| Nome da regra | Linguagens aplicáveis | Padrão do Visual Studio | Versão do Visual Studio 2017 |
| ----------- | -------------------- | ----------------------| ---------------- |
| csharp_preserve_single_line_statements | C# | true | 15.3 |
| csharp_preserve_single_line_blocks | C# | true | 15.3 |

**csharp_preserve_single_line_statements**

- Quando essa regra é definida como **true**, deixar instruções e declarações de membro na mesma linha.
- Quando essa regra é definida como **false**, deixar instruções e declarações de membro em linhas diferentes.

Exemplos de código:

```csharp
//csharp_preserve_single_line_statements = true
int i = 0; string name = "John";

//csharp_preserve_single_line_statements = false
int i = 0;
string name = "John";
```

**csharp_preserve_single_line_blocks**

- Quando essa regra é definida como **true**, deixar o bloco de código em linha única.
- Quando essa regra é definida como **false**, deixar o bloco de código em linhas separadas.

Exemplos de código:

```csharp
//csharp_preserve_single_line_blocks = true
public int Foo { get; set; }

//csharp_preserve_single_line_blocks = false
public int MyProperty
{
    get; set;
}
```

Exemplo de arquivo *.editorconfig*:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_preserve_single_line_statements = true
csharp_preserve_single_line_blocks = true
```

## <a name="example-editorconfig-file"></a>Exemplo de arquivo EditorConfig

Para ajudá-lo a começar, este é um arquivo *.editorconfig* de exemplo com as opções padrão:

```EditorConfig
###############################
# Core EditorConfig Options   #
###############################

root = true

# All files
[*]
indent_style = space

# Code files
[*.{cs,csx,vb,vbx}]
indent_size = 4
insert_final_newline = true
charset = utf-8-bom

###############################
# .NET Coding Conventions     #
###############################

[*.{cs,vb}]
# Organize usings
dotnet_sort_system_directives_first = true

# this. preferences
dotnet_style_qualification_for_field = false:none
dotnet_style_qualification_for_property = false:none
dotnet_style_qualification_for_method = false:none
dotnet_style_qualification_for_event = false:none

# Language keywords vs BCL types preferences
dotnet_style_predefined_type_for_locals_parameters_members = true:none
dotnet_style_predefined_type_for_member_access = true:none

# Parentheses preferences
dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_operators = never_if_unnecessary:silent

# Modifier preferences
dotnet_style_require_accessibility_modifiers = for_non_interface_members:none
dotnet_style_readonly_field = true:suggestion

# Expression-level preferences
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_null_propagation = true:suggestion
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_prefer_is_null_check_over_reference_equality_method = true:silent
dotnet_style_prefer_inferred_tuple_names = true:suggestion
dotnet_style_prefer_inferred_anonymous_type_member_names = true:suggestion
dotnet_style_prefer_auto_properties = true:silent
dotnet_style_prefer_conditional_expression_over_assignment = true:silent
dotnet_style_prefer_conditional_expression_over_return = true:silent

###############################
# Naming Conventions          #
###############################

# Style Definitions
dotnet_naming_style.pascal_case_style.capitalization             = pascal_case

# Use PascalCase for constant fields
dotnet_naming_rule.constant_fields_should_be_pascal_case.severity = suggestion
dotnet_naming_rule.constant_fields_should_be_pascal_case.symbols  = constant_fields
dotnet_naming_rule.constant_fields_should_be_pascal_case.style    = pascal_case_style
dotnet_naming_symbols.constant_fields.applicable_kinds            = field
dotnet_naming_symbols.constant_fields.applicable_accessibilities  = *
dotnet_naming_symbols.constant_fields.required_modifiers          = const

###############################
# C# Code Style Rules         #
###############################

[*.cs]
# var preferences
csharp_style_var_for_built_in_types = true:none
csharp_style_var_when_type_is_apparent = true:none
csharp_style_var_elsewhere = true:none

# Expression-bodied members
csharp_style_expression_bodied_methods = false:none
csharp_style_expression_bodied_constructors = false:none
csharp_style_expression_bodied_operators = false:none
csharp_style_expression_bodied_properties = true:none
csharp_style_expression_bodied_indexers = true:none
csharp_style_expression_bodied_accessors = true:none

# Pattern-matching preferences
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion

# Null-checking preferences
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = true:suggestion

# Modifier preferences
csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async:suggestion

# Expression-level preferences
csharp_prefer_braces = true:none
csharp_style_deconstructed_variable_declaration = true:suggestion
csharp_prefer_simple_default_expression = true:suggestion
csharp_style_pattern_local_over_anonymous_function = true:suggestion
csharp_style_inlined_variable_declaration = true:suggestion

###############################
# C# Formatting Rules         #
###############################

# New line preferences
csharp_new_line_before_open_brace = all
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_between_query_expression_clauses = true

# Indentation preferences
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = flush_left

# Space preferences
csharp_space_after_cast = false
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_between_method_call_parameter_list_parentheses = false
csharp_space_between_method_declaration_parameter_list_parentheses = false
csharp_space_between_parentheses = false
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_around_binary_operators = before_and_after
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_between_method_call_empty_parameter_list_parentheses = false

# Wrapping preferences
csharp_preserve_single_line_statements = true
csharp_preserve_single_line_blocks = true

##################################
# Visual Basic Code Style Rules  #
##################################

[*.vb]
# Modifier preferences
visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async:suggestion
```

## <a name="see-also"></a>Consulte também

- [Ações rápidas](../ide/quick-actions.md)
- [Convenções de nomenclatura .NET para EditorConfig](../ide/editorconfig-naming-conventions.md)
- [Criar opções do editor portátil e personalizado](../ide/create-portable-custom-editor-options.md)
- [Arquivo .editorconfig da plataforma do compilador do .NET](https://github.com/dotnet/roslyn/blob/master/.editorconfig)
