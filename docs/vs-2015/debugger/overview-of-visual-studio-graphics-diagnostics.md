---
title: Visão geral do diagnóstico de gráficos do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ddd429d9-ac70-4ac4-9e69-299c6ea2df09
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4716ac398916a869fe122b54f829bbfda2f9911b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810436"
---
# <a name="overview-of-visual-studio-graphics-diagnostics"></a>Visão geral do diagnóstico de gráficos do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio *diagnóstico de gráficos* é um conjunto de ferramentas de registro e, em seguida, analisando problemas de desempenho e a renderização em aplicativos Direct3D. Diagnóstico de gráficos pode ser usado em aplicativos que estão sendo executadas localmente no seu PC com Windows, em um emulador de dispositivo do Windows ou em um dispositivo ou computador remoto.  
  
## <a name="using-graphics-diagnostics-to-debug-rendering-problems"></a>Usando o Diagnóstico de Gráficos para depurar problemas de renderização  
 Depurar problemas de renderização em um aplicativo cheio de recursos gráficos não é tão simples quanto iniciar um depurador e percorrer alguns códigos. Em cada quadro, centenas de milhares de pixels exclusivos são produzidos, cada um de acordo com um conjunto complexo de estados, dados, parâmetros e códigos, e dentre eles, talvez apenas alguns pixels exibirão o problema que você está tentando diagnosticar. Para complicar ainda mais, o código que gera cada pixel é executado em hardware especializado que processa centenas de pixels paralelamente. As ferramentas e técnicas tradicionais de depuração (cujo aproveitamento é difícil mesmo no código em thread bastante simples) são ineficazes quando se deparam com grandes quantidades de dados.  
  
 As ferramentas de Diagnóstico de Gráficos no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] foram desenvolvidas para ajudar a localizar problemas de renderização, a começar pelos artefatos visuais que indicam o problema e rastreiam de volta para a origem do problema focando apenas o código de sombreador, os estágios de pipeline, as chamadas de desenho e o estado do dispositivo que são relevantes, no próprio código-fonte do aplicativo.  
  
## <a name="directx-version-compatibility"></a>Compatibilidade de versão do DirectX  
 Diagnóstico de gráficos oferece suporte a aplicativos que usam o Direct3D 12, Direct3D 11 e Direct3D 10 e fornece suporte limitado para aplicativos que usam Direct2D. Ele não oferece suporte a aplicativos que usam versões anteriores do Direct3D, DirectDraw ou outras APIs gráficas.  
  
### <a name="windows-10-and-direct3d-12"></a>Windows 10 e Direct3D 12  
 A próxima versão do Direct3D, apresenta o Windows 10 *Direct3D 12*, que é substancialmente diferente do Direct3D 10 e 11 do Direct3D. Essas diferenças trazer DirectX de volta para o alinhamento com hardwares gráficos modernos e liberando todo o seu potencial, mas também trazer grandes mudanças de API e colocar o maior responsabilidade para o programador para gerenciar a contenção e tempos de vida do recurso. Ter excelentes ferramentas de depuração é crucial para ajudar os programadores de gráficos a tornar essa transição, portanto, o diagnóstico de gráficos no Visual Studio 2015 oferece suporte de Direct3D12 certo desde o início. Apesar das diferenças, o diagnóstico de gráficos com o Direct3D 12 mantém paridade de recursos com o diagnóstico de gráficos com o Direct3D 11.2, com a exceção atual do recurso de análise de quadros. Em breve, suporte para análise de quadro no Direct3D 12 será adicionado, seguido de novas ferramentas de diagnóstico para ajudar a resolver os novos tipos de erros que podem ocorrer no Direct3D 12.  
  
 Windows 10 também mantém o suporte para versões anteriores do Direct3D e os jogos e aplicativos que dependem delas. Diagnóstico de gráficos no Visual Studio 2015 continua a dar suporte a Direct3D 10 e 11 do Direct3D no Windows 10, bem como no Windows 8.1.  
  
### <a name="windows-81-and-direct3d-112"></a>Windows 8.1 e Direct3D 11.2  
 No [!INCLUDE[win81](../includes/win81-md.md)], o DirectX 11.2 apresenta novos recursos que incluem suporte para capturar informações gráficas ao longo do tempo de execução. [!INCLUDE[win81](../includes/win81-md.md)] usa a nova captura baseada em tempo de execução — conhecida como *captura robusta*— exclusivamente para todas as versões do DirectX que [!INCLUDE[win81](../includes/win81-md.md)] dá suporte. A captura robusta também oferece suporte a novos recursos do Direct3D 11.2.  
  
### <a name="limited-direct2d-support"></a>Suporte limitado ao Direct2D  
 Como o Direct2D é uma API de modo de usuário que foi criada com base no Direct3D, você pode usar o Diagnóstico de Gráficos para ajudar na depuração de problemas de renderização em aplicativos que usam o Direct2D. No entanto, como apenas os eventos do Direct3D subjacentes são gravados, em vez de eventos do Direct2D de nível mais alto, os eventos do Direct2D não aparecerão na Lista de Eventos de Gráficos. Além disso, como a relação entre os eventos do Direct2D e os eventos resultantes do Direct3D nem sempre é clara, usar o Diagnóstico de Gráficos para depurar problemas de renderização em aplicativos que usam o Direct2D não é algo simples. Ainda assim, você pode usar o Diagnóstico de Gráficos para obter informações sobre problemas de renderização de nível baixo em aplicativos que usam o Direct2D.  
  
## <a name="graphics-diagnostics-features-in-visual-studio"></a>Recursos de diagnóstico de gráficos do Visual Studio  
 Diagnóstico de gráficos tem uma interface dedicada — a janela do analisador de gráficos — para diagnosticar problemas de renderização, mas ele também adiciona o algumas ferramentas para a interface do Visual Studio.  
  
### <a name="the-graphics-toolbar-visual-studio"></a>A barra de ferramentas de gráficos (Visual Studio)  
 A barra de ferramentas gráficos fornece acesso rápido aos comandos de diagnóstico de gráficos.  
  
 O **iniciar diagnóstico** botão executa o aplicativo em Diagnóstico de gráficos. Quando um aplicativo está em execução no diagnóstico de gráficos, o **capturar o próximo quadro processado** botão está habilitado.  
  
### <a name="diagnostics-capture-interface"></a>Captura de diagnóstico de interface  
 Quando você executa seu aplicativo em Diagnóstico de gráficos, o Visual Studio exibe uma interface de sessão de diagnóstico que você pode usar para capturar quadros e que também exibe a atual carga de CPU e GPU. A carga de CPU e GPU é exibida para ajudá-lo a identificar os quadros que você talvez queira capturar devido a suas características de desempenho, em vez de erros de renderização.  
  
 Isso não é a única maneira de capturar quadros entanto. Você também pode capturar quadros usando a interface de captura programática ou usando o programa de captura de linha de comando, dxcap.exe.  
  
 Ver [capturando informações de gráficos](../debugger/capturing-graphics-information.md) para obter mais informações.  
  
### <a name="gpu-usage"></a>Uso de GPU  
 Diagnóstico de gráficos também pode analisar o desempenho do seu aplicativo Direct3D. Porque a criação de perfil de dados seria inclinada por gravação de detalhes de eventos de gráficos, ela é separada da captura de quadros a serem usados examinadas com o analisador de gráficos.  
  
 Ver [uso de GPU](../debugger/gpu-usage.md) para obter mais informações.  
  
### <a name="directx-control-panel"></a>Painel de controle do DirectX  
 O painel de controle do DirectX é um componente do DirectX que você pode usar para alterar o comportamento do DirectX. Por exemplo, é possível habilitar a versão de depuração dos componentes de tempo de execução do DirectX, selecionar os tipos de mensagem de depuração que são relatados e impedir que determinados recursos de hardware gráfico sejam usados para emular um hardware menos capaz. Esse nível de controle sobre o DirectX pode ajudar você a depurar e testar seu aplicativo DirectX. É possível acessar o painel de controle do DirectX do Visual Studio.  
  
##### <a name="to-open-the-directx-control-panel"></a>Para abrir o painel de controle do DirectX  
  
-   Na barra de menus, escolha **Debug**, **gráficos**, **painel de controle do DirectX**.  
  
## <a name="graphics-analyzer"></a>Analisador de gráficos  
 O analisador de gráficos do Visual Studio é uma interface dedicada para examinar a renderização e problemas de desempenho em quadros que já capturamos. Analisador de gráficos, você encontrará várias ferramentas para ajudá-lo a explorar e compreender o comportamento de renderização de seu aplicativo. Cada ferramenta expõe um tipo diferente de informações sobre o quadro que está sendo inspecionado e as ferramentas foram projetadas para ser usado em conjunto para intuitivamente estreito-in na origem de um problema de renderização, a partir de sua aparência no framebuffer.  
  
 Esta ilustração mostra um típico layout das ferramentas no analisador de gráficos.  
  
 ![Todos os elementos gráficos janelas do depurador](../debugger/media/graphicsdebuggerwindows.png "GraphicsDebuggerWindows")  
  
### <a name="the-graphics-toolbar-graphics-analyzer"></a>A barra de ferramentas de gráficos (Analisador de gráficos)  
 A barra de ferramentas gráficos fornece acesso rápido a janelas de ferramentas do analisador de gráficos.  
  
 ![A barra de ferramentas de gráficos no modo de diagnóstico de gráficos](../debugger/media/vsg-toolbar.png "vsg_toolbar")  
  
### <a name="graphics-log-document"></a>Documento de log de gráficos  
 Dentro do analisador de gráficos, o documento de log de gráficos é a janela da ferramenta mais proeminente. Essa janela representa todos os quadros capturados executando seu aplicativo em Diagnóstico de gráficos. A partir daqui, você pode selecionar um quadro diferente para examinar ou selecione um pixel específico que você deseja examinar com a ferramenta de histórico de Pixel. A imagem de framebuffer exibida neste documento são alterados para refletir o evento selecionado no momento para que você possa ver como framebuffer é afetado ao longo do tempo.  
  
 O [documento de Log de gráficos](../debugger/graphics-log-document.md) é também o ponto de entrada para a ferramenta de análise de quadro, que ajuda você a entender o desempenho de um quadro mudando a forma como determinados aspectos de renderização são configurados e fornecendo o parâmetro de comparação de resultados para Compare com o original.  
  
### <a name="event-list"></a>Lista de eventos  
 Eventos de gráficos marcarem cada chamada à API do Direct3D e eventos definidos pelo usuário.  
  
 O [lista de eventos](../debugger/graphics-event-list.md) mostra todos os eventos de gráficos que foram registrados durante o quadro que você está examinando. Para ajudá-lo a encontrar o que é importante, a lista de eventos pode ser exibida hierarquicamente — chamada de desenho com alterações de estado recentes sob o subsequentes — ou como uma linha do tempo. Além disso, os eventos são codificadas por cores com base em fila pertençam a e você pode filtrar a lista para incluir somente os eventos que você está interessado.  
  
 Quando você seleciona um evento na lista, o restante das ferramentas de análise de gráficos refletem o estado do quadro no momento do evento. Dessa forma, você pode ver o efeito de qualquer evento na GPU. Por exemplo, você pode ver o efeito imediato de qualquer desenho chamar no framebuffer, mesmo que ele se torna obscurecido por chamadas de desenho subsequentes. Alguns eventos também têm hiperlinks que você pode seguir para ver mais detalhes sobre seus parâmetros ou objetos de recursos relacionados.  
  
### <a name="pipeline-stages"></a>Estágios de pipeline  
 Cada chamada de desenho em seu aplicativo passa pelo pipeline gráfica fornecido pelo Direct3D. Em cada estágio no pipeline, saída do estágio anterior é transformada por um pequeno programa chamada um sombreador e, em seguida, passada para o próximo estágio até que finalmente é renderizado na tela. Muitos erros de renderização ocorrerem no limite entre estágios de pipeline quando o formato de saída é diferente do que o próximo estágio espera, ou quando qualquer um estágio simplesmente produz resultados incorretos. Normalmente, só você obtém os resultados finais conforme você vê na tela e você não pode determinar facilmente a onde no pipeline ocorreu o erro.  
  
 O [estágios de Pipeline](../debugger/graphics-pipeline-stages.md) janela visualiza o resultado de cada estágio de forma independente, para que você possa determinar mais facilmente qual estágio de um problema de renderização aparece pela primeira vez no. Depois de determinar qual estágio ou seja, você pode iniciar a depuração de seu sombreador à direita da janela estágios de Pipeline.  
  
### <a name="graphics-state"></a>Estado gráfico  
 Operações de renderização dependem muito do estado que normalmente é distribuído entre vários objetos. Muitos tipos de problemas de renderização são causados por estado configurado incorretamente.  
  
 O [estado](../debugger/graphics-state.md) janela coleta as informações de estado relevantes para cada chamada de desenho junto em um único lugar para que ele é mais fácil localizar e também destaca as alterações de estado que ocorreram desde a última chamada de desenho.  
  
### <a name="pixel-history"></a>Histórico de pixel  
 Cenas complexas, não é incomum para um pixel a ser sombreado várias vezes em um único quadro. Às vezes, a cor anterior é substituídas apenas, mas outras vezes as cores são combinadas em conjunto para atingir efeitos, como transparência. Quando o resultado da combinação-los juntos não tem a aparência certa facilmente não pode determinar se é porque uma das cores estava incorreta, ou se houver um problema com a maneira como eles foram combinados. Outras vezes, um objeto pode parecer estar ausentes porque sua contribuição para o pixel foi rejeitada por algum motivo.  
  
 O [histórico de Pixel](../debugger/graphics-pixel-history.md) janela visualiza o histórico de sombreador completo de cada pixel no quadro, incluindo as contribuições rejeitadas. Para contribuições que não foram rejeitadas, ele exibe os resultados brutos de sombreador e como cada nova cor foi combinado com anterior. Com essas informações, é muito mais fácil de localizar a origem de erros em pixels que os resultados de sombreador do blend ou quando um objeto renderizado está faltando porque sua contribuição para o pixel incorretamente foi rejeitada.  
  
### <a name="event-call-stack"></a>Pilha de chamadas do evento  
 Código do sombreador não é a única fonte de problemas de renderização em um aplicativo Direct3D, às vezes, o código-fonte do seu aplicativo passa o parâmetro errado ou não configura o Direct3D é exatamente isso. Um tipo de erro que o recurso discutido anteriormente, o histórico de Pixel pode ajudá-lo a encontrar é quando um objeto renderizado está faltando porque todos os seus pixels foram rejeitados. Esse tipo de erro geralmente ocorre quando você configurado incorretamente uma configuração, chamada de desenho, como aquele que controla como o teste de profundidade é executado e você geralmente pode encontrar o erro em algum lugar na pilha de chamadas do objeto ausente.  
  
 O [pilha de chamadas do evento](../debugger/graphics-event-call-stack.md) janela exibe a pilha de chamadas completa de todos os eventos de gráficos na lista de eventos e código-fonte permite que até mesmo ir ao seu aplicativo se as informações de depuração estiverem disponível. Isso é uma ferramenta poderosa para após um erro de onde ele aparece pela primeira vez, na GPU, para onde ele foi originado no código-fonte do seu aplicativo.  
  
### <a name="object-table"></a>Tabela de objetos  
 Cada quadro provavelmente, seu aplicativo renderiza é apoiada por centenas ou mesmo milhares de objetos de recurso. Esses podem incluir os buffers de back- e renderizar destinos, texturas, buffers de vértice, buffers de índice e buffers gerais — quase tudo o que se lembra de Direct3D é um objeto.  
  
 O [tabela de objetos](../debugger/graphics-object-table.md) exibe todos os objetos que existem no momento do evento de gráficos selecionado na listam de eventos. Como a maioria dos objetos em um aplicativo típico são texturas, a lista de eventos é otimizada para mostrar os detalhes relevantes para as imagens em um relance. A coluna de tipo informa que tipo de objeto está em cada linha e a coluna de formato mostra a versão do objeto ou um subtipo. Outros detalhes também são mostrados. Alguns objetos também têm hiperlinks que você pode seguir para exibir o objeto com um visualizador mais especializado, como texturas (você pode exibir a textura como uma imagem) ou (você pode escolher como o Visualizador de buffer analisa e exibe os bytes brutos do buffer, definindo o buffer de buffers formato).  
  
### <a name="frame-analysis"></a>Análise de quadro  
 Gráficos do seu aplicativo simplesmente não precisam estar corretas – eles precisam ser muito rápidos. Até mesmo em dispositivos menos potentes, como laptops com gráficos integrados ou telefones móveis. E ainda precisam ser muito grande.  
  
 O [análise de quadros](../debugger/graphics-frame-analysis.md) ferramenta explora as otimizações de desempenho potencial automaticamente alterando o modo como o aplicativo usa o Direct3D e fornecendo os resultados do benchmark para comparação. Por exemplo, a análise de quadro pode habilitar o mapeamento de mip em cada textura, o que poderia revelar as texturas que poderiam se beneficiar com Mapeamento mip, mas atualmente não tem habilitado. No hardware que dá suporte a ele, a análise de quadros também apresenta informações coletadas dos contadores de desempenho da GPU — esse nível de informação pode identificar problemas de desempenho de nível de hardware, como números altos de vagas de busca de textura ou perdas no cache.  
  
 Mas a análise de quadro praticamente não será rápida – trata-se de obter o melhor desempenho que possível durante a mão o mínimo de qualidade visual. Às vezes, um efeito de caro ótimo aparência em um grande vídeo não faz o mesmo impacto quando exibido em tela pequena de um telefone, no qual um efeito mais simples pode ser boa da mesma forma sem descarregar a bateria. As alterações automáticas e os parâmetros de comparação que fornece análise de gráficos podem ajudá-lo a encontrar o equilíbrio que seja adequado para seu aplicativo em uma variedade de dispositivos.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramenta de captura de linha de comando](../debugger/command-line-capture-tool.md)   
 [Depurador HLSL](../debugger/hlsl-shader-debugger.md)



