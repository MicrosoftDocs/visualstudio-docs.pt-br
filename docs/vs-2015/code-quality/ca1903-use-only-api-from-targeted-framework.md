---
title: 'CA1903: Usar apenas a API da estrutura de destino | Microsoft Docs'
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
- UseOnlyAPIFromTargetedFramework
- CA1903
helpviewer_keywords:
- UseOnlyApiFromTargetedFramework
- CA1903
ms.assetid: efdb5cc7-bbd8-4fa7-9fff-02b91e59350e
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1c23b25029775cd3abca84e695c50b5a0fdf68cf
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49191562"
---
# <a name="ca1903-use-only-api-from-targeted-framework"></a>CA1903: usar apenas a API da estrutura de destino
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA1903: usar apenas a API da estrutura de destino](https://docs.microsoft.com/visualstudio/code-quality/ca1903-use-only-api-from-targeted-framework) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|UseOnlyApiFromTargetedFramework|  
|CheckId|CA1903|  
|Categoria|Microsoft.Portability|  
|Alteração Significativa|Quebrando - quando disparado em relação a assinatura de um tipo ou membro visível externamente.<br /><br /> Não separável - quando disparado no corpo de um método.|  
  
## <a name="cause"></a>Causa  
 Um membro ou tipo está usando um membro ou tipo que foi introduzido em um service pack que não foi incluído com a estrutura de destino do projeto.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Tipos e membros novos foram incluídos no .NET Framework 2.0 Service Pack 1 e 2, o .NET Framework 3.0 Service Pack 1 e 2 e o .NET Framework 3.5 Service Pack 1. Projetos direcionados as versões principais do .NET Framework, inadvertidamente, podem assumir dependências sobre essas novas APIs. Para evitar essa dependência, essa regra é acionada em usos de quaisquer novos membros e tipos que não foram incluídos por padrão com a estrutura de destino do projeto.  
  
 **Estrutura de destino e dependências do pacote de serviço**  
  
|||  
|-|-|  
|Quando é a estrutura de destino|É acionado em usos de membros, introduzidos no|  
|.NET Framework 2.0|.NET framework 2.0 SP1, .NET Framework 2.0 SP2|  
|.NET Framework 3.0|.NET framework 2.0 SP1, o .NET Framework 2.0 SP2, o .NET Framework 3.0 SP1 e o .NET Framework 3.0 SP2|  
|.NET Framework 3,5|.NET Framework 3,5 SP1|  
|.NET Framework 4|N/D|  
  
 Para alterar a estrutura de destino do projeto, consulte [visando uma versão específica do .NET Framework](../ide/targeting-a-specific-dotnet-framework-version.md).  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para remover a dependência no service pack, remova todos os usos do novo membro ou tipo. Se essa é uma dependência deliberada, suprimir o aviso ou desative essa regra.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima um aviso nessa regra, se isso não era uma dependência deliberada sobre o pacote de serviço especificado. Nessa situação, seu aplicativo pode falhar ao executar em sistemas sem este service pack instalado. Suprimir o aviso ou desative essa regra se essa fosse uma dependência deliberada.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma classe que usa o tipo DateTimeOffset só está disponível no .NET 2.0 Service Pack 1. Esse exemplo requer que o .NET Framework 2.0 foi selecionada na lista suspensa de estrutura de destino nas propriedades do projeto.  
  
 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework.cs#1)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir corrige a violação descrita anteriormente, substituindo os usos do tipo DateTimeOffset com o tipo DateTime.  
  
 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework2/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework2.cs#1)]  
  
## <a name="see-also"></a>Consulte também  
 [Avisos de portabilidade](../code-quality/portability-warnings.md)   
 [Direcionamento de uma versão específica do .NET Framework](../ide/targeting-a-specific-dotnet-framework-version.md)

