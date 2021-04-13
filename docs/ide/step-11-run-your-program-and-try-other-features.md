---
title: Execute o aplicativo visualizador de imagens e tente outros recursos
description: Execute o aplicativo visualizador de imagens e tente outros recursos no tutorial criar um visualizador de imagens.
ms.date: 09/11/2019
ms.custom: SEO-VS-2020
ms.assetid: 656614d0-4fe7-4a67-8edc-c10919377d09
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 91488b72559b2e6deff23a5cae389cd9b4001443
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296502"
---
# <a name="step-11-run-your-picture-viewer-app-and-try-other-features"></a>Etapa 11: executar o aplicativo do Visualizador de imagens e experimentar outros recursos

Seu aplicativo visualizador de imagens foi concluído e está pronto para ser executado. Você pode executar seu aplicativo e definir a cor do plano de fundo do <xref:System.Windows.Forms.PictureBox> . Para saber mais, tente melhorar o aplicativo alterando a cor do formulário, personalizando os botões e a caixa de seleção e alterando as propriedades do formulário.

## <a name="how-to-run-your-app-and-set-the-background-color"></a>Como executar seu aplicativo e definir a cor do plano de fundo

1. Selecione **F5** ou, na barra de menus, selecione **Depurar** > **Iniciar Depuração**.

1. Antes de abrir uma imagem, clique no botão **Definir a cor da tela de fundo**. A caixa de diálogo **Cor** é aberta.

     ![Caixa de diálogo Cor](../ide/media/express_colordialog.png)<br/>
***Cor** _ _dialog caixa *

1. Escolha uma cor para definir a cor do plano de fundo de PictureBox. Examine com mais detalhes o `backgroundButton_Click()` método (ou, `BackgroundButton_Click()` ) para entender como ele funciona.

    > [!NOTE]
    > Você pode carregar uma imagem da Internet colando sua URL na caixa de diálogo **Abrir Arquivo**. Tente localizar uma imagem com um plano de fundo transparente, para que sua cor do plano de fundo seja exibida.

1. Escolha o botão **Limpar a imagem** para certificar-se de que ela desaparece. Em seguida, saia do aplicativo escolhendo o botão **fechar** .

## <a name="try-other-features"></a>Experimentar outros recursos

* Altere a cor do formulário e os botões usando a propriedade **BackColor**.

* Personalize seus botões e sua caixa de seleção usando as propriedades **Font** e **ForeColor**.

* Altere as propriedades **FormBorderStyle** e **ControlBox** do formulário.

* Use as propriedades **AcceptButton** e **CancelButton** do formulário de modo que os botões sejam escolhidos automaticamente quando o usuário escolher as teclas **Enter** ou **Esc**. Faça com que o aplicativo Abra a caixa de diálogo **Abrir arquivo** quando o usuário escolher **Enter** e fechar a caixa quando o usuário escolher **ESC**.

## <a name="next-steps"></a>Próximas etapas

Para saber mais, continue com o tutorial a seguir:

> [!div class="nextstepaction"]
> [Tutorial 2: criar um teste de matemática cronometrado](../ide/tutorial-2-create-a-timed-math-quiz.md)

Para retornar à etapa anterior do tutorial, veja [Etapa 10: Escrever código para botões adicionais e uma caixa de seleção](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md).

## <a name="see-also"></a>Confira também

* [Mais tutoriais sobre C#](../get-started/csharp/index.yml)
* [Mais tutoriais Visual Basic](../get-started/visual-basic/index.yml)
* [Tutorial do C++](/cpp/get-started/tutorial-console-cpp)