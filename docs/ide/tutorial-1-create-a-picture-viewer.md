---
title: 'Tutorial 1: Criar um visualizador de imagens'
description: Saiba como criar um aplicativo que carrega uma imagem de um arquivo e a exibe em uma janela.
ms.custom: SEO-VS-2020
ms.date: 10/16/2019
ms.assetid: 3071d6df-2b2f-4e95-ab68-bef727323136
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7f66ce33d104a06e49db8b740b22abcb9c587c33
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296762"
---
# <a name="tutorial-1-create-a-picture-viewer"></a>Tutorial 1: Criar um visualizador de imagens

Neste tutorial, você cria um aplicativo que carrega uma imagem de um arquivo e a exibe em uma janela. Você aprende a usar a **Designer de formulários do Windows** para arrastar controles como botões e caixas de imagem para o formulário, definir suas propriedades e usar contêineres para redimensionar o formulário de forma suave. Você também pode começar a escrever código.

> [!NOTE]
> Este tutorial aborda tanto o C# quanto o Visual Basic, portanto, concentre-se nas informações específicas para a linguagem de programação que você está usando.

Este tutorial orienta você pelas seguintes tarefas:

* Criar um novo projeto.

* Testar (depurar) um aplicativo.

* Adicionar controles básicos como caixas de seleção e botões para um formulário.

* Posicionar controles em um formulário usando layouts.

* Adicionar as caixas de diálogo **Abrir Arquivo** e **Cor** a um formulário.

* Escreva código usando IntelliSense e trechos de código.

* Escrever métodos de manipulador de eventos.

Quando você terminar, seu aplicativo deverá ser semelhante à imagem a seguir:

![Aplicativo visualizador de imagens criado neste tutorial](../ide/media/express_pictureviewerdone.png)

## <a name="tutorial-links"></a>Links do tutorial

|Título|Descrição|
|-----------|-----------------|
|[Etapa 1: Crie um projeto de aplicativo do Windows Forms](../ide/step-1-create-a-windows-forms-application-project.md)|Comece criando um projeto de aplicativo Windows Forms.|
|[Etapa 2: executar o aplicativo visualizador de imagens](../ide/step-2-run-your-program.md)|Execute o projeto de aplicativo Windows Forms que você criou na etapa anterior.|
|[Etapa 3: Definir as propriedades do formulário](../ide/step-3-set-your-form-properties.md)|Altere a aparência do seu formulário usando a janela **Propriedades**.|
|[Etapa 4: Definir o layout do formulário com um controle TableLayoutPanel](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)|Adicione um controle `TableLayoutPanel` ao seu formulário.|
|[Etapa 5: Adicionar controles ao formulário](../ide/step-5-add-controls-to-your-form.md)|Adicione controles, como um controle `PictureBox` e um controle `CheckBox`, ao seu formulário. Adicionar botões ao seu formulário.|
|[Etapa 6: Nomear os controles de botão](../ide/step-6-name-your-button-controls.md)|Renomear os botões a algo mais significativo.|
|[Etapa 7: Adicionar componentes de diálogo ao formulário](../ide/step-7-add-dialog-components-to-your-form.md)|Adicionar um componente `OpenFileDialog` e um componente `ColorDialog` ao seu formulário.|
|[Etapa 8: escrever código para o manipulador de eventos do botão Mostrar uma imagem](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)|Escreva o código usando a ferramenta IntelliSense.|
|[Etapa 9: Examinar, comentar e testar o código](../ide/step-9-review-comment-and-test-your-code.md)|Revise e teste seu código. Adicionar comentários quando necessário.|
|[Etapa 10: Escrever código para botões adicionais e uma caixa de seleção](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md)|Escrever código para tornar outros botões e uma caixa de seleção trabalhar usando o IntelliSense.|
|[Etapa 11: Execute seu aplicativo e experimente outros recursos](../ide/step-11-run-your-program-and-try-other-features.md)|Execute seu aplicativo e defina a cor do plano de fundo. Tente outros recursos, como alterar cores, fontes, e bordas.|

Também há excelentes recursos de aprendizado de vídeo gratuitos disponíveis para você. Para saber mais sobre programação em C#, consulte [conceitos básicos do c#: desenvolvimento para iniciantes absolutos](https://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners). Para saber mais sobre programação no Visual Basic, veja [Visual Basic Fundamentals: Development for Absolute Beginners (Conceitos básicos do Visual Basic: desenvolvimento para iniciantes absolutos)](https://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners).

## <a name="next-steps"></a>Próximas etapas

Para iniciar o tutorial, comece com a **[etapa 1: criar um projeto de aplicativo Windows Forms](../ide/step-1-create-a-windows-forms-application-project.md)**.

## <a name="see-also"></a>Confira também

* [Mais tutoriais sobre C#](../get-started/csharp/index.yml)
* [Tutoriais de Visual Basic](../get-started/visual-basic/index.yml)
* [Tutoriais do C++](/cpp/get-started/tutorial-console-cpp)