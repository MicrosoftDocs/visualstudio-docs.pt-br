---
title: 'CA2122: Não expor indiretamente métodos com demandas de link | Microsoft Docs'
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
- CA2122
- DoNotIndirectlyExposeMethodsWithLinkDemands
helpviewer_keywords:
- DoNotIndirectlyExposeMethodsWithLinkDemands
- CA2122
ms.assetid: 3eda58e7-c6ec-41c3-8112-ae0841109c6a
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 563805fdd8ba8c30e9fb241cc24136ad0c9e9e06
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49912832"
---
# <a name="ca2122-do-not-indirectly-expose-methods-with-link-demands"></a>CA2122: não expor indiretamente métodos com demandas de link
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotIndirectlyExposeMethodsWithLinkDemands|
|CheckId|CA2122|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um membro público ou protegido tem um [demandas de Link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) e é chamado por um membro que não executa nenhuma verificação de segurança.

## <a name="rule-description"></a>Descrição da Regra
 Uma exigência de vínculo verifica as permissões apenas do chamador imediato. Se um membro `X` não faz com que nenhum demandas de segurança de seus chamadores e chamadas de código protegido por uma demanda de link em um chamador sem a permissão necessária pode usar `X` para acessar o membro protegido.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Adicionar uma segurança [dados e modelagem](http://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) ou vincular a demanda para o membro para que ele não fornece mais acesso desprotegido para o membro protegido por demanda de link.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para suprimir com segurança um aviso nessa regra, certifique-se de que seu código não concede seus chamadores acesso a recursos que podem ser usados de forma destrutivas ou operações.

## <a name="example"></a>Exemplo
 Os exemplos a seguir mostram uma biblioteca que viola a regra e um aplicativo que demonstra a desvantagem da biblioteca. A biblioteca de exemplo fornece dois métodos que juntos violam a regra. O `EnvironmentSetting` método é protegido por uma demanda de link para acesso irrestrito a variáveis de ambiente. O `DomainInformation` método não faz nenhuma demandas de segurança de seus chamadores antes de chamar `EnvironmentSetting`.

 [!code-csharp[FxCop.Security.UnsecuredDoNotCall#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.UnsecuredDoNotCall/cs/FxCop.Security.UnsecuredDoNotCall.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir chama o membro da biblioteca não segura.

 [!code-csharp[FxCop.Security.TestUnsecuredDoNot1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestUnsecuredDoNot1/cs/FxCop.Security.TestUnsecuredDoNot1.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **O valor do membro não seguro: seattle.corp.contoso.com**
## <a name="see-also"></a>Consulte também
 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [demandas de Link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) [dados e modelagem](http://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)



