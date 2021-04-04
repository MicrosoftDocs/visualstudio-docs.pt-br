---
title: Depurar de um projeto de DLL | Microsoft Docs
description: Você pode iniciar a depuração de um projeto de DLL do projeto em si, especificando o aplicativo de chamada nas propriedades do projeto. Consulte este artigo para obter detalhes.
ms.custom: SEO-VS-2020
ms.date: 3/30/2021
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- DLL projects, debugging
- debugging DLLs
- DLLs, debugging projects
- debugging [Visual Studio], DLLs
ms.assetid: 40a94339-d3f7-4ab9-b8a1-b8cf82942f44
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7846cc3fd17b46365da59f6fe1a744032cb8ba14
ms.sourcegitcommit: 155d5f0fd54ac1d20df2f5b0245365924faa3565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106083636"
---
# <a name="how-to-debug-from-a-dll-project-in-visual-studio-c-c-visual-basic-f"></a>Como: Depurar de um projeto de DLL no Visual Studio (C#, C++, Visual Basic, F #)

Uma maneira de depurar um projeto de DLL é especificar o aplicativo de chamada nas propriedades do projeto de DLL. Em seguida, você pode iniciar a depuração do próprio projeto de DLL. Para que esse método funcione, o aplicativo deve chamar a mesma DLL no mesmo local que você configurar. Se o aplicativo localizar e carregar uma versão diferente da DLL, essa versão não conterá seus pontos de interrupção. Para outros métodos de depuração de DLLs, consulte [Depurando projetos de dll](../debugger/debugging-dll-projects.md).

Se o aplicativo gerenciado chamar uma DLL nativa ou seu aplicativo nativo chamar uma DLL gerenciada, você poderá depurar a DLL e o aplicativo de chamada. Para obter mais informações, consulte [como depurar em modo misto](../debugger/how-to-debug-in-mixed-mode.md).

Os projetos DLL nativos e gerenciados têm configurações diferentes para especificar aplicativos de chamada.

## <a name="specify-a-calling-app-in-a-native-dll-project"></a>Especificar um aplicativo de chamada em um projeto de DLL nativo

1. Selecione o projeto de DLL C++ em **Gerenciador de soluções**. Selecione o ícone **Propriedades** , pressione **ALT** + **Enter**, ou clique com o botão direito do mouse e escolha **Propriedades**.

1. Na caixa de diálogo **\<Project> páginas de propriedades** , verifique se o campo de **configuração** na parte superior da janela está definido como **depurar**.

1. Selecione depuração de **Propriedades de configuração**  >  .

1. Na lista **depurador a ser iniciado** , escolha o **depurador local do Windows** ou o **depurador remoto do Windows**.

1. Na caixa **comando** ou **comando remoto** , adicione o caminho totalmente qualificado e o nome do arquivo do aplicativo de chamada, como um arquivo *. exe* .

   ![janela Propriedades de depuração](../debugger/media/dbg-debugging-properties-dll.png "janela Propriedades de depuração")

1. Adicione todos os argumentos de programa necessários à caixa **argumentos de comando** .

1. Selecione **OK**.

## <a name="specify-a-calling-app-in-a-managed-dll-project"></a>Especificar um aplicativo de chamada em um projeto DLL gerenciado

1. Selecione o projeto de DLL do Visual Basic ou C# no **Gerenciador de soluções**. Selecione o ícone **Propriedades** , pressione **ALT** + **Enter**, ou clique com o botão direito do mouse e escolha **Propriedades**.

1. Verifique se o campo de **configuração** na parte superior da janela está definido como **depurar**.

1. Em **ação inicial**:

   - Para .NET Framework DLLs, selecione **Iniciar programa externo** e adicione o caminho totalmente qualificado e o nome do aplicativo de chamada.

   - Ou selecione **Iniciar navegador com URL** e preencha a URL de um aplicativo ASP.net local.

   - Para as DLLs do .NET Core, a página de propriedades de **depuração** é diferente. Selecione **executável** na lista suspensa **Iniciar** e, em seguida, adicione o caminho totalmente qualificado e o nome do aplicativo de chamada no campo **executável** .

1. Adicione todos os argumentos de linha de comando necessários no campo argumentos de **linha de comando** ou **argumentos de aplicativo** .

   ![Janela Propriedades de depuração em C#](../debugger/media/dbg-debugging-properties-dll-csharp.png "Janela Propriedades de depuração em C#")

1. Use **arquivo**  >  **salvar itens selecionados** ou **Ctrl** + **S** para salvar as alterações.

## <a name="debug-from-the-dll-project"></a>Depurar do projeto de DLL

1. Defina pontos de interrupção no projeto de DLL.

1. Clique com o botão direito do mouse no projeto de DLL e escolha **definir como projeto de inicialização**.

1. Verifique se o campo de **configuração de soluções** está definido como **depurar**. Pressione **F5**, clique na seta de **início** verde ou selecione **depurar**  >  **Iniciar Depuração**.

Outras dicas:

- Se a depuração não atingir seus pontos de interrupção, verifique se a saída da DLL (por padrão, a pasta *\<project> \debug* ) é o local que o aplicativo de chamada está chamando.

- Se você quiser dividir o código em um aplicativo de chamada gerenciado de uma DLL nativa, ou vice-versa, habilite a [depuração de modo misto](../debugger/how-to-debug-in-mixed-mode.md).

- Em alguns cenários, talvez seja necessário informar ao depurador onde encontrar o código-fonte. Para obter mais informações, consulte [usar os símbolos não carregados/nenhuma página carregada de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#use-the-no-symbols-loadedno-source-loaded-pages).

## <a name="see-also"></a>Confira também
- [Depuração de projetos de DLL](../debugger/debugging-dll-projects.md)
- [Configurações do projeto para configurações de depuração do C#](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Definições do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [Configurações do projeto para uma configuração de depuração do C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)
