---
title: 'CA1500: os nomes de variável não devem corresponder aos nomes de campo'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
helpviewer_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
ms.assetid: fa0e5029-79e9-4a33-8576-787ac3c26c39
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 74f9cfadc4bc413c3b176d5f37f1017074547435
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548244"
---
# <a name="ca1500-variable-names-should-not-match-field-names"></a>CA1500: os nomes de variável não devem corresponder aos nomes de campo

|||
|-|-|
|NomeDoTipo|VariableNamesShouldNotMatchFieldNames|
|CheckId|CA1500|
|Categoria|Microsoft.Maintainability|
|Alteração Significativa|Quando disparado em um parâmetro que tem o mesmo nome como um campo:<br /><br /> Sem quebra - se o campo e o método que declara o parâmetro não podem ser vistos fora do assembly, independentemente da alteração feita.<br />-Quebrando - se você alterar o nome do campo e pode ser vistos fora do assembly.<br />-Quebrando - se você alterar o nome do parâmetro e o método que declara que ele pode ser visto de fora do assembly.<br /><br /> Quando acionado em uma variável local que tem o mesmo nome como um campo:<br /><br /> Sem quebra - se o campo não pode ser visto de fora do assembly, independentemente da alteração feita.<br />Sem quebra - se você alterar o nome da variável local e não altere o nome do campo.<br />-Quebrando - se você alterar o nome do campo e ele pode ser visto de fora do assembly.|

## <a name="cause"></a>Causa

Um método de instância declara um parâmetro ou uma variável local cujo nome corresponde a um campo de instância do tipo declarativo. Para capturar as variáveis locais que violam a regra, o assembly testado deve ser criado usando as informações de depuração e o arquivo de banco de dados (. PDB) do programa associado deve estar disponível.

## <a name="rule-description"></a>Descrição da regra

Quando o nome de um campo de instância corresponde a um parâmetro ou um nome de variável local, o campo de instância é acessado usando o `this` (`Me` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) palavra-chave quando dentro do corpo de método. Durante a manutenção de código, é fácil esquecer essa diferença e pressupõem que a variável de parâmetro/local se refere ao campo de instância, o que leva a erros. Isso vale especialmente para corpos de método demorado.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, renomeie o parâmetro/variável ou o campo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra dois violações da regra.

[!code-vb[FxCop.Maintainability.VarMatchesField#1](../code-quality/codesnippet/VisualBasic/ca1500-variable-names-should-not-match-field-names_1.vb)]
[!code-csharp[FxCop.Maintainability.VarMatchesField#1](../code-quality/codesnippet/CSharp/ca1500-variable-names-should-not-match-field-names_1.cs)]