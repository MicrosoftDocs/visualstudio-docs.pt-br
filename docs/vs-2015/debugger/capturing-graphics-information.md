---
title: Capturando informações de gráficos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.graphics.frame
- vs.graphics.capturewindow
- VS.ToolsOptionsPages.Graphics_Diagnostics.Capture
ms.assetid: 187ce86e-e340-4f6c-8937-8e8f1027a17f
caps.latest.revision: 44
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a099254acd572b3fcbb437f8933c81f3d6bd45b9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51799828"
---
# <a name="capturing-graphics-information"></a>Capturando informações de gráficos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Capture informações gráficas de seu aplicativo Direct3D para que você possa usar o analisador de gráficos do Visual Studio para diagnosticar problemas de desempenho e problemas de renderização.  
  
## <a name="capturing-graphics-information"></a>Capturando informações de gráficos  
 A captura de informações de gráficos é um processo de duas etapas. Primeiramente, você executa o aplicativo em Diagnóstico de Gráficos e depois especifica um ou mais quadros dos quais serão capturadas informações detalhadas.  
  
#### <a name="to-run-your-app-under-graphics-diagnostics"></a>Para executar o aplicativo em Diagnóstico de Gráficos  
  
- Na barra de menus, escolha **Debug**, **gráficos**, **iniciar diagnóstico**. (Teclado: pressione Alt+F5)  
  
- Sobre o **gráficos** barra de ferramentas, escolha o **iniciar diagnóstico** botão.  
  
  Enquanto um aplicativo estiver sendo executado no Diagnóstico de Gráficos, determinados tipos de informação de gráfico são capturados o tempo todo; isso inclui a configuração do dispositivo, a criação da cadeia de troca, a criação de recursos e objetos gráficos, bem como outros eventos importantes que afetam mais de um quadro. Ao mesmo tempo, você pode capturar informações detalhadas sobre quadros específicos; isso inclui chamadas de desenho e distribuições de sombreadores de cálculo, juntamente com os recursos e objetos Direct3D que oferecem suporte a eles.  
  
#### <a name="to-capture-a-frame"></a>Para capturar um quadro  
  
- No Visual Studio, sobre o **gráficos** barra de ferramentas, escolha o **capturar quadro** botão![ícone do botão de captura de elementos gráficos](../debugger/media/debuggingdirectxgraphics.png "DebuggingDirectXGraphics").  
  
- No teclado, pressione Print Screen.  
  
  > [!NOTE]
  >  Enquanto um aplicativo é executado sob **diagnóstico de gráficos**, a tecla Print Screen só pode ser usada para capturar um quadro de informações de gráficos; ela não executa sua função normal. Isso permanece em vigor até que você pare de capturar informações de gráficos, geralmente interrompendo a depuração ou saindo do aplicativo normalmente, mesmo que outro aplicativo esteja no foco.  
  
- Na interface de captura do Visual Studio, escolha o **capturar quadro** botão localizado acima do **sessão de diagnóstico** linha do tempo, ou escolha o grande **capturar quadro** botão localizado abaixo de **quadros por segundo** pista e à direita de qualquer quadro capturado anteriormente. Ambos os botões estão realçados na imagem abaixo.  
  
   ![Capture quadros usando a ferramenta uso de GPU. ](../debugger/media/pix-gpu-usage-tool-capture-frame.png "pix_gpu_usage_tool_capture_frame")  
  
   Quando você estiver pronto para examinar os quadros for capturada, inicie o **analisador de gráficos do Visual Studio** seguindo o **quadro...** Vincular acima as miniaturas de imagem, ou clicando duas vezes na miniatura.  
  
  Somente quadros inteiros podem ser capturados, de modo que quando você inicia uma captura, as informações de gráfico do próximo quadro são realmente gravadas. A gravação começa logo depois que o quadro no qual você iniciou a captura é apresentado e termina quando o quadro capturado é apresentado. É possível capturar quantos quadros você desejar enquanto o aplicativo estiver em execução no Diagnóstico de Gráficos. Se você não capturar nenhum quadro, o log de elementos gráficos será descartado.  
  
  Durante a captura de quadros, o Visual Studio exibe a janela de sessão (. diagsession) de diagnóstico. Se você fecha esta janela, pare a depuração ou fecha o aplicativo, você não pode capturar mais quadros para que o log. Para capturar mais informações de gráficos, você precisa executar o aplicativo em Diagnóstico de gráficos novamente para iniciar uma nova sessão de diagnóstico.  
  
### <a name="graphics-diagnostics-capture-options"></a>Opções de captura de diagnóstico de gráficos  
 Você pode configurar a captura para coletar as pilhas de chamada para todos os eventos de gráficos ou um subconjunto limitado, desabilitar a captura HUD e ativar ou desativar o modo de compatibilidade de captura.  
  
##### <a name="to-configure-graphics-diagnostics-capture-options"></a>Para configurar as opções de captura do diagnóstico de gráficos  
  
1.  Na barra de menus, escolha Ferramentas, Opções. A caixa de diálogo Opções é exibida.  
  
2.  Na lista da categoria opções à esquerda, escolha o diagnóstico de gráficos e configurar as opções de diagnóstico de gráficos que você deseja.  
  
     **Coletar pilhas de chamadas durante a captura (torna a captura mais lenta)**  
     Marque esta caixa para coletar as pilhas de chamadas. Por padrão, as pilhas de chamadas não são coletadas. Para capturar as pilhas de chamadas, certifique-se de que o **coletar pilha de chamada durante a captura (torna a captura mais lenta** caixa de seleção é definida como habilitar a coleta e, em seguida, defina os o **para desenho, expedição, presente e desempenho marcadores**opção (padrão) para coletar somente as mais importantes pilhas de chamadas, ou o **para tudo** opção para coletar todas as pilhas de chamadas. Para parar de coletar as pilhas de chamadas mais tarde, desmarque a **coletar pilha de chamada durante a captura (torna a captura mais lenta** caixa de seleção.  
  
     **Desabilitar o jogo HUD durante a captura**  
     Marque essa caixa para desabilitar a sobreposição HUD que um aplicativo executando em diagnóstico de gráficos geralmente exibe. Desmarque essa opção para exibir a sobreposição HUD.  
  
     **Capturar em modo de compatibilidade**  
     Marque esta caixa para capturar informações de gráficos no modo de compatibilidade. A captura no modo de compatibilidade é o padrão. No modo de compatibilidade, o Direct3D não irá relatar que a GPU é compatível com todos os recursos adicionais além daqueles definidos no nível de recurso base. Isso evita que o aplicativo sendo capturado use extensões específicas de hardware da GPU em que é capturado e garante que o log de elementos gráficos possa ser executado usando qualquer GPU compatível com o mesmo nível de recurso ou superior. Desmarque essa caixa para desabilitar o modo de compatibilidade. Os logs capturados com o modo de compatibilidade desabilitado não conseguirão reproduzir em nenhuma GPU que não seja compatível com os mesmos recursos adicionais que foram usados pelo aplicativo durante a captura.  
  
     **Parar captura se forem encontrados erros de camadas SDK**  
     Marque esta caixa para interromper a captura imediatamente se forem encontrados erros.  
  
## <a name="capturing-graphics-information-remotely"></a>Capturando informações de gráficos remotamente  
 As informações de gráficos podem ser capturadas de um aplicativo que está em execução no computador local, de um dispositivo ou computador remoto. A captura remota tem suporte em computadores com [!INCLUDE[winblue_client_2](../includes/winblue-client-2-md.md)] e dispositivos com [!INCLUDE[winblue_winrt_2](../includes/winblue-winrt-2-md.md)]. Para capturar informações de gráficos de um aplicativo que está em execução remotamente, configure seu projeto para depuração remota e execute o aplicativo em Diagnóstico de Gráficos, como descrito anteriormente. O aplicativo é executado no computador remoto e as informações de gráficos capturadas são gravadas no computador de desenvolvimento.  
  
 Como você configura o projeto para depuração remota depende do tipo de aplicativo que está sendo desenvolvido e da linguagem de programação que está sendo usada. Para obter informações sobre como configurar a depuração remota para um aplicativo da Windows Store, consulte [aplicativos de execução Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md). Para obter informações sobre como configurar a depuração remota para um aplicativo de desktop do Windows, consulte [Set Up Remote Debugging para um projeto do Visual Studio](http://msdn.microsoft.com/library/ec332dc4-400a-498b-a0e6-c8dcf10fef8a).  
  
 Posteriormente, você pode usar um dispositivo ou computador remoto para reproduzir informações de gráficos, independentemente de onde as informações foram capturadas. Para obter mais informações, consulte [como: alterar o computador de reprodução de diagnóstico de gráficos](../debugger/how-to-change-the-graphics-diagnostics-playback-machine.md).  
  
## <a name="capturing-graphics-information-from-the-command-line"></a>Captura de informações de elementos gráficos da linha de comando  
 Informações de gráficos poderão ser capturadas em um aplicativo usando uma ferramenta de linha de comando. Essa ferramenta, DXCap.exe, pode capturar e reproduzir rapidamente informações de gráficos sem usar o Visual Studio ou a captura programática. Em específico, você pode usar o DXCap.exe para automação ou em um ambiente de teste. Para obter mais informações sobre DXCap.exe, consulte [a ferramenta de captura de linha de comando](../debugger/command-line-capture-tool.md)  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: capturando informações de gráficos](../debugger/walkthrough-capturing-graphics-information.md)



