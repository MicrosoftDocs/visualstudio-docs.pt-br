---
title: 'Etapa 7: Adicionar componentes de diálogo ao formulário'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: ea98c55e-6213-4893-ba7b-f19d7f119527
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ed228c007d41d3c7a0815cb97ea9cd890b3a0c98
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34748706"
---
# <a name="step-7-add-dialog-components-to-your-form"></a>Etapa 7: Adicionar componentes de diálogo ao formulário
Para habilitar seu programa a abrir arquivos de imagem e escolher uma cor da tela de fundo, nesta etapa, você adiciona um componente <xref:System.Windows.Forms.OpenFileDialog> e um componente <xref:System.Windows.Forms.ColorDialog> ao seu formulário.

 Um componente é como um controle de certas maneiras. Use a **Caixa de Ferramentas** para adicionar um componente ao seu formulário e ajuste suas propriedades usando a janela **Propriedades**. Mas, diferentemente de um controle, adicionar um componente ao seu formulário não adiciona um item visível que o usuário possa ver no formulário. Em vez disso, fornece determinados comportamentos que você pode disparar com código. É um componente que abre uma caixa de diálogo **Abrir Arquivo**.

 ![link para vídeo](../data-tools/media/playvideo.gif)Para ver uma versão em vídeo deste tópico, confira [Tutorial 1: Criar um visualizador de imagens no Visual Basic – Vídeo 3](http://go.microsoft.com/fwlink/?LinkId=205213) ou [Tutorial 1: Criar um visualizador de imagens em C# – Vídeo 3](http://go.microsoft.com/fwlink/?LinkId=205202). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.

## <a name="to-add-dialog-components-to-your-form"></a>Para adicionar componentes da caixa de diálogo ao seu formulário

1.  Escolha o **Designer de Formulários do Windows** (**Form1.cs [Design]** ou **Form1.vb [Design]**) e abra o grupo **Caixas de Diálogo** na **Caixa de Ferramentas**.

    > [!NOTE]
    >  O grupo **Caixas de Diálogo** na **Caixa de Ferramentas** tem componentes que abrem muitas caixas de diálogo úteis para você, que podem ser usadas para abrir e salvar arquivos, navegar por pastas e escolher fontes e cores. Você usa dois componentes de caixa de diálogo no projeto: OpenFileDialog e ColorDialog.

2.  Para adicionar um componente chamado **openFileDialog1** ao formulário, clique duas vezes em **OpenFileDialog**. Para adicionar um componente chamado **colorDialog1** ao formulário, clique duas vezes em **ColorDialog** na **Caixa de Ferramentas**. (Use a referência da próxima etapa do tutorial.) Você deve ver uma área na parte inferior do **Designer de Formulários do Windows** (abaixo do formulário **visualizador de imagens**) que tem um ícone para cada um dos dois componentes da caixa de diálogo que você adicionou, conforme mostrado na seguinte imagem.

     ![Componentes da caixa de diálogo](../ide/media/express_dialogsadded.png)
Componentes de **caixa de diálogo**

3.  Escolha o ícone **openFileDialog1** na área da parte inferior do **Designer de Formulários do Windows**. Defina as duas propriedades:

    -   Defina a propriedade **Filtro** como o seguinte (você pode copiar e colar):

        ```
        JPEG Files (*.jpg)|*.jpg|PNG Files (*.png)|*.png|BMP Files (*.bmp)|*.bmp|All files (*.*)|*.*
        ```

    -   Defina a propriedade **Título** como o seguinte: **Selecionar um arquivo de imagem**

         As configurações da propriedade de **Filtro** especificam os tipos de arquivo que serão exibidos na caixa de diálogo do arquivo **Selecionar uma imagem**.

    > [!NOTE]
    >  Para ver um exemplo da caixa de diálogo **Abrir Arquivo** em um aplicativo diferente, abra o **Bloco de Notas** ou o **Paint** e, na barra de menus, escolha **Arquivo** > **Abrir**. Observe como há uma lista suspensa **Arquivos de tipo** na parte inferior. Você acabou de usar a propriedade de **Filtro** no componente **OpenFileDialog** para configurar isso. Além disso, observe como as propriedades de **Título** e de **Filtro** estão em negrito na janela **Propriedades**. O IDE faz isso para mostrar a você todas as propriedades que tiveram seus valores padrão alterados.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para ir para a próxima etapa do tutorial, veja [Etapa 8: Escrever código para o manipulador de eventos do botão Mostrar uma Imagem](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md).

-   Para retornar à etapa anterior do tutorial, veja [Etapa 6: Nomear os controles de botão](../ide/step-6-name-your-button-controls.md).
