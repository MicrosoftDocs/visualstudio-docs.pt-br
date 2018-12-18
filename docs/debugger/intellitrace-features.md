---
title: Recursos do IntelliTrace | Microsoft Docs
ms.custom: ''
ms.date: 09/19/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 59ff5fa898aa808c99dd5f52df1605336edd1694
ms.sourcegitcommit: a749c287ec7d54148505978e8ca55ccd406b71ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46542455"
---
# <a name="intellitrace-features"></a>funcionalidades do IntelliTrace

Você pode usar o IntelliTrace para registrar eventos e chamadas de método do aplicativo, que permite que você examine seu estado (pilha de chamadas e valores de variáveis locais) em pontos diferentes na execução. Basta iniciar a depuração como de costume - IntelliTrace é ativado por padrão e você pode ver as informações do IntelliTrace está gravando no novo **ferramentas de diagnóstico** janela sob o **eventos** guia. Selecione um evento e clique em **Ativar depuração histórica** para ver a pilha de chamadas e variáveis locais registradas para este evento.

Para obter uma descrição passo a passo, consulte [instruções passo a passo: usando o IntelliTrace](../debugger/walkthrough-using-intellitrace.md).

IntelliTrace está disponível no Visual Studio Enterprise edition, mas não nas edições do Visual Studio Professional ou Community.

Para confirmar que o IntelliTrace esteja ativado, abra o **Ferramentas > Opções > IntelliTrace** página de opções. **Habilitar o IntelliTrace** deverá ser marcada por padrão.

> [!NOTE]
> O escopo de todas as configurações de **IntelliTrace** página de opções é o Visual Studio como um todo, não individuais projetos ou soluções. Uma alteração nessas configurações se aplica a todas as instâncias do Visual Studio, sessões de depuração tudo e todos os projetos ou soluções.

## <a name="ChooseEvents"></a> Escolha os eventos que o IntelliTrace registra (somente código gerenciado)

Você pode ativar ou desativar a gravação de eventos específicos do IntelliTrace.

Se você estiver depurando, pare a depuração. Vá para **Ferramentas > Opções > IntelliTrace > eventos do IntelliTrace**. Escolha os eventos que você deseja que o IntelliTrace registrar.

## <a name="Snapshots"></a> Coletar instantâneos

Isso não é habilitado por padrão, mas IntelliTrace pode capturar instantâneos do seu aplicativo em cada evento de etapa do depurador e do ponto de interrupção, e você pode exibir esses instantâneos em uma sessão de depuração histórica. Um instantâneo fornece uma exibição do estado completo do aplicativo. Para habilitar a captura de instantâneos, acesse **Ferramentas > Opções > IntelliTrace > geral**e selecione **instantâneos do IntelliTrace (gerenciados e nativos)**. Para obter mais informações, consulte [inspecionar estados anteriores do aplicativo usando o IntelliTrace](../debugger/view-historical-application-state.md)

Instantâneos estão disponíveis no Visual Studio Enterprise 2017 versão 15.5 e posterior, e ela requer a atualização de aniversário do Windows 10 ou superior.  Para aplicativos .NET Core e ASP.NET Core, o Visual Studio Enterprise 2017 versão 15.7 é necessária. Para aplicativos nativos de direcionamento do Windows, versão do Visual Studio Enterprise 2017 15,9 Preview 2 é necessária.

## <a name="GoingFurther"></a> Coletar eventos do IntelliTrace e informações (somente código gerenciado) de chamada

Isso não é habilitado por padrão, mas o IntelliTrace poderá registrar chamadas de método, junto com eventos. Para habilitar a coleta de método chamadas acessem **Ferramentas > Opções > IntelliTrace > geral**e selecione **eventos do IntelliTrace e informações (somente gerenciadas) de chamada**.

Informações de chamada não estão atualmente disponíveis para aplicativos .NET Core e ASP.NET Core. 

Isso permite que você consulte o histórico da pilha de chamadas e retroceda e avance por meio de chamadas em seu código. O IntelliTrace registra dados como nomes de método, pontos de entrada e saída de método e determinados valores de parâmetros e valores de retorno.

> [!TIP]
> Essa opção não está habilitada por padrão porque ele adiciona uma sobrecarga considerável. Não apenas tem IntelliTrace interceptar todas as chamadas de método que faz com que seu aplicativo, mas ela também precisa lidar com um conjunto muito maior de dados quando se trata de mostrá-lo na tela ou persisti-los no disco.
>
> Você pode reduzir a sobrecarga de desempenho, restringindo a lista de eventos que o IntelliTrace registra e mantendo o número de módulos que você está coletando em um mínimo. Para obter mais informações, consulte [controle quanto chamar informações pelo IntelliTrace](../debugger/intellitrace-features.md#ControlCallData).

### <a name="use-the-navigation-gutter"></a>Use a medianiz de navegação

Você pode usar a medianiz de navegação que aparece à esquerda da janela de código. Se você não vir a medianiz de navegação, vá para **Ferramentas > Opções > IntelliTrace > Avançado**e selecione **exibir a medianiz de navegação em modo de depuração**.

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

### <a name="ControlCallData"></a> Controle quanto chamar informações pelo IntelliTrace

Por padrão, o IntelliTrace registra informações para todos os módulos usados pela sua solução. Você pode definir o IntelliTrace para informações de chamada de registro somente para os módulos que lhe interessam. Na **Ferramentas > Opções > IntelliTrace > módulos**, você pode especificar os módulos para incluir ou módulos a serem excluídos do IntelliTrace. IntelliTrace coletará apenas os eventos que tenham sido originados dos módulos especificados por você e as chamadas de método que ocorreram dentro de módulos que você está interessado.

Para adicionar vários módulos, use o caractere curinga * no início ou no final da cadeia de caracteres. Para nomes de módulos, use nomes de arquivos, e não nomes de assembly. Caminhos de arquivo não são aceitos.

Tente manter o número de módulos em um mínimo. Obtenha o melhor desempenho porque há menos dados a serem coletados. Você também obtém menos ruído na interface do usuário porque há menos dados para percorrer.

## <a name="SaveSession"></a> Salvar dados do IntelliTrace para arquivo

Você pode salvar os dados coletados pelo IntelliTrace vai **Depurar > IntelliTrace > Salvar a sessão do IntelliTrace** enquanto você está depurando e o aplicativo está em um estado de interrupção. O item de menu está desativado e você não poderá salvar os dados coletados pelo IntelliTrace se o aplicativo ainda está em execução ou se você interromper a depuração.

Você pode configurar o IntelliTrace para salvar automaticamente em um arquivo, vá para **Ferramentas > Opções > IntelliTrace > Avançado** e selecionando **gravações Store IntelliTrace neste diretório**. Você também pode configurar um tamanho definido para o arquivo gerado, o que faz com que o IntelliTrace para escrever sobre dados mais antigos, quando ele ficar sem espaço. Visual Studio cria dois arquivos para cada sessão do IntelliTrace quando eles são salvos automaticamente e o Visual Studio (vshost.exe) do processo de hospedagem está ativada.

> [!TIP]
> Para economizar espaço em disco, desative a salvar arquivos automaticamente quando você não precisa mais deles. Todos os arquivos existentes não serão excluídos. Você sempre pode salvar em arquivo sob demanda no menu de contexto.

Quando você salva dados do IntelliTrace para o arquivo, você obtém um arquivo. itrace para cada processo que o IntelliTrace coletado. Em seguida, você pode abrir o arquivo. itrace no Visual Studio vai **arquivo > Abrir > arquivo** e selecionando o arquivo. itrace na caixa de diálogo Abrir arquivo. Para obter mais informações, consulte [usando dados salvo do IntelliTrace](../debugger/using-saved-intellitrace-data.md).

## <a name="blogs"></a>Blogs

[IntelliTrace no Visual Studio Enterprise 2015](https://blogs.msdn.microsoft.com/devops/2015/01/16/intellitrace-in-visual-studio-ultimate-2015/)

[Instruções passo a passo de depuração tempo real usando o IntelliTrace no Visual Studio 2015 (Editor de texto)](https://blogs.msdn.microsoft.com/devops/2015/01/16/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-text-editor/)

[Instruções passo a passo de depuração tempo real usando o IntelliTrace no Visual Studio 2015 (clube Social)](https://blogs.msdn.microsoft.com/devops/2015/04/29/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-social-club/)

[IntelliTrace no Visual Studio Enterprise 2015 agora dá suporte a anexar!](https://blogs.msdn.microsoft.com/devops/2015/05/14/intellitrace-in-visual-studio-enterprise-2015-now-supports-attach/)

[Coletar dados de um serviço do windows usando o coletor do IntelliTrace autônomo](https://blogs.msdn.microsoft.com/devops/2015/05/14/collect-data-from-a-windows-service-using-the-intellitrace-standalone-collector/)

[Editar o plano de coleta do IntelliTrace](https://blogs.msdn.microsoft.com/devops/2015/03/09/editing-the-intellitrace-collection-plan/)

[TraceSource personalizado e depuração usando o IntelliTrace](https://blogs.msdn.microsoft.com/devops/2014/12/16/custom-tracesource-and-debugging-using-intellitrace/)

[IntelliTrace Standalone Collector e Pools de aplicativos executando em contas do Active Directory](https://blogs.msdn.microsoft.com/devops/2014/12/22/intellitrace-standalone-collector-and-application-pools-running-under-active-directory-accounts/)

## <a name="forums"></a>Fóruns

[Depurador do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=262263)

## <a name="videos"></a>Vídeos

[Experiência IntelliTrace](https://channel9.msdn.com/Series/Visual-Studio-2015-Enterprise-Videos/IntelliTrace-Experience)

[Histórico de depuração com o IntelliTrace no Microsoft Visual Studio Ultimate 2015](https://channel9.msdn.com/events/Ignite/2015/BRK3716)
