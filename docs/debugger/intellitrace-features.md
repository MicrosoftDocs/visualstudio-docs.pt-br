---
title: Recursos do IntelliTrace | Microsoft Docs
ms.date: 09/19/2018
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ac7ca0e59a479aff3386486d2ceaf061038db68
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536572"
---
# <a name="intellitrace-features-c-visual-basic-c"></a>Recursos do IntelliTrace (C#, Visual Basic, C++)

Você pode usar o IntelliTrace para registrar eventos e o método chama seu aplicativo, o que permite que você examine seu estado (valores de pilha de chamada e variáveis locais) em pontos diferentes na execução. Basta iniciar a depuração como de costume – o IntelliTrace é ativado por padrão e você pode ver que o IntelliTrace de informações está gravando na janela novo **ferramentas de diagnóstico** na guia **eventos** . Selecione um evento e clique em **Ativar depuração histórica** para ver a pilha de chamadas e os locais registrados para este evento.

Para obter uma descrição passo a passo, consulte [passo a passo: Usando o IntelliTrace](../debugger/walkthrough-using-intellitrace.md).

O IntelliTrace está disponível na edição Visual Studio Enterprise, mas não nas edições Visual Studio Professional ou Community.

Para confirmar que o IntelliTrace está ativado, abra as **ferramentas > opções >** página Opções do IntelliTrace. **Habilitar o IntelliTrace** deve ser verificado por padrão.

> [!NOTE]
> O escopo de todas as configurações na página de opções do **IntelliTrace** é o Visual Studio como um todo, e não projetos individuais ou soluções. Uma alteração nessas configurações se aplica a todas as instâncias do Visual Studio, todas as sessões de depuração e todos os projetos ou soluções.

## <a name="choose-the-events-that-intellitrace-records-c-visual-basic"></a><a name="ChooseEvents"></a>Escolha os eventos que o IntelliTrace registra (C#, Visual Basic)

Você pode ativar ou desativar a gravação de eventos específicos do IntelliTrace.

Se você estiver depurando, pare a depuração. Vá para **ferramentas > opções > intellitrace > eventos do IntelliTrace**. Escolha os eventos que você deseja que o IntelliTrace registre.

## <a name="collect-snapshots-c-visual-basic-c"></a><a name="Snapshots"></a>Coletar instantâneos (C#, Visual Basic, C++)

Isso não é habilitado por padrão, mas o IntelliTrace pode capturar instantâneos do seu aplicativo em cada ponto de interrupção e evento de etapa do depurador, e você pode exibir esses instantâneos em uma sessão de depuração histórica. Um instantâneo fornece uma exibição do estado completo do aplicativo. Para habilitar a captura de instantâneos, vá para **ferramentas > opções > IntelliTrace > geral**e selecione **instantâneos do IntelliTrace (gerenciados e nativos)**. Para saber mais, confira [Inspecionar estados anteriores do aplicativo usando o IntelliTrace](../debugger/view-historical-application-state.md).

Os instantâneos estão disponíveis na versão 15,5 e superior do Visual Studio Enterprise 2017 e exigem atualização de aniversário do Windows 10 ou superior.  Para aplicativos .NET Core e ASP.NET Core, Visual Studio Enterprise 2017 versão 15,7 é necessária. Para aplicativos nativos direcionados para o Windows, Visual Studio Enterprise 2017 versão 15,9 Preview 2 é necessário.

## <a name="collect-intellitrace-events-and-call-information-c-visual-basic"></a><a name="GoingFurther"></a>Coletar eventos do IntelliTrace e chamar informações (C#, Visual Basic)

Isso não é habilitado por padrão, mas o IntelliTrace pode registrar chamadas de método juntamente com eventos. Para habilitar a coleta de chamadas de método, acesse **ferramentas > opções > IntelliTrace > geral**e selecione **eventos do IntelliTrace e chame informações (somente gerenciado)**.

As informações de chamada não estão disponíveis no momento para aplicativos .NET Core e ASP.NET Core.

Isso permite que você veja o histórico da pilha de chamadas e percorra as chamadas para trás e para frente em seu código. O IntelliTrace registra dados como nomes de métodos, entrada de método e pontos de saída e certos valores de parâmetro e valores de retorno.

> [!TIP]
> Essa opção não é habilitada por padrão porque adiciona uma sobrecarga considerável. Não apenas o IntelliTrace precisa interceptar cada chamada de método que seu aplicativo faz, mas também precisa lidar com um conjunto muito maior de dados quando se trata de mostrá-lo na tela ou mantê-lo em disco.
>
> Você pode reduzir a sobrecarga de desempenho restringindo a lista de eventos que o IntelliTrace registra e mantendo o número de módulos que você está coletando para um mínimo. Para obter mais informações, consulte [controlar a quantidade de informações de chamada registros do IntelliTrace](../debugger/intellitrace-features.md#ControlCallData).

### <a name="use-the-navigation-gutter"></a>Usar a medianiz de navegação

Você pode usar a medianiz de navegação que aparece à esquerda da janela de código. Se você não vir a medianiz de navegação, vá para **ferramentas > opções > IntelliTrace > avançado**e selecione **exibir a medianiz de navegação enquanto estiver no modo de depuração**.

A medianiz de navegação permite que você avance para frente e para trás através de chamadas de método e eventos no modo de depuração histórica. Para obter mais informações sobre depuração histórica, consulte [depuração histórica](../debugger/historical-debugging.md). Ele tem vários comandos:

|Comando|Descrição|
|-|-|
|**Definir o contexto do depurador aqui**|Defina o contexto de depuração para o período de chamada onde ele aparece.<br /><br /> Esse ícone aparece apenas na pilha de chamadas atual.|
|**Voltar para o site de chamada**|Mova o ponteiro e Depurando o contexto de volta para o local em que a função atual foi chamada.<br /><br /> Se você estiver no modo de depuração dinâmica, esse comando ativará a depuração histórica em. Se você navegar de volta para a interrupção de execução original, a depuração histórica será desativada e a depuração dinâmica será ativada.|
|**Ir para chamada anterior ou para evento do IntelliTrace**|Mova o ponteiro e a depuração do contexto de volta para a chamada ou evento anterior.<br /><br /> Se você estiver no modo de depuração dinâmica, esse comando ativará a depuração histórica.|
|**Entrar**|Passe para a função selecionada no momento.<br /><br /> Esse comando está disponível somente quando você está no modo de depuração histórica.|
|**Ir para próxima chamada ou para evento do IntelliTrace**|Mova o ponteiro e o contexto de depuração para a próxima chamada ou evento para o qual os dados do IntelliTrace existem.<br /><br /> Esse comando está disponível somente quando você está no modo de depuração histórica.|
|**Ir para o modo ao vivo**|Retornar ao modo de depuração dinâmica.|

### <a name="search-for-a-line-or-method-in-intellitrace"></a>Pesquisar uma linha ou um método no IntelliTrace

Você pode Pesquisar métodos somente quando as informações de chamada de método tiverem sido habilitadas. Você pode pesquisar o histórico do IntelliTrace para uma linha ou um método específico. Enquanto a execução do depurador é interrompida, clique com o botão direito do mouse dentro do corpo da função para ver o menu de contexto e clique em **Pesquisar por essa linha no IntelliTrace** ou **pesquise esse método no IntelliTrace**.

### <a name="control-how-much-call-information-intellitrace-records"></a><a name="ControlCallData"></a> Controlar a quantidade de informações de chamada gravadas pelo IntelliTrace

Por padrão, o IntelliTrace registra informações para todos os módulos usados por sua solução. Você pode definir o IntelliTrace para registrar informações de chamada somente para os módulos que lhe interessam. Em **ferramentas > opções > módulos do intellitrace >**, você pode especificar os módulos a serem incluídos ou os módulos a serem excluídos do IntelliTrace. O IntelliTrace coletará somente os eventos originados dos módulos que você especificou e as chamadas de método que aconteceram nos módulos nos quais você está interessado.

Para adicionar vários módulos, use o caractere curinga * no início ou no final da cadeia de caracteres. Para nomes de módulos, use nomes de arquivos, e não nomes de assembly. Caminhos de arquivo não são aceitos.

Tente manter o número mínimo de módulos. Você Obtém um melhor desempenho porque há menos dados a serem coletados. Você também obtém menos ruído na interface do usuário porque há menos dados para passar.

## <a name="save-intellitrace-data-to-file-c-visual-basic-c"></a><a name="SaveSession"></a>Salvar dados do IntelliTrace em arquivo (C#, Visual Basic, C++)

Você pode salvar os dados que o IntelliTrace coletou para **depurar > o IntelliTrace > salvar a sessão do IntelliTrace** enquanto você está Depurando e o aplicativo está em um estado de interrupção. O item de menu está desabilitado e você não poderá salvar o IntelliTrace de dados coletado se o aplicativo ainda estiver em execução ou se você tiver interrompido a depuração.

Você pode configurar o IntelliTrace para salvar automaticamente em um arquivo acessando **ferramentas > opções > IntelliTrace > avançado** e selecionando **armazenar gravações do IntelliTrace nesse diretório**. Você também pode configurar um tamanho definido para o arquivo gerado, o que faz com que o IntelliTrace grave dados mais antigos quando ele ficar sem espaço. O Visual Studio cria dois arquivos para cada sessão do IntelliTrace quando eles são salvos automaticamente e o processo de hospedagem do Visual Studio (vshost.exe) é ativado.

> [!TIP]
> Para economizar espaço em disco, desative o salvamento de arquivos automaticamente quando você não precisar mais deles. Todos os arquivos existentes não serão excluídos. Você sempre pode salvar em arquivo sob demanda no menu de contexto.

Ao salvar dados do IntelliTrace no arquivo, você obtém um arquivo. itrace para cada processo que o IntelliTrace coletou. Em seguida, você pode abrir o arquivo. itrace no Visual Studio acessando **arquivo > abrir > arquivo** e selecionando o arquivo. itrace na caixa de diálogo abrir arquivo. Para obter mais informações, consulte [usando dados do IntelliTrace salvos](../debugger/using-saved-intellitrace-data.md).

## <a name="blogs"></a>Blogs

[IntelliTrace no Visual Studio Enterprise 2015](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-ultimate-2015/)

[Passo a passos de depuração dinâmica usando o IntelliTrace no Visual Studio 2015 (editor de texto)](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-text-editor/)

[Passo a passos de depuração dinâmica usando o IntelliTrace no Visual Studio 2015 (clube social)](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-social-club/)

[O IntelliTrace no Visual Studio Enterprise 2015 agora dá suporte à anexação!](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-enterprise-2015-now-supports-attach/)

[Coletar dados de um serviço do Windows usando o coletor autônomo do IntelliTrace](https://devblogs.microsoft.com/devops/collect-data-from-a-windows-service-using-the-intellitrace-standalone-collector/)

[Editando o plano de coleta do IntelliTrace](https://devblogs.microsoft.com/devops/editing-the-intellitrace-collection-plan)

[Rastreamento e depuração personalizados usando o IntelliTrace](https://devblogs.microsoft.com/devops/custom-tracesource-and-debugging-using-intellitrace/)

[Coletor autônomo do IntelliTrace e pools de aplicativos em execução em contas de Active Directory](https://devblogs.microsoft.com/devops/intellitrace-standalone-collector-and-application-pools-running-under-active-directory-accounts/)

## <a name="forums"></a>Fóruns

[Depurador do Visual Studio](https://social.msdn.microsoft.com/Forums/en-US/home)

## <a name="videos"></a>Vídeos

[Experiência do IntelliTrace](https://channel9.msdn.com/Series/Visual-Studio-2015-Enterprise-Videos/IntelliTrace-Experience)

[Depuração histórica com o IntelliTrace no Microsoft Visual Studio Ultimate 2015](https://channel9.msdn.com/events/Ignite/2015/BRK3716)
