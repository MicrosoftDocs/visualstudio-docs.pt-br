---
title: Mecanismo de depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 78bd5b732d7ea1714bb1c5627b570976e33a82c4
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39203882"
---
# <a name="debug-engine"></a>Mecanismo de depuração
Um mecanismo de depuração (DES) funciona com o sistema operacional ou interpretador para fornecer serviços de depuração, como avaliação de expressão, os pontos de interrupção e controle de execução. A Alemanha é responsável por monitorar o estado de um programa que está sendo depurado. Para fazer isso, o DE usa quaisquer métodos estão disponíveis para ele no tempo de execução com suporte, se da CPU ou de APIs fornecidas pelo tempo de execução.  
  
 Por exemplo, o common language runtime (CLR) fornece mecanismos para monitorar um programa em execução por meio de interfaces ICorDebugXXX. A DE que dá suporte a CLR usa as interfaces de ICorDebugXXX apropriadas para manter o controle de um programa de código gerenciado que está sendo depurado. Ele se comunica as alterações de estado para o Gerenciador de depuração de sessão (SDM), que encaminha essas informações para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.  
  
> [!NOTE]
>  Um mecanismo de depuração tem como alvo um tempo de execução específico, ou seja, o sistema em que o programa que está sendo depurado é executado. O CLR é o tempo de execução para código gerenciado e o tempo de execução do Win32 é para aplicativos nativos do Windows. Se o idioma que você cria pode direcionar um dos dois desses tempos de execução, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] já fornece mecanismos de depuração necessárias. Tudo o que você tem que implementar é um avaliador de expressão.  
  
## <a name="debug-engine-operation"></a>Operação do mecanismo de depuração  
 Os serviços de monitoramento são implementados por meio DE interfaces e podem fazer com que o pacote de depuração para fazer a transição entre os modos operacionais diferentes. Para obter mais informações, consulte [modos operacionais](../../extensibility/debugger/operational-modes.md). Normalmente, há apenas uma implementação DE cada ambiente de tempo de execução.  
  
> [!NOTE]
>  Embora existam implementações DE separadas para o Transact-SQL e [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)], VBScript e [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] compartilham um único DE.  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Habilita depuração depuração mecanismos para executar uma das duas maneiras: no mesmo processo que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] de shell ou no mesmo processo que o programa de destino que está sendo depurado. A segunda forma normalmente ocorre quando o processo que está sendo depurado é, na verdade, um script em execução em um interpretador. O mecanismo de depuração deve ter um conhecimento profundo do interpretador para monitorar o script. Nesse caso, o interpretador é, na verdade, um tempo de execução; mecanismos de depuração são para implementações de tempo de execução específico. Além disso, a implementação de um único DE pode ser dividida em limites de processo e de máquina (por exemplo, depuração remota).  
  
 O DE expõe o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interfaces de depuração. Toda a comunicação está usando COM. Se a Alemanha é carregada no processo, out-of-process ou em outro computador, ela não afeta a comunicação de componente.  
  
 O DE funciona com um componente do avaliador de expressão para habilitar o DE para determinado tempo de execução entender a sintaxe de expressões. O DE também funciona com um componente de manipulador de símbolo para acessar as informações de depuração simbólica geradas pelo compilador de linguagem. Para obter mais informações, consulte [avaliador de expressão](../../extensibility/debugger/expression-evaluator.md) e [provedor de símbolos](../../extensibility/debugger/symbol-provider.md).  
  
## <a name="see-also"></a>Consulte também  
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)   
 [Avaliador de expressão](../../extensibility/debugger/expression-evaluator.md)   
 [Provedor de símbolos](../../extensibility/debugger/symbol-provider.md)