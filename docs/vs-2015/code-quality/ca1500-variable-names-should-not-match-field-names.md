---
title: 'CA1500: Os nomes de variáveis não devem corresponder aos nomes de campo | Microsoft Docs'
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
- VariableNamesShouldNotMatchFieldNames
- CA1500
helpviewer_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
ms.assetid: fa0e5029-79e9-4a33-8576-787ac3c26c39
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: fdac60aa7b3fb37f45cff7c1c9e5f17920efed18
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49173934"
---
# <a name="ca1500-variable-names-should-not-match-field-names"></a>CA1500: os nomes de variável não devem corresponder aos nomes de campo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA1500: os nomes de variáveis não devem corresponder aos nomes de campo](https://docs.microsoft.com/visualstudio/code-quality/ca1500-variable-names-should-not-match-field-names) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|VariableNamesShouldNotMatchFieldNames|  
|CheckId|CA1500|  
|Categoria|Microsoft.Maintainability|  
|Alteração Significativa|Quando disparado em um parâmetro que tem o mesmo nome como um campo:<br /><br /> Sem quebra - se o campo e o método que declara o parâmetro não podem ser vistos fora do assembly, independentemente da alteração feita.<br />-Quebrando - se você alterar o nome do campo e pode ser vistos fora do assembly.<br />-Quebrando - se você alterar o nome do parâmetro e o método que declara que ele pode ser visto de fora do assembly.<br /><br /> Quando acionado em uma variável local que tem o mesmo nome como um campo:<br /><br /> Sem quebra - se o campo não pode ser visto de fora do assembly, independentemente da alteração feita.<br />Sem quebra - se você alterar o nome da variável local e não altere o nome do campo.<br />-Quebrando - se você alterar o nome do campo e ele pode ser visto de fora do assembly.|  
  
## <a name="cause"></a>Causa  
 Um método de instância declara um parâmetro ou uma variável local cujo nome corresponde a um campo de instância do tipo declarativo. Para capturar as variáveis locais que violam a regra, o assembly testado deve ser criado usando as informações de depuração e o arquivo de banco de dados (. PDB) do programa associado deve estar disponível.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Quando o nome de um campo de instância corresponde a um parâmetro ou um nome de variável local, o campo de instância é acessado usando o `this` (`Me` em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) palavra-chave quando dentro do corpo de método. Durante a manutenção de código, é fácil esquecer essa diferença e pressupõem que a variável de parâmetro/local se refere ao campo de instância, o que leva a erros. Isso vale especialmente para corpos de método demorado.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação dessa regra, renomeie o parâmetro/variável ou o campo.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima um aviso nessa regra.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra dois violações da regra.  
  
 [!code-csharp[FxCop.Maintainability.VarMatchesField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/cs/FxCop.Maintainability.VarMatchesField.cs#1)]
 [!code-vb[FxCop.Maintainability.VarMatchesField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/vb/FxCop.Maintainability.VarMatchesField.vb#1)]

