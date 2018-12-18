---
title: 'Como: usar Editar e continuar (c#) | Microsoft Docs'
ms.custom: ''
ms.date: 10/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], about Edit and Continue
ms.assetid: 40e136d8-a08c-43bd-b313-fb821c55eb3c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 41e97f488344e3d34ce326a3d35880d94da4ad9a
ms.sourcegitcommit: c5e72875206b8c5737c29d5b1ec7b86eec747303
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49382799"
---
# <a name="how-to-use-edit-and-continue-c"></a>Como usar Editar e Continuar (C#)
Com editar e continuar, você pode fazer e aplicar as alterações ao seu código no modo de interrupção durante a depuração, sem a necessidade de parar e reiniciar a sessão de depuração.  

Editar e continuar para C# ocorre automaticamente quando você faça alterações de código no modo de interrupção, e em seguida, continua a depuração usando **continuar**, **etapa**, ou **definir próxima instrução**, ou avaliar uma função em uma janela do depurador.  

Para obter mais informações, consulte [editar e continuar (Visual C#)](../debugger/edit-and-continue-visual-csharp.md).

>[!NOTE]
>Editar e continuar não dá suporte para a otimização misto, ou código de integração do SQL Server common language runtime (CLR). Para obter informações sobre outros cenários sem suporte, consulte [suporte para alterações de código (C# e Visual Basic)](../debugger/supported-code-changes-csharp.md). Se você tentar editar e continuar com um desses cenários, uma caixa de mensagem será exibida, informando que editar e continuar não é suportado.  
  
**Para habilitar ou desabilitar editar e continuar:**  
   
1. Se você estiver em uma sessão de depuração, pare a depuração (**Debug** > **parar depuração** ou **Shift**+**F5**) .
   
1. Na **ferramentas** > **opções** (ou **depurar** > **opções**) > **dedepuração**  >  **Gerais**, marque ou desmarque as **habilitar editar e continuar** caixa de seleção.  
  
A configuração entra em vigor quando você iniciar ou reiniciar a sessão de depuração.  

**Para usar Editar e continuar:**  
   
1. Durante a depuração, no modo de interrupção, faça uma alteração ao código-fonte.  
   
1. Dos **Debug** menu, clique em **continuar**, **etapa**, ou **definir próxima instrução**, ou avaliar uma função em uma janela do depurador.  
   
   Depuração continua com o novo código compilado. 

Não há suporte para alguns tipos de alterações de código por editar e continuar. Para obter mais informações, consulte [suporte para alterações de código (C# e Visual Basic)](../debugger/supported-code-changes-csharp.md).   
