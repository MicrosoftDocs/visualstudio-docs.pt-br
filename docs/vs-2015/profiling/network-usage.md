---
title: Uso de rede | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 45fa397d-d7a1-4c4c-9c97-ede6c21643bd
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 20f7003bbcd319a6a8487d496697d3dcd0b7a18a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548415"
---
# <a name="network-usage"></a>Uso de Rede
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta de diagnóstico de **rede** do Visual Studio coleta dados sobre as operações de rede executadas usando a [API Windows.Web.Http](https://msdn.microsoft.com/library/windows/apps/windows.web.http.aspx). Analisar os dados pode ajudar a resolver problemas, como problemas de autenticação e acesso, uso incorreto de cache e exibição ruim e desempenho de download.  
  
 A ferramenta de rede dá suporte somente a aplicativos da Plataforma Universal do Windows. Outras plataformas não têm suporte no momento.  
  
> [!NOTE]
> Para obter uma descrição mais completa da ferramenta de rede, consulte [Introdução à ferramenta de rede do Visual Studio](https://devblogs.microsoft.com/visualstudio/?m=20155).  
  
## <a name="collecting-network-tool-data"></a>Coleta de dados da ferramenta de rede  
 Você deve executar a ferramenta de **rede** com um projeto aberto do Visual Studio no computador do Visual Studio.  
  
1. Abra o projeto no Visual Studio.  
  
2. No menu, clique em **criador de perfil de depuração/desempenho...**. Escolha **rede**e, em seguida, escolha **Iniciar**.  
  
3. A ferramenta de rede começa coletando o tráfego HTTP do seu aplicativo.  
  
    Ao executar seu aplicativo, a exibição de resumo no painel esquerdo automaticamente exibe uma lista de operações HTTP capturadas. Selecione um item na exibição de resumo para obter mais informações no painel de detalhes no painel direito.  
  
4. Selecione **Parar** para fechar o aplicativo.  
  
   A janela de relatório deve ser semelhante a:  
  
   ![A janela rede](../profiling/media/network-fullwindow.png "NETWORK_FullWindow")  
  
## <a name="analyzing-data"></a>Análise de dados  
 Você pode analisar o tráfego HTTP capturado enquanto o aplicativo é executado ou mesmo depois que o aplicativo foi fechado, selecionando qualquer uma das operações de rede exibidas no modo de exibição de resumo.  
  
 A exibição de resumo da **rede** mostra dados para cada operação de rede na execução do seu aplicativo. Escolha um cabeçalho de coluna para classificar a lista ou escolha os tipos de conteúdo para exibir na exibição de filtro **Tipo de conteúdo**.  
  
 Escolha **Salvar como HAR** para criar um arquivo JSON que pode ser usado por ferramentas de terceiros como o Fiddler.  
  
 A exibição de detalhes da **rede** exibe mais informações sobre uma operação de rede na exibição de resumo.  
  
 ![Painel de detalhes da ferramenta de rede](../profiling/media/network-detailsviewpane.png "NETWORK_DetailsViewPane")  
  
|Nome|Descrição|  
|-|-|  
|**Cabeçalhos**|Informações sobre os cabeçalhos de solicitação do evento.|  
|**Corpo**|A solicitação e os dados de carga de resposta.|  
|**Parâmetros**|Os valores e os nomes de parâmetro de cadeia de caracteres de consulta.|  
|**Cookies**|Dados de cookie de solicitação e resposta.|  
|**Timings**|Um gráfico dos estágios de aquisição dos recursos selecionados.|  
  
 A barra de **resumo** de rede mostra o número de operações de rede que são exibidos em qualquer ponto, a quantidade de dados que foi transferida, quanto tempo levou para baixar e o número de erros (solicitações com respostas 4xx ou 5xx) visível.  
  
### <a name="analysis-tips"></a>Dicas de análise  
 Essa ferramenta destaca determinadas áreas que podem ser úteis ao executar a análise relacionada à rede:  
  
1. As solicitações que são totalmente atendidas do cache são mostradas como **(do cache)** na coluna **Recebido**. Isso pode ajudar a determinar se você está usando o cache com eficiência para economizar largura de banda do usuário ou se está armazenando em cache respostas por engano e fornecendo ao usuário final do seu aplicativo dados desatualizados.  
  
2. As respostas de erro (4xx ou 5xx) são exibidas na coluna **Resultados** com um código de status vermelho e também são realçadas na barra de resumo. Isso torna fácil a identificação de erros entre as várias solicitações em potencial em seu aplicativo.  
  
3. O botão de impressão de resposta (dentro da guia Corpo) pode ajudá-lo a analisar as cargas de resposta JSON, XML, HTML, CSS, JavaScript e TypeScript aumentando a legibilidade do conteúdo.  
  
## <a name="see-also"></a>Consulte Também  
 [Executar ferramentas de criação de perfil sem depuração](https://msdn.microsoft.com/library/e97ce1a4-62d6-4b8e-a2f7-61576437ff01)   
 [Blog do Visual Studio: introdução ao inspetor de rede do Visual Studio](https://blogs.msdn.com/b/visualstudio/)   
 [Vídeo do Channel 9: ferramentas de diagnóstico do VS – novo criador de perfil de rede](https://channel9.msdn.com/Series/ConnectOn-Demand/206)
