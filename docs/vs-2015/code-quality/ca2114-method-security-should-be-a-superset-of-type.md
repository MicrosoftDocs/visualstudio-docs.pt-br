---
title: 'CA2114: Segurança de método deve ser um superconjunto de tipo | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MethodSecurityShouldBeASupersetOfType
- CA2114
helpviewer_keywords:
- CA2114
- MethodSecurityShouldBeASupersetOfType
ms.assetid: 663f7aa4-8be5-4bd5-be92-4e9444f07077
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c9e0024ae6db5af3f1cf23c07fe29fbac8e4827d
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58927817"
---
# <a name="ca2114-method-security-should-be-a-superset-of-type"></a>CA2114: A segurança do método deve ser um superconjunto do tipo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|MethodSecurityShouldBeASupersetOfType|
|CheckId|CA2114|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo tem segurança declarativa e um de seus métodos tem segurança declarativa para a mesma ação de segurança e a ação de segurança não é [demandas de Link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) ou [demandas de herança](http://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)e as permissões verificado pelo tipo não são um subconjunto das permissões verificadas pelo método.

## <a name="rule-description"></a>Descrição da Regra
 Um método não deve ter tanto uma nível de método e tipo de segurança declarativa para a mesma ação. As duas verificações não são combinadas; somente a demanda de nível de método é aplicada. Por exemplo, se um tipo exige a permissão `X`, e um de seus métodos solicita a permissão `Y`, código não precisa ter a permissão `X` para executar o método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Revise seu código para certificar-se de que ambas as ações são necessárias. Se ambas as ações forem necessárias, certifique-se de que a ação de nível de método inclui a segurança especificada no nível do tipo. Por exemplo, se seu tipo exige a permissão `X`, e seu método também deve exigem a permissão `Y`, o método deverá exigir explicitamente `X` e `Y`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o método não exigir que o especificado pelo tipo de segurança. No entanto, isso não é um cenário comum e pode indicar a necessidade de uma revisão de design cuidadoso.

## <a name="example"></a>Exemplo
 O exemplo a seguir usa as permissões de ambiente para demonstrar os perigos da violação dessa regra. Neste exemplo, o código do aplicativo cria uma instância do tipo seguro antes de negar a permissão exigida pelo tipo. Em um cenário de ameaças do mundo real, o aplicativo exigiria outra maneira de obter uma instância do objeto.

 No exemplo a seguir, as demandas de biblioteca permissão de gravação para um tipo em a permissão de leitura para um método.

 [!code-csharp[FxCop.Security.MethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MethodLevelSecurity/cs/FxCop.Security.MethodLevelSecurity.cs#1)]

## <a name="example"></a>Exemplo
 O código de aplicativo a seguir demonstra a vulnerabilidade da biblioteca, chamando o método, mesmo que ele não atende ao requisito de segurança em nível de tipo.

 [!code-csharp[FxCop.Security.TestMethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestMethodLevelSecurity/cs/FxCop.Security.TestMethodLevelSecurity.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **[Todas as permissões] Informações pessoais: 6/16/data de 1964 12:00:00 AM**
 **[nenhuma permissão de gravação (exigida por tipo)] informações pessoais: 6/16/data de 1964 12:00:00 AM**
 **[nenhuma permissão de leitura (exigida pelo método)] não foi possível acessar informações pessoais: Falha na solicitação.**
## <a name="see-also"></a>Consulte também
 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [demandas de herança](http://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9) [demandas de Link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) [dados e modelagem](http://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
