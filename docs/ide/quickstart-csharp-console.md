---
title: 'Início Rápido: usar o Visual Studio para criar seu primeiro aplicativo de console em C#'
description: Saiba como criar passo a passo um aplicativo simples de console Olá, Mundo no Visual Studio em C#.
ms.custom: ''
ms.date: 09/21/2018
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: quickstart
ms.devlang: vb
author: TerryGLee
ms.author: tglee
manager: douge
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: ee40aadd3287018e52910ad6b4a4000db6bcce8a
ms.sourcegitcommit: 6672a1e9d135d7e5cca3cceea07c6fe5a0871475
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47443409"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-c-console-app"></a>Início Rápido: usar o Visual Studio para criar seu primeiro aplicativo de console em C#

Nesta introdução de 5 a 10 minutos ao IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará um aplicativo simples em C# para ser executado no console.

Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente.

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo em C#. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada!

1. Abra o Visual Studio 2017.

2. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

3. Na caixa de diálogo **Novo Projeto** no painel esquerdo, expanda **C#** e escolha **.NET Core**. No painel central, escolha **Aplicativo de Console (.NET Core)**. Em seguida, nomeie o projeto como *HelloWorld*.

   ![Modelo de projeto do aplicativo do console (.NET Core) na caixa de diálogo Novo projeto no IDE do Visual Studio](../ide/media/new-project-csharp-dotnetcore-helloworld-console-app.png)

     Se você não vir o modelo de projeto do **Aplicativo de Console (.NET Core)**, escolha o link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**.

   ![Escolha o link Abrir Instalador do Visual Studio na caixa de diálogo Novo Projeto](../ide/media/csharp-open-visual-studio-installer-hello-world.png)

     O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho de desenvolvimento multiplaforma do .NET Core no Instalador do Visual Studio](../ide/media/dot-net-core-xplat-dev-workload.png)

## <a name="create-the-application"></a>Criar o aplicativo

Depois que você seleciona o modelo em C# e dá um nome ao projeto, o Visual Studio cria um aplicativo simples “Olá, Mundo”. 

Para isso, ele chama o método <xref:System.Console.WriteLine%2A> para exibir a cadeia de caracteres literal "Olá, Mundo!" na janela do console.

   ![Exibir o código Olá, Mundo padrão do modelo](../ide/media/csharp-console-helloworld-template.png)

Se pressionar **F5**, você poderá executar o programa no modo de depuração. Entretanto, a janela do console fica visível somente por um momento antes de fechar.

Isso acontece porque o método `Main` é encerrado após a execução da única instrução e, portanto, o aplicativo é encerrado.

### <a name="add-some-code"></a>Adicionar código

Vamos adicionar alguns códigos para pausar o aplicativo de modo que a janela do console não seja fechada até você pressionar **Enter**.

1. Adicione o seguinte código imediatamente após a chamada ao método <xref:System.Console.WriteLine%2A>:

   ```csharp
   Console.ReadLine();
   ```

1. Verifique se tem esta aparência no editor de código:

   ![Adicione o código para pausar o aplicativo Olá, Mundo](../ide/media/csharp-console-helloworld-add-code.png)

## <a name="run-the-application"></a>Executar o aplicativo

1. Escolha o botão **HelloWorld** na barra de ferramentas para executar o aplicativo no modo de depuração. Ou pressione **F5**.

   ![Escolha o botão Olá, Mundo para executar o aplicativo da barra de ferramentas](../ide/media/csharp-console-hello-world-button.png)

1. Visualize o aplicativo na janela do console.

   ![Janela do console mostrando Olá, Mundo!](../ide/media/csharp-console-hello-world.png)

### <a name="close-the-application"></a>Feche o aplicativo

1. Pressione **Enter** para fechar a janela do console.

1. Feche o painel **Saída** no Visual Studio.

   ![Fechar o painel Saída no Visual Studio](../ide/media/csharp-hello-world-close-output-pane.png)

1. Feche o Visual Studio.

## <a name="next-steps"></a>Próximas etapas

Parabéns por concluir este Guia de Início Rápido! Esperamos que você tenha aprendido um pouco sobre C# e o IDE do Visual Studio. Para saber mais, continue com os tutoriais a seguir.

> [!div class="nextstepaction"]
> [Introdução ao aplicativo de console em C# no Visual Studio](tutorial-csharp-console.md)
