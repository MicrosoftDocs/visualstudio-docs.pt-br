---
title: 'Tutorial 1: Criar um visualizador de imagens'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: 3071d6df-2b2f-4e95-ab68-bef727323136
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 966634ee9a71854334bdd5342326c1663b9ad16c
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672152"
---
# <a name="tutorial-1-create-a-picture-viewer"></a>Tutorial 1: Criar um visualizador de imagens

Neste tutorial, você cria um programa que carrega uma imagem de um arquivo e a exibe em uma janela. Você aprende a usar o **Designer de Formulários do Windows** para arrastar controles como botões e caixas de imagem no formulário, definir as respectivas propriedades e usar contêineres para redimensionar suavemente o formulário. Você também pode começar a escrever código. Você aprenderá como:

-   Crie um novo projeto.

-   Testar (depurar) um aplicativo.

-   Adicionar controles básicos como caixas de seleção e botões para um formulário.

-   Posicionar controles em um formulário usando layouts.

-   Adicionar as caixas de diálogo **Abrir Arquivo** e **Cor** a um formulário.

-   Escrever código usando o IntelliSense e snippets de código.

-   Escrever métodos de manipulador de eventos.

Quando você terminar, seu programa será como a imagem a seguir:

![Mostre que você cria neste tutorial](../ide/media/express_pictureviewerdone.png)

## <a name="tutorial-links"></a>Links do tutorial

Para baixar uma versão concluída do exemplo, veja [Exemplo de tutorial completo do Visualizador de Imagens](https://code.msdn.microsoft.com/Complete-Picture-Viewer-7d91d3a8).

![link para o vídeo](../data-tools/media/playvideo.gif)Para ver uma versão em vídeo deste tópico, confira [How do I: Create a picture viewer in Visual Basic?](http://go.microsoft.com/fwlink/?LinkId=205207) (Como fazer para criar um visualizador de imagens no Visual Basic?) ou [How do I: Create a picture viewer in C#?](http://go.microsoft.com/fwlink/?LinkId=205198) (Como fazer para criar um visualizador de imagens em C#?).

> [!NOTE]
> Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio. O Visual C# e o Visual Basic são abordados neste tutorial, portanto concentre-se nas informações específicas da linguagem de programação que você está usando.
>
> Para ver o código para Visual Basic, escolha a guia **VB** na parte superior dos blocos de código e, para ver o código para Visual C#, escolha a guia **C#**. Se estiver interessado em aprender sobre o Visual C++, veja [Introdução](../ide/getting-started-with-cpp-in-visual-studio.md) e [Tutorial da linguagem C++](http://www.cplusplus.com/doc/tutorial/).
>
> Se você estiver interessado em aprender a escrever aplicativos UWP do Visual C# ou Visual Basic, consulte [Criar aplicativos UWP](https://developer.microsoft.com/windows/apps).

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Etapa 1: Criar um projeto de aplicativo do Windows Forms](../ide/step-1-create-a-windows-forms-application-project.md)|Comece criando um projeto de aplicativo do Windows Forms.|
|[Etapa 2: Executar o programa](../ide/step-2-run-your-program.md)|Execute o programa de aplicativo do Windows Forms que você criou na etapa anterior.|
|[Etapa 3: Definir as propriedades do formulário](../ide/step-3-set-your-form-properties.md)|Altere a aparência do seu formulário usando a janela **Propriedades**.|
|[Etapa 4: Definir o layout do formulário com um controle TableLayoutPanel](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)|Adicione um controle `TableLayoutPanel` ao seu formulário.|
|[Etapa 5: Adicionar controles ao formulário](../ide/step-5-add-controls-to-your-form.md)|Adicione controles, como um controle `PictureBox` e um controle `CheckBox`, ao seu formulário. Adicionar botões ao seu formulário.|
|[Etapa 6: Nomear os controles de botão](../ide/step-6-name-your-button-controls.md)|Renomear os botões a algo mais significativo.|
|[Etapa 7: Adicionar componentes de diálogo ao formulário](../ide/step-7-add-dialog-components-to-your-form.md)|Adicionar um componente `OpenFileDialog` e um componente `ColorDialog` ao seu formulário.|
|[Etapa 8: Escrever código para o manipulador de eventos do botão Mostrar uma Imagem](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)|Escrever código usando a ferramenta do IntelliSense.|
|[Etapa 9: Revisar, comentar e testar o código](../ide/step-9-review-comment-and-test-your-code.md)|Revise e teste seu código. Adicionar comentários quando necessário.|
|[Etapa 10: Escrever código para botões adicionais e uma caixa de seleção](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md)|Escrever código para tornar outros botões e uma caixa de seleção trabalhar usando o IntelliSense.|
|[Etapa 11: Executar o programa e experimentar outros recursos](../ide/step-11-run-your-program-and-try-other-features.md)|Execute o programa e defina a cor do plano de fundo. Tente outros recursos, como alterar cores, fontes, e bordas.|
