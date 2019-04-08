---
title: 'Como: Depurar de um projeto DLL | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- DLL projects, debugging
- debugging DLLs
- DLLs, debugging projects
- debugging [Visual Studio], DLLs
ms.assetid: 40a94339-d3f7-4ab9-b8a1-b8cf82942f44
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4a9a3e7cd63e5a485063789d9f9eeaf1227d1b5d
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58926878"
---
# <a name="how-to-debug-from-a-dll-project"></a>Como: Depurar de um projeto DLL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para iniciar a depuração de um projeto DLL, você deve especificar o aplicativo de chamada nas propriedades do projeto. As páginas de propriedades do C++ diferem no layout e conteúdo a partir do C# e Visual Basic páginas de propriedades.  
  
 Se uma DLL gerenciada for chamada por código nativo e você quiser depurar os dois, você pode especificar isso nas propriedades do projeto. Para obter mais informações, confira [Como: Depurar no modo misto](../debugger/how-to-debug-in-mixed-mode.md).  
  
> [!NOTE]
>  Você não pode especificar um aplicativo de chamada externa nas edições Express do Visual Studio. Em vez disso, você precisa adicionar um projeto executável à solução, defini-lo como o projeto de inicialização e chamar métodos na DLL do projeto executável.  
  
### <a name="to-specify-the-calling-application-in-a-c-project"></a>Para especificar o aplicativo de chamada em um projeto C++  
  
1.  Clique com botão direito no nó do projeto na **Gerenciador de soluções** e selecione **propriedades**. Vá para o **depurar** guia.  
  
2.  Certifique-se de que o **Configuration** campo na parte superior da janela é definido como **depurar**.  
  
3.  Vá para **propriedades de configuração / depuração**.  
  
4.  No **depurador a iniciar** , escolha **depurador Local do Windows** ou **depurador remoto do Windows**.  
  
5.  No **comando** ou **comando remoto** caixa, adicione o nome de caminho totalmente qualificado do aplicativo.  
  
6.  Adicione quaisquer argumentos necessários do programa para o **argumentos de comando** caixa.  
  
### <a name="to-specify-the-calling-application-in-a-c-or-visual-basic-project"></a>Para especificar o aplicativo de chamada em um projeto C# ou Visual Basic  
  
1.  Clique com botão direito no nó do projeto na **Gerenciador de soluções** e selecione **propriedades**. Vá para o **depurar** guia.  
  
     Selecione **Iniciar programa externo**e adicione o nome de caminho totalmente qualificado do programa a ser executado.  
  
     Se você precisar adicionar argumentos de linha de comando do programa externo, adicione-os **argumentos de linha de comando** campo.  
  
2.  Você também pode chamar um aplicativo como uma URL. (Você poderá fazer isso se estiver depurando uma DLL gerenciada usada por um aplicativo local do ASP.NET.)  
  
     Sob **iniciar ação**, selecione o **Iniciar navegador na URL:** botão de opção e preencha a URL.  
  
### <a name="to-start-debugging-from-the-dll-project"></a>Para iniciar a depuração do projeto da DLL  
  
1.  Defina pontos de interrupção conforme necessário.  
  
2.  Iniciar a depuração (pressione F5, clique na seta verde ou clique em **depurar / iniciar depuração**).  
  
## <a name="see-also"></a>Consulte também  
 [Depurando projetos de DLL](../debugger/debugging-dll-projects.md)   
 [Configurações do projeto para configurações de depuração de C#](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Configurações do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)
