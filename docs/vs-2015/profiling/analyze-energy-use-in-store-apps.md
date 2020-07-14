---
title: Analisar o uso de energia em aplicativos da Store | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 96d06843-b97e-45a8-8126-07478a40bfc4
caps.latest.revision: 39
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 82f5e6401ba65a0dfaffc268890ece0166432c08
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532945"
---
# <a name="analyze-energy-use-in-store-apps"></a>Analisar o uso de energia em aplicativos da Store
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O criador de perfil de **Consumo de Energia** do Visual Studio ajuda a analisar o consumo de energia de aplicativos da Windows Store em dispositivos tablet de baixa capacidade executados o tempo todo ou parte do tempo usando apenas a própria bateria. Em um dispositivo alimentado por bateria, um aplicativo que consome muita energia pode causar grande insatisfação do cliente fazendo com que ele acabe desinstalando o programa. A otimização do consumo de energia pode aumentar a adoção e o uso de seu aplicativo pelos clientes.  
  
## <a name="what-the-energy-consumption-profiler-is-how-it-works-and-what-it-measures"></a><a name="BKMK_What_the_Energy_Consumption_tool_is__how_it_works__and_what_it_measures"></a> O que é o criador de perfil Consumo de Energia, como ele funciona e o que mede  
 O criador de perfil Consumo de Energia captura as atividades do monitor, da CPU e das conexões de rede de um dispositivo durante a uma sessão de criação de perfil. Em seguida, ela gera estimativas da energia consumida por essas atividades e a quantidade total de energia para a sessão de criação de perfil.  
  
> [!NOTE]
> O criador de perfil de energia calcula uso de potência e energia por meio de um modelo de software de hardware padrão de dispositivo de referência que representa os tablets de baixa potência nos quais seu aplicativo possa estar sendo executado. Para fornecer as melhores estimativas, recomendamos coletar os dados do perfil em um tablet de baixa potência.  
>   
> Embora o modelo forneça boas estimativas para diversos dispositivos de baixa potência, os valores reais do dispositivo analisado provavelmente serão diferentes. Use os valores para localizar as atividades do monitor, da CPU e de rede que são dispendiosas em relação a outros usos de recursos e que portanto podem ser bons candidatos para otimização.  
  
 O criador de perfil Consumo de Energia usa estas definições de *potência* e *energia*:  
  
- *Potência* mede a taxa com que a força é usada para executar o trabalho realizado em determinado período. Em ciências elétricas, a unidade padrão de potência é o *watt*, a qual é definida como a taxa em que o trabalho é executado quando um ampère de corrente flui através de uma diferença de potencial elétrico de um volt. No gráfico **Consumo de Energia**, as unidades são exibidas como miliwatts **mW**, que são um milésimo de um watt.  
  
   Observe que, como a potência é uma taxa, ela tem uma direção (o trabalho pode aumentar ou diminuir em um período) e uma velocidade (quanto o trabalho aumenta ou diminui).  
  
- *Energia* mede a potência total, como capacidade ou potencial, como na capacidade de alimentação de uma bateria ou como no total de energia consumida durante um período. A unidade de energia é um watt-hora, a potência de um watt constantemente aplicada por uma hora. No **Resumo de Energia**, as unidades são exibidas como miliwatt-horas **mW-h**.  
  
  ![Capacidade de energia, energia usada, total de energia usada](../profiling/media/energyprof-capcitypowerused.png "ENERGYPROF_CapcityPowerUsed")  
  
  Por exemplo, uma bateria totalmente carregada em um tablet tem uma determinada quantidade de energia armazenada. Como a energia é usada para executar tarefas como comunicação por rede, cálculo de valores ou exibição de gráficos, a energia da bateria se dissipa em diferentes taxas. Para qualquer período, a potência total consumida também é medida por energia.  
  
## <a name="identify-scenarios-with-user-marks"></a><a name="BKMK_Identify_scenarios_with_user_marks"></a> Identificar cenários com marcas de usuário  
 Você também pode adicionar *marcas de usuário* aos seus dados de perfil para ajudar a identificar áreas na régua da linha do tempo.  
  
 ![Marcas de usuário na linha do tempo](../profiling/media/profilers-usermarktimeline.png "PROFILERS_UserMarkTimeline")  
  
 A marca aparece como um triângulo laranja na linha de tempo no momento em que o método é executado. A mensagem e a hora são exibidas como uma dica de ferramenta quando você passa o cursor do mouse sobre a marca. Se duas ou mais marcas de usuário ficarem próximas, elas serão mescladas e os dados de dica de ferramenta serão combinados. Você pode aplicar zoom na linha de tempo para separar as marcas.  
  
 **Adicionar marcas a código C#, Visual Basic, C++**  
  
 Para adicionar uma marca do usuário ao código C#, Visual Basic, C++, crie primeiro um objeto [Windows.Foundation.Diagnostics LoggingChannel](https://msdn.microsoft.com/library/windows/apps/windows.foundation.diagnostics.loggingchannel.aspx). Em seguida, insira chamadas para os métodos [LoggingChannel.LogMessage](https://msdn.microsoft.com/library/windows/apps/dn264210.aspx) nos pontos do código que você deseja marcar. Use [LoggingLevel.Information](https://msdn.microsoft.com/library/windows/apps/windows.foundation.diagnostics.logginglevel.aspx) nas chamadas.  
  
 Quando o método é executado, uma marca de usuário é adicionada aos dados de criação de perfil juntamente com uma mensagem.  
  
> [!NOTE]
> - O Windows.Foundation.Diagnostics LoggingChannel implementa a interface [Windows.Foundation.IClosable](https://msdn.microsoft.com/library/windows/apps/windows.foundation.iclosable.aspx) (projetada como [System.IDisposable](https://msdn.microsoft.com/library/System.IDisposable.aspx) em C# e VB). Para evitar a perda de recursos do sistema operacional, chame [LoggingChannel.Close](https://msdn.microsoft.com/library/windows/apps/windows.foundation.diagnostics.loggingchannel.close.aspx)() [Windows.Foundation.Diagnostics.LoggingChannel.Dispose() em C# e VB] quando concluir o trabalho em um canal de log.  
>   - Cada canal de registro em log aberto deve ter um nome exclusivo. Tentar criar um novo canal de registro em log com o mesmo nome de um canal não descartado gera uma exceção.  
  
 **Adicionar marcas ao código JavaScript**  
  
 Para adicionar marcas do usuário, adicione o seguinte código nos pontos do código que você deseja marcar:  
  
```  
if (performance && performance.mark) {  
    performance.mark(markDescription);  
}  
```  
  
 *markDescription* é uma cadeia de caracteres que contém a mensagem a ser exibida na dica de ferramenta da marca do usuário.  
  
## <a name="configure-your-environment-for-profiling"></a><a name="BKMK_Configure_your_environment_for_profiling"></a> Configurar o ambiente para criação de perfil  
 Para obter boas estimativas, você deverá criar o perfil de consumo de energia do aplicativo em um dispositivo de baixa potência alimentado por bateria. Como o Visual Studio não funciona na maioria desses dispositivos, você precisará conectar seu computador com o Visual Studio ao dispositivo usando as ferramentas remotas do Visual Studio. Para se conectar a um dispositivo remoto, você precisa configurar o projeto do Visual Studio e o dispositivo remoto. Consulte [Executar aplicativos da Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md) para obter mais informações.  
  
> [!TIP]
> - Não é recomendável criar o perfil de energia no simulador da Windows Store ou no computador que contém o Visual Studio. A criação de perfil no dispositivo real fornece dados muito mais realistas.  
>   - Crie o perfil no dispositivo de destino enquanto ele é alimentado por bateria.  
>   - Feche outros aplicativos que possam usar os mesmos recursos (rede, CPU ou tela).  
  
## <a name="collect-energy-profile-data-for-your-app"></a><a name="BKMK_Collect_energy_profile_data_for_your_app"></a> Coletar dados do perfil de energia para seu aplicativo  
  
1. No menu **Depurar**, escolha **Iniciar Diagnóstico Sem Depurar**.  
  
     ![Escolha consumo de energia no Hub de diagnóstico](../profiling/media/energyprof-diagnosticshub.png "ENERGYPROF_DiagnosticsHub")  
  
2. Selecione **Consumo de Energia** e então **Iniciar**.  
  
    > [!NOTE]
    > Ao iniciar o criador de perfil de **consumo de energia** , você poderá ver uma janela de controle de **conta de usuário** solicitando sua permissão para executar VsEtwCollector.exe. Escolha **Sim**.  
  
3. Ative seu aplicativo para coletar dados.  
  
4. Para interromper a criação do perfil, retorne ao Visual Studio (Alt + Tab) e selecione **Interromper a coleta** na página Hub de diagnóstico.  
  
     ![Parar coleta de dados](../profiling/media/xamlprof-stopcollection.png "XAMLProf_StopCollection")  
  
     O Visual Studio analisa os dados coletados e exibe os resultados.  
  
## <a name="collect-energy-profile-data-for-an-installed-app"></a><a name="BKMK_Collect_energy_profile_data_for_an_installed_app"></a> Coletar dados do perfil de energia para um aplicativo instalado  
 A ferramenta Consumo de Energia só pode ser executada nos aplicativos da Windows Store 8.1 que são iniciados a partir de uma solução do Visual Studio ou são instalados a partir da Windows Store. Quando uma solução é aberta no Visual Studio, o destino padrão é **Projeto de Inicialização**. Para direcionar um aplicativo instalado:  
  
1. Escolha **Alterar Destino** e escolha **Aplicativo Instalado**.  
  
2. Na lista **Selecionar Pacote do Aplicativo Instalado**, escolha o destino.  
  
3. Escolha **Consumo de Energia** na página de hub de diagnóstico.  
  
4. Escolha **Iniciar** para iniciar a criação de perfil.  
  
   Para interromper a criação do perfil, retorne ao Visual Studio (Alt + Tab) e selecione **Interromper a coleta** na página Hub de diagnóstico.  
  
## <a name="analyze-energy-profile-data"></a><a name="BKMK_Analyze_energy_profile_data"></a> Analisar dados do perfil de energia  
 Os dados do perfil de energia são exibidos na janela do documento do Visual Studio:  
  
 ![Página de relatório do Energy Profiler](../profiling/media/energyprof-all.png "ENERGYPROF_All")  
  
|Imagem|Descrição|  
|-|-|  
|![Etapa 1](../profiling/media/procguid-1.png "ProcGuid_1")|O arquivo de relatório é chamado Report*AAAAMMDD-HHMM*.diagsession. Você poderá alterar o nome se decidir salvar o relatório.|  
|![Etapa 2](../profiling/media/procguid-2.png "ProcGuid_2")|A linha de tempo mostra a duração da sessão de criação de perfil, os eventos de ativação de ciclo de vida do aplicativo e as marcas de usuário.|  
|![Etapa 3](../profiling/media/procguid-3.png "ProcGuid_3")|Você pode restringir o relatório a uma parte da linha do tempo arrastando as barras azuis para selecionar uma região da linha do tempo.|  
|![Etapa 4](../profiling/media/procguid-4.png "ProcGuid_4")|O gráfico **Consumo de Energia** é um gráfico de várias linhas que exibe a alteração na saída de potência causada por um recurso do dispositivo durante uma sessão de criação de perfil. O criador de perfil Consumo de Energia controla a energia usada pela CPU, pela atividade de rede e pelo monitor.|  
|![Etapa 5](../profiling/media/procguid-6.png "ProcGuid_6")|O gráfico **Recursos (Ativado/Desativado)** fornece detalhes dos custos de energia de rede. A barra **Rede** representa o tempo em que a conexão de rede permaneceu aberta. A barra filha **Transferência de Dados** corresponde ao tempo em que o aplicativo recebeu ou enviou dados pela rede.|  
|![Etapa 6](../profiling/media/procguid-6a.png "ProcGuid_6a")|O **Resumo do Consumo de Energia** mostra a quantidade proporcional de energia total usada na linha do tempo selecionada pela CPU, pela atividade de rede e pela tela.|  
  
 **Para analisar os dados do perfil de energia**  
  
 Localize uma área onde tenha ocorrido pico de energia do recurso. Relacione a área de pico à funcionalidade do aplicativo. Use as barras de controle na linha do tempo para ampliar a área. Se você estiver centrado no uso de rede, expanda o nó **Rede** no gráfico **Recursos (Ativado/Desativado)** para comparar o tempo em que a conexão de rede esteve aberta com o tempo em que o aplicativo recebeu ou transferiu dados pela conexão. Reduzir o tempo em que a rede esteve aberta desnecessariamente é uma otimização muito eficiente.  
  
## <a name="optimize-energy-use"></a><a name="BKMK_Optimize_energy_use"></a> Otimizar o consumo de energia  
 Além de transmitir dados, as conexões de rede implicam custos de energia para inicializar, manter e encerrar a conexão. Algumas redes mantêm a conexão por um período depois que os dados são enviados ou recebidos para permitir que mais dados sejam transmitidos por uma única conexão. Você pode usar o painel **Recursos (Ativado/Desativado)** para examinar a maneira como seu aplicativo interage com a conexão.  
  
 ![&#40;de recursos no painel&#47;off&#41;](../profiling/media/energyprof-resources.png "ENERGYPROF_Resources")  
  
 Se as barras **Rede** e **Transferência de Dados** mostrarem que a conexão está aberta por um longo período para transmitir uma série de pacotes pequenos de dados de maneira intermitente, você poderá dividir os dados em lotes para enviá-los em uma transmissão, reduzir o tempo em que a rede fica aberta e, portanto, economizar em custos de energia.  
  
 ![Painel Resumo de consumo de energia](../profiling/media/energyprof-summary.png "ENERGYPROF_Summary")  
  
 Você tem menos controle sobre os custos de energia da tela. A maioria das telas exige mais energia para exibir cores claras do que cores mais escuras, portanto, usar uma tela de fundo escuro é uma maneira de reduzir custos.  
  
## <a name="other-resources"></a><a name="BKMK_Other_resources"></a>Outros recursos  
  
- As seções **Estado da conexão e gerenciamento de custo** para [C#/VB/C++ e XAML](https://msdn.microsoft.com/0ee0b706-8432-4d49-9801-306ed90764e1) e [JavaScript e HTML](https://msdn.microsoft.com/372afa6a-1c7c-4657-967d-03a77cd8e933) no Centro de Desenvolvimento do Windows descrevem as APIs do Windows que fornecem informações sobre a conectividade de rede que seu aplicativo pode usar para minimizar os custos de tráfego de rede.  
  
     O simulador do Visual Studio para aplicativos da Windows Store permite que você simule propriedades de conexão de dados das APIs de informações de rede. Consulte [Executar aplicativos da Windows Store no simulador](../debugger/run-windows-store-apps-in-the-simulator.md)  
  
- As ferramentas **Temporização de Função JavaScript** e **Uso da CPU** podem ajudar a reduzir a carga da CPU quando ela for causada por funções ineficientes. Consulte [Analisar o uso de CPU](../profiling/analyze-cpu-usage-in-a-windows-universal-app.md).
