---
title: Notificações e progresso para Visual Studio | Microsoft Docs
description: Saiba mais sobre várias maneiras de informar aos usuários o que está acontecendo Visual Studio suas tarefas de desenvolvimento de software.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 994a315d04b06d1998a8c8e0c4291b6a4c54cb61
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902235"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Notificações e progresso do Visual Studio
## <a name="notification-systems"></a><a name="BKMK_NotificationSystems"></a> Sistemas de notificação

### <a name="overview"></a>Visão geral
 Há várias maneiras de informar ao usuário o que está acontecendo Visual Studio suas tarefas de desenvolvimento de software.

 Ao implementar qualquer tipo de notificação:

- **Mantenha o número de notificações para o número efetivo** mínimo. As mensagens de notificação devem ser aplicadas à maioria Visual Studio usuários ou aos usuários de uma área específica de recurso/recurso. O uso excessivo de notificações pode desviar o usuário ou diminuir a facilidade de uso do sistema.

- **Verifique se você está apresentando mensagens** claras e ativas que o usuário pode usar para invocar o contexto apropriado para fazer escolhas mais complexas e tomar mais medidas.

- **Apresente mensagens síncronas e assíncronas adequadamente.** Notificações síncronas indicam que algo precisa de atenção imediata, como quando um serviço Web falha ou uma exceção de código é lançada. O usuário deve ser informado dessas situações imediatamente de uma maneira que exija sua entrada, como em uma caixa de diálogo modal. As notificações assíncronas são aquelas sobre as quais o usuário deve saber, mas não precisam agir imediatamente, como quando uma operação de build é concluída ou uma implantação de site é concluída. Essas mensagens devem ser mais ambientes e não interromper o fluxo de tarefas do usuário.

- **Use diálogos modais somente quando** necessário para impedir que o usuário adotem mais ações antes de confirmar a mensagem ou tomar uma decisão apresentada na caixa de diálogo.

- **Remova as notificações de ambiente quando elas não são mais válidas.** Não exigir que o usuário descarte uma notificação se ele já tiver feito uma ação para resolver o problema de que foi notificado.

- **Esteja ciente de que as notificações podem levar a correlações falsas.** Os usuários podem acreditar que uma ou mais de suas ações dispararam uma notificação quando, na verdade, não havia nenhuma relação causal. Seja claro na mensagem de notificação sobre o contexto, o gatilho e a origem da notificação.

### <a name="choosing-the-right-method"></a>Escolhendo o método certo
 Use esta tabela para ajudá-lo a escolher o método certo para notificar o usuário da mensagem.

|Método|Uso|Não usar|
|------------|---------|----------------|
|[Caixas de diálogo de mensagem de erro modal](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|Use quando uma resposta do usuário for necessária antes de continuar.|Não use quando não houver necessidade de bloquear o usuário e interromper seu fluxo. Evite usar diálogos modais se for possível mostrar a mensagem de outra maneira menos invasiva.|
|[Barra de status do IDE](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|Use quando houver informações textuais de ambiente sobre o status de um processo.|Não use sozinho. Melhor usado em conjunto com outro mecanismo de comentários.|
|[Barra de informações inserida](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|Em uma janela de ferramentas ou de documento, use para notificar o progresso, o estado do erro, os resultados e/ou informações a ação.|Não use se as informações não são relevantes para o local em que a barra de informações é colocada.<br /><br /> Não use fora de uma janela de documento/ferramenta.|
|[Alterações de cursor do mouse](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|Pode ser usado para notificar que um processo está acontecendo. Também usado para notificar que há uma alteração de estado no mouse, como quando o arrastar/soltar está em andamento ou se o cursor do mouse está em um determinado modo, como modo de desenho.|Não use para alterações de progresso curto ou se a vibração do cursor for provável (por exemplo, quando vinculado a partes de um processo de execução mais longa em vez de todo o processo).|
|[Indicadores de progresso](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|Use quando precisar relatar o progresso (determinado ou indeterminado). Há uma variedade de tipos de indicadores de progresso e uso específico para cada um. Consulte [Indicadores de progresso](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators).||
|[Visual Studio de notificações](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|A janela Notificações não é extensível publicamente. No entanto, ele é usado para comunicar uma variedade de mensagens sobre Visual Studio, incluindo problemas críticos com sua licença e notificações informativas de atualizações para Visual Studio ou para pacotes.|Não use para outros tipos de notificações.|
|[Lista de erros](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|Quando o problema está relacionado diretamente à solução aberta no momento do usuário com um problema (erro/aviso/informações), talvez seja necessário tomar medidas no código.<br /><br /> Isso incluiria, por exemplo:<br /><br /> – Mensagens do compilador (erro/aviso/informações)<br /><br /> – Mensagens do Analisador de Código/Diagnóstico sobre o código<br /><br /> – Criar mensagens<br /><br /> Pode ser apropriado para problemas relacionados aos arquivos de projeto ou solução, mas considere uma Gerenciador de Soluções primeiro.|Não use para itens que não têm nenhuma relação com o código da solução aberta do usuário.|
|Notificações do editor: Lâmpada|Use quando você tiver uma correção disponível para corrigir um problema que existe no arquivo aberto.<br /><br /> Observe que a Lâmpada também deve ser usada para hospedar Ações Rápidas que são tomadas no código do usuário sob demanda, como as refações, mas, nesse caso, não aparecerão "estilo de notificação".|Não use para itens que não têm nenhuma relação com o arquivo aberto.|
|Notificações do editor: alternâncias|Use para alertar o usuário sobre um problema com um intervalo específico de seu código aberto (por exemplo, um squiggle vermelho para erros).|Não use para itens que não estão relacionados a um intervalo específico de seu código aberto.|
|[Barras de status inseridas](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|Use para fornecer o status relacionado ao conteúdo ou ao processo dentro do contexto de uma janela de ferramenta específica, janela de documento ou janela de diálogo.|Não use para notificações gerais de produtos, processos ou itens que não tenham nenhuma relação com o conteúdo dentro da janela específica.|
|[Notificações da bandeja do Windows](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|Use para expor notificações para processos fora do processo ou aplicativos de terceiros.|Não use para notificações relevantes para o IDE.|
|[Bolhas de notificação](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|Use para notificar um processo remoto ou alterar **fora** do IDE.|Não use como um meio para notificar o usuário dos processos **dentro** do IDE.|

### <a name="notification-methods"></a>Métodos de notificação

#### <a name="modal-error-message-dialogs"></a><a name="BKMK_ModalErrorMessageDialogs"></a> Caixas de diálogo de mensagem de erro modal
 Uma caixa de diálogo de mensagem de erro modal é usada para exibir uma mensagem de erro que exige a confirmação ou a ação do usuário.

 ![Mensagem de erro modal](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "0901-01_ModalErrorMessage")

 **Uma caixa de diálogo de mensagem de erro modal alertando o usuário de uma cadeia de conexão inválida para um banco de dados**

#### <a name="ide-status-bar"></a><a name="BKMK_IDEStatusBar"></a> Barra de status do IDE
 A probabilidade de que os usuários observem o texto da barra de status está relacionada à experiência do computador em todos os ambientes e à experiência específica com a plataforma Windows. A Visual Studio de clientes tende a ser experimentado em ambas as áreas, embora até mesmo usuários experientes do Windows possam perder alterações na barra de status. Portanto, a barra de status é melhor usada para fins informacionais ou como uma indicação redundante para informações apresentadas em outro lugar. Qualquer tipo de informação crítica que o usuário deve resolver imediatamente deve ser fornecido em uma caixa de diálogo ou na janela da ferramenta Notificações.

 A Visual Studio de status foi projetada para permitir que vários tipos de informações sejam exibidos. Ele é dividido em regiões para comentários, designer, barra de progresso, animação e cliente.

 A região de comentários e a região do designer estão sempre visíveis. A barra de progresso e as regiões de animação são sempre dinâmicas e baseadas no contexto do usuário. A região do designer tem uma largura estática determinada pelo comprimento da cadeia de caracteres que é extraida de um recurso que acompanha a mensagem de texto. Isso permite que a localização reize a largura sem a necessidade de uma alteração de código. Para inglês, a largura dessa cadeia de caracteres é de aproximadamente 220 pixels. A região do designer se comportará normalmente e a região de comentários vai absorver o espaço restante.

 A barra de status também é colorida para adicionar interesse visual e valor funcional comunicando várias alterações de estado do IDE, como quando o IDE está no modo de depuração.

 ![Alterações de cor da barra de status do IDE](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "0901-02_IDEStatusBar")

 **Cores da barra de status do IDE**

#### <a name="embedded-infobar"></a><a name="BKMK_EmbeddedInfobar"></a> Barra de informações inserida
 Uma barra de informações pode ser usada na parte superior de uma janela de documento ou janela de ferramentas para informar o usuário de um estado ou condição. Ele também pode oferecer comandos para que o usuário possa ter uma maneira de tomar medidas com facilidade. A barra de informações é um controle de shell padrão. Evite criar seu próprio, que atuará e aparecerá inconsistente com outras pessoas no IDE. Consulte [Infobars para](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars) obter detalhes de implementação e diretrizes de uso.

 ![Barra de informações inserida](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "0901-03_EmbeddedInfobar")

 **Uma barra de informações inserida em uma janela de documento, alertando o usuário de que o IDE está no modo de depuração histórico e o editor não responderá da mesma maneira que no modo de depuração padrão.**

#### <a name="mouse-cursor-changes"></a><a name="BKMK_MouseCursorChanges"></a> Alterações de cursor do mouse
 Ao alterar o cursor do mouse, use cores que estão vinculadas ao serviço VSColor e já estão associadas ao cursor. As alterações de cursor podem ser usadas para indicar uma operação em andamento, bem como zonas de clique em que o usuário está passeando sobre um destino que pode ser arrastado, descartado ou usado para selecionar um objeto.

 Use o cursor do mouse ocupado/de espera somente quando todo o tempo de CPU disponível deve ser reservado para uma operação, impedindo que o usuário expresse qualquer entrada posterior. Na maioria dos casos com aplicativos bem escritos usando multithreading, os momentos em que os usuários são impedidos de fazer outras operações devem ser raros.

 Tenha em mente que as alterações de cursor são úteis como uma indicação redundante para informações apresentadas em outro lugar. Não confie em uma alteração de cursor como a única maneira de se comunicar com o usuário, especialmente ao tentar transmitir algo crítico que o usuário deve abordar.

#### <a name="progress-indicators"></a><a name="BKMK_NotSysProgressIndicators"></a> Indicadores de progresso
 Indicadores de progresso são importantes para dar ao usuário comentários durante processos que levam mais de alguns segundos para ser concluídos. Os indicadores de progresso podem ser mostrados in-loco (próximos ao ponto de lançamento da ação em andamento), em uma barra de status inserida, em uma caixa de diálogo modal ou na barra Visual Studio status. Siga as diretrizes em [Indicadores de progresso](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators) sobre seu uso e implementação.

#### <a name="visual-studio-notifications-window"></a><a name="BKMK_VSNotificationsToolWindow"></a> Visual Studio de notificações
 A Visual Studio notificações notifica os desenvolvedores sobre licenciamento, ambiente (Visual Studio), extensões e atualizações. Os usuários podem ignorar notificações individuais ou optar por ignorar determinados tipos de notificações. A lista de notificações ignoradas é gerenciada em uma **página Ferramentas > Opções.**

 No momento, a janela Notificações não é extensível.

 ![Visual Studio de notificações](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "0901-06_VSNotificationsWindow")

 **Visual Studio de ferramentas notificações do Visual Studio**

#### <a name="error-list"></a><a name="BKMK_ErrorList"></a> Lista de erros
 Uma notificação na lista de erros indica erros e avisos que ocorreram durante a compilação e ou o processo de build e permite que o usuário navegue no código para esse erro de código específico.

 ![Lista de erros](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "0901-08_ErrorList")

 **Lista de erros no Visual Studio**

#### <a name="embedded-status-bars"></a><a name="BKMK_EmbeddedStatusBars"></a> Barras de status inseridas
 Como a barra de status do IDE é dinâmica, com seu contexto de região do cliente definido como a janela ativa do documento e a atualização de informações sobre o contexto do usuário e/ou as respostas do sistema, é difícil manter uma exibição contínua de informações ou dar status sobre processos assíncronos de longo prazo. Por exemplo, a barra de status do IDE não é apropriada para notificações de resultados de executar teste para várias seleções de itens ativas e/ou imediatamente. É importante manter essas informações de status no contexto do documento ou da janela de ferramentas em que o usuário faz uma seleção ou inicia um processo.

 ![Barra de status inserida](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "0901-09_EmbeddedStatusBar")

 **Barra de status inserida no Visual Studio**

#### <a name="windows-tray-notifications"></a><a name="BKMK_WindowsTray"></a> Notificações da bandeja do Windows
 A área de notificação do Windows está ao lado do relógio do sistema na barra de tarefas do Windows. Muitos utilitários e componentes de software fornecem ícones nessa área para que o usuário possa obter um menu de contexto para tarefas em todo o sistema, como alterar a resolução da tela ou obter atualizações de software.

 As notificações no nível do ambiente devem aparecer no hub Visual Studio Notificações, não na área de notificação do Windows.

#### <a name="notification-bubbles"></a><a name="BKMK_NotificationBubbles"></a> Bolhas de notificação
 As bolhas de notificação podem aparecer como informativas dentro de um editor/designer ou como parte da área notificação do Windows. O usuário percebe essas bolhas como problemas que podem ser resolvidos posteriormente, o que é um benefício para notificações não críticas. Bolhas são inadequadas para informações críticas que o usuário deve resolver imediatamente. Se você usar bolhas de notificação Visual Studio, siga as diretrizes da Área de Trabalho do [Windows para bolhas de notificação](/windows/desktop/uxguide/mess-notif).

 ![Bolha de notificação](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "0901-07_NotificationBubbles")

 **Bolha de notificação na área notificação do Windows usada para Visual Studio**

## <a name="progress-indicators"></a><a name="BKMK_ProgressIndicators"></a> Indicadores de progresso

### <a name="overview"></a>Visão geral
 Os indicadores de progresso são uma parte importante de um sistema de notificação para dar comentários ao usuário. Eles dizem ao usuário quando os processos e as operações serão concluídos. Os tipos de indicadores familiares incluem barras de progresso, cursores de rotação e ícones animados. O tipo e o posicionamento de um indicador de progresso dependem do contexto, incluindo o que está sendo relatado e quanto tempo o processo ou a operação levará para ser concluído.

#### <a name="factors"></a>Fatores
 Para determinar qual tipo de indicador é apropriado, você precisa determinar os fatores a seguir.

1. **Tempo:** período de tempo que a operação levará

2. **Modalidade:** se a operação é modal para o ambiente (bloqueia a interface do usuário até que o processo seja concluído)

3. **Persistente/Transitório:** se o resultado final do progresso precisa ser relatado e/ou visualizado posteriormente

4. **Determinado/Indeterminado: se** a hora de término da operação e o progresso podem ser calculados

5. **Local gráfico/textual:** se o progresso ou o processo é capturado em linha, no corpo de uma mensagem ou em um controle específico, como o controle Árvore

6. **Proximidade:** se o progresso deve estar próximo à interface do usuário à que ele está relacionado. (Por exemplo, ele pode estar na barra de status, que pode estar longe ou precisa estar próximo ao botão que iniciou o processo?)

#### <a name="determinate-progress"></a>Determinar o progresso

|Tipo de progresso|Quando e como usar|Observações|
|-------------------|-------------------------|-----------|
|Barra de progresso (determinada)|Duração esperada de >5 segundos.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.|**NÃO inserir texto** na animação.|
|Barra|Mensagens associadas à interface do usuário contextual. Consulte [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars).<br /><br /> Pode incluir a descrição textual dos detalhes do processo.|**NÃO use várias** barras de informações quando precisar indicar vários processos. Em vez disso, use barras de progresso empilhadas.|
|Janela de saída|Notificação transitória: processo no nível do aplicativo que o usuário deseja **analisar os** detalhes após a conclusão.|**NÃO use se** o usuário precisar consultar os dados mais tarde.|
|Arquivo de log|Emparelhado com notificação intransiente em casos em que é importante **salvar detalhes** após a conclusão.||
|Barra de Status|Notificação transitória: processo no nível do aplicativo que o usuário **não precisará de** detalhes após a conclusão.<br /><br /> Inclui uma barra de progresso inserida.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.||

#### <a name="indeterminate-progress"></a>Progresso indeterminado

|Tipo de progresso|Quando e como usar|Observações|
|-------------------|-------------------------|-----------|
|Barra de progresso (indeterminado)|Duração esperada de >5 segundos.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.|**NÃO inserir texto** na animação.|
|Animação (pontos horizontais animados)|Viagem de ida e volta para o servidor.<br /><br /> Colocado próximo ao ponto de contexto na parte superior do contêiner pai.|**NÃO use se** não for pai por contêiner inteiro.|
|Spinner (anel de progresso)|Processo associado à interface do usuário contextual ou em que espaço é uma consideração.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.||
|Barra|Mensagens associadas à interface do usuário contextual. Consulte [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars).|**NÃO use várias** barras de informações quando precisar indicar vários processos. Em vez disso, use barras de progresso empilhadas.|
|Janela de saída|Notificação transitória: processo em nível de aplicativo que o usuário vai querer **examinar** detalhes após a conclusão.|**Não** use para obter informações que precisam persistir entre sessões.|
|Arquivo de log|Emparelhado com notificação intransitória em casos em que é importante **salvar** detalhes após a conclusão.||
|Barra de Status|Notificação transitória: processo em nível de aplicativo que o usuário **não precisará** de detalhes após a conclusão.<br /><br /> Inclui a barra de progresso inserida.<br /><br /> Pode incluir a descrição textual dos detalhes do processo.||

### <a name="progress-indicator-types"></a>Tipos de indicador de progresso

#### <a name="progress-bars"></a>Barras de progresso

##### <a name="indeterminate"></a>Indeterminado
 ![Barra de progresso indeterminada](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "0901-04_Indeterminate")

 **Barra de progresso indeterminada**

 "Indeterminado" significa que o progresso geral de uma operação ou processo não pode ser determinado. Use barras de progresso indeterminadas para operações que exigem um período de tempo não associado ou que acessam um número desconhecido de objetos. Use uma descrição textual para acompanhar o que está acontecendo. Use tempos limite para dar limites a operações baseadas em tempo. As barras de progresso indeterminadas usam animações para mostrar que o progresso está sendo feito, mas não fornecem outras informações. Não escolha uma barra de progresso indeterminada com base apenas na possível falta de exatidão.

##### <a name="determinate"></a>Barra
 ![Barra de progresso de destérmino](../../extensibility/ux-guidelines/media/0901-05_determinate.png "0901-05_Determinate")

 **Barra de progresso de destérmino**

 "Desterminate" significa que uma operação ou um processo requer uma quantidade de tempo limitada, mesmo que essa quantidade de tempo não possa ser prevista com precisão. Indicar claramente a conclusão. Não deixe que uma barra de progresso vá para 100 por cento, a menos que a operação tenha sido concluída. A animação da barra de progresso de destérmino move da esquerda para a direita de 0 a 100%.

 Nunca mova o indicador de progresso para trás durante uma operação. A barra deve avançar de modo estável quando a operação começa e atinge 100% quando termina. O ponto da barra de progresso é dar ao usuário uma ideia de quanto tempo toda a operação leva, independentemente de quantas etapas estão envolvidas.

##### <a name="concurrent-reporting-stacked-progress-bars"></a>Relatórios simultâneos (barras de progresso empilhadas)
 Se uma operação levar muito tempo – talvez vários minutos, duas barras de progresso poderão ser usadas, uma que mostra o progresso geral de uma operação e outra para a progressão da etapa atual. Por exemplo, se um programa de instalação estiver copiando vários arquivos, uma barra de progresso poderá ser usada para indicar quanto tempo o processo inteiro leva enquanto um segundo pode indicar qual percentual do arquivo ou diretório atual está sendo copiado. Não relate mais de cinco operações ou processos simultâneos usando barras de progresso empilhadas. Se você tiver mais de cinco operações ou processos simultâneos a serem relatados, use uma caixa de diálogo modal com um botão Cancelar e relate os detalhes de progresso para o Janela de Saída.

##### <a name="textual-descriptions"></a>Descrições textuais
 Use uma descrição textual para acompanhar o que está acontecendo e o tempo estimado para conclusão. Se for impossível determinar quanto tempo uma operação levará, uma escolha melhor para fornecer comentários pode ser um ícone animado em vez de uma barra de progresso.

 O Visual Studio fornece uma barra de progresso padrão na barra de status que pode ser usada por qualquer produto integrado ao Visual Studio. Para obter descrições textuais do que está acontecendo enquanto a barra de progresso é animada, o texto da barra de status pode ser atualizado.

#### <a name="other-progress-indicators"></a>Outros indicadores de progresso

##### <a name="ants-animated-horizontal-dots"></a>Ants (pontos horizontais animados)
 ![Ants de progresso](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903-01_Ants")

 "Ants", pontos horizontais animados fornecem uma referência visual para um processo de servidor de viagem de ida e volta indeterminado.

##### <a name="spinner-progress-ring"></a>Controle giratório (anel de progresso)
 ![Controle giratório de progresso](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903-02_Spinner")

 O controle giratório (também conhecido como "anel de andamento") é um indicador de progresso indeterminado usado principalmente em relação à interface do usuário contextual. Exiba um controle giratório em proximidade com seu conteúdo relacionado, como um cabeçalho de categoria textual, um sistema de mensagens ou um controle.

##### <a name="cursor-feedback"></a>Comentários do cursor
 Para operações que levam entre 2-7 segundos, forneça comentários sobre o cursor. Normalmente, isso significa usar o cursor de espera fornecido pelo sistema operacional. Para obter diretrizes, consulte a [Propriedade cursores. Wait](/dotnet/api/system.windows.input.cursors.wait)do artigo do MSDN.

#### <a name="progress-indicator-locations"></a>Locais do indicador de progresso

##### <a name="status-bar"></a>Barra de Status
 A barra de status fornece ao seu aplicativo um lugar para exibir mensagens e informações úteis para o usuário sem interromper o trabalho do usuário. Normalmente exibido na parte inferior de uma janela, o status de progresso será um painel de dicas de ferramenta que inclui uma mensagem sobre a medida de progresso em combinação com um indicador de barra de progresso.

 ![Barra de status com barra de progresso](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903-03_StatusBarProgressBar")

 **Barra de status com barra de progresso**

 ![Barra de status com mensagens](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903-04_StatusBarMessage")

 **Barra de status com descrição textual**

##### <a name="infobar"></a>Barra
 Semelhante à barra de status, a barra de informações fornece notificação contextual e mensagens, que também podem ser emparelhadas com indicadores de progresso indeterminados, como a barra de progresso ou o controle giratório. A barra de informações não deve fornecer uma indicação de progresso de nível granular ou de progresso de destérmino. Consulte [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars).

 ![Barra de barra com mensagem de progresso e mensagens](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903-05_InfoBar")

 **Barra de texto com descrição de barras e de progresso**

 ![Barra de conteúdo dentro de uma janela](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903-06_InfoBarInWindow")

##### <a name="inline"></a>Embutido
 A indicação de progresso embutido pode ser representada por qualquer um dos tipos de carregador de progresso. Normalmente, o indicador de progresso é emparelhado com mensagens, mas isso não é um requisito.

 ![Controle giratório em andamento embutido](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903-07_InlineSpinner")

 **Controle giratório combinado com descrição textual**

 ![Barras de progresso empilhadas embutidas](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903-08_InlineStackedProgress")

 **Desencerrar barras de progresso empilhadas**

 ![Mensagens em andamento em linha](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903-09_InlineText")

 **Gerenciador de Servidores texto embutido: atualizando...**

##### <a name="tool-windows"></a>Janelas da ferramenta
 A indicação de progresso global é representada por uma barra de progresso indeterminada posicionada diretamente abaixo da barra de ferramentas.

 ![Barra de progresso global indeterminado](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903-23_GlobalIndeterminate")

 **Barra de progresso global indeterminado Team Explorer**

##### <a name="dialogs"></a>Diálogos
 As caixas de diálogo podem conter qualquer um dos tipos de carregador de progresso. Os indicadores de progresso podem ser emparelhados com mensagens, bem como combinados com vários níveis de indicação de progresso para representar granular e subprocessos.

 ![Caixa de diálogo com vários tipos de indicador de progresso](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903-11_Dialog")

 **Caixa de diálogo do Visual Studio com processos simultâneos e vários tipos de indicador de progresso**

 ![Caixa de diálogo com carregador de progresso e mensagens](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903-12_Dialog2")

 **Caixa de diálogo do Visual Studio com carregador de progresso e comando embutido de mensagens**

##### <a name="document-well"></a>Bem-documento
 Bem, o documento pode exibir vários tipos de carregador de progresso em combinação com controles.

 ![Mensagem de progresso em documento bem](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903-13_DocumentWell")

 **Barra de progresso indeterminada abaixo da barra de ferramentas**

##### <a name="output-window"></a>Janela de saída
 A janela de saída é apropriada para manipular a progressão de processo e o status de progresso em andamento por meio de mensagens textuais embutidas. Você deve usar a barra de status junto com qualquer relatório de progresso de janela de saída.

 ![Mensagens de progresso no Janela de Saída](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903-14_OutputWindow")

 **Janela de Saída com status de processo em andamento e mensagens de espera**

## <a name="infobars"></a><a name="BKMK_Infobars"></a> Infobars

### <a name="overview"></a>Visão geral
 O Infobars dá ao usuário um indicador perto do ponto de atenção e o uso do controle da barra de forma compartilhada garante a consistência na aparência e na interação visual.

 ![Barra](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")

 **Infobars no Visual Studio**

#### <a name="appropriate-uses-for-an-infobar"></a>Usos apropriados para uma barra de erro

- Para dar ao usuário uma mensagem sem bloqueio, mas importante, relevante para o contexto atual

- Para indicar que a interface do usuário está em um determinado Estado ou condição que transporta algumas implicações de interação, como a depuração histórica

- Para notificar o usuário de que o sistema detectou problemas, como quando uma extensão está causando problemas de desempenho

- Para fornecer ao usuário uma maneira de agir facilmente, como quando o editor detecta que um arquivo tem tabulações e espaços mistos

##### <a name="do"></a>Você deve

- Mantenha o texto da mensagem de barra de nome curto e até o ponto.

- Mantenha o texto em links e botões sucinto.

- Verifique se as opções de "ação" que você fornece aos usuários são mínimas, mostrando apenas as ações necessárias.

##### <a name="dont"></a>Não:

- Use uma barra de ferramentas para oferecer comandos padrão que devem ser colocados em uma barra de ferramentas.

- Use uma barra de entrada no lugar de uma caixa de diálogo modal.

- Crie uma mensagem flutuante fora de uma janela.

- Use vários infobars em vários locais na mesma janela.

#### <a name="can-multiple-infobars-show-at-the-same-time"></a>É possível mostrar várias infobars ao mesmo tempo?
 Sim, vários infobars podem ser mostrados ao mesmo tempo. Eles serão exibidos na primeira ordem fornecida pela primeira vez, com a primeira barra de exibição exibida na parte superior e infobars adicionais mostrados abaixo.

 O usuário verá um máximo de três infobars de cada vez, após o qual, se mais infobars estiverem disponíveis, a região de barra de informações se tornará rolável.

### <a name="creating-an-infobar"></a>Criando uma barra de erro
 A barra de espaço tem quatro seções, da esquerda para a direita:

- **Ícone:** É aqui que você adicionaria qualquer ícone que deseja exibir para a barra de exibição, como um ícone de aviso.

- **Texto:** Você pode adicionar texto para descrever o cenário/situação em que o usuário está, juntamente com os links dentro do texto, se necessário. Lembre-se de manter o texto sucinto.

- **Ações:** Esta seção deve conter links e botões para ações que o usuário pode executar em sua barra de entrada.

- **Botão fechar:** A última seção à direita pode ter um botão fechar.

#### <a name="creating-a-standard-infobar-in-managed-code"></a>Criando uma barra de entrada padrão no código gerenciado
 A classe InfoBarModel pode ser usada para criar uma fonte de dados para uma barra de código. Use um destes quatro construtores:

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

 Veja um exemplo que cria um InfoBarModel com algum texto com um hiperlink, um botão de ação e um ícone.

 ![Barra de somente com hiperlink](../../extensibility/ux-guidelines/media/0904-02_infobarhyperlink.png "0904-02_InfobarHyperlink")

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

#### <a name="creating-a-standard-infobar-in-native-code"></a>Criando uma barra de entrada padrão no código nativo
 Implemente a interface IVsInfoBar para fornecer uma barra de uma base de código nativo.

```
public interface IVsInfoBar
{
    IVsInfoBarActionItemCollection ActionItems { get; }
    ImageMoniker Image { get; }
    bool IsCloseButtonVisible { get; }
    IVsInfoBarTextSpanCollection TextSpans { get; }
}

```

#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>Obtendo um UIElement de barra de noções de uma barra de noções
 A implementação de InfoBarModel ou IVsInfoBar são modelos de dados que devem ser transformados em um UIElement para serem mostrados na interface do usuário. Um UIElement pode ser recuperado com o serviço SVsInfoBarUIFactory/IVsInfoBarUIFactory.

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
 Infobars pode ser mostrado em um ou mais dos seguintes locais:

- Janelas da ferramenta

- Dentro de uma guia de documento

> [!IMPORTANT]
> É possível posicionar uma barra de informações para fornecer uma mensagem sobre o contexto global. Isso seria exibido entre barras de ferramentas e o documento bem. Isso não é recomendado porque causa problemas com "Jump and automáticas" do IDE e deve ser evitado, a menos que seja absolutamente necessário e apropriado.

#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>Colocando uma barra de entrada em um ToolWindowPane
 O método ToolWindowPane. AddInfoBar (IVsInfoBar) pode ser usado para adicionar uma barra de ferramentas a uma janela de ferramenta. Essa API pode adicionar um IVsInfoBar (do qual InfoBarModel é uma implementação padrão) ou um Ivsuielement;.

#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>Colocando uma barra de entrada em um documento ou não ToolWindowPane
 Para colocar uma barra de espaço em qualquer IVsWindowFrame, use a propriedade VSFPROPID_InfoBarHost para obter o IVsInfoBarHost para o quadro e, em seguida, adicione o UIElement da barra de propriedades.

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

#### <a name="placing-an-infobar-in-the-main-window"></a>Colocando uma barra de entrada na janela principal
 Para colocar uma barra de espaço na janela principal, use a VSSPROPID_MainWindowInfoBarHost do serviço IVsShell para obter a IVsInfoBarHost da janela principal e, em seguida, adicione o UIElement da barra de espaço a ela.

### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>Saberei quando o usuário executar uma ação na minha barra de opinião?
 Sim, retornaremos todas as ações de evento ao autor da barra de permissões. Em seguida, o autor da barra de permissões deve agir no IDE com base na seleção do usuário na barra de permissões. Infobars será removido automaticamente do host cujo botão de fechamento foi clicado, mas trabalho adicional será necessário se outros Infobars precisarem ser removidos após o fechamento. A telemetria também precisará ser registrada independentemente por cada barra de consulta.

#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>Recebendo eventos de barra de entrada em um ToolWindowPane
 ToolWindowPane tem dois eventos para infobars. O evento InfoBarClosed é gerado quando uma barra de erro no ToolWindowPane é fechada. O evento InfoBarActionItemClicked é gerado quando um hiperlink ou botão dentro da barra de uma é clicado.

#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>Recebendo eventos de barra de mensagens diretamente do UIElement
 IVsInfoBarUIElement. Advise pode ser usado para assinar eventos diretamente do UIElement da barra de erro. A implementação de IVsInfoBarUIEvents permitirá que o autor receba eventos de fechamento e de clique.

```
public interface IVsInfoBarUIEvents
{
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);
}

```

## <a name="error-validation"></a><a name="BKMK_ErrorValidation"></a> Validação de erro
 Quando um usuário insere informações que não são aceitáveis, por exemplo, quando um campo obrigatório é ignorado ou quando os dados são inseridos no formato incorreto, é melhor usar a validação de controle ou comentários perto do controle em vez de usar uma caixa de diálogo de erro de Popup de bloqueio.

### <a name="field-validation"></a>Validação do campo
 A validação de formulário e campo consiste em três componentes: um controle, um ícone e uma dica de ferramenta. Embora vários tipos de controles possam usar isso, uma caixa de texto será usada como exemplo.

 ![Validação de campo &#40;&#41;em branco ](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905-01_FieldValidation")

 Se o campo for necessário, deve haver um texto de marca d' água indicando **\<Required>** e o plano de fundo do campo deve ser amarelo claro (VSColor: `Environment.ControlEditRequiredBackground` ) e o primeiro plano deve ser cinza (VSColor: `Environment.ControlEditRequiredHintText` ):

 ![Validação de campo com o rótulo "obrigatório"](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905-02_FieldValidationRequired")

 O programa pode determinar se o controle está em um estado de *conteúdo inválido inserido* quando o foco é movido para outro controle ou quando o usuário clica em um botão de confirmação [OK] ou quando o usuário salva o documento ou formulário.

 Quando o estado do conteúdo inválido é determinado, um ícone aparece dentro do controle ou apenas ao lado dele. Uma dica de ferramenta que descreve o erro deve aparecer ao focalizar o ícone ou o controle. Além disso, uma borda de 1 pixel deve aparecer ao contrário do controle que está criando o estado inválido.

 ![Especificações de layout de validação de campo](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905-03_LayoutSpecs")

 **Especificações de layout para validação de campo**

#### <a name="acceptable-variations-for-icon-location"></a>Variações aceitáveis para o ícone local
 Há inúmeros casos exclusivos nos quais os usuários precisam ser informados sobre erros de validação. Considerando o tipo de controle e a configuração da interface do usuário, escolha o posicionamento do ícone apropriado à sua situação.

 ![Locais aceitáveis para o ícone local](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905-04_IconLocation")

 **Variações aceitáveis para locais de ícone de validação de campo**

#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>Validação que requer uma viagem de ida e volta para um servidor ou conexão de rede
 Em alguns casos, uma viagem de ida e volta para o servidor é necessária para verificar o conteúdo, e seria importante mostrar os Estados de progresso, verificação e erro do usuário. A figura abaixo mostra um exemplo desse caso e da interface do usuário recomendada.

 ![Validação envolvendo uma viagem de ida e volta para um servidor](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905-05_RoundTrip")

 **Validação envolvendo uma viagem de ida e volta para um servidor**

 Observe que o espaço disponível adequado à direita do controle deve ser fornecido para acomodar a "verificação..." e o texto "retry".

#### <a name="in-place-warning-text"></a>Texto de aviso in-loco
 Quando há espaço disponível para colocar a mensagem de erro próxima ao controle em um estado de erro, isso é preferível a usar apenas a dica de ferramenta.

 ![Aviso em&#45;local](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905-06_InPlaceWarning")

 **Texto de aviso in-loco**

#### <a name="watermarks"></a>Marcas d' água
 Às vezes, um controle inteiro ou uma janela está em um estado de erro. Nessa situação, use uma marca-d ' água para indicar o erro.

 ![Água](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")

 **Validação do campo de marca d' água**
