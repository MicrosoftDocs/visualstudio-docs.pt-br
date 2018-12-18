---
title: 'CA2117: Os tipos APTCA só devem estender tipos base APTCA | Microsoft Docs'
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
- CA2117
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
helpviewer_keywords:
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
- CA2117
ms.assetid: c505b586-2f1e-47cb-98ee-a5afcbeda70f
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4b069674827ab266b4a4b7a99f81e039d487f6da
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49922636"
---
# <a name="ca2117-aptca-types-should-only-extend-aptca-base-types"></a>CA2117: os tipos APTCA só devem estender tipos base APTCA
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AptcaTypesShouldOnlyExtendAptcaBaseTypes|
|CheckId|CA2117|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido em um assembly com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> atributo herda de um tipo declarado em um assembly que não tem o atributo.

## <a name="rule-description"></a>Descrição da Regra
 Por padrão, os tipos de públicos ou protegidos em assemblies com nomes fortes implicitamente são protegidos por um [demandas de herança](http://msdn.microsoft.com/en-us/28b9adbb-8f08-4f10-b856-dbf59eb932d9) para confiança total. Assemblies de nome forte é marcado com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo (APTCA) não tem essa proteção. O atributo desabilita a exigência de herança. Isso torna expostos tipos declarados no assembly herdáveis por tipos que não têm confiança total.

 Quando o atributo APTCA estiver presente em um assembly totalmente confiável e um tipo no assembly for herdado de um tipo que não permita chamadores parcialmente confiáveis, será possível uma exploração de segurança. Se dois tipos `T1` e `T2` atendem às condições a seguir, chamadores mal-intencionados podem usar o tipo `T1` para ignorar a exigência de herança de confiança total implícito que protege `T2`:

- `T1` um tipo público é declarado em um assembly totalmente confiável que tem o atributo APTCA.

- `T1` herdado de um tipo `T2` fora do assembly.

- `T2`do assembly não tem o atributo APTCA e, portanto, não devem ser herdada por tipos em assemblies parcialmente confiáveis.

  Um tipo parcialmente confiável `X` podem herdar de `T1`, que concede a ele acesso a membros herdados declarados em `T2`. Porque `T2` não tem o atributo APTCA, seu tipo derivado imediato (`T1`) deve atender uma demanda de herança de confiança total; `T1` tem confiança total e, portanto, satisfaz essa verificação. O risco de segurança é porque `X` não participa de satisfazer a demanda de herança que protege `T2` de criação de subclasses não confiável. Por esse motivo, os tipos com o atributo APTCA não devem estender tipos que não têm o atributo.

  Outro problema de segurança e talvez um mais comum, é que o tipo derivado (`T1`) pode, por meio de erro do programador, expor os membros protegidos do tipo que requer confiança total (`T2`). Quando isso ocorrer, os chamadores não confiáveis obtém acesso a informações que devem estar disponíveis somente para tipos de totalmente confiáveis.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Se o tipo relatado pela violação de está em um assembly que não requer o atributo APTCA, removê-lo.

 Se o atributo APTCA for necessário, adicione uma exigência de herança de confiança total para o tipo. Isso protege contra herança por tipos não confiáveis.

 É possível corrigir uma violação, adicionando o atributo APTCA aos assemblies dos tipos base relatados pela violação. Fazer isso sem primeiro conduzir uma revisão de segurança com uso intensivo de todo o código nos assemblies e todo o código que depende dos assemblies.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para suprimir com segurança um aviso nessa regra, você deve garantir que membros protegidos expostos pelo seu tipo não direta ou indiretamente permitem chamadores não-confiáveis acessar informações confidenciais, operações ou recursos que podem ser usados de forma destrutivas.

## <a name="example"></a>Exemplo
 O exemplo a seguir usa dois assemblies e um aplicativo de teste para ilustrar a vulnerabilidade de segurança detectada por essa regra. O primeiro conjunto não tem o atributo APTCA e não devem ser herdado por tipos parcialmente confiáveis (representado por `T2` na discussão anterior).

 [!code-csharp[FxCop.Security.NoAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptcaInherit/cs/FxCop.Security.NoAptcaInherit.cs#1)]

## <a name="example"></a>Exemplo
 O segundo conjunto, representado por `T1` na discussão anterior, é totalmente confiável e permite que os chamadores parcialmente confiáveis.

 [!code-csharp[FxCop.Security.YesAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptcaInherit/cs/FxCop.Security.YesAptcaInherit.cs#1)]

## <a name="example"></a>Exemplo
 O tipo de teste, representado por `X` na discussão anterior, está em um assembly parcialmente confiável.

 [!code-csharp[FxCop.Security.TestAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaInherit/cs/FxCop.Security.TestAptcaInherit.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Meet na glen sombrio 2/22/2003 12:00:00 AM! ** 
 **De teste: Campina ensolarada**
**cumprir à Campina ensolarada 2/22/2003 12:00:00 AM!**
## <a name="related-rules"></a>Regras relacionadas
 [CA2116: os métodos APTCA só devem chamar métodos APTCA](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)

## <a name="see-also"></a>Consulte também
 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [Assemblies do .NET Framework pode ser chamados por código parcialmente confiável](http://msdn.microsoft.com/en-us/a417fcd4-d3ca-4884-a308-3a1a080eac8d) [usando bibliotecas de parcialmente confiável código](http://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74) [demandas de herança](http://msdn.microsoft.com/en-us/28b9adbb-8f08-4f10-b856-dbf59eb932d9)




