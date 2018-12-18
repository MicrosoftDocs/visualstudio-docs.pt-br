---
title: Sai do C# quando quadros nativos estiverem ausentes da pilha de chamadas de código | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- Call Stack window, missing native frames
- code, managed code
- native frames
- stepping, out of managed code
- managed code, stepping out of
ms.assetid: 97cdd2a8-02a9-4a06-a5b1-c92b1e431979
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
- dotnet
ms.openlocfilehash: 741afb6befdbc29cafab39c3c9b0d7bb2761d7b1
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53057646"
---
# <a name="how-to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-window"></a>Como: Sair do código gerenciado quando quadros nativos estiverem ausentes da janela pilha de chamadas

Se seu código tiver quadros nativos invisíveis na janela **Pilha de Chamadas**, realizar a depuração circular do código gerenciado poderá produzir resultados inesperados. Como alternativa, você pode usar um ponto de interrupção em vez da **Depuração Circular**.

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

## <a name="step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-display"></a>Realizar Depuração Circular do código gerenciado quando os quadros nativos estiverem ausentes da exibição da pilha de chamadas

1.  No código nativo, defina um ponto de interrupção do local depois da chamada para o código gerenciado.

2.  No menu **Depurar**, escolha **Continuar**.

     Quando a chamada gerenciada for concluída, a execução será interrompida no ponto de interrupção no código nativo.

## <a name="see-also"></a>Consulte também

- [Como: Usar a janela de pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md)