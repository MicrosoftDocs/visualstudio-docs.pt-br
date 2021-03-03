---
title: 'Tutorial: depurar código C# e C++ (modo misto)'
description: Saiba como depurar uma DLL nativa de um aplicativo .NET Core ou .NET Framework usando a depuração de modo misto
ms.custom: seodec18
ms.date: 11/02/2018
ms.topic: tutorial
dev_langs:
- CSharp
- C++
helpviewer_keywords:
- mixed mode debugging
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: 4d001e89993b90f6e8b7b33f43a5c06a1ffd7cd1
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683326"
---
# <a name="tutorial-debug-c-and-c-in-the-same-debugging-session"></a>Tutorial: Depurar C# e C++ na mesma sessão de depuração

O Visual Studio permite que você habilite mais de um tipo de depurador em uma sessão de depuração, o que é chamado de depuração de modo misto. Neste tutorial, você aprenderá a depurar código gerenciado e nativo em uma única sessão de depuração.

Este tutorial mostra como depurar código nativo de um aplicativo gerenciado, mas você também pode [depurar código gerenciado de um aplicativo nativo](../debugger/how-to-debug-in-mixed-mode.md). O depurador também dá suporte a outros tipos de depuração de modo misto, como a depuração de [Python e código nativo](../python/debugging-mixed-mode-c-cpp-python-in-visual-studio.md) e ao uso do depurador de scripts em tipos de aplicativo, como o ASP.NET.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Criar uma DLL nativa simples
> * Criar um aplicativo .NET Core ou .NET Framework simples para chamar a DLL
> * Configurar a depuração de modo misto
> * Iniciar o depurador
> * Atingir um ponto de interrupção no aplicativo gerenciado
> * Intervir no código nativo

## <a name="prerequisites"></a>Pré-requisitos

O Visual Studio precisa estar instalado, com as cargas de trabalho a seguir:
- **Desenvolvimento para desktop com C++**
- **Desenvolvimento para desktop com .NET** ou **Desenvolvimento multiplataforma com .NET Core**, dependendo de qual tipo de aplicativo você deseja criar.

Se você não tiver o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.

Se o Visual Studio estiver instalado, mas as cargas de trabalho necessárias não estiverem, selecione **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo projeto** do Visual Studio. No Instalador do Visual Studio, selecione as cargas de trabalho necessárias e, em seguida, selecione **Modificar**.

## <a name="create-a-simple-native-dll"></a>Criar uma DLL nativa simples

**Para criar os arquivos para o projeto de DLL:**

1. Abra o Visual Studio e crie um projeto.

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl + Q** para abrir a caixa de pesquisa, digite **projeto vazio**, escolha **modelos** e, em seguida, escolha **projeto vazio** para C++. Na caixa de diálogo que aparece, escolha **Criar**. Em seguida, digite um nome como **Mixed_Mode_Debugging** e clique em **criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **Novo projeto**, em **Visual C++**, escolha **Outro** e, em seguida, no painel central, escolha **Projeto Vazio**. Em seguida, digite um nome como **Mixed_Mode_Debugging** e clique em **OK**.
    ::: moniker-end

    Caso não veja o modelo de **Projeto Vazio**, acesse **Ferramentas** > **Obter Ferramentas e Recursos...**, que abre o Instalador do Visual Studio. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento para desktop com C++** e, em seguida, selecione **Modificar**.

    O Visual Studio cria o projeto.

1. No **Gerenciador de Soluções**, selecione **Arquivos de Origem** e, em seguida, selecione **Projeto** > **Adicionar Novo Item**. Ou clique com o botão direito do mouse em **Arquivos de Origem** e selecione **Adicionar** > **Novo Item**.

1. Na caixa de diálogo **Novo Item**, selecione **Arquivo C++ (.cpp)**. Digite **Mixed_Mode.cpp** no campo **Nome** e, em seguida, selecione **Adicionar**.

    O Visual Studio adiciona o novo arquivo C++ ao **Gerenciador de Soluções**.

1. Copie o seguinte código em *Mixed_Mode.cpp*:

    ```cpp
    #include "Mixed_Mode.h"
    ```

1. No **Gerenciador de Soluções**, selecione **Arquivos de Cabeçalho** e, em seguida, selecione **Projeto** > **Adicionar Novo Item**. Ou, clique com o botão direito do mouse em **Arquivos de Cabeçalho** e selecione **Adicionar** > **Novo Item**.

1. Na caixa de diálogo **Novo Item**, selecione **Arquivo de cabeçalho (.h)**. Digite **Mixed_Mode.h** no campo **Nome** e, em seguida, selecione **Adicionar**.

   O Visual Studio adiciona o novo arquivo de cabeçalho ao **Gerenciador de Soluções**.

1. Copie o seguinte código em *Mixed_Mode.h*:

    ```cpp
    #ifndef MIXED_MODE_MULTIPLY_HPP
    #define MIXED_MODE_MULTIPLY_HPP

    extern "C"
    {
      __declspec(dllexport) int __stdcall mixed_mode_multiply(int a, int b) {
        return a * b;
      }
    }
    #endif
    ```

1. Selecione **arquivo**  >  **salvar tudo** ou pressione **Ctrl** + **Shift** + **S** para salvar os arquivos.

**Para configurar e criar o projeto de DLL:**

1. Na barra de ferramentas do Visual Studio, selecione a configuração **Depurar** e a plataforma **x86** ou **x64**. Se o aplicativo de chamada será o .NET Core, que sempre é executado no modo de 64 bits, selecione **x64** como a plataforma.

1. No **Gerenciador de Soluções**, selecione o nó do projeto **Mixed_Mode_Debugging** e escolha o ícone **Propriedades** ou clique com o botão direito do mouse no nó do projeto e selecione **Propriedades**.

1. Na parte superior do painel **Propriedades**, verifique se a **Configuração** está definida como **Active(Debug)** e a **Plataforma** é a mesma que você definiu na barra de ferramentas: **x64** ou **Win32** para a plataforma x86.

   > [!IMPORTANT]
   > Se você mudar a plataforma de **x86** para **x64** ou vice-versa, reconfigure as propriedades da nova plataforma.

1. Nas **Propriedades de Configuração** no painel esquerdo, selecione **Vinculador** > **Avançado** e, no menu suspenso ao lado de **Nenhum Ponto de Entrada**, selecione **Não**. Se você precisou alterá-lo para **Não**, selecione **Aplicar**.

1. Nas **Propriedades de configuração**, selecione **Geral** e no menu suspenso ao lado de **Tipo de Configuração**, selecione **Biblioteca Dinâmica (.dll)**. Selecione **Aplicar** e, depois, **OK**.

   ![Mudar para uma DLL nativa](../debugger/media/mixed-mode-set-as-native-dll.png)

1. Selecione o projeto no **Gerenciador de Soluções** e, em seguida, selecione **Compilar** > **Compilar Solução**, pressione **F7** ou clique com o botão direito do mouse no projeto e selecione **Compilar**.

   O projeto deve ser compilado sem erros.

## <a name="create-a-simple-managed-app-to-call-the-dll"></a>Criar um aplicativo gerenciado simples para chamar a DLL

1. Abra o Visual Studio e crie um projeto.

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl + Q** para abrir a caixa de pesquisa, digite **console**, escolha **modelos** e, em seguida, escolha **aplicativo de console** para .NET Core ou aplicativo de **console (.NET Framework)** para C#. Na caixa de diálogo que aparece, escolha **Avançar**.

    Em seguida, digite um nome como **Mixed_Mode_Calling_App** e clique em **Avançar** ou **criar**, a opção que estiver disponível.

    Para o .NET Core, escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **Novo projeto**, em **Visual C#**, escolha **Área de Trabalho do Windows** e, em seguida, no painel central, escolha **Aplicativo de Console (.NET Framework)** ou **Aplicativo de Console (.NET Core)**.

    Em seguida, digite um nome como **Mixed_Mode_Calling_App** e clique em **OK**.
    ::: moniker-end

    Se você não vir o modelo de projeto correto, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre a instalador do Visual Studio. Escolha o **desenvolvimento de plataforma cruzada do .NET Core** ou a carga de **trabalho de desenvolvimento de desktop .net** , dependendo da estrutura de destino e, em seguida, escolha **Modificar**.

    > [!NOTE]
    > Você também pode adicionar o novo projeto gerenciado à sua solução C++ existente. Estamos criando o projeto em uma nova solução para tornar a tarefa de depuração de modo misto mais difícil.

   O Visual Studio cria o projeto vazio e exibe-o no **Gerenciador de Soluções**.

1. Substitua todo o código em *Program.cs* pelo código a seguir:

    ```csharp
    using System;
    using System.Runtime.InteropServices;

    namespace Mixed_Mode_Calling_App
    {
        public class Program
        {
            // Replace the file path shown here with the
            // file path on your computer. For .NET Core, the typical (default) path
            // for a 64-bit DLL might look like this:
            // C:\Users\username\source\repos\Mixed_Mode_Debugging\x64\Debug\Mixed_Mode_Debugging.dll
            // Here, we show a typical path for a DLL targeting the **x86** option.
            [DllImport(@"C:\Users\username\source\repos\Mixed_Mode_Debugging\Debug\Mixed_Mode_Debugging.dll", EntryPoint =
            "mixed_mode_multiply", CallingConvention = CallingConvention.StdCall)]
            public static extern int Multiply(int x, int y);
            public static void Main(string[] args)
            {
                int result = Multiply(7, 7);
                Console.WriteLine("The answer is {0}", result);
                Console.ReadKey();
            }
        }
    }
    ```

1. No novo código, substitua o caminho de arquivo em `[DllImport]` pelo caminho de arquivo para o *Mixed_Mode_Debugging.dll* que você acabou de criar. Veja o comentário do código para obter dicas. Substitua o espaço reservado *nomedousuário*.

1. Selecione **arquivo**  >  **salvar Program.cs** ou pressione **Ctrl** + **S** para salvar o arquivo.

## <a name="configure-mixed-mode-debugging"></a>Configurar a depuração de modo misto

1. No **Gerenciador de Soluções**, selecione o nó do projeto **Mixed_Mode_Calling_App** e escolha o ícone **Propriedades** ou clique com o botão direito do mouse no nó do projeto e selecione **Propriedades**.

1. Selecione **Depurar** no painel esquerdo, escolha a caixa de seleção **Habilitar depuração de código nativo** e, em seguida, feche a página Propriedades para salvar as mudanças.

    ![Habilitar depuração de modo misto](../debugger/media/mixed-mode-enable-native-code-debugging.png)

## <a name="set-a-breakpoint-and-start-debugging"></a>Definir um ponto de interrupção e iniciar a depuração

1. No projeto C#, abra *Program.cs*. Defina um ponto de interrupção na linha de código a seguir clicando na margem esquerda extrema, selecionando a linha e pressionando **F9** ou clicando com o botão direito do mouse na linha e selecionando **Ponto de interrupção** > **Inserir Ponto de Interrupção**.

    ```csharp
    int result = Multiply(7, 7);
    ```

    Um círculo vermelho aparece na margem esquerda em que você definiu o ponto de interrupção.

1. Pressione **F5**, selecione a seta verde na barra de ferramentas do Visual Studio ou selecione **Depurar** > **Iniciar Depuração** para iniciar a depuração.

   O depurador é pausado no ponto de interrupção que você definir. Uma seta amarela indica onde o depurador está em pausa no momento.

## <a name="step-in-and-out-of-native-code"></a>Intervir e usar a depuração circular no código nativo

1. Enquanto a depuração estiver em pausa no aplicativo gerenciado, pressione **F11** ou selecione **Depurar** > **Intervir**.

   O arquivo de cabeçalho nativo *Mixed_Mode.h* será aberto e você verá a seta amarela em que o depurador está em pausa.

   ![Intervir no código nativo](../debugger/media/mixed-mode-step-into-native-code.png)

1. Agora, você pode definir e usar pontos de interrupção e inspecionar variáveis no código nativo ou gerenciado.

   - Passe o mouse sobre as variáveis no código-fonte para ver seus valores.

   - Examine a variável e seus valores nas janelas **Autos** e **Locais**.

   - Enquanto o depurador está em pausa, você também pode usar as janelas **Inspecionar** e **Pilha de Chamadas**.

1. Pressione **F11** novamente para avançar uma linha no depurador.

1. Pressione **Shift** + **F11** ou selecione **depurar depuração**  >   para continuar a execução e pausar novamente no aplicativo gerenciado.

1. Pressione **F5** ou selecione a seta verde para continuar a depuração do aplicativo.

Parabéns! Você concluiu o tutorial sobre depuração de modo misto.

## <a name="next-step"></a>Próxima etapa

Neste tutorial, você aprendeu como depurar código nativo de um aplicativo gerenciado, habilitando a depuração de modo misto. Para obter uma visão geral de outros recursos do depurador, confira:

> [!div class="nextstepaction"]
> [Introdução ao depurador](../debugger/debugger-feature-tour.md)
