---
title: Analisar o uso da CPU em um aplicativo universal do Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c122b08e-e3bf-43e6-bd6c-e776e178fd9a
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 11e8587176ecc452f8f97132d296cff93b09b5ac
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741284"
---
# <a name="analyze-cpu-usage-in-a-windows-universal-app"></a>Analisar o uso de CPU em um aplicativo universal do Windows
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 Quando você precisa investigar problemas de desempenho no aplicativo, um bom começo é entender como ele usa a CPU. A ferramenta **Uso da CPU** mostra em que a CPU está dedicando tempo a executar código. Para se concentrar em cenários específicos, o uso da CPU pode ser executado com o [capacidade de resposta de interface do usuário XAML](http://msdn.microsoft.com/library/4ff84cd1-4e63-4fda-b34f-3ef862a6e480) ferramenta, o [consumo de energia](../profiling/analyze-energy-use-in-store-apps.md) ferramenta ou ambas as ferramentas em uma única sessão de diagnóstico.  
  
> [!NOTE]
>  A ferramenta **Uso da CPU** não pode ser usada com os aplicativos Windows Phone Silverlight 8.1.  
  
 Este passo a passo o conduz pela coleta e a análise do uso da CPU por um aplicativo XAML Universal do Windows simples.  
  
##  <a name="BKMK_Create_the_CpuUseDemo_project"></a> Criar o projeto CpuUseDemo  
 **CpuUseDemo** é um aplicativo criado para demonstrar como coletar e analisar dados de uso da CPU. Os botões geram um número chamando um método que seleciona o valor máximo de várias chamadas a uma função. A função chamada cria um número muito grande de valores aleatórios e retorna o último deles. Os dados são exibidos em uma caixa de texto.  
  
1.  Crie um novo projeto de aplicativo universal do Windows C# chamado **CpuUseDemo** usando o modelo **BlankApp**.  
  
     ![Criar o CpuUseDemoProject](../profiling/media/cpu-use-newproject.png "CPU_USE_NewProject")  
  
2.  Substitua MainPage.xaml por [este código](#BKMK_MainPage_xaml).  
  
3.  Substitua MainPage.xaml.cs por [este código](#BKMK_MainPage_xaml_cs).  
  
4.  Compile o aplicativo e experimente-o. O aplicativo é simples o suficiente para mostrar alguns casos comuns de análise de dados de Uso da CPU.  
  
##  <a name="BKMK_Collect_CPU_usage_data"></a> Coletar dados de uso da CPU  
 ![Executar um build de versão do aplicativo no simulador](../profiling/media/cpu-use-wt-setsimulatorandretail.png "CPU_USE_WT_SetSimulatorAndRetail")  
  
1. No Visual Studio, defina o destino de implantação como **Simulador** e a configuração da solução como **Liberação**.  
  
   -   Executar o aplicativo no simulador permite que você alterne facilmente entre o aplicativo e o Visual Studio IDE.  
  
   -   Executar este aplicativo no modo **Liberar** dá a você uma visão melhor do desempenho atual do aplicativo.  
  
2. No menu **Depurar**, escolha **Criador de Perfil de Desempenho...**.  
  
3. No hub de Desempenho e Diagnóstico, escolha **Uso da CPU** e **Iniciar**.  
  
    ![Iniciar a sessão de diagnóstico CpuUsage](../profiling/media/cpu-use-wt-perfdiaghub.png "CPU_USE_WT_PerfDiagHub")  
  
4. Quando o aplicativo for iniciado, clique em **Obter Número Máximo**. Aguarde cerca de um segundo após a exibição da saída e escolha **Obter Número Máximo Assíncrono**. Esperar entre cliques de botão torna mais fácil isolar as rotinas de clique do botão no relatório de diagnóstico.  
  
5. Depois que a segunda linha de saída for exibida, escolha **Parar Coleção** no hub Desempenho e Diagnóstico.  
  
   ![Parar a coleta de dados de CpuUsage](../profiling/media/cpu-use-wt-stopcollection.png "CPU_USE_WT_StopCollection")  
  
   A ferramenta Uso da CPU analisa os dados e exibe o relatório.  
  
   ![Relatório de CpuUsage](../profiling/media/cpu-use-wt-report.png "CPU_USE_WT_Report")  
  
##  <a name="BKMK_Analyze_the_CPU_Usage_report"></a> Analisar o relatório de Uso da CPU  
  
###  <a name="BKMK_CPU_utilization_timeline_graph"></a> Gráfico de linha do tempo de utilização da CPU  
 ![Gráfico de linha do tempo CpuUtilization &#40;%&#41;](../profiling/media/cpu-use-wt-timelinegraph.png "CPU_USE_WT_TimelineGraph")  
  
 O gráfico de uso da CPU mostra a atividade da CPU do aplicativo como um percentual de todo o tempo de CPU de todos os núcleos do processador no dispositivo. Os dados deste relatório foram coletados em um computador com dois núcleos. Os dois maiores picos representam a atividade da CPU de dois cliques de botões. `GetMaxNumberButton_Click` trabalha de modo síncrono em um único núcleo, por isso faz sentido que a altura do grafo de método nunca exceda 50%. `GetMaxNumberAsycButton_Click` executa de modo assíncrono entre os dois núcleos, por isso, está certo que o pico se aproxime ao uso de todos os recursos da CPU nos dois núcleos.  
  
####  <a name="BKMK_Select_timeline_segments_to_view_details"></a> Selecionar segmentos de linha do tempo para exibir detalhes  
 Use as barras de seleção na linha de tempo **Sessão de diagnóstico** para se concentrar nos dados GetMaxNumberButton_Click:  
  
 ![GetMaxNumberButton&#95;Click selecionado](../profiling/media/cpu-use-wt-getmaxnumberreport.png "CPU_USE_WT_GetMaxNumberReport")  
  
 Agora, a linha de tempo **Sessão de diagnóstico** exibe o tempo gasto no segmento selecionado (um pouco mais de 2 segundos neste relatório) e filtra a árvore de chamadas para os métodos executados na seleção.  
  
 Agora, escolha o segmento `GetMaxNumberAsyncButton_Click`.  
  
 ![GetMaxNumberAsyncButton&#95;Clique em seleção de relatório](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 Esse método é concluído cerca de um segundo mais rápido que o `GetMaxNumberButton_Click`, mas o significado das entradas da árvore de chamadas é menos óbvio.  
  
###  <a name="BKMK_The_CPU_Usage_call_tree"></a> A árvore de chamadas de Uso da CPU  
 Para começar a compreender as informações da árvore de chamadas, escolha novamente o segmento `GetMaxNumberButton_Click`, e veja os detalhes da árvore de chamadas.  
  
####  <a name="BKMK_Call_tree_structure"></a> Estrutura da árvore de chamadas  
 ![GetMaxNumberButton&#95;Clique na árvore de chamada](../profiling/media/cpu-use-wt-getmaxnumbercalltree-annotated.png "CPU_USE_WT_GetMaxNumberCallTree_annotated")  
  
|||  
|-|-|  
|![Etapa 1](../profiling/media/procguid-1.png "ProcGuid_1")|O nó de nível superior nas árvores de chamada de uso da CPU é um pseudo-nó|  
|![Etapa 2](../profiling/media/procguid-2.png "ProcGuid_2")|Na maioria dos aplicativos, quando a opção **Mostrar Código Externo** está desabilitada, o nó de segundo nível é um nó **[Código Externo]** que contém o código do sistema e da estrutura que inicia e para o aplicativo, desenha a interface do usuário, controla o agendamento de thread e fornece ao aplicativo outros serviços de nível inferior.|  
|![Etapa 3](../profiling/media/procguid-3.png "ProcGuid_3")|Os filhos do nó de segundo nível são métodos e rotinas assíncronas do código de usuário que são chamados ou criados pelo sistema de segundo nível e código do framework.|  
|![Etapa 4](../profiling/media/procguid-4.png "ProcGuid_4")|Os nós filhos de um método só contêm dados das chamadas do método pai. Quando **Mostrar Código Externo** é desabilitado, os métodos de aplicativo também podem conter um nó **[Código Externo]**.|  
  
####  <a name="BKMK_External_Code"></a> Código externo  
 O código externo consiste em funções nos componentes do sistema e da estrutura executados pelo código que você escreve. O código externo inclui funções que iniciam e param o aplicativo, elaboram a interface do usuário, controlam o threading e fornecem ao aplicativo outros serviços de nível inferior. Na maioria dos casos, você não se interessará pelo código externo, então, a árvore de chamadas de Uso da CPU coletará as funções externas de um método de usuário em um nó de **[Código Externo]**.  
  
 Quando desejar exibir os caminhos de chamada do código externo, escolha **Mostrar Código Externo** na lista **Exibição de filtro** e escolha **Aplicar**.  
  
 ![Escolher a exibição de filtro e mostrar o código externo](../profiling/media/cpu-use-wt-filterview.png "CPU_USE_WT_FilterView")  
  
 Saiba que muitas correntes de chamada de código externo são muito aninhadas, de forma que a largura da coluna Nome da Função pode exceder a largura da tela de todos os monitores de computador, exceto dos maiores. Quando isso ocorre, os nomes de função são mostrados como **[…]**:  
  
 ![Código externo aninhado na árvore de chamadas](../profiling/media/cpu-use-wt-showexternalcodetoowide.png "CPU_USE_WT_ShowExternalCodeTooWide")  
  
 Use a caixa de pesquisa para encontrar um nó que você está procurando, em seguida, use a barra de rolagem horizontal para trazer os dados para exibição:  
  
 ![Pesquisar código externo aninhado](../profiling/media/cpu-use-wt-showexternalcodetoowide-found.png "CPU_USE_WT_ShowExternalCodeTooWide_Found")  
  
###  <a name="BKMK_Call_tree_data_columns"></a> Colunas de dados da árvore de chamadas  
  
|||  
|-|-|  
|**CPU total (%)**|![Equação de % total de dados](../profiling/media/cpu-use-wt-totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> A porcentagem de atividade da CPU do aplicativo no intervalo de tempo selecionado que foi usado por chamadas para as funções e as funções chamadas pela função. Observe que isso é diferente do gráfico de linha de tempo **Utilização da CPU**, que compara a atividade total do aplicativo em um intervalo de tempo com a capacidade total disponível da CPU.|  
|**CPU própria (%)**|![Equação % própria](../profiling/media/cpu-use-wt-selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> A porcentagem de atividade da CPU do aplicativo no intervalo de tempo selecionado que foi usada pelas chamadas para as funções, exceto a atividade das funções chamadas pela função.|  
|**CPU total (ms)**|O número de milissegundos gastos em chamadas para a função no intervalo de tempo escolhido e as funções chamadas pela função.|  
|**CPU própria (ms)**|O número de milissegundos gastos em chamadas para a função no intervalo de tempo escolhido e as funções chamadas pela função.|  
|**Módulo**|O nome do módulo que contém a função ou o número de módulos que contêm as funções em um nó de [Código Externo].|  
  
###  <a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a> Funções assíncronas na árvore de chamadas de Uso da CPU  
 Quando o compilador encontra um método assíncrono, ele cria uma classe oculta para controlar o método de execução. Conceitualmente, a classe é uma máquina de estado que inclui uma lista de funções geradas pelo compilador que chamam corretamente as operações do método original de modo assíncrono, os retornos de chamadas, o agendador e os iteradores necessários a eles. Quando o método original é chamado por um método pai, o tempo de execução remove o método do contexto de execução do pai e executa os métodos da classe oculta no contexto do código do sistema e do framework que controla a execução do aplicativo. Os métodos assíncronos são geralmente, mas nem sempre, executados em uma ou mais segmentos diferentes. Esse código é mostrado na árvore de chamadas de Uso da CPU como filhos do nó **[Código Externo]** logo abaixo do nó superior da árvore.  
  
 Para ver isso em nosso exemplo, escolha novamente o segmento `GetMaxNumberAsyncButton_Click` na linha de tempo.  
  
 ![GetMaxNumberAsyncButton&#95;Clique em seleção de relatório](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 Os dois primeiros nós em **[Código Externo]** são os métodos gerados pelo compilador da classe de computador de estado. O terceiro é a chamada ao método original. Expandir os métodos gerados mostra o que está acontecendo.  
  
 ![Árvore de chamadas expandida GetMaxNumberAsyncButton&#95;Click](../profiling/media/cpu-use-wt-getmaxnumberasync-expandedcalltree.png "CPU_USE_WT_GetMaxNumberAsync_ExpandedCallTree")  
  
-   `MainPage::GetMaxNumberAsyncButton_Click` faz muito pouco; gerencia uma lista de valores da tarefa, computa o máximo de resultados e exibe a saída.  
  
-   `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` mostra a atividade necessária para agendar e iniciar as 48 tarefas que encapsulam a chamada para `GetNumberAsync`.  
  
-   `MainPage::<GetNumberAsync>b__b` mostra a atividade das tarefas que chamam `GetNumber`.  
  
##  <a name="BKMK_Next_steps"></a> Próximas etapas  
 O aplicativo CpuUseDemo não é o mais perfeito dos aplicativos, mas você pode estender sua utilidade usando-o para experimentos com operação assíncrona e outras ferramentas no hub de Desempenho e Diagnóstico.  
  
-   Observe que `MainPage::<GetNumberAsync>b__b` gasta mais tempo no [Código Externo] do que para executar o método GetNumber. Muito desse tempo é a sobrecarga de operações assíncronas. Tente aumentar o número de tarefas (definidas na constante `NUM_TASKS` de MainPage.xaml.cs) e reduzir o número de iterações em `GetNumber` (mudar o valor de `MIN_ITERATIONS`). Execute o cenário de coleta e compare a atividade da CPU do `MainPage::<GetNumberAsync>b__b`com a da sessão de diagnóstico de uso da CPU original. Tente reduzir as tarefas e aumentar as iterações.  
  
-   Os usuários não se importam com o desempenho real de seu aplicativo; eles se importam com o desempenho percebido e a capacidade de resposta do aplicativo. A ferramenta Capacidade de resposta da interface de usuário XAML mostra os detalhes da atividade no segmento da interface do usuário que afeta a capacidade de resposta percebida.  
  
     Crie uma nova sessão no de hub Desempenho e Diagnóstico e adicione as duas ferramentas Capacidade de resposta da interface de usuário XAML e Uso da CPU. Execute o cenário de coleta. Se você leu até aqui, o relatório provavelmente não diz nada que você ainda não tenha descoberto, mas as diferenças no gráfico da linha do tempo de **Utilização do Thread da interface do usuário** dos dois métodos são marcantes. Em aplicativos complexos do mundo real, a combinação de ferramentas pode ser muito útil.  
  
##  <a name="BKMK_MainPage_xaml"></a> MainPage.xaml  
  
```csharp  
<Page  
    x:Class="CpuUseDemo.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:local="using:CpuUseDemo"  
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    mc:Ignorable="d">  
  
    <Page.Resources>  
        <Style TargetType="TextBox">  
            <Setter Property="FontFamily"  Value="Lucida Console" />  
        </Style>  
    </Page.Resources>  
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">  
        <Grid.RowDefinitions>  
            <RowDefinition Height="Auto" />  
            <RowDefinition Height="*" />  
        </Grid.RowDefinitions>  
        <StackPanel Grid.Row="0" Orientation="Horizontal"  Margin="0,40,0,0">  
            <Button Name="GetMaxNumberButton" Click="GetMaxNumberButton_Click"  Content="Get Max Number" />  
            <Button Name="GetMaxNumberAsyncButton" Click="GetMaxNumberAsyncButton_Click"  Content="Get Max Number Async" />  
        </StackPanel>  
        <StackPanel Grid.Row="1">  
            <TextBox Name="TextBox1" AcceptsReturn="True" />  
        </StackPanel>  
    </Grid>  
  
</Page>  
  
```  
  
##  <a name="BKMK_MainPage_xaml_cs"></a> MainPage.xaml.cs  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.IO;  
using System.Linq;  
using System.Runtime.InteropServices.WindowsRuntime;  
using Windows.Foundation;  
using Windows.Foundation.Collections;  
using Windows.UI.Xaml;  
using Windows.UI.Xaml.Controls;  
using Windows.UI.Xaml.Controls.Primitives;  
using Windows.UI.Xaml.Data;  
using Windows.UI.Xaml.Input;  
using Windows.UI.Xaml.Media;  
using Windows.UI.Xaml.Navigation;  
using Windows.Foundation.Diagnostics;  
using System.Threading;  
using System.Threading.Tasks;  
using System.Collections.Concurrent;  
  
// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238  
  
namespace CpuUseDemo  
{  
    /// <summary>  
    /// An empty page that can be used on its own or navigated to within a Frame.  
    /// </summary>  
    public sealed partial class MainPage : Page  
    {  
        public MainPage()  
        {  
            this.InitializeComponent();  
        }  
  
        const int NUM_TASKS = 48;  
        const int MIN_ITERATIONS = int.MaxValue / 1000;  
        const int MAX_ITERATIONS = MIN_ITERATIONS + 10000;  
  
        long m_totalIterations = 0;  
        readonly object m_totalItersLock = new object();  
  
        private void GetMaxNumberButton_Click(object sender, RoutedEventArgs e)  
        {  
            GetMaxNumberAsyncButton.IsEnabled = false;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations = 0;  
            }  
            List<int> tasks = new List<int>();  
            for (var i = 0; i < NUM_TASKS; i++)  
            {  
                var result = 0;  
                result = GetNumber();  
                tasks.Add(result);  
            }  
            var max = tasks.Max();  
            var s = GetOutputString("GetMaxNumberButton_Click", NUM_TASKS, max, m_totalIterations);  
            TextBox1.Text += s;  
            GetMaxNumberAsyncButton.IsEnabled = true;  
        }  
  
        private async void GetMaxNumberAsyncButton_Click(object sender, RoutedEventArgs e)  
        {  
            GetMaxNumberButton.IsEnabled = false;  
            GetMaxNumberAsyncButton.IsEnabled = false;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations = 0;  
            }  
            var tasks = new ConcurrentBag<Task<int>>();  
            for (var i = 0; i < NUM_TASKS; i++)  
            {  
                tasks.Add(GetNumberAsync());  
            }  
            await Task.WhenAll(tasks.ToArray());  
            var max = 0;  
            foreach (var task in tasks)  
            {  
                max = Math.Max(max, task.Result);  
            }  
            var func = "GetMaxNumberAsyncButton_Click";  
            var outputText = GetOutputString(func, NUM_TASKS, max, m_totalIterations);  
            TextBox1.Text += outputText;  
            this.GetMaxNumberButton.IsEnabled = true;  
            GetMaxNumberAsyncButton.IsEnabled = true;  
        }  
  
        private int GetNumber()  
        {  
            var rand = new Random();  
            var iters = rand.Next(MIN_ITERATIONS, MAX_ITERATIONS);  
            var result = 0;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations += iters;  
            }  
            // we're just spinning here  
            // and using Random to frustrate compiler optimizations  
            for (var i = 0; i < iters; i++)  
            {  
                result = rand.Next();  
            }  
            return result;  
        }  
  
        private Task<int> GetNumberAsync()  
        {  
            return Task<int>.Run(() =>  
            {  
                return GetNumber();  
            });  
        }  
  
        string GetOutputString(string func, int cycles, int max, long totalIters)  
        {  
            var fmt = "{0,-35}Tasks:{1,3}    Maximum:{2, 12}    Iterations:{3,12}\n";  
            return String.Format(fmt, func, cycles, max, totalIters);  
        }  
  
    }  
}  
  
```



