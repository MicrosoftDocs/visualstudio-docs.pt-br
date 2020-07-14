---
title: 'CA2122: não expõe indiretamente métodos com demandas de link | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2122
- DoNotIndirectlyExposeMethodsWithLinkDemands
helpviewer_keywords:
- DoNotIndirectlyExposeMethodsWithLinkDemands
- CA2122
ms.assetid: 3eda58e7-c6ec-41c3-8112-ae0841109c6a
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 846ce010cddfd505bb967ec612a5c31dd8321977
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544320"
---
# <a name="ca2122-do-not-indirectly-expose-methods-with-link-demands"></a>CA2122: Não expor indiretamente métodos com demandas de link
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotIndirectlyExposeMethodsWithLinkDemands|
|CheckId|CA2122|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um membro público ou protegido tem uma [demanda de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) e é chamado por um membro que não executa nenhuma verificação de segurança.

## <a name="rule-description"></a>Descrição da Regra
 Uma exigência de vínculo verifica as permissões apenas do chamador imediato. Se um membro `X` não fizer nenhuma demanda de segurança de seus chamadores e chamar o código protegido por uma demanda de link, um chamador sem a permissão necessária poderá usar `X` o para acessar o membro protegido.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Adicione dados de segurança [e modelagem](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) ou demanda de link ao membro para que ele não forneça mais acesso sem segurança ao membro protegido por demanda de link.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para suprimir um aviso dessa regra com segurança, você deve certificar-se de que seu código não concede aos chamadores acesso a operações ou recursos que podem ser usados de maneira destrutiva.

## <a name="example"></a>Exemplo
 Os exemplos a seguir mostram uma biblioteca que viola a regra e um aplicativo que demonstra a fraqueza da biblioteca. A biblioteca de exemplo fornece dois métodos que juntos violam a regra. O `EnvironmentSetting` método é protegido por uma demanda de link para acesso irrestrito a variáveis de ambiente. O `DomainInformation` método não faz nenhuma demanda de segurança de seus chamadores antes de chamar `EnvironmentSetting` .

 [!code-csharp[FxCop.Security.UnsecuredDoNotCall#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.UnsecuredDoNotCall/cs/FxCop.Security.UnsecuredDoNotCall.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir chama o membro da biblioteca não segura.

 [!code-csharp[FxCop.Security.TestUnsecuredDoNot1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestUnsecuredDoNot1/cs/FxCop.Security.TestUnsecuredDoNot1.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Valor de membro não seguro: seattle.corp.contoso.com**
## <a name="see-also"></a>Consulte Também
 [Diretrizes de codificação seguras](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [link exige](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) [dados e modelagem](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
