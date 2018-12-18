---
title: 'Como: depurar de um projeto DLL | Microsoft Docs'
ms.custom: ''
ms.date: 10/10/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e006bbd27acc0fa88cfee1b22cb435acba1e282e
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388248"
---
# <a name="how-to-debug-from-a-dll-project-in-visual-studio-c-c-visual-basic-f"></a>Como: depurar de um projeto DLL no Visual Studio (C#, C++, Visual Basic, F#)

Uma maneira de depurar um projeto de DLL é especificar o aplicativo de chamada nas propriedades do projeto DLL. Em seguida, você pode iniciar a depuração a partir do projeto de DLL. Para esse método funcione, o aplicativo deve chamar a mesma DLL no mesmo local que você configurar. Se o aplicativo localiza e carrega uma versão diferente da DLL, essa versão não conterá seus pontos de interrupção. Para outros métodos de depuração de DLLs, consulte [projetos de DLL de depuração](../debugger/debugging-dll-projects.md).
  
Se seu aplicativo gerenciado chama uma DLL nativa, ou se seu aplicativo nativo chama uma DLL gerenciada, você pode depurar a DLL e o aplicativo de chamada. Para obter mais informações, consulte [como: depurar no modo misto](../debugger/how-to-debug-in-mixed-mode.md).   

Projetos DLL nativos e gerenciados tem configurações diferentes para especificar os aplicativos de chamada. 

## <a name="specify-a-calling-app-in-a-native-dll-project"></a>Especifique um aplicativo de chamada em um projeto DLL nativo  
  
1. Selecione o projeto de DLL do C++ no **Gerenciador de soluções**. Selecione o **propriedades** ícone, pressione **Alt**+**Enter**, ou clique com botão direito e escolha **propriedades**.
   
1. No  **\<projeto > páginas de propriedades** caixa de diálogo caixa, certifique-se a **Configuration** campo na parte superior da janela é definido como **depurar**. 
   
1. Selecione **propriedades de configuração** > **depuração**.  
   
1. No **depurador a iniciar** lista, escolha **depurador Local do Windows** ou **depurador remoto do Windows**.  
   
1. No **comando** ou **comando remoto** caixa, adicione o caminho totalmente qualificado e o nome do arquivo do aplicativo de chamada, como um *.exe* arquivo.
   
   ![Janela de propriedades de depuração](../debugger/media/dbg-debugging-properties-dll.png "janela de propriedades de depuração")  
   
1. Adicione quaisquer argumentos necessários do programa para o **argumentos de comando** caixa.  
   
1. Selecione **OK**.

## <a name="specify-a-calling-app-in-a-managed-dll-project"></a>Especifique um aplicativo de chamada em um projeto DLL gerenciado  
  
1. Selecione o C# ou o projeto de DLL do Visual Basic no **Gerenciador de soluções**. Selecione o **propriedades** ícone, pressione **Alt**+**Enter**, ou clique com botão direito e escolha **propriedades**.
   
1. Certifique-se de que o **Configuration** campo na parte superior da janela é definido como **depurar**.
   
1. Sob **iniciar ação**:
   
   - Para DLLs do .NET Framework, selecione **Iniciar programa externo**e adicione o caminho totalmente qualificado e o nome do aplicativo de chamada.
     
   - Ou, selecione **Iniciar navegador com URL** e preencha a URL de um aplicativo ASP.NET local. 
   
   - Para DLLs do .NET Core, o **depurar** página de propriedades for diferente. Selecione **executável** da **inicie** lista suspensa e, em seguida, adicione o caminho totalmente qualificado e o nome do aplicativo de chamada no **executável** campo. 
   
1. Adicionar todos os argumentos de linha de comando necessários na **argumentos de linha de comando** ou **argumentos do aplicativo** campo.
   
   ![C#Janela de propriedades de depuração](../debugger/media/dbg-debugging-properties-dll-csharp.png " C# janela Propriedades de depuração") 
   
1. Use **arquivo** > **salvar itens selecionados** ou **Ctrl**+**S** para salvar as alterações.

## <a name="debug-from-the-dll-project"></a>Depurar a partir do projeto de DLL  
 
1. Definir pontos de interrupção no projeto de DLL.

1. Clique com botão direito do projeto de DLL e escolha **definir como projeto de inicialização**. 

1. Verifique se o **configuração de soluções** campo é definido como **depurar**. Pressione **F5**, clique em verde **inicie** seta ou selecione **depurar** > **iniciar depuração**.

Se a depuração não atinge seus pontos de interrupção, certifique-se de que sua DLL de saída (por padrão, o  *\<projeto > \Debug* pasta) é o local em que o aplicativo de chamada está chamando.
  
## <a name="see-also"></a>Consulte também  
 [Depurando projetos de DLL](../debugger/debugging-dll-projects.md)   
 [Configurações do projeto para configurações de depuração do C#](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Definições do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)