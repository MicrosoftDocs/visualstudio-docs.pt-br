---
title: Analisar o uso de energia em aplicativos UWP | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 96d06843-b97e-45a8-8126-07478a40bfc4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
monikerRange: vs-2017
ms.openlocfilehash: 524eb76696414cbbdba72266cc732ccb7e089f86
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537235"
---
# <a name="analyze-energy-use-in-uwp-apps"></a>Analisar o uso de energia em aplicativos UWP

O criador de perfil de **Consumo de Energia** do Visual Studio ajuda a analisar o consumo de energia de aplicativos UWP em dispositivos tablet de baixa capacidade executados o tempo todo ou parte do tempo usando apenas a própria bateria. Em um dispositivo alimentado por bateria, um aplicativo que consome muita energia pode causar grande insatisfação do cliente fazendo com que ele acabe desinstalando o programa. A otimização do consumo de energia pode aumentar a adoção e o uso de seu aplicativo pelos clientes.

## <a name="what-the-energy-consumption-profiler-is-how-it-works-and-what-it-measures"></a>O que é o criador de perfil Consumo de Energia, como ele funciona e o que ele mede

O criador de perfil Consumo de Energia captura as atividades do monitor, da CPU e das conexões de rede de um dispositivo durante a uma sessão de criação de perfil. Em seguida, ela gera estimativas da energia consumida por essas atividades e a quantidade total de energia para a sessão de criação de perfil.

> [!NOTE]
> O criador de perfil de energia calcula uso de potência e energia por meio de um modelo de software de hardware padrão de dispositivo de referência que representa os tablets de baixa potência nos quais seu aplicativo possa estar sendo executado. Para fornecer as melhores estimativas, recomendamos coletar os dados do perfil em um tablet de baixa potência.
>
> Embora o modelo forneça boas estimativas para diversos dispositivos de baixa potência, os valores reais do dispositivo analisado provavelmente serão diferentes. Use os valores para localizar as atividades do monitor, da CPU e de rede que são dispendiosas em relação a outros usos de recursos e que portanto podem ser bons candidatos para otimização.

O criador de perfil Consumo de Energia usa estas definições de *potência* e *energia*:

- *Potência* mede a taxa com que a força é usada para executar o trabalho realizado em determinado período. Em ciências elétricas, a unidade padrão de potência é o *watt*, a qual é definida como a taxa em que o trabalho é executado quando um ampère de corrente flui através de uma diferença de potencial elétrico de um volt. No gráfico **Consumo de Energia**, as unidades são exibidas como miliwatts **mW**, que são um milésimo de um watt.

   Observe que, como a potência é uma taxa, ela tem uma direção (o trabalho pode aumentar ou diminuir em um período) e uma velocidade (quanto o trabalho aumenta ou diminui).

- *Energia* mede a potência total, como capacidade ou potencial, como na capacidade de alimentação de uma bateria ou como no total de energia consumida durante um período. A unidade de energia é um watt-hora, a potência de um watt constantemente aplicada por uma hora. No **Resumo de Energia**, as unidades são exibidas como miliwatt-horas **mW-h**.

![Capacidade de energia, energia usada, total de energia usada](../profiling/media/energyprof_capcitypowerused.png)

Por exemplo, uma bateria totalmente carregada em um tablet tem uma determinada quantidade de energia armazenada. Como a energia é usada para executar tarefas como comunicação por rede, cálculo de valores ou exibição de gráficos, a energia da bateria se dissipa em diferentes taxas. Para qualquer período, a potência total consumida também é medida por energia.

## <a name="identify-scenarios-with-user-marks"></a>Identificar cenários com marcas do usuário
 Você também pode adicionar *marcas de usuário* aos seus dados de perfil para ajudar a identificar áreas na régua da linha do tempo.

 ![Marcas de usuário na linha do tempo](../profiling/media/profilers_usermarktimeline.png "PROFILERS_UserMarkTimeline")

 A marca aparece como um triângulo laranja na linha de tempo no momento em que o método é executado. A mensagem e a hora são exibidas como uma dica de ferramenta quando você passa o cursor do mouse sobre a marca. Se duas ou mais marcas de usuário ficarem próximas, elas serão mescladas e os dados de dica de ferramenta serão combinados. Você pode aplicar zoom na linha de tempo para separar as marcas.

 **Adicionar marcas a código C#, Visual Basic, C++**

 Para adicionar uma marca de usuário para código C#, Visual Basic, C++, primeiro crie um objeto <xref:Windows.Foundation.Diagnostics.LoggingChannel?displayProperty=fullName>. Em seguida, insira chamadas para os métodos <xref:Windows.Foundation.Diagnostics.LoggingChannel.LogMessage%2A?displayProperty=nameWithType> nos pontos do código que você deseja marcar. Use [LoggingLevel.Information](xref:Windows.Foundation.Diagnostics.LoggingLevel) nas chamadas.

 Quando o método é executado, uma marca de usuário é adicionada aos dados de criação de perfil juntamente com uma mensagem.

> [!NOTE]
> - <xref:Windows.Foundation.Diagnostics.LoggingChannel?displayProperty=nameWithType> implementa a interface <xref:Windows.Foundation.IClosable?displayProperty=nameWithType> (projetada como <xref:System.IDisposable?displayProperty=nameWithType> em C# e VB). Para evitar a perda de recursos do sistema operacional, chame <xref:Windows.Foundation.Diagnostics.LoggingChannel.Close%2A?displayProperty=nameWithType> (<xref:Windows.Foundation.Diagnostics.LoggingChannel.Dispose%2A?displayProperty=nameWithType> em C# e VB) quando tiver terminado com um canal de registro em log.
> - Cada canal de registro em log aberto deve ter um nome exclusivo. Se você tentar criar um novo canal de registro em log com o mesmo nome que um canal não descartado, uma exceção será lançada.

Para ver um exemplo de código, consulte [Exemplo de LoggingSession](https://code.msdn.microsoft.com/windowsapps/LoggingSession-Sample-ccd52336) do SDK do Windows.

::: moniker range="vs-2017"
**Adicionar marcas ao código JavaScript**

Para adicionar marcas do usuário, adicione o seguinte código nos pontos do código que você deseja marcar:

```JavaScript
if (performance && performance.mark) {
    performance.mark(markDescription);
}
```

*markDescription* é uma cadeia de caracteres que contém a mensagem a ser exibida na dica de ferramenta da marca do usuário.
::: moniker-end

## <a name="configure-your-environment-for-profiling"></a>Configurar seu ambiente para criação de perfis
 Para obter boas estimativas, você deverá criar o perfil de consumo de energia do aplicativo em um dispositivo com baixo consumo de energia alimentado por bateria. Como o Visual Studio não funciona na maioria desses dispositivos, você precisará conectar seu computador com o Visual Studio ao dispositivo usando as ferramentas remotas do Visual Studio. Para se conectar a um dispositivo remoto, você precisa configurar o projeto do Visual Studio e o dispositivo remoto. Consulte [Executar aplicativos UWP em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md) para obter mais informações.

> [!TIP]
> - Não é recomendado criar o perfil de energia no simulador UWP ou no computador com o Visual Studio. A criação de perfil no dispositivo real fornece dados muito mais realistas.
> - Crie o perfil no dispositivo de destino enquanto ele é alimentado por bateria.
> - Feche outros aplicativos que possam usar os mesmos recursos (rede, CPU ou tela).

## <a name="collect-energy-profile-data-for-your-app"></a>Coletar dados do perfil de energia para seu aplicativo

1. No menu **Depurar**, escolha **Iniciar Diagnóstico Sem Depurar**.

     ![Escolha consumo de energia no Hub de diagnóstico](../profiling/media/energyprof_diagnosticshub.png "ENERGYPROF_DiagnosticsHub")

2. Selecione **Consumo de Energia** e então **Iniciar**.

    > [!NOTE]
    > Ao iniciar o criador de perfil **Consumo de Energia**, talvez você veja uma janela **Controle de Conta de Usuário** solicitando sua permissão para executar o *VsEtwCollector.exe*. Escolha **Sim**.

3. Ative seu aplicativo para coletar dados.

4. Para interromper a criação do perfil, retorne ao Visual Studio (Alt + Tab) e selecione **Interromper a coleta** na página Hub de diagnóstico.

     ![Parar coleta de dados](../profiling/media/xamlprof_stopcollection.png "XAMLProf_StopCollection")

     O Visual Studio analisa os dados coletados e exibe os resultados.

## <a name="collect-energy-profile-data-for-an-installed-app"></a>Coletar dados do perfil de energia para um aplicativo instalado
 A ferramenta Consumo de Energia só pode ser executada em aplicativos UWP que são iniciados a partir de uma solução do Visual Studio ou são instalados a partir da Microsoft Store. Quando uma solução é aberta no Visual Studio, o destino padrão é **Projeto de Inicialização**. Para direcionar um aplicativo instalado:

1. Escolha **Alterar Destino** e escolha **Aplicativo Instalado**.

2. Na lista **Selecionar Pacote do Aplicativo Instalado**, escolha o destino.

3. Escolha **Consumo de Energia** na página de hub de diagnóstico.

4. Escolha **Iniciar** para iniciar a criação de perfil.

   Para interromper a criação do perfil, retorne ao Visual Studio (Alt + Tab) e selecione **Interromper a coleta** na página Hub de diagnóstico.

## <a name="analyze-energy-profile-data"></a>Analisar dados do perfil de energia
 Os dados do perfil de energia são exibidos na janela do documento do Visual Studio:

 ![Página de relatório do Energy Profiler](../profiling/media/energyprof_all.png "ENERGYPROF_All")

|Imagem|Descrição|
|-|-|
|![Etapa 1](../profiling/media/procguid_1.png "ProcGuid_1")|O arquivo de relatório é chamado Report*AAAAMMDD-HHMM*.diagsession. Você poderá alterar o nome se decidir salvar o relatório.|
|![Etapa 2](../profiling/media/procguid_2.png "ProcGuid_2")|A linha de tempo mostra a duração da sessão de criação de perfil, os eventos de ativação de ciclo de vida do aplicativo e as marcas de usuário.|
|![Etapa 3](../profiling/media/procguid_3.png "ProcGuid_3")|Você pode restringir o relatório a uma parte da linha do tempo arrastando as barras azuis para selecionar uma região da linha do tempo.|
|![Etapa 4](../profiling/media/procguid_4.png "ProcGuid_4")|O gráfico **Consumo de Energia** é um gráfico de várias linhas que exibe a alteração na saída de potência causada por um recurso do dispositivo durante uma sessão de criação de perfil. O criador de perfil Consumo de Energia controla a energia usada pela CPU, pela atividade de rede e pelo monitor.|
|![Etapa 5](../profiling/media/procguid_6.png "ProcGuid_6")|O gráfico **Recursos (Ativado/Desativado)** fornece detalhes dos custos de energia de rede. A barra **Rede** representa o tempo em que a conexão de rede permaneceu aberta. A barra filha **Transferência de Dados** corresponde ao tempo em que o aplicativo recebeu ou enviou dados pela rede.|
|![Etapa 6](../profiling/media/procguid_6a.png "ProcGuid_6a")|O **Resumo do Consumo de Energia** mostra a quantidade proporcional de energia total usada na linha do tempo selecionada pela CPU, pela atividade de rede e pela tela.|

 **Para analisar os dados do perfil de energia**

 Localize uma área onde tenha ocorrido pico de energia do recurso. Relacione a área de pico à funcionalidade do aplicativo. Use as barras de controle na linha do tempo para ampliar a área. Se você estiver centrado no uso de rede, expanda o nó **Rede** no gráfico **Recursos (Ativado/Desativado)** para comparar o tempo em que a conexão de rede esteve aberta com o tempo em que o aplicativo recebeu ou transferiu dados pela conexão. Reduzir o tempo em que a rede esteve aberta desnecessariamente é uma otimização muito eficiente.

## <a name="optimize-energy-use"></a>Otimizar o uso de energia
 Além de transmitir dados, as conexões de rede implicam custos de energia para inicializar, manter e encerrar a conexão. Algumas redes mantêm a conexão por um período depois que os dados são enviados ou recebidos para permitir que mais dados sejam transmitidos por uma única conexão. Você pode usar o painel **Recursos (Ativado/Desativado)** para examinar a maneira como seu aplicativo interage com a conexão.

 ![&#40;de recursos no painel&#47;off&#41;](../profiling/media/energyprof_resources.png "ENERGYPROF_Resources")

 Se as barras **Rede** e **Transferência de Dados** mostrarem que a conexão está aberta por um longo período para transmitir uma série de pacotes pequenos de dados de maneira intermitente, você poderá dividir os dados em lotes para enviá-los em uma transmissão, reduzir o tempo em que a rede fica aberta e, portanto, economizar em custos de energia.

 ![Painel Resumo de consumo de energia](../profiling/media/energyprof_summary.png "ENERGYPROF_Summary")

 Você tem menos controle sobre os custos de energia da tela. A maioria das telas exige mais energia para exibir cores claras do que cores mais escuras, portanto, usar uma tela de fundo escuro é uma maneira de reduzir custos.

## <a name="other-resources"></a>Outros recursos

- As seções **Estado da conexão e gerenciamento de custos** para [C#/VB/C++ e XAML](/previous-versions/windows/apps/hh452985\(v\=win.10\)) descrevem as APIs do Windows que fornecem informações sobre a conectividade de rede que seu aplicativo pode usar para minimizar os custos de tráfego de rede.

   O simulador do Visual Studio para aplicativos UWP permite que você simule propriedades de conexão de dados das APIs de informações de rede. Consulte [Executar aplicativos UWP no simulador](../debugger/run-windows-store-apps-in-the-simulator.md)

- As ferramentas de **Uso da CPU** podem ajudar a reduzir a carga da CPU quando ela for causada por funções ineficientes. Consulte [analisar o uso da CPU](../profiling/beginners-guide-to-performance-profiling.md).

## <a name="see-also"></a>Confira também

- [Criação de perfis no Visual Studio](../profiling/index.yml)
- [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)