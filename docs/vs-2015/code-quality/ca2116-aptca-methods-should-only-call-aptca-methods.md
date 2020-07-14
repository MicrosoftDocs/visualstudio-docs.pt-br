---
title: 'CA2116: os métodos APTCA devem chamar apenas os métodos APTCA | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
helpviewer_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
ms.assetid: 8b91637e-891f-4dde-857b-bf8012270ec4
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 115c0e733716994ba463eada938f8ff908612d0f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547752"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116: Métodos APTCA devem chamar somente métodos APTCA
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método em um assembly com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> atributo chama um método em um assembly que não tem o atributo.

## <a name="rule-description"></a>Descrição da Regra
 Por padrão, os métodos públicos ou protegidos em assemblies com nomes fortes são implicitamente protegidos por uma [demanda de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) para confiança total; somente chamadores totalmente confiáveis podem acessar um assembly de nome forte. Os assemblies de nome forte marcados com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo (APTCA) não têm essa proteção. O atributo desabilita a demanda de link, tornando o assembly acessível a chamadores que não têm confiança total, como a execução de código de uma intranet ou da Internet.

 Quando o atributo APTCA está presente em um assembly totalmente confiável e o assembly executa o código em outro assembly que não permite chamadores parcialmente confiáveis, uma exploração de segurança é possível. Se dois métodos `M1` e `M2` atenderem às condições a seguir, os chamadores mal-intencionados poderão usar o método `M1` para ignorar a demanda de link de confiança total implícita que protege `M2` :

- `M1`é um método público declarado em um assembly totalmente confiável que tem o atributo APTCA.

- `M1`chama um método `M2` fora `M1` do assembly.

- `M2`o assembly do não tem o atributo APTCA e, portanto, não deve ser executado por ou em nome de chamadores que são parcialmente confiáveis.

  Um chamador parcialmente confiável `X` pode chamar o método `M1` , causando `M1` a chamada `M2` . Como o `M2` não tem o atributo APTCA, seu chamador imediato ( `M1` ) deve atender a uma demanda de link para confiança total; `M1` tem confiança total e, portanto, satisfaz essa verificação. O risco de segurança é porque o `X` não participa da demanda de link que protege `M2` contra chamadores não confiáveis. Portanto, os métodos com o atributo APTCA não devem chamar métodos que não tenham o atributo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Se o atributo APCTA for necessário, use uma demanda para proteger o método que chama o assembly de confiança total. As permissões exatas que você exige dependerão da funcionalidade exposta pelo método. Se possível, proteja o método com uma demanda de confiança total para garantir que a funcionalidade subjacente não seja exposta a chamadores parcialmente confiáveis. Se isso não for possível, selecione um conjunto de permissões que proteja efetivamente a funcionalidade exposta. Para obter mais informações sobre as demandas, consulte [demandas](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48).

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para suprimir um aviso dessa regra com segurança, você deve garantir que a funcionalidade exposta por seu método não direta ou indiretamente permita que os chamadores acessem informações confidenciais, operações ou recursos que podem ser usados de maneira destrutiva.

## <a name="example"></a>Exemplo
 O exemplo a seguir usa dois assemblies e um aplicativo de teste para ilustrar a vulnerabilidade de segurança detectada por essa regra. O primeiro assembly não tem o atributo APTCA e não deve ser acessível a chamadores parcialmente confiáveis (representados pelo `M2` na discussão anterior).

 [!code-csharp[FxCop.Security.NoAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptca/cs/FxCop.Security.NoAptca.cs#1)]

## <a name="example"></a>Exemplo
 O segundo assembly é totalmente confiável e permite chamadores parcialmente confiáveis (representados pela `M1` na discussão anterior).

 [!code-csharp[FxCop.Security.YesAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptca/cs/FxCop.Security.YesAptca.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo de teste (representado pela `X` na discussão anterior) é parcialmente confiável.

 [!code-csharp[FxCop.Security.TestAptcaMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaMethods/cs/FxCop.Security.TestAptcaMethods.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Demanda de confiança total: falha na solicitação.** 
 **ClassRequiringFullTrust. DoWork foi chamado.**
## <a name="related-rules"></a>Regras relacionadas
 [CA2117: Tipos APTCA devem estender somente tipos base APTCA](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>Consulte Também
 [Diretrizes de codificação seguras](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [.NET Framework assemblies que podem ser chamados por código parcialmente confiável](https://msdn.microsoft.com/a417fcd4-d3ca-4884-a308-3a1a080eac8d) [usando bibliotecas de códigos parcialmente confiáveis](https://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74) [demandam](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48) [dados e modelagem](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) de [demandas de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
