---
title: Convenções de nomenclatura do .NET para arquivos EditorConfig
ms.date: 11/20/2017
ms.topic: reference
helpviewer_keywords:
- naming conventions [EditorConfig]
- EditorConfig naming conventions
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: df74252361e330ac992f8f3e852d9c33006d18e7
ms.sourcegitcommit: 6672a1e9d135d7e5cca3cceea07c6fe5a0871475
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47443578"
---
# <a name="net-naming-conventions-for-editorconfig"></a>Convenções de nomenclatura do .NET para EditorConfig

As convenções de nomenclatura referem-se à nomenclatura dos elementos de código, como classes, propriedades e métodos. Por exemplo, é possível especificar que membros públicos devem ser escritos em maiúsculas ou que métodos assíncronos devem terminar com "Async". É possível aplicar essas regras especificando-as em um [arquivo .editorconfig](../ide/create-portable-custom-editor-options.md). Violações de regras de nomenclatura são exibidas na **Lista de Erros** ou como uma sugestão embaixo do nome, dependendo da gravidade escolhida para a regra. Não é necessário criar o projeto para ver as violações.

As convenções de nomenclatura devem ser ordenadas da mais específica para a menos específica no arquivo *.editorconfig*. A primeira regra encontrada que pode ser aplicada é a única regra que é aplicada.

Para cada convenção de nomenclatura, é necessário especificar os símbolos aos quais ela se aplica, um estilo de nomenclatura e uma gravidade para impor a convenção, usando as propriedades descritas abaixo. A ordem das propriedades não é importante.

Para começar, escolha um título para a regra de nomenclatura que será usada em cada uma das propriedades necessárias para descrever completamente a regra. Por exemplo, `public_members_must_be_capitalized` é um nome bom e descritivo para uma regra de nomenclatura. Vamos nos referir ao título escolhido como **<namingRuleTitle\>** nas seções a seguir.

## <a name="symbols"></a>Símbolos

Primeiro, identifique um grupo de símbolos ao qual aplicar a regra de nomenclatura. Essa propriedade tem o seguinte formato:

`dotnet_naming_rule.<namingRuleTitle>.symbols = <symbolTitle>`

Dê um nome ao grupo de símbolos, substituindo o valor **<symbolTitle\>** por um título descritivo, por exemplo `public_symbols`. Você usará o valor **<symbolTitle\>** nos três nomes de propriedade que descrevem a quais símbolos a regra é aplicada (tipos de símbolo, níveis de acessibilidade e modificadores).

### <a name="kinds-of-symbols"></a>Tipos de símbolos

Para descrever o tipo de símbolos aos quais aplicar a regra de nomenclatura, especifique uma propriedade no formato a seguir:

`dotnet_naming_symbols.<symbolTitle>.applicable_kinds = <values>`

A lista a seguir mostra os valores permitidos e é possível especificar vários valores separando-os por vírgula.

- \* (use este valor para especificar todos os símbolos)
- namespace
- classe
- struct
- interface
- enum
- propriedade
- method
- campo
- evento
- delegado
- parâmetro
- type_parameter
- local
- local_function

### <a name="accessibility-levels-of-symbols"></a>Níveis de acessibilidade de símbolos

Para descrever os níveis de acessibilidade dos símbolos aos quais você deseja aplicar a regra de nomenclatura, especifique um nome de propriedade no formato a seguir:

`dotnet_naming_symbols.<symbolTitle>.applicable_accessibilities = <values>`

A lista a seguir mostra os valores permitidos e é possível especificar vários valores separando-os por vírgula.

- \* (use este valor para especificar todos os níveis de acessibilidade)
- públicos
- interno ou amigo
- particulares
- protegidos
- protected\_internal or protected_friend
- local

> [!NOTE]
> Não especifique um nível de acessibilidade como parte de sua convenção de nomenclatura se a acessibilidade não for aplicável ao tipo de símbolo para o qual você está direcionando. Por exemplo, parâmetros não tem níveis de acessibilidade. Se você especificar um nível de acessibilidade para uma convenção de nomenclatura de parâmetro, a regra de nomenclatura não funcionará corretamente.

### <a name="symbol-modifiers"></a>Modificadores de símbolo

Para descrever os modificadores dos símbolos aos quais você deseja aplicar a regra de nomenclatura, especifique um nome de propriedade no formato a seguir:

`dotnet_naming_symbols.<symbolTitle>.required_modifiers = <values>`

A lista a seguir mostra os valores permitidos e é possível especificar vários valores separando-os por vírgula.

- `abstract` ou `must_inherit`
- `async`
- `const`
- `readonly`
- `static` ou `shared`

   > [!NOTE]
   > Se você tiver uma regra de nomenclatura para os símbolos `static` ou `shared`, ela também se aplicará aos símbolos `const` porque são implicitamente estáticos. Se não quiser que a regra de nomenclatura `static` se aplique aos símbolos `const`, crie uma regra de nomenclatura separada para os símbolos `const`.

`required_modifiers` é uma propriedade opcional. Se você omitir esta propriedade, a regra de nomenclatura será aplicada a todos os modificadores.

## <a name="style"></a>Estilo

Agora que identificamos o grupo de símbolos ao qual aplicar a regra de nomenclatura, é necessário descrever o estilo de nomenclatura. Pode ser que um estilo tenha um determinado prefixo ou sufixo ou que palavras individuais no nome sejam separadas por um determinado caractere. Também é possível especificar um estilo de uso de maiúsculas. A propriedade do estilo tem o seguinte formato:

`dotnet_naming_rule.<namingRuleTitle>.style = <styleTitle>`

Dê um nome ao estilo substituindo o valor **<styleTitle\>** por um título descritivo, por exemplo `first_word_upper_case_style`. Use o valor **<styleTitle\>** nos nomes de propriedade que descrevem o estilo de nomenclatura (prefixo, sufixo, caractere separador de palavras e uso de maiúsculas). Use uma ou mais propriedades dessas para descrever seu estilo.

### <a name="require-a-prefix"></a>Exigir um prefixo

Para especificar que os nomes de símbolos devem começar com determinados caracteres, use esta propriedade:

`dotnet_naming_style.<styleTitle>.required_prefix = <prefix>`

### <a name="require-a-suffix"></a>Exigir um sufixo

Para especificar que os nomes de símbolos devem terminar com determinados caracteres, use esta propriedade:

`dotnet_naming_style.<styleTitle>.required_suffix = <suffix>`

### <a name="require-a-certain-word-separator"></a>Exigir um determinado separador de palavras

Para especificar que palavras individuais em nomes de símbolos devem ser separadas por um determinado caractere, use esta propriedade:

`dotnet_naming_style.<styleTitle>.word_separator = <separator character>`

### <a name="require-a-capitalization-style"></a>Exigir um estilo de uso de maiúsculas

Para especificar um estilo de uso de maiúsculas específico para nomes de símbolos, use esta propriedade:

`dotnet_naming_style.<styleTitle>.capitalization = <value>`

Os valores permitidos para essa propriedade são:

- pascal_case
- camel_case
- first\_word_upper
- all\_upper
- all_lower

> [!NOTE]
> É necessário especificar um estilo de uso de maiúsculas como parte do seu estilo de nomenclatura; caso contrário, o estilo de nomenclatura poderá ser ignorado.

## <a name="severity"></a>Severidade

Para descrever a gravidade de uma violação da sua regra de nomenclatura, especifique uma propriedade no seguinte formato:

`dotnet_naming_rule.<namingRuleTitle>.severity = <value>`

A tabela a seguir mostra os valores de gravidade permitidos e o que eles significam:

Severidade | Efeito
------------ | -------------
nenhuma ou silenciosa | Quando este estilo não estiver sendo seguido, não mostre nada para o usuário; no entanto, o código gerado automaticamente seguirá esse estilo.
sugestão | Quando esse estilo não estiver sendo seguido, mostre-o para o usuário como uma sugestão, como pontos subjacentes nos dois primeiros caracteres. Isso não terá nenhum efeito em tempo de compilação.
aviso | Quando esse estilo não estiver sendo seguido, mostre um aviso do compilador na **Lista de Erros**.
erro | Quando esse estilo não estiver sendo seguido, mostre um erro do compilador na **Lista de Erros**.

> [!NOTE]
> Não é necessário criar seu projeto para ver as violações de regras de nomenclatura. Elas são exibidas à medida que o código é editado, na **Lista de Erros** ou como uma sugestão.

## <a name="example"></a>Exemplo

O arquivo *.editorconfig* a seguir contém uma convenção de nomenclatura que especifica que propriedades públicas, métodos, campos, eventos e delegados devem sempre ser escritos com maiúsculas. Observe que esta convenção de nomenclatura especifica vários tipos de símbolo aos quais aplicar a regra, usando uma vírgula para separar os valores.

```EditorConfig
# Public members must be capitalized (public_members_must_be_capitalized)
[*.{cs,vb}]
dotnet_naming_rule.public_members_must_be_capitalized.symbols   = public_symbols
dotnet_naming_symbols.public_symbols.applicable_kinds           = property,method,field,event,delegate
dotnet_naming_symbols.public_symbols.applicable_accessibilities = public
dotnet_naming_symbols.public_symbols.required_modifiers         = readonly

dotnet_naming_rule.public_members_must_be_capitalized.style    = first_word_upper_case_style
dotnet_naming_style.first_word_upper_case_style.capitalization = first_word_upper

dotnet_naming_rule.public_members_must_be_capitalized.severity = suggestion
```

A captura de tela a seguir mostra o efeito desta convenção de nomenclatura no editor. Duas variáveis públicas foram nomeadas sem a primeira letra ser maiúscula. Uma é um `const` e a outra é `readonly`. Como a regra de nomenclatura aplica-se apenas aos símbolos `readonly`, apenas a variável `readonly` mostra uma sugestão de regra de nomenclatura.

![Sugestão de regra de nomenclatura](media/editorconfig-naming-rule-suggestion.png)

Agora vamos alterar a gravidade da violação para `warning`:

```EditorConfig
dotnet_naming_rule.public_members_must_be_capitalized.severity = warning
```

Se você fechar e reabrir o arquivo de código, em vez de ver a sugestão embaixo da violação de nome, você verá um rabisco verde e um aviso na **Lista de Erros**:

![Aviso de regra de nomenclatura](media/editorconfig-naming-rule-warning.png)

## <a name="see-also"></a>Consulte também

- [Convenções de formatação e linguagem .NET](../ide/editorconfig-code-style-settings-reference.md)
- [Criar opções do editor portátil e personalizado](../ide/create-portable-custom-editor-options.md)
- [Arquivo .editorconfig da plataforma do compilador do .NET](https://github.com/dotnet/roslyn/blob/master/.editorconfig)
