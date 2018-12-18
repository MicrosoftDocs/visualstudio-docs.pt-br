---
title: Recursos do IntelliTrace | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IntelliTrace, debugging with events
- IntelliTrace, recording execution history
- debugging [Visual Studio ALM], recording execution history
- IntelliTrace, turn off
- IntelliTrace, navigating event and call history
- IntelliTrace, saving your session
- IntelliTrace, enabling
- IntelliTrace, start debugging
- IntelliTrace, debugging with events and call information
- IntelliTrace, disabling
- IntelliTrace, turn on
- debugging [Visual Studio ALM], IntelliTrace
ms.assetid: 5ccc059c-6097-46b4-9d4b-34236c02d549
caps.latest.revision: 73
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d1d7e949236067331408c6b9a8268891ff8b88db
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817471"
---
# <a name="intellitrace-features"></a>funcionalidades do IntelliTrace
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o IntelliTrace para registrar eventos e chamadas de método do aplicativo, que permite que você examine seu estado (pilha de chamadas e valores de variáveis locais) em pontos diferentes na execução. Basta iniciar a depuração como de costume - IntelliTrace é ativado por padrão e você pode ver as informações do IntelliTrace está gravando no novo **ferramentas de diagnóstico** janela sob o **eventos** guia. Selecione um evento e clique em **Ativar depuração histórica** para ver a pilha de chamadas e variáveis locais registradas para este evento.  
  
 Para obter uma descrição passo a passo, consulte [instruções passo a passo: usando o IntelliTrace](../debugger/walkthrough-using-intellitrace.md).  
  
 IntelliTrace está disponível no Visual Studio Enterprise edition, mas não nas edições do Visual Studio Professional ou Community.  
  
 Para confirmar que o IntelliTrace esteja ativado, abra o **Ferramentas / opções / IntelliTrace** página de opções. **Habilitar o IntelliTrace** deverá ser marcada por padrão.  
  
> [!NOTE]
>  O escopo de todas as configurações de **IntelliTrace** página de opções é o Visual Studio como um todo, não individuais projetos ou soluções. Uma alteração nessas configurações se aplica a todas as instâncias do Visual Studio, sessões de depuração tudo e todos os projetos ou soluções.  
  
##  <a name="ChooseEvents"></a> Escolha os eventos que o IntelliTrace registra  
 Você pode ativar ou desativar a gravação de eventos específicos do IntelliTrace.  
  
 Se você estiver depurando, pare a depuração. Vá para **Ferramentas / opções / IntelliTrace / eventos do IntelliTrace**. Escolha os eventos que você deseja que o IntelliTrace registrar.  
  
##  <a name="GoingFurther"></a> Coletar eventos do IntelliTrace e informações de chamada  
 Isso não é habilitado por padrão, mas o IntelliTrace poderá registrar chamadas de método, junto com eventos. Para habilitar a coleta de método chamadas acessem **Ferramentas / opções / IntelliTrace / contabilidade**e selecione **eventos do IntelliTrace e informações de chamada**.  
  
 Isso permite que você consulte o histórico da pilha de chamadas e retroceda e avance por meio de chamadas em seu código. O IntelliTrace registra dados como nomes de método, pontos de entrada e saída de método e determinados valores de parâmetros e valores de retorno.  
  
> [!TIP]
>  Essa opção não está habilitada por padrão porque ele adiciona uma sobrecarga considerável. Não apenas tem IntelliTrace interceptar todas as chamadas de método que faz com que seu aplicativo, mas ela também precisa lidar com um conjunto muito maior de dados quando se trata de mostrá-lo na tela ou persisti-los no disco.  
>   
>  Você pode reduzir a sobrecarga de desempenho, restringindo a lista de eventos que o IntelliTrace registra e mantendo o número de módulos que você está coletando em um mínimo. Para obter mais informações, consulte [controle quanto chamar informações pelo IntelliTrace](../debugger/intellitrace-features.md#ControlCallData).  
  
### <a name="using-the-navigation-gutter"></a>Usando a medianiz de navegação  
 Você pode usar a medianiz de navegação que aparece à esquerda da janela de código. Se você não vir a medianiz de navegação, vá para **Ferramentas / opções / IntelliTrace / avançados**e selecione **exibir a medianiz de navegação em modo de depuração**.  
  
 A medianiz de navegação permite que você mova a frente e para trás por meio de chamadas de método e eventos no modo de depuração histórica. Para obter mais informações sobre o histórico de depuração, consulte [depuração histórica](../debugger/historical-debugging.md). Ele tem um número de comandos:  
  
|||  
|-|-|  
|**Definir o contexto do depurador aqui**|Defina o contexto de depuração para o período de chamada onde ele aparece.<br /><br /> Esse ícone é exibido apenas na pilha de chamadas atual.|  
|**Voltar para Site de chamada**|Mova o ponteiro e o contexto de depuração para qual a função atual foi chamada.<br /><br /> Se você estiver no modo de depuração ao vivo, este comando ativa a depuração histórica. Se você navegar de volta para a interrupção da execução original, depuração histórica está desativado e ao vivo de depuração está ativado.|  
|**Ir para chamada anterior ou evento do IntelliTrace**|Mova o ponteiro e o contexto de depuração de volta para a chamada anterior ou evento.<br /><br /> Se você estiver no modo de depuração ao vivo, este comando ativa a depuração histórica.|  
|**Entrar**|Passar para a função selecionada no momento.<br /><br /> Esse comando está disponível somente quando você estiver no modo de depuração histórica.|  
|**Ir para próxima chamada ou evento do IntelliTrace**|Mova o ponteiro e o contexto de depuração para a próxima chamada ou evento do qual IntelliTrace dados existem.<br /><br /> Esse comando está disponível somente quando você estiver no modo de depuração histórica.|  
|**Ir para modo dinâmico**|Retornar ao modo de depuração ao vivo.|  
  
### <a name="search-for-a-line-or-method-in-intellitrace"></a>Procure uma linha ou um método no IntelliTrace  
 Você pode pesquisar métodos somente quando as informações de chamada de método tem sido habilitadas. Você pode pesquisar o histórico do IntelliTrace para uma linha específica ou um método. Embora a execução do depurador é interrompida, clique com botão direito dentro do corpo da função para ver o menu de contexto e clique em **pesquisa para esta linha no IntelliTrace** ou **pesquisa para este método no IntelliTrace do**.  
  
###  <a name="ControlCallData"></a> Controle quanto chamar informações pelo IntelliTrace  
 Por padrão, o IntelliTrace registra informações para todos os módulos usados pela sua solução. Você pode definir o IntelliTrace para informações de chamada de registro somente para os módulos que lhe interessam. Na **Ferramentas / opções / IntelliTrace / módulos**, você pode especificar os módulos para incluir ou módulos a serem excluídos do IntelliTrace. IntelliTrace coletará apenas os eventos que tenham sido originados dos módulos especificados por você e as chamadas de método que ocorreram dentro de módulos que você está interessado.  
  
 Para adicionar vários módulos, use o caractere curinga * no início ou no final da cadeia de caracteres. Para nomes de módulos, use nomes de arquivos, e não nomes de assembly. Caminhos de arquivo não são aceitos.  
  
 Tente manter o número de módulos em um mínimo. Obtenha o melhor desempenho porque há menos dados a serem coletados. Você também obtém menos ruído na interface do usuário porque há menos dados para percorrer.  
  
##  <a name="SaveSession"></a> Salvando dados do IntelliTrace em arquivo  
 Você pode salvar os dados coletados pelo IntelliTrace vai **Debug / IntelliTrace / salvar a sessão do IntelliTrace** enquanto você está depurando e o aplicativo está em um estado de interrupção. O item de menu está desativado e você não poderá salvar os dados coletados pelo IntelliTrace se o aplicativo ainda está em execução ou se você interromper a depuração.  
  
 Você pode configurar o IntelliTrace para salvar automaticamente em um arquivo, vá para **Ferramentas / opções / IntelliTrace / avançados** e selecionando **gravações Store IntelliTrace neste diretório**. Você também pode configurar um tamanho definido para o arquivo gerado, o que faz com que o IntelliTrace para escrever sobre dados mais antigos, quando ele ficar sem espaço. Visual Studio cria dois arquivos para cada sessão do IntelliTrace quando eles são salvos automaticamente e o Visual Studio (vshost.exe) do processo de hospedagem está ativada.  
  
> [!TIP]
>  Para economizar espaço em disco, desative a salvar arquivos automaticamente quando você não precisa mais deles. Todos os arquivos existentes não serão excluídos. Você sempre pode salvar em arquivo sob demanda no menu de contexto.  
  
 Quando você salva dados do IntelliTrace para o arquivo, você obtém um arquivo. itrace para cada processo que o IntelliTrace coletado. Em seguida, você pode abrir o arquivo. itrace no Visual Studio vai **arquivo / abrir / arquivo** e selecionando o arquivo. itrace na caixa de diálogo Abrir arquivo. Para obter mais informações, consulte [usando dados salvo do IntelliTrace](../debugger/using-saved-intellitrace-data.md).  
  
## <a name="blogs"></a>Blogs  
 [IntelliTrace no Visual Studio Enterprise 2015](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/16/intellitrace-in-visual-studio-ultimate-2015.aspx)  
  
 [Instruções passo a passo de depuração tempo real usando o IntelliTrace no Visual Studio 2015 (Editor de texto)](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/16/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-text-editor.aspx)  
  
 [Instruções passo a passo de depuração tempo real usando o IntelliTrace no Visual Studio 2015 (clube Social)](http://blogs.msdn.com/b/visualstudioalm/archive/2000/1/1/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-social-club.aspx)  
  
 [IntelliTrace no Visual Studio Enterprise 2015 agora dá suporte a anexar!](http://blogs.msdn.com/b/visualstudioalm/archive/2015/05/14/intellitrace-in-visual-studio-enterprise-2015-now-supports-attach.aspx)  
  
 [Coletar dados de um serviço do windows usando o coletor do IntelliTrace autônomo](http://blogs.msdn.com/b/visualstudioalm/archive/2015/05/14/collect-data-from-a-windows-service-using-the-intellitrace-standalone-collector.aspx)  
  
 [Editar o plano de coleta do IntelliTrace](http://blogs.msdn.com/b/visualstudioalm/archive/2015/03/09/editing-the-intellitrace-collection-plan.aspx)  
  
 [TraceSource personalizado e depuração usando o IntelliTrace](http://blogs.msdn.com/b/visualstudioalm/archive/2014/12/17/custom-tracesource-and-debugging-using-intellitrace.aspx)  
  
 [IntelliTrace Standalone Collector e Pools de aplicativos executando em contas do Active Directory](http://blogs.msdn.com/b/visualstudioalm/archive/2014/12/22/intellitrace-standalone-collector-and-application-pools-running-under-active-directory-accounts.aspx)  
  
## <a name="forums"></a>Fóruns  
 [Depurador do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=262263)  
  
## <a name="videos"></a>Vídeos  
 [Experiência IntelliTrace](https://channel9.msdn.com/Series/Visual-Studio-2015-Enterprise-Videos/IntelliTrace-Experience)  
  
 [Histórico de depuração com o IntelliTrace no Microsoft Visual Studio Ultimate 2015](https://channel9.msdn.com/events/Ignite/2015/BRK3716)





