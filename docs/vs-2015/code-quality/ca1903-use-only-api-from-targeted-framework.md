---
title: 'CA1903: usar somente a API da estrutura de destino | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseOnlyAPIFromTargetedFramework
- CA1903
helpviewer_keywords:
- UseOnlyApiFromTargetedFramework
- CA1903
ms.assetid: efdb5cc7-bbd8-4fa7-9fff-02b91e59350e
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 10649b4106a280089fd6b086167c7e92bff1300b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545243"
---
# <a name="ca1903-use-only-api-from-targeted-framework"></a>CA1903: Usar apenas a API da estrutura de destino
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente sobre o Visual Studio, consulte [CA1903: usar somente a API da estrutura de destino](/visualstudio/code-quality/ca1903-use-only-api-from-targeted-framework).

|Item|Valor|
|-|-|
|TypeName|UseOnlyApiFromTargetedFramework|
|CheckId|CA1903|
|Categoria|Microsoft. portabilidade|
|Alteração Significativa|Quebra-quando acionada na assinatura de um membro ou tipo visível externamente.<br /><br /> Não separável – quando disparado no corpo de um método.|

## <a name="cause"></a>Causa
 Um membro ou tipo está usando um membro ou tipo que foi introduzido em um service pack que não foi incluído com a estrutura de destino do projeto.

## <a name="rule-description"></a>Descrição da Regra
 Novos membros e tipos foram incluídos no .NET Framework 2,0 Service Pack 1 e 2, .NET Framework 3,0 Service Pack 1 e 2 e .NET Framework 3,5 Service Pack 1. Os projetos que visam as versões principais do .NET Framework podem usar involuntariamente dependências dessas novas APIs. Para evitar essa dependência, essa regra é acionada em usos de novos membros e tipos que não foram incluídos por padrão com a estrutura de destino do projeto.

 **Dependências de estrutura de destino e Service Pack**

|Item|Valor|
|-|-|
|Quando a estrutura de destino é|Acionado em usos de membros introduzidos em|
|.NET Framework 2.0|.NET Framework 2,0 SP1, .NET Framework 2,0 SP2|
|.NET Framework 3.0|.NET Framework 2,0 SP1, .NET Framework 2,0 SP2, .NET Framework 3,0 SP1, .NET Framework 3,0 SP2|
|.NET Framework 3.5|.NET Framework 3,5 SP1|
|.NET Framework 4|N/D|

 Para alterar a estrutura de destino de um projeto, consulte [direcionando uma versão de .NET Framework específica](../ide/targeting-a-specific-dotnet-framework-version.md).

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para remover a dependência no service pack, remova todos os usos do novo membro ou tipo. Se essa for uma dependência deliberada, suprima o aviso ou desative essa regra.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não omita um aviso dessa regra se essa não fosse uma dependência deliberada no service pack especificado. Nessa situação, seu aplicativo pode falhar ao ser executado em sistemas sem esse service pack instalado. Suprimir o aviso ou desativar essa regra se essa fosse uma dependência deliberada.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe que usa o tipo DateTimeOffset que está disponível somente no .NET 2,0 Service Pack 1. Este exemplo requer que .NET Framework 2,0 tenha sido selecionado na lista suspensa estrutura de destino nas propriedades do projeto.

 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework.cs#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação descrita anteriormente, substituindo os usos do tipo DateTimeOffset pelo tipo DateTime.

 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework2/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework2.cs#1)]

## <a name="see-also"></a>Consulte Também
 [Avisos de portabilidade](../code-quality/portability-warnings.md) [direcionados a uma versão de .NET Framework específica](../ide/targeting-a-specific-dotnet-framework-version.md)
