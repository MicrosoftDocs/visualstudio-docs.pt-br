---
title: Analisar o uso de rede em aplicativos UWP no Visual Studio | Microsoft Docs
ms.custom: H1Hack27Feb2017
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 45fa397d-d7a1-4c4c-9c97-ede6c21643bd
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 03b5a669c0977aa35ef6943af3fa6afe6dda2aaa
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220782"
---
# <a name="analyze-network-usage-in-uwp-apps"></a>Analisar o uso de rede em aplicativos UWP
A ferramenta de diagnóstico de **rede** do Visual Studio coleta dados sobre as operações de rede executadas usando a [API Windows.Web.Http](/uwp/api/windows.web.http). Analisar os dados pode ajudar a resolver problemas, como problemas de autenticação e acesso, uso incorreto de cache e exibição ruim e desempenho de download.  
  
 A ferramenta de Rede oferece suporte apenas a aplicativos UWP. Outras plataformas não têm suporte no momento.  
  
> [!NOTE]
>  Para obter uma descrição mais completa da ferramenta de rede, consulte [Introducing Visual Studio's network tool](https://blogs.msdn.microsoft.com/visualstudio/2015/05/04/introducing-visual-studios-network-tool/) (Apresentando a ferramenta de rede do Visual Studio).  
  
## <a name="collect-network-tool-data"></a>Coletar dados da ferramenta de rede  
 Você deve executar a ferramenta de **rede** com um projeto aberto do Visual Studio no computador do Visual Studio.  
  
1. Abra o projeto no Visual Studio.  
  
2. No menu, clique em **Depurar/Criador de Perfil de Desempenho**. Escolha **Rede**, **Iniciar**.  
  
3. A ferramenta de rede começa coletando o tráfego HTTP do seu aplicativo.  
  
    Ao executar seu aplicativo, a exibição de resumo no painel esquerdo automaticamente exibe uma lista de operações HTTP capturadas. Selecione um item na exibição de resumo para obter mais informações no painel de detalhes no painel direito.  
  
4. Selecione **Parar** para fechar o aplicativo.  
  
   A janela de relatório deve ser semelhante a essa:  
  
   ![A janela de rede](../profiling/media/network_fullwindow.png "NETWORK_FullWindow")  
  
## <a name="analyze-data"></a>Analisar dados  
 Você pode analisar o tráfego HTTP capturado enquanto o aplicativo é executado ou mesmo depois que o aplicativo foi fechado, selecionando qualquer uma das operações de rede exibidas no modo de exibição de resumo.  
  
 A exibição de resumo da **rede** mostra dados para cada operação de rede na execução do seu aplicativo. Escolha um cabeçalho de coluna para classificar a lista ou escolha os tipos de conteúdo para exibir na exibição de filtro **Tipo de conteúdo**.  
  
 Escolha **Salvar como HAR** para criar um arquivo JSON que pode ser usado por ferramentas de terceiros como o Fiddler.  
  
 A exibição de detalhes da **rede** exibe mais informações sobre uma operação de rede na exibição de resumo.  
  
 ![Painel de detalhes da ferramenta de rede](../profiling/media/network_detailsviewpane.png "NETWORK_DetailsViewPane")  
  
|||  
|-|-|  
|**Cabeçalhos**|Informações sobre os cabeçalhos de solicitação do evento.|  
|**Corpo**|A solicitação e os dados de carga de resposta.|  
|**Parâmetros**|Os valores e os nomes de parâmetro de cadeia de caracteres de consulta.|  
|**Cookies**|Dados de cookie de solicitação e resposta.|  
|**Tempo**|Um gráfico dos estágios de aquisição dos recursos selecionados.|  
  
 A barra de **resumo** de rede mostra o número de operações de rede que são exibidos em qualquer ponto, a quantidade de dados que foi transferida, quanto tempo levou para baixar e o número de erros (solicitações com respostas 4xx ou 5xx) visível.  
  
### <a name="analysis-tips"></a>Dicas de análise  
 Essa ferramenta destaca determinadas áreas que podem ser úteis ao executar a análise relacionada à rede:  
  
1.  As solicitações que são totalmente atendidas do cache são mostradas como **(do cache)** na coluna **Recebido**. Isso pode ajudar a determinar se você está usando o cache com eficiência para economizar largura de banda do usuário ou se está armazenando em cache respostas por engano e fornecendo ao usuário final do seu aplicativo dados desatualizados.  
  
2.  As respostas de erro (4xx ou 5xx) são exibidas na coluna **Resultados** com um código de status vermelho e também são realçadas na barra de resumo. Isso torna fácil a identificação de erros entre as várias solicitações em potencial em seu aplicativo.  
  
3.  O botão de impressão de resposta (dentro da guia Corpo) pode ajudá-lo a analisar as cargas de resposta JSON, XML, HTML, CSS, JavaScript e TypeScript aumentando a legibilidade do conteúdo.  
  
## <a name="see-also"></a>Consulte também  
 [Executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md)  
 [Blog do Visual Studio: apresentando o inspetor de rede do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=535022)   
 [Channel 9 Video: VS Diagnostics tools - New Network Profiler](https://channel9.msdn.com/Series/ConnectOn-Demand/206) (Vídeo do Channel 9: Ferramentas de diagnóstico do VS – novo criador de perfil de rede)  
 [Criação de perfis no Visual Studio](../profiling/index.md)  
 [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)
