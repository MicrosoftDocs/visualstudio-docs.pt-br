---
title: Depurar um aplicativo que não faz parte de uma solução do Visual Studio
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/19/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], executables
- executable files, importing
- executable files, debugging outside of projects
ms.assetid: 3ea176e8-1ce5-42c4-b7a2-abe3a2765033
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8c408ca42f82c0419c6570068e2a83e97f2371e9
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066607"
---
# <a name="debug-an-app-that-isnt-part-of-a-visual-studio-solution-c-c-visual-basic-f"></a>Depurar um aplicativo que não faz parte de uma solução do Visual Studio (C++, C#, Visual Basic, F#)

Você talvez queira depurar um aplicativo (*.exe* arquivo) que não faça parte de uma solução do Visual Studio. Você ou outra pessoa pode ter criado o aplicativo fora do Visual Studio, ou você colocou o aplicativo de outro lugar. 

A maneira usual de depurar um aplicativo que não existe no Visual Studio é iniciar o aplicativo fora do Visual Studio e, em seguida, anexar a ele usando **anexar ao processo** no depurador do Visual Studio. Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
Anexar a um aplicativo requer etapas manuais que levam alguns segundos. Devido a esse atraso, anexação não ajudará a depurar um problema de inicialização ou um aplicativo que não aguarda o usuário de entrada e fecha rapidamente. 

Nessas situações, você pode criar um projeto EXE do Visual Studio para o aplicativo ou importá-lo para um existente C#, Visual Basic ou C++ solução. Nem todas as linguagens de programação oferecem suporte a projetos EXE. 

>[!IMPORTANT]
>Recursos de depuração para um aplicativo que não foi compilado no Visual Studio são limitados, se você anexa ao aplicativo ou adicioná-lo a uma solução do Visual Studio. 
>
>Se você tiver o código-fonte, a melhor abordagem é importar o código em um projeto do Visual Studio. Em seguida, execute uma compilação de depuração do aplicativo.
>
>Se você não tiver o código-fonte e o aplicativo não tiver [informações de depuração](../debugger/how-to-set-debug-and-release-configurations.md) em um formato compatível, recursos de depuração disponíveis são muito poucos. 

### <a name="to-create-a-new-exe-project-for-an-existing-app"></a>Para criar um novo projeto EXE para um aplicativo existente  
   
1. No Visual Studio, selecione **arquivo** > **abra** > **projeto**.  
   
1. No **Abrir projeto** caixa de diálogo, selecione **todos os arquivos de projeto**, se ainda não estiver selecionado, no menu suspenso próximo a **nome do arquivo**.  
   
1. Navegue até a *.exe* do arquivo, selecione-o e selecione **abrir**.  
   
   O arquivo aparece em uma solução nova, temporária do Visual Studio.

1. Iniciar a depuração do aplicativo, selecionando um comando de execução, como **iniciar depuração**, da **depurar** menu.    
  
### <a name="to-import-an-app-into-an-existing-visual-studio-solution"></a>Para importar um aplicativo para uma solução existente do Visual Studio  
  
1.  Com um C++, C#, ou solução do Visual Basic aberta no Visual Studio, selecione **arquivo** > **Add** > **projeto existente**.  
  
1. No **Abrir projeto** caixa de diálogo, selecione **todos os arquivos de projeto**, se ainda não estiver selecionado, no menu suspenso próximo a **nome do arquivo**.  
   
1. Navegue até a *.exe* do arquivo, selecione-o e selecione **abrir**.  
   
   O arquivo aparece como um novo projeto na solução atual.  
   
1. Com o novo arquivo selecionado, inicie a depuração do aplicativo, selecionando um comando de execução, como **iniciar depuração**, da **depurar** menu.    
  
### <a name="see-also"></a>Consulte também  
 [Configurações e preparação do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Arquivos DBG](/previous-versions/visualstudio/visual-studio-2010/da528y14(v=vs.100))