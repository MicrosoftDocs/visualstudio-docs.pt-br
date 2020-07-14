---
title: Uso de GPU | Microsoft Docs
ms.date: 11/01/2018
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6aa4cce032a5eb80a11568a83c1166b5690bd688
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85279868"
---
# <a name="gpu-usage"></a>Uso de GPU

Use a ferramenta uso de GPU no Hub de desempenho e diagnóstico do Visual Studio para entender melhor o uso de hardware de alto nível de seu aplicativo do Direct3D. Ele ajuda você a ver se o desempenho do seu aplicativo é associado à CPU ou à GPU e a obter informações sobre como você pode usar o hardware da plataforma com mais eficiência. O uso de GPU dá suporte a aplicativos que usam o Direct3D 12, o Direct3D 11 e o Direct3D 10. Ele não dá suporte a outras APIs de gráficos, como Direct2D ou OpenGL.

Esta é a aparência da janela de **relatório uso da GPU** :

![Captura de tela do relatório uso de GPU, com cronogramas de CPU e GPU](media/gfx_diag_gpu_usage_report.png "gfx_diag_gpu_usage_report")

## <a name="requirements"></a>Requisitos

Além dos requisitos para Diagnóstico de Gráficos, o seguinte é necessário para usar a ferramenta de uso de GPU:

- Uma GPU e drivers que dão suporte à instrumentação de intervalo necessária.

  > [!NOTE]
  > Para obter mais informações sobre o hardware e os drivers com suporte, consulte [Suporte de hardware e driver](#hwsupport) ao final deste documento.

Para obter mais informações sobre os requisitos de Diagnóstico de Gráficos, consulte [Guia de introdução](../debugger/graphics/getting-started-with-visual-studio-graphics-diagnostics.md).

## <a name="use-the-gpu-usage-tool"></a>Usar a ferramenta de uso de GPU

Quando você executa seu aplicativo na ferramenta de uso de GPU, o Visual Studio cria uma sessão de diagnóstico. Esta sessão grafa informações de alto nível sobre o desempenho de renderização do aplicativo e uso de GPU em tempo real.

Para iniciar a ferramenta Uso de GPU:

1. No menu principal, escolha **depurar**  >  **desempenho e diagnóstico** (ou, no teclado, pressione Alt + F2).

2. No Hub **desempenho e diagnóstico** , marque a caixa ao lado de **uso de GPU**. Opcionalmente, marque as caixas ao lado de outras ferramentas nas quais você esteja interessado. Você pode executar várias ferramentas de desempenho e diagnóstico simultaneamente para obter uma visão mais completa do desempenho do aplicativo.

    ![Captura de tela do hub de desempenho e diagnóstico, com uso de GPU selecionado](media/gpuusageselected.png "Uso de GPU selecionado")

   > [!NOTE]
   > Nem todas as ferramentas de diagnóstico e desempenho podem ser usadas ao mesmo tempo.

3. Na parte inferior do Hub **desempenho e diagnóstico** , selecione **Iniciar** para executar seu aplicativo nas ferramentas que você selecionou.

As informações de alto nível mostradas em tempo real incluem tempo de quadro, taxa de quadros e uso de GPU. Cada uma dessas informações é grafada de forma independente, mas todas usam uma escala de tempo comum para que você possa entender facilmente as relações.

Os grafos de **quadro (MS)** e **quadros por segundo (FPS)** têm duas linhas horizontais vermelhas que mostram as metas de desempenho de 60 e 30 quadros por segundo. No grafo Tempo de quadro, o aplicativo supera a meta de desempenho quando o grafo está abaixo da linha e não alcança a meta quando o grafo está acima da linha. Para o gráfico de quadros por segundo, é o oposto: seu aplicativo excede o destino de desempenho quando o grafo está acima da linha e perde o destino quando o grafo está abaixo da linha. Você usa esses gráficos principalmente para obter uma ideia de alto nível do desempenho do seu aplicativo e para identificar os lentos que talvez você queira investigar. Por exemplo, uma investigação mais aprofundada poderá ser garantida se você vir uma queda repentina na taxa de quadros ou um pico na utilização da GPU.

Enquanto seu aplicativo é executado sob a ferramenta de uso da GPU, a sessão de diagnóstico também coleta informações detalhadas sobre eventos gráficos que foram executados na GPU. Você usa essas informações para gerar um relatório mais granular de como seu aplicativo utiliza o hardware. Como esse relatório leva algum tempo para ser gerado com base nas informações coletadas, ele só estará disponível depois que a sessão de diagnóstico concluir a coleta de informações.

Quando você quiser examinar um problema de desempenho ou utilização mais de mais de precisão, interrompa a coleta de informações de desempenho para que possa gerar o relatório.

Para gerar e exibir o relatório de uso de GPU:

1. Na parte inferior da janela de sessão de diagnóstico, escolha o link **parar coleção** ou selecione **parar** no canto superior esquerdo.

   ![Captura de tela da janela de sessão de diagnóstico](media/gfx_diag_gpu_usage_collect.png "gfx_diag_gpu_usage_collect")

2. Na parte superior do relatório, selecione uma seção de um dos gráficos que mostra o problema que você deseja investigar. Sua seleção pode ter até 3 segundos de comprimento. As seções mais longas são truncadas em direção ao início.

   ![Captura de tela da janela de sessão de diagnóstico](media/gfx_diag_gpu_usage_select1.png "gfx_diag_gpu_usage_select1")

3. Para exibir uma linha do tempo detalhada da sua seleção, na parte inferior do relatório, na seção **... Clique aqui para exibir detalhes do uso de GPU para essa** mensagem de intervalo, selecione **Exibir detalhes**.

   ![Captura de tela da janela de sessão de diagnóstico com o intervalo selecionado](media/gfx_diag_gpu_usage_select2.png "gfx_diag_gpu_usage_select2")

Essa seleção abre um novo documento com guias que contém o relatório. O relatório uso de GPU ajuda você a ver quando um evento de gráficos é iniciado na CPU, quando ele atinge a GPU e por quanto tempo a GPU leva para executá-la. Essas informações podem ajudá-lo a identificar gargalos e oportunidades de aumento de paralelismo no código.

<!-- VERSIONLESS -->
## <a name="export-to-gpuview-or-windows-performance-analyzer"></a>Exportar para o GPUView ou o Windows Performance Analyzer

Começando com o Visual Studio 2017, é possível abrir esses dados com [GPUView](/windows-hardware/drivers/display/using-gpuview) e com o [Windows Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer). Basta selecionar os links **abrir no GpuView** ou **abrir em WPA** localizados no canto inferior direito da sessão de diagnóstico.

![Captura de tela da janela de sessão de diagnóstico, com links realçados](media/gfx_diag_open_in.png)
<!-- /VERSIONLESS -->

## <a name="use-the-gpu-usage-report"></a>Usar o relatório uso de GPU

A parte superior do relatório uso de GPU mostra linhas do tempo para a atividade de processamento da CPU, atividade de renderização da GPU e atividade de cópia de GPU. Essas linhas do tempo são divididas por barras verticais de cinza claro que indicam o vsync de exibição. A frequência das barras corresponde à taxa de atualização de uma das exibições (selecionadas usando a lista suspensa **exibição** ) da qual os dados de uso da GPU foram coletados.

Como a exibição pode ter uma taxa de atualização mais alta do que a meta de desempenho do aplicativo, talvez não haja uma relação um para um entre o vsync e a taxa de quadros que você deseja que o aplicativo atinja. Para atender a seu destino de desempenho, um aplicativo deve concluir todo o processamento, fazer a renderização e fazer uma `Present()` chamada na taxa de quadros de destino. No entanto, o quadro renderizado não será exibido até o próximo vsync `Present()` .

A parte inferior do relatório uso de GPU lista os eventos gráficos que ocorreram durante o período de tempo do relatório. Quando você seleciona um evento, um marcador é exibido em eventos correspondentes nas linhas do tempo relevantes. Normalmente, um evento em um thread da CPU mostra a chamada à API, enquanto outro evento em uma das linhas do tempo da GPU mostra quando a GPU concluiu a tarefa. Da mesma forma, quando você seleciona um evento em uma linha do tempo, o relatório realça o evento gráfico correspondente na parte inferior do relatório.

Quando você estiver com um zoom das linhas do tempo na parte superior do relatório, somente os eventos mais demorados estarão visíveis. Para ver os eventos que têm uma duração menor, aplique o zoom nos cronogramas usando Ctrl + Wheel no seu dispositivo apontador ou o controle de dimensionamento no canto inferior esquerdo do painel superior. Também é possível arrastar o conteúdo do painel de linha do tempo para percorrer os eventos registrados.

Para ajudar a encontrar o que você está procurando, filtre o relatório uso de GPU com base em nomes de processo, IDs de thread e o nome do evento. Além disso, é possível escolher qual taxa de atualização da exibição determina as linhas do vsync. Será possível classificar os eventos hierarquicamente se o aplicativo usar a interface [ID3DUserDefinedAnnotation](/windows/desktop/api/d3d11_1/nn-d3d11_1-id3duserdefinedannotation) para agrupar comandos de renderização.

 Estes são mais detalhes:

|Controle de filtro|Descrição|
|--------------------|-----------------|
|**Processo**|O nome do processo no qual você está interessado. Todos os processos que usaram a GPU durante a sessão de diagnóstico são incluídos nessa lista suspensa. A cor associada ao processo é a cor da atividade do thread nos cronogramas.|
|**Processo**|A ID do thread em que você está interessado. Em um aplicativo multi-threaded, essas informações podem ajudá-lo a isolar threads específicos que pertencem ao processo de seu interesse. Os eventos associados ao thread selecionado são realçados em cada linha do tempo.|
|**Exibição**|O número da exibição cuja taxa de atualização é mostrada. Alguns drivers podem ser configurados para apresentar vários vídeos físicos como um único vídeo virtual grande. Talvez você veja apenas um vídeo listado, mesmo se o computador tiver vários vídeos anexados.|
|**Filter**|Palavras-chave nas quais você está interessado. Os eventos na parte inferior do relatório incluirão apenas aqueles que correspondem a uma palavra-chave, de forma totalmente ou parcial. É possível especificar várias palavras-chave separando-as com um ponto-e-vírgula (;).|
|**Classificação de Hierarquia**|Uma caixa de seleção que indica se as hierarquias de eventos, definidas por meio de marcadores de usuário, são preservadas ou ignoradas.|

A lista de eventos na parte inferior do relatório uso de GPU mostra os detalhes de cada evento.

|Coluna|Descrição|
|------------|-----------------|
|**Nome do evento**|O nome do evento de gráficos. Normalmente, um evento corresponde a um evento em uma linha do tempo do thread de CPU e a um evento de linha do tempo de GPU. Os nomes de evento podem não ter *atributo* se o uso da GPU não puder determinar o nome de um evento. Para obter mais informações, consulte a observação após esta tabela.|
|**Início da CPU (ns)**|A hora em que o evento foi iniciado na CPU com uma chamada a uma API do Direct3D. O tempo é medido em nanossegundos, relativo à hora de início do aplicativo.|
|**Início da GPU (ns)**|A hora em que o evento foi iniciado na GPU. O tempo é medido em nanossegundos, relativo à hora de início do aplicativo.|
|**Duração da GPU (ns)**|O tempo, em nanossegundos, que o evento levou para ser concluído na GPU.|
|**Nome do processo**|O nome do aplicativo do qual o evento foi originado.|
|**ID do thread**|A ID do thread da qual o evento foi obtido.|

> [!IMPORTANT]
> Se a GPU ou o driver não oferecer suporte aos recursos de instrumentação necessários, todos os eventos aparecerão como sem *atributo*. Se você tiver esse problema, atualize seu driver de GPU e tente novamente. Para obter mais informações, consulte [suporte a hardware e driver](#hwsupport) no final deste documento.

## <a name="gpu-usage-settings"></a>Configurações de Uso de GPU

É possível configurar a ferramenta Uso de GPU para adiar a coleta de informações de criação de perfil, em vez de iniciar a coleta de informações logo após a inicialização do aplicativo. Como o tamanho das informações de criação de perfil pode ser significativo, essa ação será útil quando você souber que os problemas de lentidão no desempenho do aplicativo apenas serão exibidos posteriormente.

Para adiar a criação de perfil após a inicialização do aplicativo:

1. No menu principal, escolha **depurar**  >  **desempenho e diagnóstico** (ou, no teclado, pressione Alt + F2).

2. No Hub **desempenho e diagnóstico** , ao lado de **uso de GPU**, selecione o link **configurações** .

3. Em **configuração de criação de perfil de GPU**, na página de propriedades **geral** , desmarque a caixa de seleção **Iniciar criação de perfil no início do aplicativo** para adiar a criação de perfil.

   ![Captura de tela das páginas de propriedades do objeto, mostrando opções de coleta](media/gfx_diag_gpu_usage_config.png "gfx_diag_gpu_usage_config")

> [!IMPORTANT]
> Neste momento, você não pode adiar a criação de perfil para aplicativos do Direct3D 12.

Depois de executar seu aplicativo na ferramenta Uso de GPU, um link adicional se tornará disponível na parte inferior da janela de ferramentas Uso de GPU. Para iniciar a coleta de informações de criação de perfil, escolha o link **Iniciar** na mensagem **Iniciar coleta de dados detalhados de Uso de GPU adicionais**.

## <a name="hardware-and-driver-support"></a><a name="hwsupport"></a> Suporte de hardware e driver

Há suporte para os seguintes hardware e drivers de GPU:

|Fornecedor|Descrição da GPU|Versão do driver necessária|
|------------|---------------------|-----------------------------|
|Intel®|Processadores Intel® Core da 4ª geração (“Haswell”)<br /><br /> -   Intel® HD Graphics (GT1)<br />-   Intel® HD Graphics 4200 (GT2)<br />-   Intel® HD Graphics 4400 (GT2)<br />-   Intel® HD Graphics 4600 (GT2)<br />-   Intel® HD Graphics P4600 (GT2)<br />-   Intel® HD Graphics P4700 (GT2)<br />-   Intel® HD Graphics 5000 (GT3)<br />-   Intel® Iris™ Graphics 5100 (GT3)<br />-   Intel® Iris™ Pro Graphics 5200 (GT3e)|(usar drivers mais recentes)|
|AMD®|A maioria desde a série AMD Radeon™ HD 7000 (exclui o AMD Radeon™ HD 7350-7670)<br /><br /> AMD Radeon™ GPU, AMD FirePro™ GPUs e aceleradores de GPU do AMD FirePro, com a arquitetura de núcleos principais a seguir (GCN)<br /><br /> APUs (Unidades de Processamento Acelerado) AMD® série E e AMD série A com a arquitetura GCN (Graphics Core Next) (“Kaveri”, “Kabini”, “Temash”, “Beema”, “Mullins”)|14,7 RC3 ou posterior|
|NVIDIA®|A maioria desde o NVIDIA® GeForce® série 400<br /><br /> GPUs NVIDIA® GeForce®, NVIDIA Quadro® GPUs e NVIDIA® Tesla™ a arquitetura de GPU, com Fermi™, Kepler™ ou Maxwell™ Architecture|343,37 ou posterior|

 As configurações de várias GPU, como NVIDIA® SLI™ e AMD Crossfire™, não têm suporte no momento. As configurações de gráficos híbridos, como NVIDIA® Optimus™ e AMD Enduro™, têm suporte.
