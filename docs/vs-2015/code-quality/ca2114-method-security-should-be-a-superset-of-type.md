---
title: 'CA2114: o método de segurança deve ser um superconjunto do tipo | Microsoft Docs'
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d7879d8b2aa9eb4ece1ce07f89681b6c0b0f5f31
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534700"
---
# <a name="ca2114-method-security-should-be-a-superset-of-type"></a>CA2114: A segurança do método deve ser um superconjunto do tipo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MethodSecurityShouldBeASupersetOfType|
|CheckId|CA2114|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo tem segurança declarativa e um de seus métodos tem segurança declarativa para a mesma ação de segurança, e a ação de segurança não é uma [demanda de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) ou [demandas de herança](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9), e as permissões verificadas pelo tipo não são um subconjunto das permissões verificadas pelo método.

## <a name="rule-description"></a>Descrição da Regra
 Um método não deve ter uma segurança declarativa em nível de método e de nível de tipo para a mesma ação. As duas verificações não são combinadas; somente a demanda de nível de método é aplicada. Por exemplo, se um tipo exigir permissão `X` e um de seus métodos exigir permissão `Y` , o código não precisará ter permissão `X` para executar o método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Examine seu código para certificar-se de que ambas as ações são necessárias. Se ambas as ações forem necessárias, verifique se a ação no nível do método inclui a segurança especificada no nível de tipo. Por exemplo, se o tipo exige a permissão e `X` seu método também deve exigir permissão `Y` , o método deve solicitar explicitamente `X` e `Y` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o método não exigir a segurança especificada pelo tipo. No entanto, esse não é um cenário comum e pode indicar uma necessidade de uma revisão cuidadosa do design.

## <a name="example"></a>Exemplo
 O exemplo a seguir usa permissões de ambiente para demonstrar os perigos de violar essa regra. Neste exemplo, o código do aplicativo cria uma instância do tipo protegido antes de negar a permissão exigida pelo tipo. Em um cenário de ameaças do mundo real, o aplicativo exigiria outra maneira de obter uma instância do objeto.

 No exemplo a seguir, a biblioteca solicita permissão de gravação para um tipo e permissão de leitura para um método.

 [!code-csharp[FxCop.Security.MethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MethodLevelSecurity/cs/FxCop.Security.MethodLevelSecurity.cs#1)]

## <a name="example"></a>Exemplo
 O código do aplicativo a seguir demonstra a vulnerabilidade da biblioteca chamando o método, mesmo que ele não atenda ao requisito de segurança em nível de tipo.

 [!code-csharp[FxCop.Security.TestMethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestMethodLevelSecurity/cs/FxCop.Security.TestMethodLevelSecurity.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **[Todas as permissões] informações pessoais: 6/16/1964 12:00:00 am** 
 **[Nenhuma permissão de gravação (exigida por tipo)] informações pessoais: 6/16/1964 12:00:00 am** 
 **[Nenhuma permissão de leitura (exigida pelo método)] não pôde acessar informações pessoais: falha na solicitação.**
## <a name="see-also"></a>Consulte Também
 [Diretrizes de codificação seguras](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [exige](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9) [dados e modelagem de](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) [demandas de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
