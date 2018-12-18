---
title: Uso de GPU | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d8265ae81b5ea1c6395af352f8f981f41f77cea8
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220938"
---
# <a name="gpu-usage"></a>Uso de GPU

Use a ferramenta Uso de GPU no Hub de Desempenho e Diagnóstico do Visual Studio para entender melhor o uso de hardware de alto nível do aplicativo Direct3D. Ela ajuda a ver se o desempenho do aplicativo está associado à CPU ou à GPU e a obter informações sobre como você pode usar o hardware da plataforma com mais eficiência. O Uso de GPU dá suporte a aplicativos que usam o Direct3D 12, Direct3D 11 e Direct3D 10; ele não dá suporte a outras APIs de gráficos como Direct2D ou OpenGL.

Esta captura de tela mostra a janela do **Relatório de Uso de GPU**:

![O relatório Uso de GPU, com as linhas do tempo CPU e GPU](media/gfx_diag_gpu_usage_report.png "gfx_diag_gpu_usage_report")

## <a name="requirements"></a>Requisitos

Os seguintes requisitos para usar a ferramenta Uso de GPU são adicionados aos requisitos de Diagnóstico de gráficos.

- Uma GPU e drivers que dão suporte à instrumentação de intervalo necessária.

  > [!NOTE]
  > Para obter mais informações sobre o hardware e os drivers com suporte, consulte [Suporte de hardware e driver](#hwsupport) ao final deste documento.

  Para obter mais informações sobre os requisitos do Diagnóstico de Gráficos, consulte [Introdução](../debugger/graphics/getting-started-with-visual-studio-graphics-diagnostics.md).

## <a name="using-the-gpu-usage-tool"></a>Usando a ferramenta Uso de GPU

 Quando você executa o aplicativo na ferramenta Uso de GPU, o Visual Studio cria uma sessão de diagnóstico que apresenta gráficos de informações de alto nível sobre o desempenho de renderização e o uso de GPU do aplicativo em tempo real.

**Para iniciar a ferramenta Uso de GPU:**

1. No menu principal, escolha **Depurar** e, em seguida, **Desempenho e Diagnóstico** (teclado: pressione Alt + F2).

2. No hub Desempenho e Diagnóstico, marque a caixa ao lado de **Uso de GPU**. Opcionalmente, marque as caixas ao lado de outras ferramentas nas quais você esteja interessado. É possível executar várias ferramentas de Desempenho e Diagnóstico simultaneamente para obter uma visão mais completa do desempenho do aplicativo.

    ![Escolha as ferramentas de diagnóstico que você deseja usar.](media/gfx_diag_diagsession_tools.png "gfx_diag_diagsession_tools")

   > [!NOTE]
   > Nem todas as ferramentas de Desempenho e Diagnóstico podem ser usadas ao mesmo tempo.

3. Escolha o botão azul **Iniciar** na parte inferior do hub Desempenho e Diagnóstico para executar o aplicativo nas ferramentas selecionadas.

   As informações de alto nível exibidas em tempo real incluem o intervalo de quadros, a taxa de quadros e o uso de GPU. Cada uma dessas informações é apresentada em gráficos de maneira independente, mas usam uma escala de tempo comum para que você possa estabelecer uma relação fácil entre elas.

   Os grafos **Tempo de quadro (ms)** e **Quadros por segundo (FPS)** têm duas linhas horizontais vermelhas que mostram metas de desempenho de 60 e 30 quadros por segundo. No grafo **Tempo de quadro**, o aplicativo supera a meta de desempenho quando o grafo está abaixo da linha e não alcança a meta quando o grafo está acima da linha. Para o grafo Quadros por segundo, é o oposto; seu aplicativo supera a meta de desempenho quando o grafo está acima da linha e não alcança a meta quando o grafo está abaixo da linha. Basicamente, esses grafos são usados para obter uma ideia de alto nível do desempenho do aplicativo e para identificar problemas de lentidão que talvez você deseje investigar – como uma queda repentina na taxa de quadros ou um pico na Utilização de GPU.

   Enquanto o aplicativo é executado na ferramenta Uso de GPU, a sessão de diagnóstico também coleta informações detalhadas sobre eventos de gráficos que foram executados na GPU. Essas informações são usadas para gerar um relatório mais granular de como o aplicativo utiliza o hardware. Como esse relatório leva algum tempo para ser gerado com base nas informações coletadas, ele só estará disponível depois que a sessão de diagnóstico concluir a coleta de informações.

   Quando desejar examinar um problema de desempenho ou de utilização mais detalhadamente, pare a coleta de informações de desempenho para que o relatório possa ser gerado.

**Para gerar e exibir o Relatório de Uso de GPU:**

1. Na parte inferior da janela da sessão de diagnóstico, escolha o link **Parar Coleta** ou pressione **Parar** no canto superior esquerdo.

   ![Colete informações de intervalo de GPU e CPU.](media/gfx_diag_gpu_usage_collect.png "gfx_diag_gpu_usage_collect")

2. Na parte superior do relatório, selecione uma seção de um dos gráficos que mostra o problema que você deseja investigar. A seleção pode ser feita em até 3 segundos; seções mais longas serão truncadas no início.

   ![Pós&#45;coleta, selecionar um intervalo para exibir os detalhes](media/gfx_diag_gpu_usage_select1.png "gfx_diag_gpu_usage_select1")

3. Na parte inferior do relatório, escolha o link **exibir detalhes** na mensagem **... clique aqui para exibir detalhes de uso de GPU para esse intervalo** para exibir uma linha do tempo detalhada da seleção.

   ![Pós&#45;coleção, com o intervalo selecionado](media/gfx_diag_gpu_usage_select2.png "gfx_diag_gpu_usage_select2")

   Essa seleção abre um novo documento com guias que contém o relatório. O relatório Uso de GPU ajuda você a ver quando um evento de gráficos é iniciado na CPU, quando ele atinge a GPU e quanto tempo a GPU leva para executá-lo. Essas informações podem ajudá-lo a identificar gargalos e oportunidades de aumento de paralelismo no código.

<!-- VERSIONLESS -->
## <a name="export-to-gpuview-or-windows-performance-analyzer"></a>Exportar para o GPUView ou o Windows Performance Analyzer

Começando com o Visual Studio 2017, é possível abrir esses dados com [GPUView](/windows-hardware/drivers/display/using-gpuview) e com o [Windows Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer). Basta selecionar os links **Abrir no GpuView** ou **Abrir no WPA** localizados no canto inferior direito da sessão de diagnóstico.

![Abrir em...](media/gfx_diag_open_in.png)
<!-- /VERSIONLESS -->

## <a name="using-the-gpu-usage-report"></a>Usando o relatório Uso de GPU

A parte superior do relatório Uso de GPU exibe linhas do tempo da atividade de processamento da CPU, atividade de renderização da GPU e atividade de cópia da GPU. Essas linhas do tempo são divididas por barras verticais cinza que indicam o vsync da exibição. A frequência das barras corresponde à taxa de atualização de um dos vídeos (selecionados com a lista suspensa **Exibição**) dos quais esses dados de Uso de GPU foram coletados. Como a exibição pode ter uma taxa de atualização mais alta do que a meta de desempenho do aplicativo, talvez não haja uma relação um para um entre o vsync e a taxa de quadros que você deseja que o aplicativo atinja. Para atender sua meta de desempenho, um aplicativo deve concluir todo o processamento, fazer a renderização e fazer uma chamada Present() à taxa de quadros de destino. Contudo, o quadro renderizado não será exibido até o próximo vsync após Present().

A parte inferior exibe uma listagem dos eventos de gráficos que ocorreram durante o período do relatório.

Esta é a janela **Relatório de Uso de GPU**:

![O relatório Uso de GPU, com as linhas do tempo CPU e GPU](media/gfx_diag_gpu_usage_report.png "gfx_diag_gpu_usage_report")

Quando você seleciona um evento na parte inferior do relatório, um marcador é exibido nos eventos correspondentes nas respectivas linhas do tempo. Normalmente, um evento em um thread da CPU mostra a chamada à API, enquanto outro evento em uma das linhas do tempo da GPU mostra quando a GPU concluiu a tarefa. Da mesma forma, quando você seleciona um evento em uma linha do tempo, o relatório realça o evento correspondente na parte inferior do relatório. Quando as linhas do tempo são reduzidas na parte superior do relatório, apenas os eventos mais demorados são visíveis. Para ver os eventos que têm uma duração menor, amplie as linhas do tempo usando Ctrl + roda no dispositivo apontador ou o controle de colocação em escala no canto inferior esquerdo do painel superior. Também é possível arrastar o conteúdo do painel de linha do tempo para percorrer os eventos registrados.

Para ajudar a encontrar o que você está procurando, filtre o Relatório Uso da GPU com base em nomes de processo, IDs do Thread e o nome do evento. Além disso, é possível escolher qual taxa de atualização da exibição determina as linhas do vsync. Será possível classificar os eventos hierarquicamente se o aplicativo usar a interface [ID3DUserDefinedAnnotation](/windows/desktop/api/d3d11_1/nn-d3d11_1-id3duserdefinedannotation) para agrupar comandos de renderização.

 Estes são mais detalhes:

|Controle de filtro|Descrição|
|--------------------|-----------------|
|**Processo**|O nome do processo de seu interesse. Todos os processos que usaram a GPU durante a sessão de diagnóstico são incluídos nessa lista suspensa. A cor associada ao processo nessa lista suspensa é a cor da atividade do thread nas linhas do tempo abaixo.|
|**Thread**|A ID do thread de seu interesse. Em um aplicativo multi-threaded, essas informações podem ajudá-lo a isolar threads específicos que pertencem ao processo de seu interesse. Os eventos associados ao thread selecionado são realçados em cada linha do tempo.|
|**Vídeo**|O número do vídeo cuja taxa de atualização é exibida **Observação:** alguns drivers podem ser configurados para apresentar vários vídeos físicos como um único vídeo virtual grande. Talvez você veja apenas um vídeo listado, mesmo se o computador tiver vários vídeos anexados.|
|**Filtrar**|Palavras-chave de seu interesse. Os eventos na parte inferior do relatório incluirão apenas aqueles que correspondem a uma palavra-chave, no todo ou em parte. É possível especificar várias palavras-chave separando-as com um ponto-e-vírgula (;).|
|**Classificação de Hierarquia**|Uma caixa de seleção que indica se as hierarquias de eventos – definidas por meio de marcadores do usuário – são preservadas ou ignoradas.|

 A lista de eventos na parte inferior do Relatório de Uso de GPU exibe os detalhes de cada evento.

|Column|Descrição|
|------------|-----------------|
|**Nome do Evento**|O nome do evento de gráficos. Normalmente, um evento corresponde a um evento em uma linha do tempo do thread de CPU e a um evento de linha do tempo de GPU.<br /><br /> Os nomes de eventos podem ser “não atribuídos” se o Uso de GPU não pôde determinar o nome de um evento. Para obter mais informações, consulte a observação abaixo desta tabela.|
|**Início da CPU (ns)**|A hora em que o evento foi iniciado na CPU com uma chamada a uma API do Direct3D. O tempo é medido em nanossegundos, relativo à hora de início do aplicativo.|
|**Início da GPU (ns)**|A hora em que o evento foi iniciado na GPU. O tempo é medido em nanossegundos, relativo à hora de início do aplicativo.|
|**Duração da GPU (ns)**|O tempo que o evento levou para ser concluído na GPU, em nanossegundos.|
|**Nome do Processo**|O nome do aplicativo do qual o evento foi originado.|
|**ID do Thread**|A ID do thread da qual o evento foi obtido.|

> [!IMPORTANT]
> Se a GPU ou o driver não derem suporte aos recursos de instrumentação necessários, todos os eventos serão exibidos como "não atribuídos". Lembre-se de atualizar o driver da GPU e tente novamente caso ocorra esse problema. Para obter mais informações, consulte [Suporte de hardware e driver](#hwsupport) abaixo.

## <a name="gpu-usage-settings"></a>Configurações de Uso de GPU

É possível configurar a ferramenta Uso de GPU para adiar a coleta de informações de criação de perfil, em vez de iniciar a coleta de informações logo após a inicialização do aplicativo. Como o tamanho das informações de criação de perfil pode ser significativo, essa ação será útil quando você souber que os problemas de lentidão no desempenho do aplicativo apenas serão exibidos posteriormente.

**Para adiar a criação de perfil após a inicialização do aplicativo:**

1. No menu principal, escolha **Depurar** e, em seguida, **Desempenho e Diagnóstico** (teclado: pressione Alt + F2).

2. No hub Desempenho e Diagnóstico, siga o link **Configurações** ao lado de **Uso de GPU**.

3. Em **Configuração de Criação de Perfil da GPU**, na página de propriedades **Geral**, desmarque a caixa de seleção **Iniciar a criação de perfil após a inicialização do aplicativo** para adiar a criação de perfil.

   ![Configurar o início da coleta de Uso de GPU](media/gfx_diag_gpu_usage_config.png "gfx_diag_gpu_usage_config")

> [!IMPORTANT]
> Não há suporte para o adiamento da criação de perfil em aplicativos Direct3D 12.

Depois de executar seu aplicativo na ferramenta Uso de GPU, um link adicional se tornará disponível na parte inferior da janela de ferramentas Uso de GPU. Para iniciar a coleta de informações de criação de perfil, escolha o link **Iniciar** na mensagem **Iniciar coleta de dados detalhados de Uso de GPU adicionais**.

## <a name="hwsupport"></a> Suporte de hardware e driver

Há suporte para os seguintes hardware e drivers de GPU:

|Fornecedor|Descrição da GPU|Versão de driver necessária|
|------------|---------------------|-----------------------------|
|Intel®|Processadores Intel® Core da 4ª geração (“Haswell”)<br /><br /> -   Intel® HD Graphics (GT1)<br />-   Intel® HD Graphics 4200 (GT2)<br />-   Intel® HD Graphics 4400 (GT2)<br />-   Intel® HD Graphics 4600 (GT2)<br />-   Intel® HD Graphics P4600 (GT2)<br />-   Intel® HD Graphics P4700 (GT2)<br />-   Intel® HD Graphics 5000 (GT3)<br />-   Intel® Iris™ Graphics 5100 (GT3)<br />-   Intel® Iris™ Pro Graphics 5200 (GT3e)|- (usar os últimos drivers)|
|AMD®|A maioria, a partir da AMD Radeon™ HD série 7000 (excluindo AMD Radeon™ HD 7350-7670)<br /><br /> Aceleradores de GPUs AMD Radeon™, AMD FirePro™ e AMD FirePro com a arquitetura GCN (Graphics Core Next).<br /><br /> APUs (Unidades de Processamento Acelerado) AMD® série E e AMD série A com a arquitetura GCN (Graphics Core Next) (“Kaveri”, “Kabini”, “Temash”, “Beema”, “Mullins”)|14.7 RC3 ou superior|
|NVIDIA®|A maioria, a partir da NVIDIA® GeForce® série 400.<br /><br /> Aceleradores de GPUs NVIDIA® GeForce®, NVIDIA Quadro® e NVIDIA® Tesla™ com a arquitetura Fermi™, Kepler™ ou Maxwell™.|343.37 ou superior|

 No momento, não há suporte para configurações de GPU múltipla, como NVIDIA® SLI™ e AMD Crossfire™. Há suporte para a configuração de elementos gráficos híbridos, como NVIDIA® Optimus™ e AMD Enduro™.

## <a name="see-also"></a>Consulte também

- [Resolver problemas difíceis de elementos gráficos no jogo usando as ferramentas do DirectX (vídeo)](https://channel9.msdn.com/Events/GDC/GDC-2015/Solve-the-Tough-Graphics-Problems-with-your-Game-Using-DirectX-Tools)
- [Ferramenta Uso de GPU no Visual Studio (vídeo)](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2014/715)
- [Ferramenta Uso de GPU no Visual Studio 2013 Atualização 4 CTP1 (blog)](https://blogs.msdn.microsoft.com/vcblog/2014/09/04/gpu-usage-tool-in-visual-studio-2013-update-4-ctp1/)
- [Uso de GPU para o DirectX no Visual Studio (blog)](https://blogs.msdn.microsoft.com/ianhu/2014/12/16/gpu-usage-for-directx-in-visual-studio/)
- [GPUView](/windows-hardware/drivers/display/using-gpuview)
- [Windows Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer)