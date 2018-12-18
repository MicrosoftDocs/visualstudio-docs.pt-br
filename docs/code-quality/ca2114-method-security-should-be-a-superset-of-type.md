---
title: 'CA2114: a segurança de método deve ser um superconjunto de tipo'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MethodSecurityShouldBeASupersetOfType
- CA2114
helpviewer_keywords:
- CA2114
- MethodSecurityShouldBeASupersetOfType
ms.assetid: 663f7aa4-8be5-4bd5-be92-4e9444f07077
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 66fe0031380139c55942a1a47f71066a327d5e24
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551414"
---
# <a name="ca2114-method-security-should-be-a-superset-of-type"></a>CA2114: a segurança de método deve ser um superconjunto de tipo

|||
|-|-|
|NomeDoTipo|MethodSecurityShouldBeASupersetOfType|
|CheckId|CA2114|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo tem segurança declarativa e um de seus métodos tem segurança declarativa para a mesma ação de segurança e a ação de segurança não é [demandas de Link](/dotnet/framework/misc/link-demands), e a permissão é verificada pelo tipo não é um subconjunto das permissões verificado pelo método.

## <a name="rule-description"></a>Descrição da regra
 Um método não deve ter tanto uma nível de método e tipo de segurança declarativa para a mesma ação. As duas verificações não são combinadas; somente a demanda de nível de método é aplicada. Por exemplo, se um tipo exige a permissão `X`, e um de seus métodos solicita a permissão `Y`, código não precisa ter a permissão `X` para executar o método.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Revise seu código para certificar-se de que ambas as ações são necessárias. Se ambas as ações forem necessárias, certifique-se de que a ação de nível de método inclui a segurança especificada no nível do tipo. Por exemplo, se seu tipo exige a permissão `X`, e seu método também deve exigem a permissão `Y`, o método deverá exigir explicitamente `X` e `Y`.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se o método não exigir que o especificado pelo tipo de segurança. No entanto, isso não é um cenário comum e pode indicar a necessidade de uma revisão de design cuidadoso.

## <a name="example-1"></a>Exemplo 1

O exemplo a seguir usa as permissões de ambiente para demonstrar os perigos da violação dessa regra. Neste exemplo, o código do aplicativo cria uma instância do tipo seguro antes de negar a permissão exigida pelo tipo. Em um cenário de ameaças do mundo real, o aplicativo exigiria outra maneira de obter uma instância do objeto.

No exemplo a seguir, as demandas de biblioteca permissão de gravação para um tipo em a permissão de leitura para um método.

[!code-csharp[FxCop.Security.MethodLevelSecurity#1](../code-quality/codesnippet/CSharp/ca2114-method-security-should-be-a-superset-of-type_1.cs)]

## <a name="example-2"></a>Exemplo 2

O código de aplicativo a seguir demonstra a vulnerabilidade da biblioteca, chamando o método, mesmo que ele não atende ao requisito de segurança em nível de tipo.

[!code-csharp[FxCop.Security.TestMethodLevelSecurity#1](../code-quality/codesnippet/CSharp/ca2114-method-security-should-be-a-superset-of-type_2.cs)]

Este exemplo gera a seguinte saída:

```txt
[All permissions] Personal information: 6/16/1964 12:00:00 AM
[No write permission (demanded by type)] Personal information: 6/16/1964 12:00:00 AM
[No read permission (demanded by method)] Could not access personal information: Request failed.
```

## <a name="see-also"></a>Consulte também

- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines)
- [Demandas de link](/dotnet/framework/misc/link-demands)
- [Dados e modelagem](/dotnet/framework/data/index)