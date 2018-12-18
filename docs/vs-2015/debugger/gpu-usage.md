---
title: Uso de GPU | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 957fed3c-4ded-4e05-87c6-ccc33de65349
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3068f614275c14d022ed4d74fa6a10ffe396f68b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817497"
---
# <a name="gpu-usage"></a>Uso de GPU
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use a ferramenta Uso de GPU no Hub de Desempenho e Diagnóstico do Visual Studio para entender melhor a utilização de hardware de alto nível do aplicativo Direct3D. É possível usá-la para determinar se o desempenho do aplicativo está associado à CPU ou à GPU e obter informações sobre como você pode usar o hardware da plataforma com mais eficiência. O Uso de GPU dá suporte a aplicativos que usam o Direct3D 12, Direct3D 11 e Direct3D 10; ele não dá suporte a outras APIs de gráficos como Direct2D ou OpenGL.  
  
 Esta é a janela **Relatório de Uso de GPU**:  
  
 ![O relatório Uso de GPU, com as linhas do tempo CPU e GPU](../debugger/media/gfx-diag-gpu-usage-report.png "gfx_diag_gpu_usage_report")  
  
## <a name="requirements"></a>Requisitos  
 Veja a seguir os requisitos para o uso da ferramenta Uso de GPU, além dos requisitos do Diagnóstico de Gráficos.  
  
- Uma GPU e drivers que dão suporte à instrumentação de intervalo necessária.  
  
  > [!NOTE]
  >  Para obter mais informações sobre o hardware e os drivers com suporte, consulte [Suporte de hardware e driver](#hwsupport) ao final deste documento.  
  
  Para obter mais informações sobre os requisitos do Diagnóstico de Gráficos, consulte [Introdução](../debugger/getting-started-with-visual-studio-graphics-diagnostics.md).  
  
## <a name="using-the-gpu-usage-tool"></a>Usando a ferramenta Uso de GPU  
 Quando você executa o aplicativo na ferramenta Uso de GPU, o Visual Studio cria uma sessão de diagnóstico que apresenta gráficos de informações de alto nível sobre o desempenho de renderização e a utilização de GPU do aplicativo em tempo real.  
  
#### <a name="to-start-the-gpu-usage-tool"></a>Para iniciar a ferramenta Uso de GPU:  
  
1. No menu principal, escolha **Depurar** e, em seguida, **Desempenho e Diagnóstico** (teclado: pressione Alt + F2).  
  
2. No hub Desempenho e Diagnóstico, marque a caixa ao lado de **Uso de GPU**. Opcionalmente, marque as caixas ao lado de outras ferramentas de seu interesse. É possível executar várias ferramentas de Desempenho e Diagnóstico simultaneamente para obter uma visão mais completa do desempenho do aplicativo.  
  
    ![Escolha as ferramentas de diagnóstico que você deseja usar.](../debugger/media/gfx-diag-diagsession-tools.png "gfx_diag_diagsession_tools")  
  
   > [!NOTE]
   >  Nem todas as ferramentas de Desempenho e Diagnóstico podem ser usadas ao mesmo tempo.  
  
3. Escolha o botão azul **Iniciar** na parte inferior do hub Desempenho e Diagnóstico para executar o aplicativo nas ferramentas selecionadas.  
  
   As informações de alto nível exibidas em tempo real incluem o intervalo de quadro, a taxa de quadros e a utilização de GPU. Cada uma dessas informações é apresentada em gráficos de forma independente, mas usa uma escala de tempo comum para que você possa estabelecer uma relação fácil entre elas.  
  
   Os gráficos **Tempo de quadro (ms)** e **Quadros por segundo (FPS)** contêm duas linhas horizontais vermelhas que representam metas de desempenho de 30 e 60 quadros por segundo. No gráfico **Tempo de quadro**, o aplicativo supera a meta de desempenho quando o gráfico está abaixo da linha e não alcança a meta quando o gráfico está acima da linha. Para o gráfico Quadros por segundo, ocorre o contrário – o aplicativo supera a meta de desempenho quando o gráfico está acima da linha e não alcança a meta quando o gráfico está abaixo da linha. Basicamente, esses gráficos são usados para obter uma ideia de alto nível do desempenho do aplicativo e identificar problemas de lentidão que talvez você deseje investigar – por exemplo, uma queda repentina na taxa de quadros ou um pico na Utilização de GPU.  
  
   Enquanto o aplicativo é executado na ferramenta Uso de GPU, a sessão de diagnóstico também coleta informações detalhadas sobre eventos de gráficos que foram executados na GPU. Essas informações são usadas para gerar um relatório mais granular de como o aplicativo utiliza o hardware. Como esse relatório leva algum tempo para ser gerado com base nas informações coletadas, ele só estará disponível depois que a sessão de diagnóstico concluir a coleta de informações.  
  
   Quando desejar examinar um problema de desempenho ou de utilização mais detalhadamente, pare a coleta de informações de desempenho para que o relatório possa ser gerado.  
  
#### <a name="to-generate-and-view-the-gpu-usage-report"></a>Para gerar e exibir o Relatório de Uso de GPU:  
  
1. Na parte inferior da janela da sessão de diagnóstico, escolha o link **Parar Coleta** ou pressione **Parar** no canto superior esquerdo.  
  
    ![Colete informações de intervalo de GPU e CPU.](../debugger/media/gfx-diag-gpu-usage-collect.png "gfx_diag_gpu_usage_collect")  
  
2. Na parte superior do relatório, selecione uma seção de um dos gráficos que mostra o problema que você deseja investigar. A seleção pode ser feita em até 3 segundos; seções mais longas serão truncadas no início.  
  
    ![Pós&#45;coleta, selecionar um intervalo para exibir os detalhes](../debugger/media/gfx-diag-gpu-usage-select1.png "gfx_diag_gpu_usage_select1")  
  
3. Na parte inferior do relatório, escolha o link **Exibir detalhes** na mensagem **... Clique aqui para exibir detalhes de uso de GPU para esse intervalo** para exibir uma linha do tempo detalhada da seleção.  
  
    ![Pós&#45;coleção, com o intervalo selecionado](../debugger/media/gfx-diag-gpu-usage-select2.png "gfx_diag_gpu_usage_select2")  
  
   Isso abrirá um novo documento com guias que contém o relatório. O relatório Uso de GPU ajuda você a ver quando um evento de gráficos é iniciado na CPU, quando ele atinge a GPU e quanto tempo a GPU leva para executá-lo. Essas informações podem ajudá-lo a identificar gargalos e oportunidades de aumento de paralelismo no código.  
  
## <a name="using-the-gpu-usage-report"></a>Usando o relatório Uso de GPU  
 A parte superior do relatório Uso de GPU exibe linhas do tempo da atividade de processamento da CPU, atividade de renderização da GPU e atividade de cópia da GPU. Essas linhas do tempo são separadas por barras verticais cinza-claro que representam o VSync do vídeo; a frequência das barras corresponde à taxa de atualização de um dos vídeos (selecionados com a lista suspensa **Vídeo**) dos quais esses dados de Uso de GPU foram coletados. Como o vídeo pode ter uma taxa de atualização mais alta do que a meta de desempenho do aplicativo, talvez não haja uma relação um para um entre o VSync e a taxa de quadros que você deseja que o aplicativo atinja. Para atender sua meta de desempenho, um aplicativo deve concluir todo o processamento, executar a renderização e fazer uma chamada Present() à taxa de quadros de destino. Porém, o quadro renderizado só será exibido no próximo VSync após Present().  
  
 A parte inferior exibe uma listagem dos eventos de gráficos que ocorreram durante o período do relatório.  
  
 Esta é a janela **Relatório de Uso de GPU**:  
  
 ![O relatório Uso de GPU, com as linhas do tempo CPU e GPU](../debugger/media/gfx-diag-gpu-usage-report.png "gfx_diag_gpu_usage_report")  
  
 A seleção de um dos eventos na parte inferior do relatório coloca um marcador nos eventos correspondentes nas linhas do tempo relevantes, geralmente, um evento em um thread de CPU que representa a chamada à API e outro evento em uma das linhas do tempo da GPU que representa a hora em que a GPU concluiu a tarefa. Da mesma forma, a seleção de um dos eventos em uma linha do tempo realça o evento correspondente na parte inferior do relatório. Quando reduzidos nas linhas de tempo da parte superior do relatório, somente os eventos mais demorados são visíveis. Para ver os eventos que têm uma duração menor, amplie as linhas do tempo usando Ctrl + roda no dispositivo apontador ou o controle de colocação em escala no canto inferior esquerdo do painel superior. Também é possível arrastar o conteúdo do painel de linha do tempo para percorrer os eventos registrados.  
  
 Para ajudá-lo a encontrar o que você está procurando, é possível filtrar o Relatório de Uso de GPU com base nos nomes do Processo, nas IDs do Thread e no nome do evento; além disso, você pode escolher a taxa de atualização de qual vídeo determina as linhas do VSync e classificar os eventos hierarquicamente, caso o aplicativo use a interface ID3DUserDefinedAnnotation para agrupar comandos de renderização.  
  
 Estes são mais detalhes:  
  
|Controle de filtro|Descrição|  
|--------------------|-----------------|  
|**Processo**|O nome do processo de seu interesse. Todos os processos que usaram a GPU durante a sessão de diagnóstico são incluídos nessa lista suspensa. A cor associada ao processo nessa lista suspensa é a cor da atividade do thread nas linhas do tempo abaixo.|  
|**Thread**|A ID do thread de seu interesse. Em um aplicativo com multi-thread, isso pode ajudá-lo a isolar threads específicos que pertencem ao processo de seu interesse. Os eventos associados ao thread selecionado são realçados em cada linha do tempo.|  
|**Vídeo**|O número do vídeo cuja taxa de atualização é exibida **Observação:** alguns drivers podem ser configurados para apresentar vários vídeos físicos como um único vídeo virtual grande. Talvez você veja apenas um vídeo listado, mesmo se o computador tiver vários vídeos anexados.|  
|**Filtrar**|Palavras-chave de seu interesse. Os eventos na parte inferior do relatório incluirão apenas aqueles que correspondem a uma palavra-chave, no todo ou em parte. É possível especificar várias palavras-chave separando-as com um ponto-e-vírgula (;).|  
|**Classificação de Hierarquia**|Uma caixa de seleção que indica se as hierarquias de eventos – definidas por meio de marcadores do usuário – são preservadas ou ignoradas.|  
  
 A lista de eventos na parte inferior do Relatório de Uso de GPU exibe os detalhes de cada evento.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome do Evento**|O nome do evento de gráficos. Normalmente, um evento corresponde a um evento em uma linha do tempo do thread da CPU e a um evento em uma linha do tempo da GPU.<br /><br /> Os nomes de eventos podem ser “não atribuídos” se o Uso de GPU não pôde determinar o nome de um evento. Para obter mais informações, consulte a observação abaixo desta tabela.|  
|**Início da CPU (ns)**|A hora em que o evento foi iniciado na CPU com uma chamada a uma API do Direct3D. O tempo é medido em nanossegundos, relativo à hora de início do aplicativo.|  
|**Início da GPU (ns)**|A hora em que o evento foi iniciado na GPU. O tempo é medido em nanossegundos, relativo à hora de início do aplicativo.|  
|**Duração da GPU (ns)**|O tempo que o evento levou para ser concluído na GPU, em nanossegundos.|  
|**Nome do Processo**|O nome do aplicativo do qual o evento foi originado.|  
|**ID do Thread**|A ID do thread da qual o evento foi obtido.|  
  
> [!IMPORTANT]
>  O Windows 8.1 é necessário para a atribuição de eventos. Além disso, se a GPU ou o driver não derem suporte aos recursos de instrumentação necessários, todos os eventos serão exibidos como “não atribuídos”. Lembre-se de atualizar o driver da GPU e tente novamente caso ocorra esse problema. Para obter mais informações, consulte [Suporte de hardware e driver](#hwsupport) abaixo.  
  
## <a name="gpu-usage-settings"></a>Configurações de Uso de GPU  
 É possível configurar a ferramenta Uso de GPU para adiar a coleta de informações de criação de perfil, em vez de iniciar a coleta de informações logo após a inicialização do aplicativo. Como o tamanho das informações de criação de perfil pode ser significativo, isso será útil quando você souber que os problemas de lentidão no desempenho do aplicativo só serão exibidos posteriormente.  
  
#### <a name="to-postpone-profiling-from-the-start-of-the-app"></a>Para adiar a criação de perfil após a inicialização do aplicativo:  
  
1.  No menu principal, escolha **Depurar** e, em seguida, **Desempenho e Diagnóstico** (teclado: pressione Alt + F2).  
  
2.  No hub Desempenho e Diagnóstico, siga o link **Configurações** ao lado de **Uso de GPU**.  
  
3.  Em **Configuração de Criação de Perfil da GPU**, na página de propriedades **Geral**, desmarque a caixa de seleção **Iniciar a criação de perfil após a inicialização do aplicativo** para adiar a criação de perfil.  
  
     ![Configurar o início da coleta de Uso de GPU](../debugger/media/gfx-diag-gpu-usage-config.png "gfx_diag_gpu_usage_config")  
  
> [!IMPORTANT]
>  Não há suporte para o adiamento da criação de perfil em aplicativos Direct3D 12.  
  
 Ao adiar a coleta de informações de criação de perfil usando essa configuração, outro link ficará disponível na parte inferior da janela de ferramentas Uso de GPU quando o aplicativo for executado na ferramenta Uso de GPU. Para iniciar a coleta de informações de criação de perfil, escolha o link **Iniciar** na mensagem **Iniciar coleta de dados detalhados de Uso de GPU adicionais**.  
  
##  <a name="hwsupport"></a> Suporte de hardware e driver  
 Há suporte para os seguintes hardware e drivers de GPU:  
  
|Fornecedor|Descrição da GPU|Versão de driver necessária|  
|------------|---------------------|-----------------------------|  
|Intel®|Processadores Intel® Core da 4ª geração (“Haswell”)<br /><br /> -   Intel® HD Graphics (GT1)<br />-   Intel® HD Graphics 4200 (GT2)<br />-   Intel® HD Graphics 4400 (GT2)<br />-   Intel® HD Graphics 4600 (GT2)<br />-   Intel® HD Graphics P4600 (GT2)<br />-   Intel® HD Graphics P4700 (GT2)<br />-   Intel® HD Graphics 5000 (GT3)<br />-   Intel® Iris™ Graphics 5100 (GT3)<br />-   Intel® Iris™ Pro Graphics 5200 (GT3e)|- (usar os últimos drivers)|  
|AMD®|A maioria, a partir da AMD Radeon™ HD série 7000 (excluindo AMD Radeon™ HD 7350-7670)<br /><br /> Aceleradores de GPUs AMD Radeon™, AMD FirePro™ e AMD FirePro com a arquitetura GCN (Graphics Core Next).<br /><br /> APUs (Unidades de Processamento Acelerado) AMD® série E e AMD série A com a arquitetura GCN (Graphics Core Next) (“Kaveri”, “Kabini”, “Temash”, “Beema”, “Mullins”)|14.7 RC3 ou superior|  
|NVIDIA®|A maioria, a partir da NVIDIA® GeForce® série 400.<br /><br /> Aceleradores de GPUs NVIDIA® GeForce®, NVIDIA Quadro® e NVIDIA® Tesla™ com a arquitetura Fermi™, Kepler™ ou Maxwell™.|343.37 ou superior|  
  
 No momento, não há suporte para configurações de GPU múltipla, como NVIDIA® SLI™ e AMD Crossfire™. Há suporte para a configuração de elementos gráficos híbridos, como NVIDIA® Optimus™ e AMD Enduro™.  
  
## <a name="see-also"></a>Consulte também  
  
-   [Resolver problemas difíceis de elementos gráficos no jogo usando as ferramentas do DirectX (vídeo)](http://channel9.msdn.com/Events/GDC/GDC-2015/Solve-the-Tough-Graphics-Problems-with-your-Game-Using-DirectX-Tools)  
  
-   [Ferramenta Uso de GPU no Visual Studio (vídeo)](http://channel9.msdn.com/Events/Visual-Studio/Connect-event-2014/715)  
  
-   [Ferramenta Uso de GPU no Visual Studio 2013 Atualização 4 CTP1 (blog)](http://blogs.msdn.com/b/vcblog/archive/2014/09/05/gpu-usage-tool-in-visual-studio-2013-update-4-ctp1.aspx)  
  
-   [Uso de GPU para o DirectX no Visual Studio (blog)](http://blogs.msdn.com/b/ianhu/archive/2014/12/16/gpu-usage-for-directx-in-visual-studio.aspx)



