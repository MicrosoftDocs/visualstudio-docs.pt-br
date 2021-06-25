---
title: Mecanismo de depuração | Microsoft Docs
description: Saiba como um mecanismo de depuração funciona com o intérprete ou o sistema operacional para fornecer serviços como controle de execução, pontos de interrupção e avaliação de expressão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 87c4648ed37ef4fad0d79b7048593ff0c5b7d6d0
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905703"
---
# <a name="debug-engine"></a>Mecanismo de depuração
Um mecanismo DE depuração (DE) funciona com o interpretador ou o sistema operacional para fornecer serviços de depuração, como controle de execução, pontos de interrupção e avaliação de expressão. O DE é responsável por monitorar o estado de um programa que está sendo depurado. Para fazer isso, o DE usa quaisquer métodos disponíveis no tempo de execução com suporte, seja da CPU ou das APIs fornecidas pelo tempo de execução.

 Por exemplo, o Common Language Runtime (CLR) fornece mecanismos para monitorar um programa em execução por meio das interfaces ICorDebugXXX. Um DE que dá suporte ao CLR usa as interfaces ICorDebugXXX apropriadas para controlar um programa de código gerenciado que está sendo depurado. Em seguida, ele comunica todas as alterações de estado para o SDM (Gerenciador de depuração de sessão), que encaminha essas informações para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

> [!NOTE]
> Um mecanismo de depuração tem como alvo um tempo de execução específico, ou seja, o sistema no qual o programa que está sendo depurado é executado. O CLR é o tempo de execução para código gerenciado e o tempo de execução do Win32 é para aplicativos nativos do Windows. Se o idioma que você criar puder direcionar um desses dois tempos de execução, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o já fornecerá os mecanismos de depuração necessários. Tudo o que você precisa implementar é um avaliador de expressão.

## <a name="debug-engine-operation"></a>Operação do mecanismo de depuração
 Os serviços de monitoramento são implementados por meio de interfaces DE e podem fazer com que o pacote de depuração faça a transição entre diferentes modos operacionais. Para obter mais informações, consulte [modos operacionais](../../extensibility/debugger/operational-modes.md). Normalmente, há apenas uma DE implementação por ambiente DE tempo DE execução.

> [!NOTE]
> Embora haja implementações separadas para Transact-SQL e [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] , VBScript e [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] Compartilhe um único de.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] a depuração permite que os mecanismos de depuração executem uma das duas maneiras: no mesmo processo que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell ou no mesmo processo que o programa de destino que está sendo depurado. A última forma geralmente ocorre quando o processo que está sendo depurado é, na verdade, um script em execução em um intérprete. O mecanismo de depuração deve ter conhecimento profundo do intérprete para monitorar o script. Nesse caso, o intérprete é, na verdade, um tempo de execução; mecanismos de depuração são para implementações de tempo de execução específicas. Além disso, a implementação de um único DE pode ser dividida entre os limites do processo e da máquina (por exemplo, depuração remota).

 O DE expõe as [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interfaces de depuração. Toda a comunicação é por meio de COM. Independentemente de ser carregado em processo, fora do processo ou em outro computador, ele não afeta a comunicação do componente.

 O DE funciona com um componente avaliador de expressão para habilitar o DE para esse tempo de execução específico entender a sintaxe das expressões. O DE também funciona com um componente de manipulador de símbolo para acessar as informações de depuração simbólicas geradas pelo compilador de linguagem. Para obter mais informações, consulte [avaliador de expressão](../../extensibility/debugger/expression-evaluator.md) e [provedor de símbolos](../../extensibility/debugger/symbol-provider.md).

## <a name="see-also"></a>Confira também
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
- [Avaliador de expressão](../../extensibility/debugger/expression-evaluator.md)
- [Provedor de símbolos](../../extensibility/debugger/symbol-provider.md)
