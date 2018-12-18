---
title: 'CA2116: Os métodos APTCA só devem chamar métodos APTCA | Microsoft Docs'
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
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
helpviewer_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
ms.assetid: 8b91637e-891f-4dde-857b-bf8012270ec4
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 766de62f4781dc7ce164155a2090ffabac913a22
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49819544"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116: os métodos APTCA só devem chamar métodos APTCA
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método em um assembly com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> atributo chama um método em um assembly que não tem o atributo.

## <a name="rule-description"></a>Descrição da Regra
 Por padrão, os métodos públicos ou protegidos em assemblies com nomes fortes implicitamente são protegidos por um [demandas de Link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) para confiança total; apenas totalmente confiável os chamadores podem acessar um assembly de nome forte. Assemblies de nome forte é marcado com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo (APTCA) não tem essa proteção. O atributo desabilita a demanda de link, fazendo com que o assembly acessível aos chamadores que não têm confiança total, como o código em execução de uma intranet ou da Internet.

 Quando o atributo APTCA estiver presente em um assembly totalmente confiável e o assembly executar código em outro assembly que não permita chamadores parcialmente confiáveis, será possível uma exploração de segurança. Se dois métodos `M1` e `M2` atendem às condições a seguir, chamadores mal-intencionados podem usar o método `M1` para ignorar a demanda de link de confiança total implícito que protege `M2`:

- `M1` um método público é declarado em um assembly totalmente confiável que tem o atributo APTCA.

- `M1` chama um método `M2` fora `M1`do assembly.

- `M2`do assembly não tem o atributo APTCA e, portanto, não devem ser executado por, ou em nome dos chamadores parcialmente confiáveis.

  Um chamador parcialmente confiável `X` pode chamar o método `M1`, causando `M1` chamar `M2`. Porque `M2` não tem o atributo APTCA, seu chamador imediato (`M1`) deve atender uma demanda de link para confiança total; `M1` tem confiança total e, portanto, satisfaz essa verificação. O risco de segurança é porque `X` não participa de satisfazer a demanda de link que protege `M2` de chamadores não confiáveis. Portanto, os métodos com o atributo APTCA não devem chamar métodos que não têm o atributo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Se o atributo APCTA for necessário, use uma demanda para proteger o método que chama o assembly de confiança total. As permissões exatas que você demanda dependerá a funcionalidade exposta pelo seu método. Se for possível, proteja o método com uma demanda de confiança total garantir que a funcionalidade subjacente não é exposta a chamadores parcialmente confiáveis. Se isso não for possível, selecione um conjunto de permissões que efetivamente protege a funcionalidade exposta. Para obter mais informações sobre as demandas, consulte [demandas](http://msdn.microsoft.com/en-us/e5283e28-2366-4519-b27d-ef5c1ddc1f48).

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para suprimir com segurança um aviso nessa regra, você deve garantir que a funcionalidade exposta pelo seu método não direta ou indiretamente permite chamadores acessem informações confidenciais, operações ou recursos que podem ser usados de forma destrutivas.

## <a name="example"></a>Exemplo
 O exemplo a seguir usa dois assemblies e um aplicativo de teste para ilustrar a vulnerabilidade de segurança detectada por essa regra. O primeiro conjunto não tem o atributo APTCA e não deve ser acessível a chamadores parcialmente confiáveis (representado por `M2` na discussão anterior).

 [!code-csharp[FxCop.Security.NoAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptca/cs/FxCop.Security.NoAptca.cs#1)]

## <a name="example"></a>Exemplo
 O segundo conjunto é totalmente confiável e permite que os chamadores parcialmente confiáveis (representado por `M1` na discussão anterior).

 [!code-csharp[FxCop.Security.YesAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptca/cs/FxCop.Security.YesAptca.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo de teste (representado por `X` na discussão anterior) é parcialmente confiável.

 [!code-csharp[FxCop.Security.TestAptcaMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaMethods/cs/FxCop.Security.TestAptcaMethods.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Falha na demanda de confiança: solicitação completa. ** 
 **ClassRequiringFullTrust.DoWork foi chamado.**
## <a name="related-rules"></a>Regras relacionadas
 [CA2117: os tipos APTCA só devem estender tipos base APTCA](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>Consulte também
 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [Assemblies do .NET Framework pode ser chamados por código parcialmente confiável](http://msdn.microsoft.com/en-us/a417fcd4-d3ca-4884-a308-3a1a080eac8d) [usando bibliotecas de parcialmente confiável código](http://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74) [demandas](http://msdn.microsoft.com/en-us/e5283e28-2366-4519-b27d-ef5c1ddc1f48) [Demandas de link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) [dados e modelagem](http://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)



