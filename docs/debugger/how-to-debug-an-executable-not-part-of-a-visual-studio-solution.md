---
title: Depurar um aplicativo que não faz parte de uma solução do Visual Studio
titleSuffix: ''
description: Saiba como depurar um aplicativo que não faz parte de uma solução do Visual Studio. Talvez você possa anexar o depurador do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 02/21/2020
ms.topic: how-to
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f201121eb65f7c045ac42783ac71b2d49fafd802
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154997"
---
# <a name="debug-an-app-that-isnt-part-of-a-visual-studio-solution-c-c-visual-basic-f"></a>Depurar um aplicativo que não faz parte de uma solução do Visual Studio (C++, C#, Visual Basic, F #)

Talvez você queira depurar um aplicativo (arquivo *. exe* ) que não faça parte de uma solução do Visual Studio. Pode ser um projeto de [pasta aberta](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) , ou você ou outra pessoa pode ter criado o aplicativo fora do Visual Studio, ou você tem o aplicativo de outro lugar.

- Para um projeto de pasta aberta no Visual Studio (que não tem um arquivo de projeto ou de solução), consulte [executar e depurar seu código](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md#run-and-debug-your-code) ou, para C++, [configurar parâmetros de depuração com launch.vs.jsem](/cpp/build/open-folder-projects-cpp#configure-debugging-parameters-with-launchvsjson).

- Para um aplicativo que não existe no Visual Studio, a maneira usual de Depurar é iniciar o aplicativo fora do Visual Studio e, em seguida, anexá-lo a ele usando **anexar ao processo** no depurador do Visual Studio. Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).

   Anexar a um aplicativo requer etapas manuais que levam alguns segundos. Devido a esse atraso, a anexação não ajudará a depurar um problema de inicialização ou um aplicativo que não aguarde a entrada do usuário e seja concluído rapidamente.

   Nessas situações, você pode criar um projeto EXE do Visual Studio para o aplicativo ou importá-lo para uma solução existente em C#, Visual Basic ou C++. Nem todas as linguagens de programação oferecem suporte a projetos EXE.

>[!IMPORTANT]
>Os recursos de depuração para um aplicativo que não foi criado no Visual Studio são limitados, independentemente de você anexar ao aplicativo ou adicioná-lo a uma solução do Visual Studio.
>
>Se você tiver o código-fonte, a melhor abordagem é importar o código para um projeto do Visual Studio. Em seguida, execute uma compilação de depuração do aplicativo.
>
>Se você não tiver o código-fonte e o aplicativo não tiver [informações de depuração](../debugger/how-to-set-debug-and-release-configurations.md) em um formato compatível, os recursos de depuração disponíveis serão muito poucos.

### <a name="to-create-a-new-exe-project-for-an-existing-app"></a>Para criar um novo projeto EXE para um aplicativo existente

1. No Visual Studio, selecione **arquivo**  >  **abrir**  >  **projeto**.

1. Na caixa de diálogo **Abrir projeto** , selecione **todos os arquivos de projeto**, se ainda não estiver selecionado, na lista suspensa ao lado de **nome do arquivo**.

1. Navegue até o arquivo *. exe* , selecione-o e selecione **abrir**.

   O arquivo aparece em uma nova solução temporária do Visual Studio.

1. Inicie a depuração do aplicativo selecionando um comando de execução, como **Iniciar Depuração**, no menu **depurar** .

### <a name="to-import-an-app-into-an-existing-visual-studio-solution"></a>Para importar um aplicativo para uma solução existente do Visual Studio

1. Com uma solução C++, C# ou Visual Basic aberta no Visual Studio, selecione **arquivo**  >  **Adicionar**  >  **projeto existente**.

1. Na caixa de diálogo **Abrir projeto** , selecione **todos os arquivos de projeto**, se ainda não estiver selecionado, na lista suspensa ao lado de **nome do arquivo**.

1. Navegue até o arquivo *. exe* , selecione-o e selecione **abrir**.

   O arquivo aparece como um novo projeto na solução atual.

1. Com o novo arquivo selecionado, inicie a depuração do aplicativo selecionando um comando de execução, como **Iniciar Depuração**, no menu **depurar** .

### <a name="see-also"></a>Confira também
- [Configurações e preparação do depurador](../debugger/debugger-settings-and-preparation.md)
- [Segurança do depurador](../debugger/debugger-security.md)
- [Arquivos DBG](/previous-versions/visualstudio/visual-studio-2010/da528y14(v=vs.100))
