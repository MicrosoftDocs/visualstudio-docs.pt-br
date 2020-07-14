---
title: 'CA1500: nomes de variáveis não devem corresponder a nomes de campos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
helpviewer_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
ms.assetid: fa0e5029-79e9-4a33-8576-787ac3c26c39
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9565bc1ae3166c0475e8af7f0fde381497309b01
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547908"
---
# <a name="ca1500-variable-names-should-not-match-field-names"></a>CA1500: Nomes de variável não devem corresponder a nomes de campo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente sobre o Visual Studio, consulte [CA1500: nomes de variáveis não devem corresponder a nomes de campos](/visualstudio/code-quality/ca1500-variable-names-should-not-match-field-names).

|Item|Valor|
|-|-|
|TypeName|VariableNamesShouldNotMatchFieldNames|
|CheckId|CA1500|
|Categoria|Microsoft. Maintainabilidade|
|Alteração Significativa|Quando acionado em um parâmetro que tem o mesmo nome de um campo:<br /><br /> -Não separável – se o campo e o método que declara o parâmetro não puderem ser vistos fora do assembly, independentemente da alteração feita.<br />-Separável-se você alterar o nome do campo e puder ser visto fora do assembly.<br />-Quebra-se você alterar o nome do parâmetro e o método que o declara pode ser visto fora do assembly.<br /><br /> Quando acionado em uma variável local que tem o mesmo nome de um campo:<br /><br /> -Não separável – se o campo não puder ser visto fora do assembly, independentemente da alteração feita.<br />-Não separável – se você alterar o nome da variável local e não alterar o nome do campo.<br />-Quebra-se você alterar o nome do campo e ele pode ser visto fora do assembly.|

## <a name="cause"></a>Causa
 Um método de instância declara um parâmetro ou uma variável local cujo nome corresponde a um campo de instância do tipo declarativo. Para capturar variáveis locais que violam a regra, o assembly testado deve ser criado usando informações de depuração e o arquivo de banco de dados do programa (. pdb) associado deve estar disponível.

## <a name="rule-description"></a>Descrição da Regra
 Quando o nome de um campo de instância corresponde a um parâmetro ou a um nome de variável local, o campo de instância é acessado usando a `this` `Me` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] palavra-chave (in) quando está dentro do corpo do método. Ao manter o código, é fácil esquecer essa diferença e assumir que a variável de parâmetro/local se refere ao campo de instância, que leva a erros. Isso é verdadeiro especialmente para corpos de métodos longos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, renomeie o parâmetro/variável ou o campo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra duas violações da regra.

 [!code-csharp[FxCop.Maintainability.VarMatchesField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/cs/FxCop.Maintainability.VarMatchesField.cs#1)]
 [!code-vb[FxCop.Maintainability.VarMatchesField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/vb/FxCop.Maintainability.VarMatchesField.vb#1)]
