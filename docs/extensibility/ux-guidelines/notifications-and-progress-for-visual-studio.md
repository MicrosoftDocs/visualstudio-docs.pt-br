---
title: Notificações e progresso para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: aee6e5656142d0597ff6101da5e2e5f690f8fcc5
ms.sourcegitcommit: b6dfa1bdf4c23c2e341754454bbd4758db2218e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48863940"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Notificações e progresso para o Visual Studio
##  <a name="BKMK_NotificationSystems"></a> Sistemas de notificação  
  
### <a name="overview"></a>Visão geral  
 Há várias maneiras para informar ao usuário que está acontecendo no Visual Studio sobre suas tarefas de desenvolvimento de software.  
  
 Ao implementar qualquer tipo de notificação:  
  
-   **Mantenha o número de notificações para o mínimo** número efetivo. Mensagens de notificação devem ser aplicada para a maioria dos usuários do Visual Studio ou para usuários de uma área de recurso/recurso específico. O uso excessivo de notificações pode sidetrack o usuário ou ser reduzido percebida facilidade de uso do sistema.  
  
-   **Verifique se você está apresentando mensagens claras e acionáveis** que o usuário pode usar para invocar o contexto apropriado para fazer escolhas mais complexas e executar uma ação adicional.  
  
-   **Apresente mensagens síncronas e assíncronas adequadamente.** Notificações síncronas indicarem que algo precisa de atenção imediata, como quando um serviço web falha ou um código de exceção é lançada. O usuário deve ser informado dessas situações imediatamente de uma maneira que requer sua entrada, como em uma caixa de diálogo modal. Notificações assíncronas são aqueles que o usuário deve saber, mas não ser necessário para agir imediatamente, como quando uma operação de compilação for concluída ou quando uma implantação de site da web for concluída. Essas mensagens devem ser mais ambiente e não interromperá o fluxo de tarefas do usuário.  
  
-   **Use as caixas de diálogo modais somente quando necessário para impedir que o usuário executar uma ação adicional** antes confirmando a mensagem ou tomar uma decisão apresentada na caixa de diálogo.  
  
-   **Remova notificações de ambientes quando eles não são mais válidos.** Não exigem que o usuário ignorar uma notificação se eles já executou a ação para resolver o problema que eles foram notificados sobre.  
  
-   **Lembre-se de que as notificações podem levar a correlações falsas.** Os usuários podem acreditar que um ou mais de suas ações disparou uma notificação quando na verdade não havia nenhum relacionamento causal com. Ser clara na mensagem de notificação sobre o contexto, o gatilho e a origem da notificação.  
  
### <a name="choosing-the-right-method"></a>Escolha o método certo  
 Use esta tabela para ajudá-lo a escolher o método certo para notificar o usuário de sua mensagem.  
  
|Método|Use|Não use|  
|------------|---------|----------------|  
|[Caixas de diálogo de mensagem de erro modal](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|Use quando uma resposta do usuário é necessária antes de continuar.|Não use quando não é necessário para impedir que o usuário e seu fluxo de interrupção. Evite usar caixas de diálogo modais se for possível mostrar a mensagem de outra forma menos intrusiva.|  
|[Barra de status do IDE](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|Use quando houver ambientes informações textuais sobre o status de um processo.|Não use sozinho. Melhor usada em conjunto com outro mecanismo de comentários.|  
|[Barra de informações inserida](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|Em uma janela de documento ou janela de ferramentas, use para notificar de progresso, estado de erro, resultados e/ou informações acionáveis.|Não use se as informações não são relevantes para o local em que a barra de informações é colocada.<br /><br /> Não use fora de uma janela de ferramenta do documento.|  
|[Alterações de cursor do mouse](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|Pode ser usado para notificar um processo está acontecendo. Também é usado para notificar que há uma alteração de estado do mouse, como quando arrastar/soltar está em andamento ou que o cursor do mouse em um determinado modo, como o modo de desenho.|Não use para alterações de progresso de curto ou se fluttering do cursor é provável (por exemplo, quando vinculados a partes de um processo em execução mais longo, em vez de todo o processo).|  
|[Indicadores de progresso](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|Usar quando for necessário para relatar o progresso (determinado ou indeterminado). Há uma variedade de tipos de indicador de progresso e de uso específicos para cada um. Ver [indicadores de progresso](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators).||  
|[Janela de notificações do Studio Visual](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|A janela de notificações não é publicamente extensível. No entanto, ele é usado para comunicar-se um intervalo de mensagens sobre o Visual Studio, incluindo os problemas críticos com sua licença e informativas notificações de atualizações para o Visual Studio ou aos pacotes.|Não use para outros tipos de notificações.|  
|[Lista de erros](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|Quando o problema está diretamente relacionado a solução aberta no momento do usuário, há um problema (erro/aviso/informação), eles precisam agir no código.<br /><br /> Isso inclui, por exemplo:<br /><br /> -Mensagens de compilador (info/aviso/erro)<br /><br /> -Mensagens do analisador/diagnóstico código sobre o código<br /><br /> -Mensagens de build<br /><br /> Pode ser apropriado para problemas relacionados aos arquivos de projeto ou solução, mas considere uma indicação do Gerenciador de soluções primeiro.|Não use para itens que não têm qualquer relação com o código do usuário solução aberta.|  
|Notificações do Editor: lâmpada|Use quando tiver uma correção disponível para solucionar um problema que existe no arquivo aberto.<br /><br /> Observe que a lâmpada também deve ser usado para hospedar as ações rápidas que são executados com o código do usuário sob demanda, como refatorações, mas nesse caso, não será exibido "style de notificação".|Não use para itens que não têm qualquer relação com o arquivo aberto.|  
|Notificações do Editor: rabiscos|Use para alertar o usuário para um problema com um intervalo específico de seu código aberto (por exemplo, um rabisco vermelho para erros).|Não use para itens que não estão relacionados a uma extensão específica do seu código aberto.|  
|[Barras de status inserido](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|Use para fornecer status relacionados ao conteúdo ou processo dentro do contexto de uma janela de ferramenta específica, documento ou janela de diálogo.|Não use para notificações gerais do produto, processos ou itens que não têm qualquer relação com o conteúdo dentro da janela específica.|  
|[Notificações da bandeja do Windows](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|Use para notificações para processos fora do processo de superfície ou complementar os aplicativos.|Não use para notificações que são relevantes para o IDE.|  
|[Bolhas de notificação](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|Use para notificá-lo de um processo remoto ou alterar **fora** do IDE.|Não use como um meio para notificar o usuário de processos **dentro do** o IDE.|  
  
### <a name="notification-methods"></a>Métodos de notificação  
  
####  <a name="BKMK_ModalErrorMessageDialogs"></a> Caixas de diálogo de mensagem de erro modal  
 Uma caixa de diálogo de mensagem de erro modal é usada para exibir uma mensagem de erro que requer a confirmação ou a ação do usuário.  
  
 ![Mensagem de erro modal](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "01_ModalErrorMessage 0901")  
  
 **Uma caixa de diálogo de mensagem de erro modal alertando o usuário de uma cadeia de caracteres de conexão inválido para um banco de dados**  
  
####  <a name="BKMK_IDEStatusBar"></a> Barra de status do IDE  
 A probabilidade de que os usuários percebem o texto da barra de status se correlaciona com sua experiência e completo do computador e a experiência específica com a plataforma Windows. A base de clientes do Visual Studio tende a ser experiente em ambas as áreas, embora os usuários do Windows experientes ainda poderá perder as alterações na barra de status. Portanto, a barra de status é usada para fins informativos, ou como uma indicação redundante melhor para as informações apresentadas em outro lugar. Qualquer tipo de informações importantes que o usuário deve resolver imediatamente deve ser fornecido em uma caixa de diálogo ou na janela da ferramenta de notificações.  
  
 A barra de status do Visual Studio foi projetada para permitir vários tipos de informação a ser exibido. Ele é dividido em regiões de designer, comentários, barra de progresso, animação e cliente.  
  
 A região de comentários e a região de designer são sempre visíveis. A barra de progresso e a animação regiões sempre são dinâmicas e com base no contexto do usuário. A região de designer tem uma largura estática, determinada pelo comprimento da cadeia de caracteres que é recebida de um recurso que acompanha este artigo para a mensagem de texto. Isso permite que a localização redimensionar a largura sem a necessidade de uma alteração de código. Para o inglês, a largura dessa cadeia de caracteres é aproximadamente 220 pixels. A região de designer irá se comportar normalmente e a região de comentários absorve o espaço restante.  
  
 A barra de status também é colorizada para adicionar interesse visual e funcional valor comunicando-se várias alterações de estado IDE, como quando o IDE está no modo de depuração.  
  
 ![As alterações de cores da barra de status do IDE](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "02_IDEStatusBar 0901")  
  
 **Cores da barra de status IDE**  
  
####  <a name="BKMK_EmbeddedInfobar"></a> Barra de informações inserida  
 Uma barra de informações pode ser usada na parte superior de uma janela de documento ou janela de ferramentas para informar o usuário de um estado ou condição. Ele também pode oferecer os comandos para que o usuário pode ter uma maneira de agir facilmente. A barra de informações é um controle padrão do shell. Evite criar seus próprios, que atuará e exibida inconsistente com outras pessoas no IDE. Ver [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars) para detalhes de implementação e diretrizes de uso.  
  
 ![Incorporados da barra de informações](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "03_EmbeddedInfobar 0901")  
  
 **Uma barra de informações é inserido em uma janela de documento, alertando o usuário que o IDE está no modo de depuração histórica e o editor não responderá da mesma maneira como faz no modo de depuração padrão.**  
  
####  <a name="BKMK_MouseCursorChanges"></a> Alterações de cursor do mouse  
 Ao alterar o cursor do mouse, use cores que são associadas ao serviço VSColor e já estão associados com o cursor. Alterações de cursor podem ser usadas para indicar uma operação em andamento, bem como regiões em que o usuário está passando o mouse sobre um destino que pode ser arrastado, solto ou usado para selecionar um objeto de ocorrências.  
  
 Use o cursor do mouse ocupado/espera somente quando todo o tempo disponível da CPU deve ser reservado para uma operação, impedindo que o usuário expressar qualquer entrada adicional. Na maioria dos casos com aplicativos bem escritos usando multithreading, vezes quando os usuários são impedidos de realizar outras operações devem ser raras.  
  
 Tenha em mente que as alterações de cursor são úteis como uma indicação redundante para obter informações apresentado em outro lugar. Não confie em uma alteração do cursor como a única maneira de se comunicar com o usuário, especialmente ao tentar transmitir algo que é essencial que o usuário deve resolver.  
  
####  <a name="BKMK_NotSysProgressIndicators"></a> Indicadores de progresso  
 Indicadores de progresso são importantes para fornecer os comentários do usuário durante os processos que levam mais de alguns segundos para concluir. Indicadores de progresso podem ser mostradas no local (quase o ponto de partida da ação em andamento), em uma barra de status incorporada, em uma caixa de diálogo modal ou na barra de status do Visual Studio. Siga as orientações [indicadores de progresso](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators) em relação ao seu uso e a implementação.  
  
####  <a name="BKMK_VSNotificationsToolWindow"></a> Janela de notificações do Studio Visual  
 A janela de notificações do Visual Studio notifica os desenvolvedores sobre licenciamento, ambiente (Visual Studio), extensões e atualizações. Os usuários podem ignorar notificações individuais ou podem optar por ignorar determinados tipos de notificações. A lista de notificações ignoradas é gerenciada em uma **Ferramentas > Opções** página.  
  
 A janela de notificações não é extensível no momento.  
  
 ![Janela de notificações do Studio Visual](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "06_VSNotificationsWindow 0901")  
  
 **Janela de ferramentas do Visual Studio notificações**  
  
####  <a name="BKMK_ErrorList"></a> Lista de erros  
 Uma notificação dentro da lista de erro indicar erros e avisos que ocorreram durante a compilação e ou processo de compilação e permite que o usuário navegue em código para esse erro de código específico.  
  
 ![Lista de erros](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "08_ErrorList 0901")  
  
 **Lista de erros no Visual Studio**  
  
####  <a name="BKMK_EmbeddedStatusBars"></a> Barras de status inserido  
 Como a barra de status do IDE é dinâmica, com seu contexto de região de cliente definido como a janela do documento ativo e atualizados de acordo com o contexto do usuário e/ou respostas de sistema de informações, é difícil a manter uma exibição contínua das informações de status em longo prazo processos assíncronos. Por exemplo, a barra de status do IDE não é apropriada para as notificações de resultados de execução de teste para várias execuções de e/ou seleções de item podem ser acionados imediatamente. É importante manter essas informações de status no contexto da janela de ferramentas ou documento em que o usuário fizer uma seleção ou inicia um processo.  
  
 ![Barra de status incorporados](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "09_EmbeddedStatusBar 0901")  
  
 **Barra de status incorporada no Visual Studio**  
  
####  <a name="BKMK_WindowsTray"></a> Notificações da bandeja do Windows  
 Os Windows na área de notificação está ao lado de sistema do relógio na barra de tarefas do Windows. Muitos utilitários e componentes de software fornecem ícones nessa área, para que o usuário pode obter um menu de contexto para tarefas de todo o sistema, como alterar a resolução de tela ou obter as atualizações de software.  
  
 Notificações de nível de ambiente devem ser apresentadas no hub de notificações do Visual Studio, não é a área de notificação do Windows.  
  
####  <a name="BKMK_NotificationBubbles"></a> Bolhas de notificação  
 Bolhas de notificação podem aparecer como informação dentro de um designer/editor ou como parte da área de notificação do Windows. O usuário percebe que essas bolhas como problemas que eles podem ser resolvidos mais tarde, que é um benefício para notificações não críticas. Bolhas são inapropriadas para informações importantes que o usuário deve resolver imediatamente. Se você usar bolhas de notificação no Visual Studio, execute as [diretrizes de área de trabalho do Windows para bolhas de notificação](/windows/desktop/uxguide/mess-notif).  
  
 ![Balão de notificação](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "07_NotificationBubbles 0901")  
  
 **Balão de notificação na área de notificação do Windows usada para o Visual Studio**  
  
##  <a name="BKMK_ProgressIndicators"></a> Indicadores de progresso  
  
### <a name="overview"></a>Visão geral  
 Indicadores de progresso são uma parte importante de um sistema de notificação para fornecer os comentários do usuário. Eles informam o usuário quando processos e as operações serão concluídas. Tipos de indicador familiar incluem barras de progresso, cursores de rotação e ícones animados. O tipo e o posicionamento de um indicador de progresso depende do contexto, incluindo o que está sendo relatado e quanto tempo o processo ou operação levará para ser concluída.  
  
#### <a name="factors"></a>Fatores  
 Para determinar qual tipo de indicador é apropriado, você precisa determinar os fatores a seguir.  
  
1.  **Medição de tempo:** período de tempo a operação levará  
  
2.  **Modalidade:** se a operação está restrita ao ambiente (bloqueios de interface do usuário até que o processo é concluído)  
  
3.  **Persistente/transitório:** se o resultado final do progresso precisa ser relatada e/ou visível em um momento posterior  
  
4.  **Determinada/indeterminado:** se a hora de término da operação e o progresso podem ser calculados  
  
5.  **Local do elemento gráfico/Textual:** se o progresso ou o processo é capturado em linha, no corpo de uma mensagem ou um controle específico, como o controle de árvore  
  
6.  **Proximidade:** se o progresso deve ser em estreita proximidade com a interface do usuário que está relacionado ao. (Por exemplo, pode ser na barra de status, que pode ser muito longe, ou ele tem estejam perto do botão que iniciou o processo?)  
  
#### <a name="determinate-progress"></a>Progresso determinada  
  
|Tipo de andamento|Quando e como usar o|Observações|  
|-------------------|-------------------------|-----------|  
|Barra de progresso (determinada)|Duração da esperada > 5 segundos.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.|**Não** inserir texto em animação.|  
|Barra de informações|Sistema de mensagens associado contextual da interface do usuário. Ver [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars).<br /><br /> Pode incluir a descrição textual dos detalhes do processo.|**Não** usar vários infobars quando você precisa indicar vários processos. Use as barras de progresso gráfico empilhado.|  
|Janela Saída|Notificação transitória: processo de nível de aplicativo que o usuário deseja **examine** detalhes de após a conclusão.|**Não** usar se o usuário precisará se referem aos dados mais tarde.|  
|Arquivo de log|Emparelhado com notificação intransient em casos quando é importante **salvar** detalhes após a conclusão.||  
|Barra de status|Notificação transitória: que o usuário de processo no nível do aplicativo serão **não precisa** detalhes de após a conclusão.<br /><br /> Inclui uma barra de progresso incorporado.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.||  
  
#### <a name="indeterminate-progress"></a>Progresso indeterminado  
  
|Tipo de andamento|Quando e como usar o|Observações|  
|-------------------|-------------------------|-----------|  
|Barra de progresso (indeterminada)|Duração da esperada > 5 segundos.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.|**Não** inserir texto em animação.|  
|ANTS (animados pontos horizontais)|Ida e volta ao servidor.<br /><br /> Colocado próximo ponto de contexto na parte superior do contêiner pai.|**Não** usar se todo o contêiner não tem como pai.|  
|Controle giratório (anel de progresso)|Processo associado ao contextual da interface do usuário, ou onde o espaço é uma consideração.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.||  
|Barra de informações|Sistema de mensagens associado contextual da interface do usuário. Ver [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars).|**Não** usar vários infobars quando você precisa indicar vários processos. Use as barras de progresso gráfico empilhado.|  
|Janela Saída|Notificação transitória: processo de nível de aplicativo que o usuário desejará **examine** detalhes de após a conclusão.|**Não** usar para obter informações que precise ser mantido entre as sessões.|  
|Arquivo de log|Emparelhado com notificação intransient em casos quando é importante **salvar** detalhes após a conclusão.||  
|Barra de status|Notificação transitória: que o usuário de processo no nível do aplicativo serão **não precisa** detalhes de após a conclusão.<br /><br /> Inclui a barra de progresso incorporado.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.||  
  
### <a name="progress-indicator-types"></a>Tipos de indicador de progresso  
  
#### <a name="progress-bars"></a>Barras de progresso  
  
##### <a name="indeterminate"></a>Indeterminado  
 ![Barra de progresso indeterminado](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "04_Indeterminate 0901")  
  
 **Barra de progresso indeterminado**  
  
 "Indeterminado" significa que o progresso geral de uma operação ou processo não pode ser determinado. Use as barras de progresso indeterminado para operações que exigem uma quantidade ilimitada de tempo ou que acessam um número desconhecido de objetos. Use uma descrição textual para acompanhar o que está acontecendo. Use tempos limite para fornecer limites operações baseadas em tempo. Barras de progresso indeterminado usam animações para mostrar que o progresso está sendo feita, mas não fornecer nenhuma outra informação. Não escolha uma barra de progresso indeterminado com base apenas nos possíveis falta de precisão sozinho.  
  
##### <a name="determinate"></a>Determinada  
 ![Barra de progresso determinada](../../extensibility/ux-guidelines/media/0901-05_determinate.png "05_Determinate 0901")  
  
 **Barra de progresso determinada**  
  
 "Determinada" significa que um processo ou operação requer uma quantidade limitada de tempo, mesmo se essa quantidade de tempo não pode ser prevista com precisão. Indica claramente a conclusão. Não deixe que uma barra de progresso até 100 por cento, a menos que a operação foi concluída. Animação da barra de progresso determinada move esquerda para a direita de 0 a 100%.  
  
 Nunca mova o indicador de progresso com versões anteriores durante uma operação. A barra deve seguir em frente constantemente quando a operação é iniciada e atingir 100%, quando ele termina. O ponto da barra de progresso é dar ao usuário uma ideia de quanto tempo leva de toda a operação, independentemente de quantas etapas envolvidas.  
  
##### <a name="concurrent-reporting-stacked-progress-bars"></a>Simultâneas reporting (barras de progresso empilhada)  
 Se uma operação levará um longo tempo - talvez podem ser usado vários minutos - em seguida, duas barras de andamento, um que mostra o progresso geral para uma operação e outro para a progressão da etapa atual. Por exemplo, se um programa de instalação está copiando vários arquivos, uma barra de progresso pode ser usada para indicar quanto tempo leva para todo o processo enquanto o segundo pode indicar qual é a porcentagem do arquivo atual ou diretório está sendo copiado. Não relate os mais de cinco processos usando barras de progresso empilhadas ou operações simultâneas. Se você tiver mais de cinco operações simultâneas ou processos para relatório, use uma caixa de diálogo modal com um relatório e um botão Cancelar os detalhes de progresso para a janela de saída.  
  
##### <a name="textual-descriptions"></a>Descrições  
 Use uma descrição textual para acompanhar o que está acontecendo e o tempo estimado para conclusão. Se for impossível determinar quanto tempo levará uma operação, uma opção melhor para fornecer comentários pode ser um ícone animado em vez de uma barra de progresso.  
  
 Visual Studio fornece uma barra de progresso padrão na barra de status que pode ser usada por qualquer produto integrado ao Visual Studio. Para obter descrições textuais do que está acontecendo enquanto a barra de progresso é animada, o texto da barra de status pode ser atualizado.  
  
#### <a name="other-progress-indicators"></a>Outros indicadores de progresso  
  
##### <a name="ants-animated-horizontal-dots"></a>ANTS (animados pontos horizontais)  
 ![Progresso ants](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903 01_Ants")  
  
 "Ants," pontos horizontais animados, fornecer uma referência visual para um processo do servidor de ida e volta indeterminado.  
  
##### <a name="spinner-progress-ring"></a>Controle giratório (anel de progresso)  
 ![Controle giratório de progresso](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903 02_Spinner")  
  
 O controle giratório (também conhecido como um "anel de progresso") é um indicador de progresso indeterminado usado principalmente em relação à interface do usuário contextual. Exiba um controle giratório em estreita proximidade com seu conteúdo relacionado, como um cabeçalho de categoria textual, o sistema de mensagens ou o controle.  
  
##### <a name="cursor-feedback"></a>Comentários do cursor  
 Operações que levam entre segundos 2 a 7, fornece comentários de cursor. Normalmente, isso significa usar o cursor de espera fornecido pelo sistema operacional. Para obter diretrizes, consulte o artigo do MSDN [Cursors.Wait propriedade](/dotnet/api/system.windows.input.cursors.wait).  
  
#### <a name="progress-indicator-locations"></a>Locais de indicador de progresso  
  
##### <a name="status-bar"></a>Barra de status  
 A barra de status fornece um local para exibir as mensagens e informações úteis para o usuário sem interromper o trabalho do usuário de seu aplicativo. Normalmente na parte inferior de uma janela, status de progresso será exibido um painel de dica de ferramenta que inclui uma mensagem sobre a medida de progresso em combinação com um indicador da barra de progresso.  
  
 ![Barra de status com a barra de progresso](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903 03_StatusBarProgressBar")  
  
 **Barra de status com a barra de progresso**  
  
 ![Barra de status com o sistema de mensagens](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903 04_StatusBarMessage")  
  
 **Barra de status com descrição textual**  
  
##### <a name="infobar"></a>Barra de informações  
 Semelhante à barra de status, da barra de informações fornece notificação contextual e mensagens, que também pode ser emparelhado com indicadores de progresso indeterminado, como a barra de progresso ou um controle giratório. Da barra de informações não deve fornecer a indicação de progresso determinada ou de andamento de nível granular. Ver [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars).  
  
 ![Barra de informações com a barra de progresso e o sistema de mensagens](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903 05_InfoBar")  
  
 **Barra de informações com a barra de progresso e a descrição textual**  
  
 ![Barra de informações dentro de uma janela](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903 06_InfoBarInWindow")  
  
##### <a name="inline"></a>Embutido  
 Indicação de progresso embutido pode ser representada por qualquer um dos tipos de carregador de progresso. Normalmente, o indicador de progresso é emparelhado com mensagens, mas isso não é um requisito.  
  
 ![Controle giratório de progresso embutido](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903 07_InlineSpinner")  
  
 **Controle giratório combinado com descrição textual**  
  
 ![Embutido empilhada barras de progresso](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903 08_InlineStackedProgress")  
  
 **Barras de progresso empilhadas determinada**  
  
 ![Mensagens de progresso embutido](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903 09_InlineText")  
  
 **Texto do Server Explorer embutido: atualizando...**  
  
##### <a name="tool-windows"></a>Janelas de ferramentas  
 Indicação de progresso global é representada por uma barra de progresso indeterminado posicionada diretamente abaixo da barra de ferramentas.  
  
 ![Barra de progresso indeterminado global](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903 23_GlobalIndeterminate")  
  
 **Barra de progresso indeterminado global do Team Explorer**  
  
##### <a name="dialogs"></a>Caixas de diálogo  
 Caixas de diálogo podem conter qualquer um dos tipos de carregador de progresso. Indicadores de progresso podem ser emparelhados com mensagens bem como combinados com vários níveis de indicação de progresso para representar granular e subprocessos.  
  
 ![Caixa de diálogo com vários tipos de indicador de progresso](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903 11_Dialog")  
  
 **Caixa de diálogo Visual Studio com vários tipos de indicador de progresso e de processos simultâneos**  
  
 ![Caixa de diálogo com o carregador de progresso e o sistema de mensagens](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903 12_Dialog2")  
  
 **Caixa de diálogo Visual Studio com o carregador de progresso e embutida dos comandos de mensagens**  
  
##### <a name="document-well"></a>Documente também  
 O documento também pode exibir vários tipos de carregador de progresso em combinação com os controles.  
  
 ![Progresso das mensagens no documento bem](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903 13_DocumentWell")  
  
 **Barra de progresso indeterminado abaixo da barra de ferramentas**  
  
##### <a name="output-window"></a>Janela Saída  
 A janela de saída é apropriada para lidar com a progressão de processo e o status de progresso em andamento por meio de mensagens textual embutidos. Você deve usar a barra de Status, juntamente com qualquer relatório de progresso de janela Saída.  
  
 ![Na janela de saída de mensagens de progresso](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903 14_OutputWindow")  
  
 **Janela de saída com o status do processo em andamento e aguarde o sistema de mensagens**  
  
##  <a name="BKMK_Infobars"></a> Infobars  
  
### <a name="overview"></a>Visão geral  
 Infobars dar ao usuário um indicador perto de seu ponto de atenção e usando o controle de barra de informações compartilhadas garante a consistência na aparência visual e interação.  
  
 ![Infobar](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")  
  
 **Infobars no Visual Studio**  
  
#### <a name="appropriate-uses-for-an-infobar"></a>Uso apropriado para uma barra de informações  
  
-   Dar ao usuário uma mensagem sem bloqueio, mas importante relevante para o contexto atual  
  
-   Para indicar que a interface do usuário está em um determinado estado ou condição que traz algumas implicações de interação, como a depuração histórica  
  
-   Para notificar o usuário que o sistema detectou problemas, como quando uma extensão está causando problemas de desempenho  
  
-   Para fornecer ao usuário uma maneira facilmente tomar a ação, como quando o editor detecta que um arquivo tiver mistos tabulações e espaços  
  
##### <a name="do"></a>Faça:  
  
-   Mantenha o texto da mensagem da barra de informações curtas e para o ponto.  
  
-   Manter o texto nos links e botões sucinta.  
  
-   Certifique-se de fornecer aos usuários as opções de "ação" são mínimas, mostrando apenas as ações necessárias.  
  
##### <a name="dont"></a>Não:  
  
-   Use uma barra de informações para oferecer comandos padrão devem ser colocados em uma barra de ferramentas.  
  
-   Use uma barra de informações no lugar de uma caixa de diálogo modal.  
  
-   Crie uma mensagem flutuante fora de uma janela.  
  
-   Use vários infobars em vários locais dentro da mesma janela.  
  
#### <a name="can-multiple-infobars-show-at-the-same-time"></a>Vários infobars pode mostrar ao mesmo tempo?  
 Sim, vários infobars pode mostrar ao mesmo tempo. Elas serão exibidas na ordem primeiro a chegar, chegada com a barra de informações primeiro, mostrando em infobars adicionais e superior mostrando abaixo.  
  
 O usuário verá um máximo de três infobars por vez, depois que, se houver mais infobars disponíveis, a região de barra de informações se tornará rolável.  
  
### <a name="creating-an-infobar"></a>Criando uma barra de informações  
 A barra de informações tem quatro seções, da esquerda para a direita:  
  
-   **Ícone:** isso é onde você adicionaria um ícone você gostaria de exibir para a barra de informações, como um ícone de aviso.  
  
-   **Texto:** você pode adicionar texto para descrever o usuário cenário/situação é, juntamente com links dentro do texto, se necessário. Lembre-se de manter o texto sucinta.  
  
-   **Ações:** esta seção deve conter links e botões para ações que o usuário pode executar em sua barra de informações.  
  
-   **Botão Fechar:** a última seção à direita pode ter um botão Fechar.  
  
#### <a name="creating-a-standard-infobar-in-managed-code"></a>Criando uma barra de informações padrão em código gerenciado  
 A classe InfoBarModel pode ser usada para criar uma fonte de dados para uma barra de informações. Use um desses quatro construtores:  
  
```  
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);  
  
```  
  
```  
public InfoBarModel(string text, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);  
  
```  
  
```  
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);  
  
```  
  
```  
public InfoBarModel(string text, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);  
```  
  
 Aqui está um exemplo que cria um InfoBarModel com algum texto com um hiperlink, um botão de ação e um ícone.  
  
 ![Barra de informações com hiperlink](../../extensibility/ux-guidelines/media/0904-02_infobarhyperlink.png "0904 02_InfobarHyperlink")  
  
```  
var infoBar = new InfoBarModel(  
    textSpans: new[]  
    {  
        new InfoBarTextSpan("This is a "),  
        new InfoBarHyperlink("hyperlink"),  
        new InfoBarTextSpan(" InfoBar.")  
    },  
    actionItems: new[]  
    {  
        new InfoBarButton("Click Me")  
    },  
    image: KnownMonikers.StatusInformation,  
    isCloseButtonVisible: true);  
  
```  
  
#### <a name="creating-a-standard-infobar-in-native-code"></a>Criando uma barra de informações padrão em código nativo  
 Implementar a interface de IVsInfoBar a fim de fornecer uma barra de informações do código nativo.  
  
```  
public interface IVsInfoBar  
{  
    IVsInfoBarActionItemCollection ActionItems { get; }  
    ImageMoniker Image { get; }  
    bool IsCloseButtonVisible { get; }  
    IVsInfoBarTextSpanCollection TextSpans { get; }  
}  
  
```  
  
#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>Obtendo uma UIElement da barra de informações de uma barra de informações  
 A implementação InfoBarModel ou IVsInfoBar são modelos de dados que devem ser transformados em um UIElement para ser mostrado na interface do usuário. Um UIElement pode ser recuperado com o serviço SVsInfoBarUIFactory/IVsInfoBarUIFactory.  
  
```  
private bool TryCreateInfoBarUI(IVsInfoBar infoBar, out IVsInfoBarUIElement uiElement)  
{  
    IVsInfoBarUIFactory infoBarUIFactory = serviceProvider.GetService(typeof(SVsInfoBarUIFactory)) as IVsInfoBarUIFactory;  
    if (infoBarUIFactory == null)  
    {  
        uiElement = null;  
        return false;  
    }  
  
    uiElement = infoBarUIFactory.CreateInfoBar(infoBar);  
    return uiElement != null;  
}  
```  
  
### <a name="placement"></a>Posicionamento  
 Infobars pode ser mostrada em uma ou mais dos seguintes locais:  
  
-   Janelas de ferramentas  
  
-   Dentro de uma guia de documento  
  
> [!IMPORTANT]
>  É possível posicionar uma barra de informações para fornecer uma mensagem sobre o contexto global. Isso seria exibido entre as barras de ferramentas e o documento bem. Isso não é recomendado, pois isso causa problemas com "saltar e puxão" do IDE e deve ser evitada, a menos que absolutamente necessário e apropriado.  
  
#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>Colocando uma barra de informações em um ToolWindowPane  
 O método ToolWindowPane.AddInfoBar(IVsInfoBar) pode ser usado para adicionar uma barra de informações para uma janela de ferramentas. Essa API pode adicionar um IVsInfoBar (do qual InfoBarModel é uma implementação padrão), ou um IVsUIElement.  
  
#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>Colocando uma barra de informações em um documento ou não ToolWindowPane  
 Para colocar uma barra de informações em qualquer IVsWindowFrame, use a propriedade VSFPROPID_InfoBarHost para obter o IVsInfoBarHost para o quadro e, em seguida, adicione a UIElement da barra de informações.  
  
```  
private void AddInfoBar(IVsWindowFrame frame, IVsUIElement uiElement)  
{  
    IVsInfoBarHost infoBarHost;  
    if (TryGetInfoBarHost(frame, out infoBarHost))  
    {  
        infoBarHost.AddInfoBar(uiElement);  
    }  
}  
private bool TryGetInfoBarHost(IVsWindowFrame frame, out IVsInfoBarHost infoBarHost)  
{  
    object infoBarHostObj;  
    if (ErrorHandler.Failed(frame.GetProperty((int)__VSFPROPID7.VSFPROPID_InfoBarHost, out infoBarHostObj)))  
    {  
        infoBarHost = null;  
        return false;  
    }  
  
    infoBarHost = infoBarHostObj as IVsInfoBarHost;  
    return infoBarHost != null;  
}  
  
```  
  
#### <a name="placing-an-infobar-in-the-main-window"></a>Colocando uma barra de informações na janela principal  
 Para colocar uma barra de informações na janela principal, use o VSSPROPID_MainWindowInfoBarHost do serviço IVsShell para obter IVsInfoBarHost da janela principal e, em seguida, adicione a UIElement da barra de informações a ele.  
  
### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>Saber quando o usuário entra em ação na minha barra de informações?  
 Sim, podemos retornará cada ação de evento para o autor da barra de informações. Então, cabe ao autor da barra de informações agir no IDE com base na seleção do usuário na barra de informações. Infobars será removido automaticamente do host cujo fechar botão foi clicado, mas o trabalho adicional é necessário se outros infobars precisam ser removidos depois de fechar. Telemetria também será necessário estar conectado de forma independente por cada barra de informações.  
  
#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>Recebimento de eventos da barra de informações em um ToolWindowPane  
 ToolWindowPane tem dois eventos para infobars. O evento InfoBarClosed é gerado quando uma barra de informações no ToolWindowPane está fechada. O evento InfoBarActionItemClicked é gerado quando um hiperlink ou botão de barra de informações é clicado.  
  
#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>Recebimento de eventos da barra de informações diretamente do UIElement  
 IVsInfoBarUIElement.Advise pode ser usado para assinar eventos diretamente de UIElement de uma barra de informações. Implementar IVsInfoBarUIEvents permitirá que o autor receber fechar e clique em eventos.  
  
```  
public interface IVsInfoBarUIEvents  
{  
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);  
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);  
}  
  
```  
  
##  <a name="BKMK_ErrorValidation"></a> Validação de erros  
 Quando um usuário insere informações que não não aceitáveis, como quando um campo obrigatório será ignorado ou quando os dados são inseridos no formato incorreto, é melhor validação de controle do uso ou comentários próximo ao controle em vez de usar uma caixa de diálogo de erro pop-up bloqueio.  
  
### <a name="field-validation"></a>Validação de campo  
 Validação de formulário e campo consiste em três componentes: um controle, um ícone e uma dica de ferramenta. Embora vários tipos de controles podem usar isso, uma caixa de texto será usada como exemplo.  
  
 ![Validação do campo &#40;em branco&#41;](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905 01_FieldValidation")  
  
 Se o campo é obrigatório, deve haver texto informando de marca d'água  **\<necessárias >** e o plano de fundo do campo deve ser uma luz amarelo (VSColor: `Environment.ControlEditRequiredBackground`) e o primeiro plano deve ser cinza (VSColor: `Environment.ControlEditRequiredHintText`):  
  
 ![Validação com "Required" rótulo do campo](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905 02_FieldValidationRequired")  
  
 O programa pode determinar que o controle está em um estado de *conteúdo inválido inserido* quando o foco é movido para outro controle ou quando o usuário clica em um botão de confirmação [Okey] ou quando o usuário salva o documento ou formulário.  
  
 Quando for determinado que o estado de conteúdo inválido, um ícone é exibido dentro do controle ou ao lado dela. Uma dica de ferramenta que descreve o erro deve aparecer ao focalizar do ícone ou o controle. Além disso, uma borda de 1 pixel deve aparecer em torno do controle que está criando o estado inválido.  
  
 ![Especificações de layout de validação de campo](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905 03_LayoutSpecs")  
  
 **Especificações de layout para validação de campo**  
  
#### <a name="acceptable-variations-for-icon-location"></a>Variações de aceitáveis para a localização do ícone  
 Há inúmeros casos exclusivos no qual os usuários precisarão ser informados sobre erros de validação. Considerando o tipo de controle e a configuração da interface do usuário, escolha o posicionamento de ícone apropriado para sua situação.  
  
 ![Locais de aceitáveis para a localização do ícone](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905 04_IconLocation")  
  
 **Variações aceitáveis para locais de ícone de validação de campo**  
  
#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>Exigir uma viagem de ida e para uma conexão de rede ou servidor de validação  
 Em alguns casos, uma ida e volta para o servidor é necessária para verificar o conteúdo e seria importante mostrar o progresso do usuário, verificado e os estados de erro. A figura abaixo mostra um exemplo de neste caso e a interface do usuário recomendada.  
  
 ![Envolvendo uma ida e volta a um servidor de validação](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905 05_RoundTrip")  
  
 **Validação envolvendo uma ida e volta a um servidor**  
  
 Observe que o espaço disponível suficiente para a direita do controle deve ser fornecido para acomodar o texto "Verificando..." e "Repetir".  
  
#### <a name="in-place-warning-text"></a>Texto de aviso no local  
 Quando houver espaço disponível para colocar a mensagem de erro perto o controle em um estado de erro, isso é preferível a usar a dica de ferramenta sozinha.  
  
 ![No&#45;coloca aviso](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905 06_InPlaceWarning")  
  
 **Texto de aviso no local**  
  
#### <a name="watermarks"></a>Marcas d'água  
 Às vezes, um todo controle ou janela está em um estado de erro. Nessa situação, use uma marca d'água para indicar o erro.  
  
 ![Watermark](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")  
  
 **Validação do campo de marca d'água**