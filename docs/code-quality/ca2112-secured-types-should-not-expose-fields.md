---
title: 'CA2112: os tipos seguros não devem expor campos'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2112
- SecuredTypesShouldNotExposeFields
helpviewer_keywords:
- SecuredTypesShouldNotExposeFields
- CA2112
ms.assetid: 9eb13a78-3487-49f2-81d1-3c3866db132f
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 538c7ac89643c168086d6bdcb514d88295e482dc
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548282"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112: os tipos seguros não devem expor campos

|||
|-|-|
|NomeDoTipo|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém campos públicos e é protegido por um [demandas de Link](/dotnet/framework/misc/link-demands).

## <a name="rule-description"></a>Descrição da regra
 Se tiver acesso a uma instância de um tipo protegido por uma exigência de vínculo, o código não precisará atender à exigência de vínculo para acessar os campos do tipo.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, tornar os campos não públicos e adicione propriedades públicas nem os métodos que retornam os dados do campo. Verificações de segurança de LinkDemand em tipos de protegem o acesso a métodos e propriedades do tipo. No entanto, a segurança de acesso do código não se aplica aos campos.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Para problemas de segurança e para um bom design, você deve corrigir violações fazendo não públicos campos públicos. Você pode suprimir um aviso nessa regra, se o campo não mantém informações que devem permanecer protegidas, e você não confiar no conteúdo do campo.

## <a name="example"></a>Exemplo
 O exemplo a seguir é composto de um tipo de biblioteca (`SecuredTypeWithFields`) com os campos não seguros, um tipo (`Distributor`) que pode criar instâncias do tipo biblioteca incorreta passa instâncias de tipos não tem permissão para criá-los e código de aplicativo pode ler os campos de uma instância mesmo que ele não tem a permissão que protege o tipo.

 O seguinte código de biblioteca viola a regra.

 [!code-csharp[FxCop.Security.LinkDemandOnField#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_1.cs)]

## <a name="example-1"></a>Exemplo 1
 O aplicativo não é possível criar uma instância devido à exigência de vínculo que protege o tipo seguro. A classe a seguir permite que o aplicativo para obter uma instância do tipo seguro.

 [!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_2.cs)]

## <a name="example-2"></a>Exemplo 2
 O aplicativo a seguir ilustra como fazer isso, sem a permissão para acessar os métodos do tipo seguro, o código pode acessar seus campos.

 [!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_3.cs)]

Este exemplo gera a seguinte saída:

```txt
Creating an instance of SecuredTypeWithFields.
Secured type fields: 22, 33
Changing secured type's field...
Cached Object fields: 99, 33
```

## <a name="related-rules"></a>Regras relacionadas

- [CA1051: não declarar campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>Consulte também

- [Demandas de link](/dotnet/framework/misc/link-demands)
- [Dados e modelagem](/dotnet/framework/data/index)