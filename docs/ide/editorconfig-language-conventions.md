---
title: Convenções de linguagem .NET para EditorConfig
ms.date: 03/31/2020
ms.topic: reference
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- language code style rules [EditorConfig]
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 3fa32e6155959df6e665a807af3b364923ba3f54
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533452"
---
# <a name="language-conventions"></a>Convenções de linguagem

As convenções de linguagem para o EditorConfig no Visual Studio se enquadram em duas categorias: as que são aplicáveis ao Visual Basic e ao C# e as que são específicas do C#. As convenções de linguagem afetam o modo como vários aspectos de uma linguagem de programação são usados, por exemplo, modificadores e parênteses.

> [!TIP]
> - Para ver os exemplos de código na sua linguagem de programação preferida, escolha-a usando o seletor de idioma no canto superior direito da janela do navegador.
>
>   ![Controle de seletor de linguagem de código](media/code-language-picker.png)
>
> - Use os links **Neste artigo** para saltar para seções diferentes da página.

## <a name="rule-format"></a>Formatação de regra

As regras para convenções de linguagem têm o seguinte formato geral:

`option_name = value:severity`

Para cada convenção de linguagem, você pode especificar um valor que define se ou quando preferir o estilo. Muitas regras aceitam um valor de `true` (prefira esse estilo) ou `false` (não prefiro esse estilo). Outras regras aceitam valores como `when_on_single_line` ou `never` . A segunda parte da regra especifica a [severidade](#severity-levels).

::: moniker range=">=vs-2019"

> [!NOTE]
> Como as convenções de linguagem são impostas por analisadores, você também pode definir sua gravidade usando a sintaxe de configuração padrão para analisadores. A sintaxe assume a forma `dotnet_diagnostic.<rule ID>.severity = <severity>` , por exemplo, `dotnet_diagnostic.IDE0040.severity = silent` . Para obter mais informações, consulte [definir a severidade da regra em um arquivo EditorConfig](../code-quality/use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file).

::: moniker-end

## <a name="severity-levels"></a>Níveis de severidade

Uma severidade de convenção de linguagem especifica o nível no qual impor esse estilo. A tabela a seguir lista os valores possíveis de gravidade e seus efeitos:

Severity | Efeito
:------- | ------
`error` | Quando esta regra de estilo for violada, deverá ser exibido um erro do compilador.
`warning` | Quando esta regra de estilo for violada, deverá ser exibido um aviso do compilador.
`suggestion` | Quando esta regra de estilo for violada, deverá ser mostrada ao usuário como uma sugestão. As sugestões são exibidas como três pontos cinza sob os dois primeiros caracteres.
`silent` | Não mostra nada para o usuário quando esta regra é violada. No entanto, os recursos de geração de código geram código neste estilo. As regras com `silent` severidade participam da limpeza e aparecem no menu **ações rápidas e refatoração** .
`none` | Não mostra nada para o usuário quando esta regra é violada. No entanto, os recursos de geração de código geram código neste estilo. As regras com a severidade `none` nunca são exibidas no menu **Ações Rápidas e Refatorações**. Na maioria dos casos, isso é considerado "desabilitado" ou "ignorado".

::: moniker range=">=vs-2019"

## <a name="automatically-configure-code-styles"></a>Configurar estilos de código automaticamente

A partir do Visual Studio 2019 versão 16,3, você pode configurar regras de estilo de código no menu de lâmpada de [ações rápidas](quick-actions.md) após a ocorrência de uma violação de estilo.

Para alterar a Convenção do estilo de código:

1. Passe o mouse sobre o rabisco no editor e, em seguida, abra o menu de lâmpada que aparece. Escolha **Configurar ou suprimir problemas**  >  **Configurar o \<rule ID> estilo de código**.

   ![Configurar o estilo de código no menu de lâmpada no Visual Studio](media/vs-2019/configure-code-style.png)

2. A partir daí, escolha uma das opções de estilo de código.

   ![Definir configuração de estilo de código](media/vs-2019/configure-code-style-setting.png)

   O Visual Studio adiciona ou modifica a definição de configuração no arquivo EditorConfig, conforme mostrado na caixa de visualização.

Para alterar a severidade da violação de estilo de código, siga as mesmas etapas, mas escolha **Configurar \<rule ID> severidade** em vez de **Configurar o estilo de \<rule ID> código**. Para obter mais informações, consulte [Configurar automaticamente a severidade da regra](../code-quality/use-roslyn-analyzers.md#automatically-configure-rule-severity).

::: moniker-end

## <a name="net-code-style-settings"></a>Configurações de estilo de código do .NET

As regras de estilo nesta seção são aplicáveis tanto para C# quanto para Visual Basic.

- [Qualificadores "This." e "Me."](#this-and-me)
  - dotnet\_style\_qualification\_for_field
  - dotnet\_style\_qualification\_for_property
  - dotnet\_style\_qualification\_for_method
  - dotnet\_style\_qualification\_for_event
- [Palavras-chave de linguagem em vez de nomes de tipo de estrutura para referências de tipo](#language-keywords)
  - dotnet\_style\_predefined\_type\_for\_locals\_parameters_members
  - dotnet\_style\_predefined\_type\_for\_member_access
- [Preferências de modificador](#normalize-modifiers)
  - dotnet\_style\_require\_accessibility_modifiers
  - visual\_basic\_preferred\_modifier_order
  - dotnet\_style\_readonly\_field
- [Preferências de parênteses](#parentheses-preferences)
  - dotnet\_style\_parentheses\_in\_arithmetic\_binary\_operators
  - dotnet\_style\_parentheses\_in\_other\_binary\_operators
  - dotnet\_style\_parentheses\_in\_other\_operators
  - dotnet\_style\_parentheses\_in\_relational\_binary\_operators
- [Preferências de nível de expressão](#expression-level-preferences)
  - dotnet\_style\_object_initializer
  - dotnet\_style\_collection_initializer
  - dotnet\_style\_explicit\_tuple_names
  - dotnet\_style\_prefer\_inferred\_tuple_names
  - dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names
  - dotnet\_style\_prefer\_auto\_properties
  - dotnet\_style\_prefer\_conditional\_expression\_over\_assignment
  - dotnet\_style\_prefer\_conditional\_expression\_over\_return
  - dotnet\_style\_prefer\_compound\_assignment
- [Preferências de verificação "NULL"](#null-checking-preferences)
  - dotnet\_style\_coalesce_expression
  - dotnet\_style\_null_propagation
  - dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method

### <a name="this-and-me-qualifiers"></a><a name="this-and-me"></a>"Isso". "Este." e "Eu.

Essa regra de estilo pode ser aplicada a campos, propriedades, métodos ou eventos. Um valor **true** significa a preferência pelo símbolo de código ser precedido de `this.` em C# ou `Me.` no Visual Basic. Um valor **false** significa a preferência pelo elemento de código _não_ ser precedido de `this.` ou `Me.`.

Essas regras podem aparecer em um arquivo *. editorconfig* da seguinte maneira:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion
```

#### <a name="dotnet_style_qualification_for_field"></a>dotnet\_style\_qualification\_for_field

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_qualification_for_field |
| **ID da regra** | IDE0003 e IDE0009 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir que os campos sejam precedidos por `this.` em C# ou `Me.` no Visual Basic<br /><br />`false` – preferir que os campos _não_ sejam precedidos por `this.` ou `Me.` |
| **Padrão do Visual Studio** | `false:silent` |

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

#### <a name="dotnet_style_qualification_for_property"></a>dotnet\_style\_qualification\_for_property

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_qualification_for_property |
| **ID da regra** | IDE0003 e IDE0009 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir que as propriedades sejam precedidas com `this.` em C# ou `Me.` no Visual Basic<br /><br />`false` – preferir que as propriedades _não_ sejam precedidas com `this.` ou `Me.` |
| **Padrão do Visual Studio** | `false:silent` |

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

#### <a name="dotnet_style_qualification_for_method"></a>dotnet\_style\_qualification\_for_method

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_qualification_for_method |
| **ID da regra** | IDE0003 e IDE0009 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir que os métodos sejam precedidos por `this.` em C# ou `Me.` no Visual Basic.<br /><br />`false` – preferir que os métodos _não_ sejam precedidos por `this.` ou `Me.`. |
| **Padrão do Visual Studio** | `false:silent` |

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

#### <a name="dotnet_style_qualification_for_event"></a>dotnet\_style\_qualification\_for_event

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_qualification_for_event |
| **ID da regra** | IDE0003 e IDE0009 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir que os eventos sejam precedidos por `this.` em C# ou `Me.` no Visual Basic.<br /><br />`false` – preferir que os eventos _não_ sejam precedidos por `this.` ou `Me.`. |
| **Padrão do Visual Studio** | `false:silent` |

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

### <a name="language-keywords-instead-of-framework-type-names-for-type-references"></a><a name="language-keywords"></a>Palavras-chave de linguagem em vez de nomes de tipos de estrutura para referências de tipo

Essa regra de estilo pode ser aplicada a variáveis locais, parâmetros de método e membros de classe ou como uma regra separada para expressões de acesso a membro de tipo. Um valor **true** significa preferência pela palavra-chave de linguagem (por exemplo, `int` ou `Integer`) em vez do nome do tipo (por exemplo, `Int32`) para tipos que têm uma palavra-chave para representá-los. Um valor **false** significa preferência pelo nome do tipo em vez da palavra-chave de linguagem.

Essas regras podem aparecer em um arquivo *. editorconfig* da seguinte maneira:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion
```

#### <a name="dotnet_style_predefined_type_for_locals_parameters_members"></a>dotnet\_style\_predefined\_type\_for\_locals\_parameters_members

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_predefined_type_for_locals_parameters_members |
| **ID da regra** | IDE0012 e IDE0014 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir a palavra-chave de linguagem para variáveis locais, parâmetros de método e membros de classe, em vez do nome de tipo, para tipos que têm uma palavra-chave para representá-los<br /><br />`false` – preferir o nome do tipo para variáveis locais, parâmetros de método e membros de classe, em vez da palavra-chave de linguagem |
| **Padrão do Visual Studio** | `true:silent` |

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

#### <a name="dotnet_style_predefined_type_for_member_access"></a>dotnet\_style\_predefined\_type\_for\_member_access

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_predefined_type_for_member_access |
| **ID da regra** | IDE0013 e IDE0015 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir a palavra-chave de linguagem para expressões de acesso a membro, em vez do nome de tipo, para tipos que têm uma palavra-chave para representá-los<br /><br />`false` – preferir o nome do tipo para expressões de acesso a membro, em vez da palavra-chave de linguagem |
| **Padrão do Visual Studio** | `true:silent` |

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

### <a name="modifier-preferences"></a><a name="normalize-modifiers"></a>Preferências do modificador

As regras de estilo desta seção dizem respeito às preferências do modificador, incluindo a exigência de modificadores de acessibilidade, a especificação da ordem de classificação de modificador desejada e a exigência do modificador somente leitura.

Essas regras podem aparecer em um arquivo *. editorconfig* da seguinte maneira:

```ini
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

#### <a name="dotnet_style_require_accessibility_modifiers"></a>dotnet\_style\_require\_accessibility_modifiers

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_require_accessibility_modifiers |
| **ID da regra** | IDE0040 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `always` – preferir que modificadores de acessibilidade sejam especificados.<br /><br />`for_non_interface_members` – preferir que modificadores de acessibilidade sejam declarados, exceto os membros de interface pública. (Isso é o mesmo que **always** e foi adicionado para durabilidade, caso o C# adicione métodos de interface padrão.)<br /><br />`never` – não preferir que modificadores de acessibilidade sejam especificados.<br /><br />`omit_if_default` – preferir que modificadores de acessibilidade sejam especificados, exceto se forem o modificador padrão. |
| **Padrão do Visual Studio** | `for_non_interface_members:silent` |
| **Versão introduzida** | Visual Studio 2017 versão 15.5 |

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

#### <a name="csharp_preferred_modifier_order"></a>csharp_preferred_modifier_order

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_preferred_modifier_order |
| **ID da regra** | IDE0036 |
| **Idiomas aplicáveis** | C# |
| **Valores** | Um ou mais modificadores de C#, como `public`, `private`, e `protected` |
| **Padrão do Visual Studio** | `public, private, protected, internal, static, extern, new, virtual, abstract, sealed, override, readonly, unsafe, volatile, async:silent` |
| **Versão introduzida** | Visual Studio 2017 versão 15.5 |

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

#### <a name="visual_basic_preferred_modifier_order"></a>visual_basic_preferred_modifier_order

|Propriedade|Valor|
|-|-|
| **Nome da regra** | visual_basic_preferred_modifier_order |
| **ID da regra** | IDE0036 |
| **Idiomas aplicáveis** | Visual Basic |
| **Valores** | Um ou mais modificadores de Visual Basic, como `Partial`, `Private`, e `Public` |
| **Padrão do Visual Studio** | `Partial, Default, Private, Protected, Public, Friend, NotOverridable, Overridable, MustOverride, Overloads, Overrides, MustInherit, NotInheritable, Static, Shared, Shadows, ReadOnly, WriteOnly, Dim, Const,WithEvents, Widening, Narrowing, Custom, Async:silent` |
| **Versão introduzida** | Visual Studio 2017 versão 15.5 |

- Quando esta regra for definida como uma lista de modificadores, prefira a ordenação especificada.
- Quando esta regra for omitida do arquivo, não prefira uma ordem de modificador.

Exemplos de código:

```vb
' visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async
Public Class MyClass
    Private Shared ReadOnly daysInYear As Int = 365
End Class
```

#### <a name="visual_basic_style_unused_value_expression_statement_preference"></a>visual_basic_style_unused_value_expression_statement_preference

|Propriedade|Valor|
|-|-|
| **Nome da regra** | visual_basic_style_unused_value_expression_statement_preference |
| **ID da regra** | IDE0058 |
| **Idiomas aplicáveis** | Visual Basic |
| **Valores** | `unused_local_variable:silent` |
| **Padrão do Visual Studio** | `unused_local_variable:silent` |

Exemplos de código:

```vb
' visual_basic_style_unused_value_expression_statement_preference = unused_local_variable:silent

Dim unused = Computation()
```

#### <a name="visual_basic_style_unused_value_assignment_preference"></a>visual_basic_style_unused_value_assignment_preference

|Propriedade|Valor|
|-|-|
| **Nome da regra** | visual_basic_style_unused_value_assignment_preference |
| **ID da regra** | IDE0059 |
| **Idiomas aplicáveis** | Visual Basic |
| **Valores** | `unused_local_variable:silent` |
| **Padrão do Visual Studio** | `unused_local_variable:silent` |

Exemplos de código:

```vb
' visual_basic_style_unused_value_assignment_preference = unused_local_variable:suggestion

Dim unused = Computation()
Dim x = 1;
```

#### <a name="dotnet_style_readonly_field"></a>dotnet_style_readonly_field

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_readonly_field |
| **ID da regra** | IDE0044 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir que os campos sejam marcados com `readonly` (C#) ou `ReadOnly` (Visual Basic), caso sejam somente atribuídos de maneira embutida ou dentro de um construtor<br /><br />`false` – não especifique nenhuma preferência sobre se os campos devem ser marcados com `readonly` (C#) ou `ReadOnly` (Visual Basic) |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2017 versão 15.7 |

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

### <a name="parentheses-preferences"></a>Preferências de parênteses

As regras de estilo nesta seção referem-se às preferências de parênteses, incluindo o uso de parênteses para operadores aritméticos, relacionais e outros operadores binários.

Essas regras podem aparecer em um arquivo *. editorconfig* da seguinte maneira:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_operators = never_if_unnecessary:silent
```

#### <a name="dotnet_style_parentheses_in_arithmetic_binary_operators"></a>dotnet\_style\_parentheses\_in\_arithmetic\_binary_operators

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_parentheses_in_arithmetic_binary_operators |
| **ID da regra** | IDE0047 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `always_for_clarity` – preferir parênteses para esclarecer a precedência do operador aritmético (`*`, `/`, `%`, `+`, `-`, `<<`, `>>`, `&`, `^`, `|`)<br /><br />`never_if_unnecessary` – preferir não usar parênteses quando a precedência do operador aritmético (`*`, `/`, `%`, `+`, `-`, `<<`, `>>`, `&`, `^`, `|`) for óbvia |
| **Padrão do Visual Studio** | `always_for_clarity:silent` |
| **Versão introduzida** | Visual Studio 2017 versão 15.8 |

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

#### <a name="dotnet_style_parentheses_in_relational_binary_operators"></a>dotnet\_style\_parentheses\_in\_relational\_binary_operators

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_parentheses_in_relational_binary_operators |
| **ID da regra** | IDE0047 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `always_for_clarity` - preferir parênteses para esclarecer a precedência do operador relacional (`>`, `<`, `<=`, `>=`, `is`, `as`, `==`, `!=`)<br /><br />`never_if_unnecessary` – preferir não usar parênteses quando a precedência do operador relacional (`>`, `<`, `<=`, `>=`, `is`, `as`, `==`, `!=`) for óbvia |
| **Padrão do Visual Studio** | `always_for_clarity:silent` |
| **Versão introduzida** | Visual Studio 2017 versão 15.8 |

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

#### <a name="dotnet_style_parentheses_in_other_binary_operators"></a>dotnet\_style\_parentheses\_in\_other\_binary_operators

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_parentheses_in_other_binary_operators |
| **ID da regra** | IDE0047 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `always_for_clarity` – preferir parênteses para esclarecer a precedência do outro operador binário (`&&`, `||`, `??`)<br /><br />`never_if_unnecessary` – preferir não usar parênteses quando a precedência do outro operador binário (`&&`, `||`, `??`) for óbvia |
| **Padrão do Visual Studio** | `always_for_clarity:silent` |
| **Versão introduzida** | Visual Studio 2017 versão 15.8 |

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

#### <a name="dotnet_style_parentheses_in_other_operators"></a>dotnet\_style\_parentheses\_in\_other_operators

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_parentheses_in_other_operators |
| **ID da regra** | IDE0047 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `always_for_clarity` – preferir parênteses para esclarecer a precedência do operador<br /><br />`never_if_unnecessary` – preferir não usar parênteses quando a precedência do operador for óbvia |
| **Padrão do Visual Studio** | `never_if_unnecessary:silent` |
| **Versão introduzida** | Visual Studio 2017 versão 15.8 |

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

### <a name="expression-level-preferences"></a>Preferências de nível de expressão

As regras de estilo nesta seção referem-se às preferências no nível da expressão, incluindo o uso de inicializadores de objeto, inicializadores de coleção, nomes de tupla explícitos ou inferidos e tipos anônimos inferidos.

Essas regras podem aparecer em um arquivo *. editorconfig* da seguinte maneira:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_prefer_inferred_tuple_names = true:suggestion
dotnet_style_prefer_inferred_anonymous_type_member_names = true:suggestion
dotnet_style_prefer_auto_properties = true:silent
dotnet_style_prefer_conditional_expression_over_assignment = true:suggestion
dotnet_style_prefer_conditional_expression_over_return = true:suggestion
dotnet_style_prefer_compound_assignment = true:suggestion
```

#### <a name="dotnet_style_object_initializer"></a>dotnet\_style\_object_initializer

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_object_initializer |
| **ID da regra** | IDE0017 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir objetos que sejam inicializados usando inicializadores de objeto quando possível<br /><br />`false` – preferir objetos que *não* sejam inicializados usando inicializadores de objeto |
| **Padrão do Visual Studio** | `true:suggestion` |

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

#### <a name="dotnet_style_collection_initializer"></a>dotnet\_style\_collection_initializer

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_collection_initializer |
| **ID da regra** | IDE0028 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – prefira coleções que sejam inicializadas usando inicializadores de coleção quando possível<br /><br />`false` – preferir objetos que *não* sejam inicializados usando inicializadores de coleção |
| **Padrão do Visual Studio** | `true:suggestion` |

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

#### <a name="dotnet_style_explicit_tuple_names"></a>dotnet\_style\_explicit\_tuple_names

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_explicit_tuple_names |
| **ID da regra** | IDE0033 |
| **Idiomas aplicáveis** | C# 7.0+ e Visual Basic 15+ |
| **Valores** | `true` – preferir nomes de tupla a propriedades ItemX<br /><br />`false` – preferir propriedades ItemX a nomes de tupla |
| **Padrão do Visual Studio** | `true:suggestion` |

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

#### <a name="dotnet_style_prefer_inferred_tuple_names"></a>dotnet\_style\_prefer\_inferred\_tuple_names

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_inferred_tuple_names |
| **ID da regra** | IDE0037 |
| **Idiomas aplicáveis** | C# 7.1+ e Visual Basic 15+ |
| **Valores** | `true` – preferir nomes de elementos de tupla inferidos<br /><br />`false` – preferir nomes de elemento de tupla explícita |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2017 versão 15.6 |

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

#### <a name="dotnet_style_prefer_inferred_anonymous_type_member_names"></a>dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_inferred_anonymous_type_member_names |
| **ID da regra** | IDE0037 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir nomes de membro do tipo anônimo inferidos<br /><br />`false` – preferir nomes de membro do tipo anônimo explícitos |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2017 versão 15.6 |

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

#### <a name="dotnet_style_prefer_auto_properties"></a>dotnet\_style\_prefer\_auto\_properties

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_auto_properties |
| **ID da regra** | IDE0032 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir propriedades automáticas em vez de propriedades com campos de suporte particular<br /><br />`false` – preferir propriedades com campos de suporte particular em vez de propriedades automáticas |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2017 versão 15.7 |

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

#### <a name="dotnet_style_prefer_is_null_check_over_reference_equality_method"></a>dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_is_null_check_over_reference_equality_method |
| **ID da regra** | IDE0041 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir usar uma verificação nula com correspondência de padrões em vez de `object.ReferenceEquals`<br /><br />`false` – preferir usar `object.ReferenceEquals` em vez de uma verificação nula com correspondência de padrões |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2017 versão 15.7 |

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

#### <a name="dotnet_style_prefer_conditional_expression_over_assignment"></a>dotnet\_style\_prefer\_conditional\_expression\_over_assignment

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_conditional_expression_over_assignment |
| **ID da regra** | IDE0045 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir atribuições com uma condicional ternária em vez de uma instrução if-else<br /><br />`false` – preferir atribuições com uma instrução if-else em vez de uma condicional ternária |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2017 versão 15.8 |

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

#### <a name="dotnet_style_prefer_conditional_expression_over_return"></a>dotnet\_style\_prefer\_conditional\_expression\_over_return

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_conditional_expression_over_return |
| **ID da regra** | IDE0046 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir que as instruções de retorno usem uma condicional ternária em vez de uma instrução if-else<br /><br />`false` – preferir que as instruções de retorno usem uma instrução if-else em vez de uma condicional ternária |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2017 versão 15.8 |

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

#### <a name="dotnet_style_prefer_compound_assignment"></a>dotnet\_style\_prefer\_compound\_assignment

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_compound_assignment |
| **ID da regra** | IDE0054 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir expressões [de atribuição composta](/dotnet/csharp/language-reference/operators/assignment-operator#compound-assignment)<br /><br />`false` – não preferir expressões de atribuição composta |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// dotnet_style_prefer_compound_assignment = true
x += 1;

// dotnet_style_prefer_compound_assignment = false
x = x + 1;
```

```vb
' dotnet_style_prefer_compound_assignment = true
x += 1

' dotnet_style_prefer_compound_assignment = false
x = x + 1
```

### <a name="null-checking-preferences"></a>Preferências de verificação nula

As regras de estilo nesta seção referem-se às preferências de verificação de nulo.

Essas regras podem aparecer em um arquivo *. editorconfig* da seguinte maneira:

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion
dotnet_style_prefer_is_null_check_over_reference_equality_method = true:silent
```

#### <a name="dotnet_style_coalesce_expression"></a>dotnet\_style\_coalesce_expression

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_coalesce_expression |
| **ID da regra** | IDE0029 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `true` – preferir expressões de coalescência nula a verificação do operador ternário<br /><br />`false` – preferir verificação do operador ternário a expressões de coalescência nula |
| **Padrão do Visual Studio** | `true:suggestion` |

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

#### <a name="dotnet_style_null_propagation"></a>dotnet\_style\_null_propagation

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_null_propagation |
| **ID da regra** | IDE0031 |
| **Idiomas aplicáveis** | C# 6.0+ e Visual Basic 14+ |
| **Valores** | `true` – preferir usar o operador condicional nulo quando possível<br /><br />`false` – preferir usar a verificação nula ternária quando possível |
| **Padrão do Visual Studio** | `true:suggestion` |

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

### <a name="dotnet_style_prefer_is_null_check_over_reference_equality_method"></a>dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_style_prefer_is_null_check_over_reference_equality_method |
| **ID da regra** | IDE0041 |
| **Idiomas aplicáveis** | C# 6.0+ e Visual Basic 14+ |
| **Valores** | `true`-Preferência é nulo verificar o método de igualdade de referência<br /><br />`false`-Preferência de método de igualdade de referência é nulo |
| **Padrão do Visual Studio** | `true:silent` |

## <a name="net-code-quality-settings"></a>Configurações de qualidade de código do .NET

As regras de qualidade nesta seção aplicam-se ao código do C# e do Visual Basic. Elas são usadas para configurar analisadores de código inseridos no IDE (ambiente de desenvolvimento integrado) do Visual Studio. Para saber mais sobre como configurar analisadores FxCop com um arquivo EditorConfig, confira [Configurar analisadores FxCop](../code-quality/configure-fxcop-analyzers.md).

- [Preferências de parâmetro](#parameter-preferences)
  - dotnet\_code\_quality\_unused\_parameters

### <a name="parameter-preferences"></a>Preferências de parâmetro

As regras de qualidade nesta seção dizem respeito aos parâmetros do método.

Essas regras podem aparecer em um arquivo *. editorconfig* da seguinte maneira:

```ini
# CSharp and Visual Basic code quality settings:
[*.{cs,vb}]
dotnet_code_quality_unused_parameters = all:suggestion
```

#### <a name="dotnet_code_quality_unused_parameters"></a>dotnet\_code\_quality\_unused\_parameters

|Propriedade|Valor|
|-|-|
| **Nome da regra** | dotnet_code_quality_unused_parameters |
| **ID da regra** | IDE0060 |
| **Idiomas aplicáveis** | C# e Visual Basic |
| **Valores** | `all` – sinalizar métodos com qualquer acessibilidade que contenha parâmetros não utilizados<br /><br />`non_public` – sinalizar somente métodos não públicos que contêm parâmetros não utilizados |
| **Padrão do Visual Studio** | `all:suggestion` |

Exemplos de código:

```csharp
// dotnet_code_quality_unused_parameters = all:suggestion
public int GetNum() { return 1; }

// dotnet_code_quality_unused_parameters = non_public:suggestion
public int GetNum(int arg1) { return 1; }
```

```vb
' dotnet_code_quality_unused_parameters = all:suggestion
Public Function GetNum()
    Return 1
End Function

' dotnet_code_quality_unused_parameters = non_public:suggestion
Public Function GetNum(arg1 As Integer)
    Return 1
End Function
```

## <a name="c-code-style-settings"></a>Configurações de estilo de código de C#

As regras de estilo nesta seção são aplicáveis somente á linguagem C#.

- [Tipos implícitos e explícitos](#implicit-and-explicit-types)
  - csharp\_style\_var\_for\_built\_in_types
  - csharp\_style\_var\_when\_type\_is_apparent
  - csharp\_style\_var_elsewhere
- [Membros aptos para expressão](#expression-bodied-members)
  - csharp\_style\_expression\_bodied_methods
  - csharp\_style\_expression\_bodied_constructors
  - csharp\_style\_expression\_bodied_operators
  - csharp\_style\_expression\_bodied_properties
  - csharp\_style\_expression\_bodied_indexers
  - csharp\_style\_expression\_bodied_accessors
  - csharp\_style\_expression\_bodied_lambdas
  - csharp\_style\_expression\_bodied\_local_functions
- [Correspondência de padrões](#pattern-matching)
  - csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check
  - csharp\_style\_pattern\_matching\_over\_as\_with\_null_check
- [Declarações de variável embutida](#inlined-variable-declarations)
  - csharp\_style\_inlined\_variable_declaration
- [Preferências de nível de expressão](#c-expression-level-preferences)
  - csharp\_prefer\_simple\_default_expression
- [Preferências de verificação "NULL"](#c-null-checking-preferences)
  - csharp\_style\_throw_expression
  - csharp\_style\_conditional\_delegate_call
- [Preferências de modificador](#normalize-modifiers)
  - csharp\_preferred\_modifier_order
- [Preferências de bloco de código](#code-block-preferences)
  - csharp\_prefer_braces
- [Preferências de valor não utilizadas](#unused-value-preferences)
  - csharp\_style\_unused\_value\_expression\_statement_preference
  - csharp\_style\_unused\_value\_assignment_preference
- [Preferências de índice e de intervalo](#index-and-range-preferences)
  - csharp\_style\_prefer\_index_operator
  - csharp\_style\_prefer\_range_operator
- [Preferências diversas](#miscellaneous-preferences)
  - csharp\_style\_deconstructed\_variable_declaration
  - csharp\_style\_pattern\_local\_over\_anonymous_function
  - csharp\_using\_directive\_placement
  - csharp\_prefer\_static\_local_function
  - csharp\_prefer\_simple\_using_statement
  - csharp\_style\_prefer\_switch_expression

### <a name="implicit-and-explicit-types"></a>Tipos implícitos e explícitos

As regras de estilo nesta seção referem-se ao uso da palavra-chave [var](/dotnet/csharp/language-reference/keywords/var) em vez de um tipo explícito em uma declaração de variável. Essa regra pode ser aplicada separadamente a tipos internos, quando o tipo é aparente e em qualquer outro local.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_var_for_built_in_types = true:suggestion
csharp_style_var_when_type_is_apparent = true:suggestion
csharp_style_var_elsewhere = true:suggestion
```

#### <a name="csharp_style_var_for_built_in_types"></a>csharp\_style\_var\_for\_built\_in_types

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_var_for_built_in_types |
| **ID da regra** | IDE0007 e IDE0008 |
| **Idiomas aplicáveis** | C#  |
| **Valores** | `true` – preferir usar `var` para declarar variáveis com tipos de sistema internos, como `int`<br /><br />`false` – preferir o tipo explícito em vez de `var` para declarar variáveis com tipos de sistema internos, como `int` |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_style_var_for_built_in_types = true
var x = 5;

// csharp_style_var_for_built_in_types = false
int x = 5;
```

#### <a name="csharp_style_var_when_type_is_apparent"></a>csharp\_style\_var\_when\_type\_is_apparent

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_var_when_type_is_apparent |
| **ID da regra** | IDE0007 e IDE0008 |
| **Idiomas aplicáveis** | C#  |
| **Valores** | `true` – preferir `var` quando o tipo já tiver sido mencionado no lado direito de uma expressão de declaração<br /><br />`false` – preferir o tipo explícito em vez de `var` quando o tipo já tiver sido mencionado no lado direito de uma expressão de declaração |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_style_var_when_type_is_apparent = true
var obj = new Customer();

// csharp_style_var_when_type_is_apparent = false
Customer obj = new Customer();
```

#### <a name="csharp_style_var_elsewhere"></a>csharp\_style\_var_elsewhere

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_var_elsewhere |
| **ID da regra** | IDE0007 e IDE0008 |
| **Idiomas aplicáveis** | C#  |
| **Valores** | `true` – preferir `var` em vez de tipo explícito em todos os casos, a menos que a regra seja substituída por outra regra de estilo de código<br /><br />`false` – preferir o tipo explícito em vez de `var` em todos os casos, a menos que a regra seja substituída por outra regra de estilo de código |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_style_var_elsewhere = true
var f = this.Init();

// csharp_style_var_elsewhere = false
bool f = this.Init();
```

### <a name="expression-bodied-members"></a>Membros aptos para expressão

As regras de estilo nesta seção envolvem o uso de [membros aptos para expressão](/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members) quando a lógica consiste em uma única expressão. Essa regra pode ser aplicada a métodos, construtores, operadores, propriedades, indexadores e acessadores.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_expression_bodied_methods = false:silent
csharp_style_expression_bodied_constructors = false:silent
csharp_style_expression_bodied_operators = false:silent
csharp_style_expression_bodied_properties = true:suggestion
csharp_style_expression_bodied_indexers = true:suggestion
csharp_style_expression_bodied_accessors = true:suggestion
csharp_style_expression_bodied_lambdas = true:silent
csharp_style_expression_bodied_local_functions = false:silent
```

#### <a name="csharp_style_expression_bodied_methods"></a>csharp\_style\_expression\_bodied_methods

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_methods |
| **ID da regra** | IDE0022 |
| **Idiomas aplicáveis** | C# 6.0+  |
| **Valores** | `true` – preferir corpos de expressão para métodos<br /><br />`when_on_single_line` – preferir corpos de expressão para métodos quando eles forem uma única linha<br /><br />`false` – preferir corpos de bloco para métodos |
| **Padrão do Visual Studio** | `false:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_methods = true
public int GetAge() => this.Age;

// csharp_style_expression_bodied_methods = false
public int GetAge() { return this.Age; }
```

#### <a name="csharp_style_expression_bodied_constructors"></a>csharp\_style\_expression\_bodied_constructors

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_constructors |
| **ID da regra** | IDE0021 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir corpos de expressão para construtores<br /><br />`when_on_single_line` – preferir corpos de expressão para construtores quando eles forem uma única linha<br /><br />`false` – preferir corpos de bloco para construtores |
| **Padrão do Visual Studio** | `false:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_constructors = true
public Customer(int age) => Age = age;

// csharp_style_expression_bodied_constructors = false
public Customer(int age) { Age = age; }
```

#### <a name="csharp_style_expression_bodied_operators"></a>csharp\_style\_expression\_bodied_operators

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_operators |
| **ID da regra** | IDE0023 e IDE0024 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir corpos de expressão para operadores<br /><br />`when_on_single_line` – preferir corpos de expressão para operadores quando eles forem uma única linha<br /><br />`false` – preferir corpos de blocos para operadores |
| **Padrão do Visual Studio** | `false:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_operators = true
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
    => new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);

// csharp_style_expression_bodied_operators = false
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
{ return new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary); }
```

#### <a name="csharp_style_expression_bodied_properties"></a>csharp\_style\_expression\_bodied_properties

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_properties |
| **ID da regra** | IDE0025 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir corpos de expressão para propriedades<br /><br />`when_on_single_line` – preferir corpos de expressão para propriedades quando eles forem uma única linha<br /><br />`false` – preferir blocos do corpo para propriedades |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_properties = true
public int Age => _age;

// csharp_style_expression_bodied_properties = false
public int Age { get { return _age; }}
```

#### <a name="csharp_style_expression_bodied_indexers"></a>csharp\_style\_expression\_bodied_indexers

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_indexers |
| **ID da regra** | IDE0026 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir corpos de expressão para indexadores<br /><br />`when_on_single_line` – preferir corpos de expressão para indexadores quando eles forem uma única linha<br /><br />`false` – preferir blocos do corpo para indexadores |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_indexers = true
public T this[int i] => _values[i];

// csharp_style_expression_bodied_indexers = false
public T this[int i] { get { return _values[i]; } }
```

#### <a name="csharp_style_expression_bodied_accessors"></a>csharp\_style\_expression\_bodied_accessors

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_accessors |
| **ID da regra** | IDE0027 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir corpos de expressão para acessadores<br /><br />`when_on_single_line` – preferir corpos de expressão para acessadores quando eles forem uma única linha<br /><br />`false` – preferir blocos do corpo para acessadores |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_accessors = true
public int Age { get => _age; set => _age = value; }

// csharp_style_expression_bodied_accessors = false
public int Age { get { return _age; } set { _age = value; } }
```

#### <a name="csharp_style_expression_bodied_lambdas"></a>csharp\_style\_expression\_bodied_lambdas

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_lambdas |
| **ID da regra** | IDE0053 |
| **Valores** | `true` – preferir corpos de expressão para lambdas<br /><br />`when_on_single_line` – preferir corpos de expressão para lambdas quando eles forem uma única linha<br /><br />`false` – preferir corpos de bloco para lambdas |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_lambdas = true
Func<int, int> square = x => x * x;

// csharp_style_expression_bodied_lambdas = false
Func<int, int> square = x => { return x * x; };
```

#### <a name="csharp_style_expression_bodied_local_functions"></a>csharp\_style\_expression\_bodied\_local_functions

Começando com o C# 7.0, o C# é compatível com [funções locais](/dotnet/csharp/programming-guide/classes-and-structs/local-functions). Funções locais são métodos privados de um tipo que estão aninhados em outro membro.

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_expression_bodied_local_functions |
| **ID da regra** | IDE0061 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir corpos de expressão para funções locais<br /><br />`when_on_single_line` – preferir corpos de expressão para funções locais quando eles forem uma única linha<br /><br />`false` – preferir corpos de bloco para funções locais |
| **Padrão do Visual Studio** | `false:silent` |

Exemplos de código:

```csharp
// csharp_style_expression_bodied_local_functions = true
void M()
{
    Hello();
    void Hello() => Console.WriteLine("Hello");
}

// csharp_style_expression_bodied_local_functions = false
void M()
{
    Hello();
    void Hello()
    {
        Console.WriteLine("Hello");
    }
}
```

### <a name="pattern-matching"></a>Correspondência de padrões

As regras de estilo nesta seção envolvem o uso de [correspondência de padrões](/dotnet/csharp/pattern-matching) em C#.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
```

#### <a name="csharp_style_pattern_matching_over_is_with_cast_check"></a>csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_pattern_matching_over_is_with_cast_check |
| **ID da regra** | IDE0020 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – prefira a correspondência de padrões a expressões `is` com conversões de tipo<br /><br />`false` – prefira expressões `is` com conversões de tipo a correspondência de padrões |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_style_pattern_matching_over_is_with_cast_check = true
if (o is int i) {...}

// csharp_style_pattern_matching_over_is_with_cast_check = false
if (o is int) {var i = (int)o; ... }
```

#### <a name="csharp_style_pattern_matching_over_as_with_null_check"></a>csharp\_style\_pattern\_matching\_over\_as\_with\_null_check

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_pattern_matching_over_as_with_null_check |
| **ID da regra** | IDE0019 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – prefira correspondência de padrões a expressões `as` com verificações nulas para determinar se algo é de um tipo específico<br /><br />`false` – prefira expressões `as` com verificações de null a correspondência de padrões para determinar se algo é de um tipo específico |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_style_pattern_matching_over_as_with_null_check = true
if (o is string s) {...}

// csharp_style_pattern_matching_over_as_with_null_check = false
var s = o as string;
if (s != null) {...}
```

### <a name="inlined-variable-declarations"></a>Declarações de variável embutida

Essa regra de estilo é relacionada a se as variáveis `out` são declaradas embutidas ou não. Após o C#7, você pode [declarar uma variável de saída na lista de argumentos de uma chamada de método](/dotnet/csharp/language-reference/keywords/out-parameter-modifier#calling-a-method-with-an-out-argument) em vez de declará-la em uma declaração de variável separada.

#### <a name="csharp_style_inlined_variable_declaration"></a>csharp\_style\_inlined\_variable_declaration

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_inlined_variable_declaration |
| **ID da regra** | IDE0018 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir que as variáveis `out` sejam declaradas embutidas na lista de argumentos de uma chamada de método quando possível<br /><br />`false` – preferir `out` variáveis sejam declaradas antes da chamada de método |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_style_inlined_variable_declaration = true
if (int.TryParse(value, out int i) {...}

// csharp_style_inlined_variable_declaration = false
int i;
if (int.TryParse(value, out i) {...}
```

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_inlined_variable_declaration = true:suggestion
```

### <a name="c-expression-level-preferences"></a>Preferências de nível de expressão do C#

As regras de estilo nesta seção referem-se às preferências de nível de expressão.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_prefer_simple_default_expression = true:suggestion
```

#### <a name="csharp_prefer_simple_default_expression"></a>csharp\_prefer\_simple\_default_expression

Essa regra de estilo se refere ao uso do [ `default` literal para expressões de valor padrão](/dotnet/csharp/language-reference/operators/default#default-literal) quando o compilador pode inferir o tipo da expressão.

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_prefer_simple_default_expression |
| **ID da regra** | IDE0034 |
| **Idiomas aplicáveis** | C# 7.1+  |
| **Valores** | `true` – preferir `default` a `default(T)`<br /><br />`false` – preferir `default(T)` a `default` |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_prefer_simple_default_expression = true
void DoWork(CancellationToken cancellationToken = default) { ... }

// csharp_prefer_simple_default_expression = false
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }
```

### <a name="c-null-checking-preferences"></a>Preferências de verificação nula do C#

Essas regras de estilo referem-se à sintaxe da verificação de `null`, incluindo o uso de expressões `throw` ou instruções `throw`, e se é desejável executar uma verificação nula ou usar o operador de união condicional (`?.`) ao invocar uma [expressão lambda](/dotnet/csharp/lambda-expressions).

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = false:suggestion
```

#### <a name="csharp_style_throw_expression"></a>csharp\_style\_throw_expression

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_throw_expression |
| **ID da regra** | IDE0016 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir usar expressões `throw` a usar instruções `throw`<br /><br />`false` – preferir usar instruções `throw` a usar expressões `throw` |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_style_throw_expression = true
this.s = s ?? throw new ArgumentNullException(nameof(s));

// csharp_style_throw_expression = false
if (s == null) { throw new ArgumentNullException(nameof(s)); }
this.s = s;
```

#### <a name="csharp_style_conditional_delegate_call"></a>csharp\_style\_conditional\_delegate_call

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_conditional_delegate_call |
| **ID da regra** | IDE0041 |
| **Idiomas aplicáveis** | C# 6.0+  |
| **Valores** | `true` – preferir usar o operador de união condicional (`?.`) ao invocar uma expressão lambda, em vez de realizar uma verificação nula<br /><br />`false` – preferir realizar uma verificação nula antes de invocar uma expressão lambda a usar o operador de união condicional (`?.`) |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_style_conditional_delegate_call = true
func?.Invoke(args);

// csharp_style_conditional_delegate_call = false
if (func != null) { func(args); }
```

### <a name="code-block-preferences"></a>Preferências de bloco de código

Essa regra de estilo diz respeito ao uso de chaves `{ }` para cercar blocos de código.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_prefer_braces = true:silent
```

#### <a name="csharp_prefer_braces"></a>csharp\_prefer\_braces

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_prefer_braces |
| **ID da regra** | IDE0011 |
| **Idiomas aplicáveis** | C# |
| **Valores** | `true` – preferir chaves, até mesmo para uma linha de código<br /><br />`false` – preferir não usar chaves se permitido<br /><br />`when_multiline`-Preferir chaves em várias linhas |
| **Padrão do Visual Studio** | `true:silent` |

Exemplos de código:

```csharp
// csharp_prefer_braces = true
if (test) { this.Display(); }

// csharp_prefer_braces = false
if (test) this.Display();
```

### <a name="unused-value-preferences"></a>Preferências de valor não utilizadas

Essas regras de estilo referem-se a expressões e atribuições de valor não utilizadas.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_unused_value_expression_statement_preference = discard_variable:silent
csharp_style_unused_value_assignment_preference = discard_variable:suggestion
```

#### <a name="csharp_style_unused_value_expression_statement_preference"></a>csharp_style_unused_value_expression_statement_preference

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_unused_value_expression_statement_preference |
| **ID da regra** | IDE0058 |
| **Idiomas aplicáveis** | C# |
| **Valores** | `discard_variable` – preferir atribuir uma expressão não utilizada a um [descarte](/dotnet/csharp/discards) <br /><br />`unused_local_variable` – preferir atribuir uma expressão não utilizada a uma variável local |
| **Padrão do Visual Studio** | `discard_variable:silent` |

Exemplos de código:

```csharp
// Original code:
System.Convert.ToInt32("35");

// After code fix for IDE0058:

// csharp_style_unused_value_expression_statement_preference = discard_variable
_ = System.Convert.ToInt32("35");

// csharp_style_unused_value_expression_statement_preference = unused_local_variable
var unused = Convert.ToInt32("35");
```

#### <a name="csharp_style_unused_value_assignment_preference"></a>csharp_style_unused_value_assignment_preference

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_unused_value_assignment_preference |
| **ID da regra** | IDE0059 |
| **Idiomas aplicáveis** | C# |
| **Valores** | `discard_variable` – preferir usar um [descarte](/dotnet/csharp/discards) ao atribuir um valor que não é usado<br /><br />`unused_local_variable` – preferir usar uma variável local ao atribuir um valor que não é usado |
| **Padrão do Visual Studio** | `discard_variable:suggestion` |

Exemplos de código:

```csharp
// csharp_style_unused_value_assignment_preference = discard_variable
int GetCount(Dictionary<string, int> wordCount, string searchWord)
{
    _ = wordCount.TryGetValue(searchWord, out var count);
    return count;
}

// csharp_style_unused_value_assignment_preference = unused_local_variable
int GetCount(Dictionary<string, int> wordCount, string searchWord)
{
    var unused = wordCount.TryGetValue(searchWord, out var count);
    return count;
}
```

### <a name="index-and-range-preferences"></a>Preferências de índice e de intervalo

Essas regras de estilo referem-se ao uso de operadores de índice e de intervalo, que estão disponíveis no C# 8.0 e posterior.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_prefer_index_operator = true:suggestion
csharp_style_prefer_range_operator = true:suggestion
```

#### <a name="csharp_style_prefer_index_operator"></a>csharp\_style\_prefer\_index_operator

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_prefer_index_operator |
| **ID da regra** | IDE0056 |
| **Idiomas aplicáveis** | C# 8.0+ |
| **Valores** | `true` – preferir usar o operador `^` ao calcular um índice com base no final de uma coleção<br /><br />`false` – não preferir usar o operador `^` ao calcular um índice com base no final de uma coleção |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_style_prefer_index_operator = true
string[] names = { "Archimedes", "Pythagoras", "Euclid" };
var index = names[^1];

// csharp_style_prefer_index_operator = false
string[] names = { "Archimedes", "Pythagoras", "Euclid" };
var index = names[names.Length - 1];
```

#### <a name="csharp_style_prefer_range_operator"></a>csharp\_style\_prefer\_range_operator

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_prefer_range_operator |
| **ID da regra** | IDE0057 |
| **Idiomas aplicáveis** | C# 8.0+ |
| **Valores** | `true` – preferir usar o operador de intervalo `..` ao extrair uma "fatia" de uma coleção<br /><br />`false` – não preferir usar o operador de intervalo `..` ao extrair uma "fatia" de uma coleção |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_style_prefer_range_operator = true
string sentence = "the quick brown fox";
var sub = sentence[0..^4];

// csharp_style_prefer_range_operator = false
string sentence = "the quick brown fox";
var sub = sentence.Substring(0, sentence.Length - 4);
```

### <a name="miscellaneous-preferences"></a>Preferências diversas

Esta seção contém regras de estilo diversas.

Exemplo de arquivo *.editorconfig*:

```ini
# CSharp code style settings:
[*.cs]
csharp_style_deconstructed_variable_declaration = true:suggestion
csharp_style_pattern_local_over_anonymous_function = true:suggestion
csharp_using_directive_placement = outside_namespace:silent
csharp_prefer_static_local_function = true:suggestion
csharp_prefer_simple_using_statement = true:suggestion
csharp_style_prefer_switch_expression = true:suggestion
```

#### <a name="csharp_style_deconstructed_variable_declaration"></a>csharp\_style\_deconstructed\_variable_declaration

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_deconstructed_variable_declaration |
| **ID da regra** | IDE0042 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir declaração de variável desconstruída<br /><br />`false` – não preferir a desconstrução em declarações de variável |
| **Padrão do Visual Studio** | `true:suggestion` |

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

#### <a name="csharp_style_pattern_local_over_anonymous_function"></a>csharp\_style\_pattern\_local\_over\_anonymous_function

Começando com o C# 7.0, o C# é compatível com [funções locais](/dotnet/csharp/programming-guide/classes-and-structs/local-functions). Funções locais são métodos privados de um tipo que estão aninhados em outro membro.

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_pattern_local_over_anonymous_function |
| **ID da regra** | IDE0039 |
| **Idiomas aplicáveis** | C# 7.0+ |
| **Valores** | `true` – preferir as funções locais em vez de funções anônimas<br /><br />`false` – preferir as funções anônimas em vez de funções locais |
| **Padrão do Visual Studio** | `true:suggestion` |

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

#### <a name="csharp_using_directive_placement"></a>csharp\_using\_directive_placement

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_using_directive_placement |
| **ID da regra** | IDE0065 |
| **Idiomas aplicáveis** | C# |
| **Valores** | `outside_namespace` – preferir que diretivas `using` sejam colocadas fora do namespace<br /><br />`inside_namespace` – preferir que diretivas `using` sejam colocadas dentro do namespace |
| **Padrão do Visual Studio** | `outside_namespace:silent` |

Exemplos de código:

```csharp
// csharp_using_directive_placement = outside_namespace
using System;

namespace Conventions
{
    ...
}

// csharp_using_directive_placement = inside_namespace
namespace Conventions
{
    using System;
    ...
}
```

#### <a name="csharp_prefer_static_local_function"></a>csharp\_prefer\_static\_local_function

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_prefer_static_local_function |
| **ID da regra** | IDE0062 |
| **Idiomas aplicáveis** | C# 8.0+ |
| **Valores** | `true` – preferir que as funções locais sejam marcadas `static`<br /><br />`false` – não preferir que as funções locais sejam marcadas `static` |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_prefer_static_local_function = true
void M()
{
    Hello();
    static void Hello()
    {
        Console.WriteLine("Hello");
    }
}

// csharp_prefer_static_local_function = false
void M()
{
    Hello();
    void Hello()
    {
        Console.WriteLine("Hello");
    }
}
```

#### <a name="csharp_prefer_simple_using_statement"></a>csharp\_prefer\_simple\_using_statement

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_prefer_simple_using_statement |
| **ID da regra** | IDE0063 |
| **Idiomas aplicáveis** | C# 8.0+ |
| **Valores** | `true`-Preferir usar uma instrução *simples* `using`<br /><br />`false`-Não prefiro usar uma instrução *simples* `using` |
| **Padrão do Visual Studio** | `true:suggestion` |

Exemplos de código:

```csharp
// csharp_prefer_simple_using_statement = true
using var a = b;

// csharp_prefer_simple_using_statement = false
using (var a = b) { }
```

#### <a name="csharp_style_prefer_switch_expression"></a>csharp\_style\_prefer\_switch_expression

|Propriedade|Valor|
|-|-|
| **Nome da regra** | csharp_style_prefer_switch_expression |
| **ID da regra** | IDE0066 |
| **Idiomas aplicáveis** | C# 8.0+ |
| **Valores** | `true` – Preferir usar uma expressão `switch` (introduzida com C# 8.0)<br /><br />`false` – Preferir usar uma [instrução switch](/dotnet/csharp/language-reference/keywords/switch) |
| **Padrão do Visual Studio** | `true:suggestion` |
| **Versão introduzida** | Visual Studio 2019 versão 16.2 |

Exemplos de código:

```csharp
// csharp_style_prefer_switch_expression = true
return x switch
{
    1 => 1 * 1,
    2 => 2 * 2,
    _ => 0,
};

// csharp_style_prefer_switch_expression = false
switch (x)
{
    case 1:
        return 1 * 1;
    case 2:
        return 2 * 2;
    default:
        return 0;
}
```

## <a name="see-also"></a>Confira também

- [Convenções de formatação](editorconfig-formatting-conventions.md)
- [Convenções de nomenclatura](editorconfig-naming-conventions.md)
- [Configurações da Convenção de codificação .NET para EditorConfig](editorconfig-code-style-settings-reference.md)
