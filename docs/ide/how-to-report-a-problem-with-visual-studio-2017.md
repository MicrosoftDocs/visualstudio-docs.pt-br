---
title: Como relatar um problema com o Visual Studio 2017
description: Saiba como relatar um problema com o Visual Studio 2017 para a Microsoft para que possamos diagnosticá-lo e corrigi-lo.
ms.custom: ''
ms.date: 03/11/2018
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: bee01179-cde5-4419-9095-190ee0ba5902
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 539e6c95dd16e091b7f0ff2cf792a9f8b2fa416b
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51348326"
---
# <a name="how-to-report-a-problem-with-visual-studio-2017"></a>Como relatar um problema com o Visual Studio 2017

Se tiver algum problema com o Visual Studio, gostaríamos de saber o que é. Veja a seguir como relatar o problema para a [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/) para que possamos diagnosticá-lo e corrigi-lo.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Como relatar um problema no Visual Studio para Mac](/visualstudio/mac/report-a-problem).

## <a name="report-a-problem-by-using-visual-studio"></a>Relatar um problema usando o Visual Studio

Para relatar um problema para o Visual Studio, você deve iniciar o relatório do Visual Studio ou do Instalador do Visual Studio. Você não pode fazer isso diretamente por meio do site da [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/). Fazer o relatório por meio do Visual Studio permite que as informações de diagnóstico sejam incluídas automaticamente no relatório.

![Relatar um pop-up do problema na Comunidade de Desenvolvedores do Visual Studio](media/report-an-issue.png)

1. No Visual Studio, selecione **Ajuda** > **Enviar Comentários** > **Relatar um Problema**.

   > [!TIP]
   > Se não for possível concluir a instalação do Visual Studio ou acessar a ferramenta de comentários dentro do Visual Studio, você poderá relatar um problema usando o **Instalador do Visual Studio**. Para fazer isso, escolha o ícone de comentários no canto superior direito do **Instalador do Visual Studio**.

1. Se você não estiver conectado, selecione **Entrar**; essa opção está do lado direito da ferramenta, conforme mostrado na captura de tela a seguir. Siga as instruções na tela para se conectar.

   ![Entrar para relatar um problema](../ide/media/sign-in-new-ux.png)

   Quando você entra, pode relatar um problema que está enfrentando. Você também pode votar ou comentar em qualquer outro problema postado.

1. Depois de entrar, você poderá ver seus **Problemas** e **Atividade** na tela **Itens que Acompanho**

    ![Itens que Acompanho](../ide/media/items-i-follow.png)

1. O Visual Studio fornece uma interface para pesquisar o problema e ver se outras pessoas já o relataram. Se alguém tiver relatado, "vote como positivo" para nos informar.
   > [!NOTE]
   > Para pesquisar, insira o texto desejado na caixa de pesquisa e clique em Enter ou pressione o ícone Pesquisar.

   ![Pesquisar e votar em problemas semelhantes](../ide/media/search-and-vote.png)

1. Se você não encontrar o problema enfrentado, escolha **Relatar novo problema** na parte inferior da tela.

   > [!NOTE]
   > O botão **Relatar novo problema** aparece apenas na interface do Visual Studio para a Comunidade de Desenvolvedores. Você não pode relatar um problema diretamente no site da [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/).

1. Crie um título descritivo para o problema que nos ajude a encaminhá-lo à equipe correta do Visual Studio.

1. Forneça todos os detalhes adicionais e, se possível, forneça as etapas para reproduzir o problema.

   ![Relatar um problema novo](../ide/media/report-new-problem.png)

1. Selecione **Avançar** para passar para a guia **Anexos**. Aqui, você pode capturar a tela atual para enviá-la à Microsoft. Para anexar capturas de tela adicionais ou outros arquivos, escolha **Anexar Arquivos Adicionais**.

   ![Anexe uma captura de tela a um relatório de problema do Visual Studio](media/report-a-problem-screenshot.png)

1. Se você não quiser anexar uma captura de tela ou [gravar uma reprodução](#record-a-repro), selecione **Avançar** para passar para a guia **Resumo**.

1. Selecione **Enviar** para enviar seu relatório, juntamente com as imagens e os arquivos de despejo ou de rastreamento. (Se o botão **Enviar** estiver esmaecido, verifique se você forneceu um título e uma descrição para o relatório.)

   Para obter informações sobre quais dados são coletados, consulte [Data we collect](developer-community-privacy.md#data-we-collect) (Dados que coletamos).

## <a name="record-a-repro"></a>Gravar uma reprodução

Os arquivos de despejo de heap e rastreamento são muito úteis para nos ajudar a diagnosticar problemas. Apreciamos quando você usa a ferramenta **Relatar um Problema** para registrar as etapas de reprodução e enviar os dados para a Microsoft. Veja como fazer isso:

1. Depois de inserir um título e uma descrição para o problema, selecione **Avançar** para passar para a guia **Anexos**.

1. Selecione a guia **Gravar**.

1. Em **Gravar suas ações**, selecione a instância atual do Visual Studio se você puder reproduzir o problema nela. Se não puder, por exemplo, se o Visual Studio estiver travado, selecione **\<Criar uma nova instância>** para gravar as ações em uma nova instância do Visual Studio.

1. Selecione **Iniciar Gravação**. Conceda permissão para executar a ferramenta.

   ![Escolha “Iniciar Gravação” para fornecer um arquivo de despejo de heap e rastreamento em um relatório de problema do Visual Studio](../ide/media/record-dialog-box.png)

1. Quando a ferramenta **Gravador de Passos** aparecer, execute as etapas que reproduzem o problema.

1. Ao terminar, escolha o botão **Parar Gravação**.

1. Aguarde alguns minutos para o Visual Studio coletar e compactar as informações gravadas.

   Para obter informações sobre quais dados são coletados, consulte [Data we collect](developer-community-privacy.md#data-we-collect) (Dados que coletamos).

## <a name="when-further-information-is-needed-need-more-info"></a>Quando mais informações são necessárias (Precisa de Mais Informações)

Começando no Visual Studio 2017 versão 15.5, há um novo fluxo de trabalho para ajudar os usuários a fornecerem informações adicionais sobre relatórios de problemas.

1. Quando um engenheiro da Microsoft define o problema da [Comunidade de Desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) com o estado **Precisa de Mais Informações**, todos os usuários que postaram, votaram, seguiram ou comentaram no problema recebem uma notificação na ferramenta **Relatar um Problema** no Visual Studio.

   ![Notificação de Precisa de Mais Informações no Visual Studio](../ide/media/nmi-notification.png)

1. Clique no link **Exibir Problemas** para filtrar e classificar a exibição dos problemas que precisam de atenção. Esses problemas também têm um indicador ao lado deles para diferenciá-los na pesquisa geral.

1. Clique em um problema para ver a exibição dos detalhes do problema.

   ![Notificação de Precisa de Mais Informações](../ide/media/nmi-details-view.png)

1. Para exibir a solicitação **Precisa de Mais Informações**, clique no link **Exibir a solicitação e responder** na exibição de detalhes do problema. Uma caixa de diálogo mostra a solicitação.

   ![Notificação de Precisa de Mais Informações](../ide/media/nmi-request.png)

1. Você pode fornecer mais informações adicionando comentários, anexos ou gravando as etapas. Essa experiência é semelhante a relatar um novo problema ou fornecer informações adicionais ao votar em um problema.

1. O engenheiro da Microsoft fazendo a solicitação recebe uma notificação sobre as informações extras fornecidas. Se ele tiver informações suficientes para investigar, o estado do problema mudará. Caso contrário, o engenheiro solicita ainda mais informações.

   > [!NOTE]
   > * Quando você responde, a notificação desaparece. No seu lugar, você vê uma faixa que agradece e torna fácil uma maneira de fornecer ainda mais informações.
   > * Depois que o problema muda o estado, a notificação desaparece para todas as pessoas que estão acompanhando o problema.
   > * Mais de uma pessoa pode responder na mesma solicitação de **Precisa de Mais Informações**.
   > * Não existe um fluxo de trabalho de **Precisa de Mais Informações** na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/) quando você a acessa diretamente por meio de um navegador da Web, mas também é possível fornecer comentários e anexos lá.

## <a name="search-for-solutions-or-provide-feedback"></a>Pesquisar soluções ou fornecer comentários

Se você não quiser ou não puder usar o Visual Studio para relatar um problema, há a possibilidade de que o problema já tenha sido relatado e uma solução tenha sido postada na página da [Comunidade de Desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/).

Se você não tem um problema a ser relatado, mas deseja sugerir um recurso, há um local para fazer isso também. Para saber mais, confira a página [Sugerir um recurso](https://developercommunity.visualstudio.com/content/idea/post.html?space=8).

## <a name="see-also"></a>Consulte também

* [Fale conosco](../ide/talk-to-us.md)
* [Relatar um problema com o Visual Studio para Mac](/visualstudio/mac/report-a-problem)
* [Relatar um problema com C++](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Comunidade de Desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/)
* [Privacidade de dados da Comunidade de Desenvolvedores](developer-community-privacy.md)