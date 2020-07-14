---
title: IntelliTrace | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.overview
helpviewer_keywords:
- debugger, recording execution history
- debugging, recording execution history
- IntelliTrace [Visual Studio ALM]
- IntelliTrace, debugging applications
- debugger, (See also IntelliTrace [Visual Studio ALM])
- debugging, (See also IntelliTrace [Visual Studio ALM])
- IntelliTrace, collecting data from Test Manager
- IntelliTrace
- Test Manager, debugging with IntelliTrace
- IntelliTrace, debugging after a crash
ms.assetid: 486bfec2-39bd-4d78-892a-42352128ee52
caps.latest.revision: 142
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c379054506672f36368b6da99c40a0a75a25e0ac
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543917"
---
# <a name="intellitrace"></a>IntelliTrace
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A versão mais recente deste tópico pode ser encontrada no [IntelliTrace](/visualstudio/debugger/intellitrace) .  
  
Você pode gastar menos tempo Depurando seu aplicativo ao usar o IntelliTrace para registrar e rastrear o histórico de execução do código. Você pode encontrar bugs facilmente porque o IntelliTrace permite:  
  
- Registrar eventos específicos  
  
   Examine o código relacionado, os dados que aparecem na janela **locais** durante os eventos do depurador e informações de chamada de função  
  
- Depurar erros difíceis de reproduzir ou que ocorrem na implantação  
  
  Você pode usar o IntelliTrace no Visual Studio Enterprise Edition (mas não as edições Professional ou Community).  
  
## <a name="what-do-you-want-to-do"></a>O que você deseja fazer?  
  
|Cenário|Artigos|  
|-|-|  
|**Depurar meu aplicativo com o IntelliTrace:**<br /><br /> -Mostre-me eventos passados.<br />-Mostre-me informações de chamada com eventos passados.<br />-Salve minha sessão do IntelliTrace.<br />-Controlar os dados coletados pelo IntelliTrace.|-   [Walkthrough: usando o IntelliTrace](../debugger/walkthrough-using-intellitrace.md)<br />     [funcionalidades do IntelliTrace](../debugger/intellitrace-features.md)<br />-   [Configurar o IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)<br />-   [Depuração histórica](../debugger/historical-debugging.md)|  
|**Coletar dados do IntelliTrace durante uma sessão de teste no Test Manager**|-   [Coletar mais dados de diagnóstico em testes manuais](https://msdn.microsoft.com/library/bb5a2cc0-84f5-4dfe-9560-ca3d313aefd2)|  
|**Coletar dados do IntelliTrace de aplicativos implantados**|-   [Usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md)|  
|**Iniciar a depuração a partir de um arquivo de log do IntelliTrace (arquivo .iTrace).**|-   [Usando dados do IntelliTrace salvos](../debugger/using-saved-intellitrace-data.md)|  
  
## <a name="what-apps-can-i-debug-with-intellitrace"></a><a name="IntelliTraceSupport"></a> Que aplicativos posso depurar com o IntelliTrace?  
  
|Nível de suporte|Tipos de aplicativo|  
|-|-|  
|**Com suporte**|-Visual Basic e aplicativos do Visual C# que usam .NET Framework 2,0 ou versões posteriores.<br />     É possível depurar a maioria dos aplicativos, inclusive ASP.NET, Microsoft Azure, Windows Forms, WCF, WPF, Windows Workflow, SharePoint 2010, SharePoint 2013 e aplicativos de 64 bits.<br />     Para depurar aplicativos do SharePoint com o IntelliTrace, consulte [Walkthrough: Depurando um aplicativo do SharePoint usando o IntelliTrace](https://msdn.microsoft.com/library/4bd80d2f-f680-4bf4-81c3-f14e8185f6a4).<br />     Para depurar Microsoft Azure aplicativos com o IntelliTrace, consulte [Depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md).|  
|**Suporte limitado**|-F # aplicativos em uma base experimental<br />-Aplicativos da Windows Store com suporte somente para eventos|  
|**Sem suporte**|-C++, outras linguagens e script<br />-Serviços do Windows, Silverlight, Xbox ou [!INCLUDE[winmobile](../includes/winmobile-md.md)] aplicativos|  
  
> [!NOTE]
> Para depurar um processo que já está sendo executado, não é possível usar o IntelliTrace. Você deverá iniciar o IntelliTrace quando o processo for iniciado.  
  
## <a name="why-debug-with-intellitrace"></a><a name="IntelliTraceVSTraditional"></a> Por que depurar com o IntelliTrace?  
 A depuração tradicional ou *dinâmica* mostra apenas o estado atual do aplicativo, com dados limitados sobre eventos passados. Você precisa inferir esses eventos com base no estado atual do aplicativo ou precisa recriar esses eventos executando novamente seu aplicativo.  
  
 O IntelliTrace expande esta experiência tradicional de depuração ao registrar eventos específicos e os dados nesses pontos de tempo. Isso permite que você veja o que aconteceu em seu aplicativo sem reiniciá-lo, especialmente se você passar para onde o bug está. O IntelliTrace é ativado por padrão durante a depuração tradicional e coleta dados automaticamente e de forma invisível. Isso permite que você alterne facilmente entre a depuração tradicional e a depuração do IntelliTrace para consultar as informações registradas. Confira os [recursos do IntelliTrace](../debugger/intellitrace-features.md) e [quais dados o IntelliTrace coleta?](#WhatData)  
  
 O IntelliTrace também pode ajudá-lo a depurar erros que são difíceis de reproduzir ou que ocorrem na implantação. Você pode coletar dados do IntelliTrace e salvá-los em um arquivo de log do IntelliTrace (arquivo .iTrace). Um arquivo .iTrace contém detalhes sobre exceções, eventos de desempenho, solicitações da Web, dados de teste, threads, módulos e outras informações do sistema. Você pode abrir esse arquivo em Visual Studio Enterprise, selecionar um item e iniciar a depuração com o IntelliTrace. Isso permite que você vá para qualquer evento no arquivo e veja detalhes específicos sobre seu aplicativo nesse momento.  
  
 Você pode salvar dados do IntelliTrace a partir destas fontes:  
  
- Uma sessão do IntelliTrace no Visual Studio 2015 Enterprise ou versões anteriores do Visual Studio Ultimate.  
  
- Uma sessão de teste no Microsoft Test Manager  
  
- Aplicativos Web em ASP.NET hospedados no IIS ou aplicativos SharePoint 2010 e SharePoint 2013 em execução na implantação quando você usa o Agente de Monitoramento da Microsoft, sozinhos ou com o System Center 2012. Consulte [usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md) e [monitoramento com Microsoft Monitoring Agent](https://technet.microsoft.com/library/dn465153.aspx).  
  
  Estes são alguns exemplos de como o IntelliTrace pode ajudar na depuração:  
  
- Seu aplicativo danificou um arquivo de dados, mas você não sabe onde esse evento ocorreu.  
  
   Sem o IntelliTrace, você precisa examinar o código para localizar todos os acessos de arquivo possíveis, colocar pontos de interrupção nesses acessos e executar novamente o aplicativo para descobrir onde o problema ocorreu. Com o IntelliTrace, você pode ver todos os eventos de acesso a arquivos coletados e detalhes específicos sobre seu aplicativo quando cada evento ocorreu.  
  
- Uma exceção ocorre.  
  
   Sem o IntelliTrace, você receberá uma mensagem sobre uma exceção, mas não terá muitas informações sobre os eventos que levaram à exceção. Você pode examinar a pilha de chamadas para ver a cadeia de chamadas que conduziu à exceção, mas não pode ver a sequência dos eventos que aconteceram durante essas chamadas. Com o IntelliTrace, você pode examinar os eventos que ocorreram antes da exceção.  
  
- O aplicativo falha em um computador de teste, mas é executado com êxito em um computador de desenvolvimento.  
  
   Você pode coletar dados do IntelliTrace do Microsoft Test Manager, salvar os dados em um arquivo .iTrace e anexar esse arquivo a um item de trabalho do Team Foundation Server para investigação posterior. Consulte [coletar mais dados de diagnóstico em testes manuais](https://msdn.microsoft.com/library/bb5a2cc0-84f5-4dfe-9560-ca3d313aefd2) e [usando dados do IntelliTrace salvos](../debugger/using-saved-intellitrace-data.md).  
  
- Um bug ou uma falha ocorre em um aplicativo implantado.  
  
   Para aplicativos baseados em Microsoft Azure, você pode configurar a coleta de dados do IntelliTrace antes de publicar o aplicativo. Enquanto o aplicativo é executado, o IntelliTrace salva os dados em um arquivo. iTrace. Consulte [Depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md).  
  
   Para aplicativos Web em ASP.NET hospedados no IIS 7.0, 7.5 e 8.0 e aplicativos SharePoint 2010 ou SharePoint 2013, use o Agente de Monitoramento da Microsoft sozinho ou com o System Center 2012 para salvar dados do IntelliTrace em um arquivo .iTrace.  
  
   Isso é útil quando você deseja diagnosticar problemas com os aplicativos durante a implantação. Consulte [usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md).  
  
## <a name="what-data-does-intellitrace-collect"></a><a name="WhatData"></a> Que dados são coletados pelo IntelliTrace?  
 **Coletando informações do evento**  
  
 Por padrão, o IntelliTrace registra apenas eventos do IntelliTrace: eventos do depurador, exceções, .NET Framework eventos e outros eventos do sistema que podem ajudá-lo com a depuração. Você pode escolher os tipos de eventos do IntelliTrace que deseja coletar, exceto para eventos do depurador e exceções, os quais são coletados sempre. Consulte [Configurar IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e).  
  
- **Eventos do depurador**  
  
   O IntelliTrace sempre registra eventos que acontecem no depurador do Visual Studio. Por exemplo, iniciar seu aplicativo é um evento do depurador. Outros eventos do depurador estão parando eventos, o que faz com que seu aplicativo interrompa a execução. Por exemplo, seu programa atinge um ponto de interrupção, atinge um ponto de controle ou executa um comando **Etapa**.  
  
   Para ajudar no desempenho, o IntelliTrace não registra todos os valores possíveis para um evento do depurador. Em vez de isso, ele registra estes valores:  
  
  - Valores na janela **Locais**. Mantenha a janela **Locais** aberta para consultar esses valores.  
  
  - Valores na janela **Autos** somente se a janela **Autos** estiver aberta  
  
  - Valores em DataTips que surgem quando você move o ponteiro do mouse sobre uma variável na janela de origem para ver seu valor. O IntelliTrace não coleta valores em DataTips fixados.  
  
- **Exceções**  
  
   O IntelliTrace registra o tipo e a mensagem de exceção para estes tipos de exceções:  
  
  - Exceções tratadas onde a exceção é gerada e capturada  
  
  - Exceções sem tratamento  
  
- **Eventos do .NET Framework**  
  
   Por padrão, o IntelliTrace registra os eventos mais comuns do .NET Framework. Por exemplo:  
  
  - Para um evento de acesso a arquivo, o IntelliTrace coleta o nome de arquivo.  
  
  - Para um evento de marcar caixa de seleção, o IntelliTrace coleta o estado e o texto da caixa de seleção.  
  
- **Eventos de aplicativos SharePoint 2010 e SharePoint 2013**  
  
   Você pode registrar eventos de perfil de usuário e um subconjunto de eventos do ULS (Sistema de Registro Unificado) para os aplicativos SharePoint 2010 e 2013 que são executados fora do Visual Studio. Você pode salvar esses eventos em um arquivo de .iTrace. Requer Visual Studio Enterprise 2015, uma versão anterior do Visual Studio Ultimate ou [Microsoft Monitoring Agent](https://go.microsoft.com/fwlink/?LinkID=309771) em execução no modo de **rastreamento** .  
  
   Ao abrir o arquivo .iTrace, insira uma identificação de correlação do SharePoint para localizar a solicitação da Web correspondente, exibir os eventos registrados e iniciar a depuração de um evento específico. Se o arquivo contiver exceções sem tratamento, você poderá escolher uma identificação de correlação para iniciar a depuração de uma exceção.  
  
   Consulte:  
  
  - [Usar o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md)  
  
  - [Usando os dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)  
  
  - [Instruções passo a passo: depurando um aplicativo do SharePoint usando o IntelliTrace](https://msdn.microsoft.com/library/4bd80d2f-f680-4bf4-81c3-f14e8185f6a4)  
  
  **Coletando informações de chamadas de funções**  
  
  Você pode configurar o IntelliTrace para coletar informações de chamada para funções. Essas informações permitem que você veja um histórico da pilha de chamadas e permitem que você percorra para frente e para trás as chamadas no código. Para cada chamada de função, o IntelliTrace registra estes dados:  
  
- Nome da função  
  
- Valores de tipos de dados primitivos passados como parâmetros em pontos de entrada de função e retornados em pontos de saída de função  
  
- Valores de propriedades automáticas quando elas são lidas ou alteradas  
  
- Ponteiros para objetos filhos de primeiro nível, mas não seus valores diferentes caso eles fossem nulos ou não  
  
> [!NOTE]
> O IntelliTrace coleta somente os 256 primeiros objetos em matrizes e os 256 primeiros caracteres para cadeias de caracteres.  
  
 Consulte [Configurar IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e).  
  
 **Coletando informações do módulo**  
  
 Para controlar a quantidade de informações de chamadas que o IntelliTrace coleta, especifique somente os módulos que interessem a você. Isso pode ajudar a melhorar o desempenho do seu aplicativo durante a coleta. Consulte [Configurar IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e).  
  
## <a name="will-intellitrace-slow-down-my-application"></a><a name="AffectPerformance"></a>O IntelliTrace reduzirá o meu aplicativo?  
 Por padrão, o IntelliTrace coleta dados somente para eventos do IntelliTrace selecionados. Isso pode ou não retardar o seu aplicativo, dependendo da estrutura e da organização do seu código. Por exemplo, se o IntelliTrace registra um evento com frequência, isso pode tornar o aplicativo mais lento. Isso também pode fazer com que você considere refatorar seu aplicativo.  
  
 Coletar informações de chamada pode retardar significativamente seu aplicativo. Ela também pode aumentar o tamanho de qualquer arquivo de log do IntelliTrace (arquivos .iTrace) que você possa estar salvando em disco. Para minimizar esses efeitos, colete informações de chamada somente para os módulos desejados.  Para alterar o tamanho máximo de seus arquivos de .iTrace, vá para **Ferramentas**, **Opções**, **IntelliTrace**, **Avançado**. Consulte [Configurar IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e).  
  
## <a name="in-this-section"></a>Nesta seção  
 [funcionalidades do IntelliTrace](../debugger/intellitrace-features.md)  
  
 [Configurar o IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)  
  
 [Incluindo dados de rastreamento de diagnóstico que sejam difíceis de reproduzir](https://msdn.microsoft.com/library/944ae9af-5a55-4c58-b520-0108c03b3564)  
  
 [Diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md)  
  
 [Usando os dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)  
  
### <a name="blogs"></a>Blogs  
 [Team Foundation Server do Visual Studio ALM +](https://devblogs.microsoft.com/devops/welcome-to-the-visual-studio-alm-team-foundation-server-blog/)  
  
### <a name="forums"></a>Fóruns  
 [Diagnóstico do Visual Studio](https://social.msdn.microsoft.com/Forums/vsdebug)
