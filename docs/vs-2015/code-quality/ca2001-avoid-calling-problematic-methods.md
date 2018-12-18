---
title: 'CA2001: Evitar chamar métodos problemáticos | Microsoft Docs'
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
- CA2001
- AvoidCallingProblematicMethods
helpviewer_keywords:
- CA2001
- AvoidCallingProblematicMethods
ms.assetid: 19db8edb-31ce-441c-b0de-a0f2746155b7
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ddc96857cf0c3c54472eded5545ca0f328eba213
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49902783"
---
# <a name="ca2001-avoid-calling-problematic-methods"></a>CA2001: evitar métodos problemáticos de chamada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidCallingProblematicMethods|
|CheckId|CA2001|
|Categoria|Microsoft.Reliability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um membro chama um método potencialmente perigoso ou problemático.

## <a name="rule-description"></a>Descrição da Regra
 Evite fazer chamadas de método desnecessários e potencialmente perigosos.

 Uma violação dessa regra ocorre quando um membro chama um dos métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|<xref:System.GC.Collect%2A?displayProperty=fullName>|Chamar GC. Coletar pode afetar significativamente o desempenho do aplicativo e é raramente necessário. Para obter mais informações, consulte o [dados sobre o desempenho de Rico Mariani](http://go.microsoft.com/fwlink/?LinkId=169256) entrada de blog no MSDN.|
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName><br /><br /> <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>|Thread. Suspend e resume foram substituídos por conta do comportamento imprevisível.  Use outras classes na <xref:System.Threading> namespace, tal como <xref:System.Threading.Monitor>, <xref:System.Threading.Mutex>, e <xref:System.Threading.Semaphore> para sincronizar threads ou proteger recursos.|
|<xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A?displayProperty=fullName>|O método DangerousGetHandle representa um risco de segurança porque ele pode retornar um identificador que não é válido. Consulte a <xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A> e o <xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A> métodos para obter mais informações sobre como usar o método DangerousGetHandle com segurança.|
|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>|Esses métodos podem carregar assemblies de locais inesperados. Por exemplo, consulte as postagens de blog do .NET CLR notas Suzanne Cook [LoadFile vs. LoadFrom](http://go.microsoft.com/fwlink/?LinkId=164450) e [escolhendo um contexto de associação](http://go.microsoft.com/fwlink/?LinkId=164451) no site do MSDN para obter informações sobre os métodos que carregar assemblies.|
|[CoSetProxyBlanket](http://go.microsoft.com/fwlink/?LinkID=169250) (Ole32)<br /><br /> [CoInitializeSecurity](http://go.microsoft.com/fwlink/?LinkId=169255) (Ole32)|No momento em que o código do usuário inicia a execução em um processo gerenciado, é tarde demais chamam CoSetProxyBlanket de forma confiável. O common language runtime (CLR) executa ações de inicialização que podem impedir que os usuários de P/Invoke tenham êxito.<br /><br /> Se você precisa chamar CoSetProxyBlanket para um aplicativo gerenciado, é recomendável que você iniciar o processo por meio de um executável de código nativo (C++), chama CoSetProxyBlanket no código nativo e, em seguida, inicia o aplicativo de código gerenciado no processo. (Certifique-se de especificar um número de versão de tempo de execução.)|

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova ou substitua a chamada ao método perigoso ou problemático.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você deve suprimir mensagens dessa regra somente quando não há alternativas para o método problemático estão disponíveis.

## <a name="see-also"></a>Consulte também
 [Avisos de confiabilidade](../code-quality/reliability-warnings.md)



