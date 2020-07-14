---
title: Como você pode aumentar as chances de um problema de desempenho ser corrigido
description: Informações adicionais e práticas recomendadas para o envio de problemas de desempenho no Visual Studio
author: madskristensen
ms.author: madsk
ms.date: 11/19/2019
ms.topic: conceptual
ms.openlocfilehash: 2e5718740b9219ee988859e530591305394fb239
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284302"
---
# <a name="how-to-increase-the-chances-of-a-performance-issue-being-fixed"></a>Como aumentar as chances de um problema de desempenho ser corrigido

A ferramenta "[relatar um problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio?view=vs-2019)" é amplamente usada pelos usuários do Visual Studio para relatar uma variedade de problemas. A equipe do Visual Studio se enquadra nas tendências de pane e lentidão nos comentários do usuário e resolve problemas que afetam uma ampla lançamento de usuários. Quanto mais acionável for um tíquete de comentários específico, mais provável será diagnosticado e resolvido rapidamente pela equipe do produto. Este documento descreve as práticas recomendadas ao relatar problemas de pane ou lentidão para torná-los mais acionáveis.

## <a name="general-best-practices"></a>Práticas recomendadas gerais

O Visual Studio é uma plataforma grande e complexa que dá suporte a uma infinidade de linguagens, tipos de projeto, plataformas e muito mais. A forma como ele é executado é uma função de quais componentes estão instalados e ativos em uma sessão, as extensões instaladas, as configurações do Visual Studio, a configuração da máquina e, por fim, a forma do código que está sendo editado. Dado o número de variáveis, é difícil dizer se o relatório de problemas de um usuário tem o mesmo problema subjacente que um relatório de problema de outro usuário, mesmo que o sintoma visível seja o mesmo. Considerando que, aqui estão algumas práticas recomendadas para garantir que o relatório de problemas específico tenha uma maior probabilidade de ser diagnosticado.

**Fornecer um título o mais específico possível**

Procure assinaturas distintas para o problema que está sendo relatado e inclua o máximo possível no título. Se o título for descritivo, é menos provável que os usuários com problemas não relacionados (mas o mesmo sintoma superficial) votem ou comentem sobre seu tíquete, tornando o diagnóstico do *seu* problema mais difícil.

**Em caso de dúvida, registre um novo relatório de problema**

Muitos problemas podem não ter nenhuma assinatura ou etapa distinta para reproduzir. Nesses casos, um novo relatório é melhor do que um voto ou um comentário em outro relatório, que está relatando um *sintoma*de fora semelhante. Dependendo do tipo de relatório, inclua arquivos de diagnóstico adicionais para o relatório, conforme descrito posteriormente neste documento.

**Práticas recomendadas específicas do problema**

Descritos abaixo estão os problemas que são difíceis de diagnosticar sem bons arquivos de diagnóstico. Depois de identificar o caso que melhor descreve seu problema, siga as etapas de comentários específicas para esse caso.

-   [Falhas:](#crashes) Uma falha ocorre quando o processo (Visual Studio) termina inesperadamente.

-   [Falta de resposta:](#unresponsiveness) O VS deixa de responder por um longo período de tempo.

-   [Problemas de lentidão:](#slowness-and-high-cpu-issues) Qualquer ação específica no VS é mais lenta do que o desejado

-   [Alta CPU:](#slowness-and-high-cpu-issues) Períodos estendidos de alto uso inesperado da CPU

-   [Problemas fora do processo:](#out-of-process-issues) Um problema causado por um processo de satélite do Visual Studio

## <a name="crashes"></a>Falhas
Uma falha ocorre quando o processo (Visual Studio) termina inesperadamente.

**Falhas reproduzíveis diretamente**

Falhas que podem ser reproduzidas diretamente são casos que têm todas as seguintes características:

- Pode ser observado seguindo um conjunto conhecido de etapas

- Pode ser observado em vários computadores (se disponível)

- Pode ser reproduzido no código de exemplo ou em um projeto que possa ser vinculado ou fornecido como parte dos comentários (se as etapas envolvem a abertura de um projeto ou documento)

Para esses problemas, siga as etapas em "[como relatar um problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)" e certifique-se de incluir:

-   As etapas para reproduzir o problema

-   Um projeto de reprodução autônomo, conforme descrito acima. Se a reprodução autônoma não for possível, inclua:

    -   O idioma dos projetos abertos (C \# , C++, etc.)

    -   O tipo de projeto (aplicativo de console, ASP.NET, etc.)


> [!NOTE]
> **Comentários mais valiosos:** Para esse caso, os comentários mais valiosos são o conjunto de etapas para reproduzir o problema junto com o código-fonte de exemplo.

**Falhas desconhecidas**

Se você não tiver certeza do que está causando as falhas ou se elas parecem aleatórias, você poderá capturar despejos localmente toda vez que o Visual Studio falhar e anexá-los a itens de comentários separados. Para salvar despejos localmente quando o Visual Studio falha, execute os seguintes comandos em uma janela de comando do administrador:

```
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\devenv.exe" /v DumpType /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\devenv.exe" /v DumpCount /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\devenv.exe" /v DumpFolder /t REG_SZ /d "C:\CrashDumps"

reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService32.exe" /v DumpType /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService32.exe" /v DumpCount /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService32.exe" /v DumpFolder /t REG_SZ /d "C:\CrashDumps"

reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService.exe" /v DumpType /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService.exe" /v DumpCount /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService.exe" /v DumpFolder /t REG_SZ /d "C:\CrashDumps"
```

Personalize a contagem de despejo e a pasta de despejo conforme apropriado. Encontre mais informações sobre essas configurações [aqui](/windows/win32/wer/collecting-user-mode-dumps).

> [!NOTE]
> Despejos capturados usando o Gerenciador de tarefas provavelmente serão de um bit de bit incorreto, o que os torna menos utilizáveis. O procedimento descrito acima é a maneira preferida de capturar um despejo de heap. Se você quiser usar o Gerenciador de tarefas, feche aquele que está em execução no momento, inicie o Gerenciador de tarefas de 32 bits (% windir% \\ syswow64 \\taskmgr.exe) e colete um despejo de heap a partir daí.

> [!NOTE] 
> Cada arquivo de despejo produzido por esse método terá até 4 GB de tamanho. Certifique-se de definir DumpFolder como um local com espaço em disco adequado ou ajuste o DumpCount adequadamente.

Cada vez que o Visual Studio falhar, ele criará um arquivo de despejo **devenv.exe. [ number] arquivo. dmp** no local configurado.

Em seguida, use o Visual Studio "relatar um problema..." recurso. Ele permitirá que você anexe o despejo apropriado.

1.  Localize o arquivo de despejo para a falha que você está relatando (procure um arquivo com o horário de criação correto)

2.  Se possível, compacte o arquivo ( \* . zip) para reduzir seu tamanho antes de enviar comentários

3.  Siga as etapas em "[como relatar um problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)" e anexe o despejo de heap a um novo item de comentário.

> [!NOTE] 
> **Comentários mais valiosos:** Para esse caso, os comentários mais valiosos são o despejo de heap capturado no momento da falha.

## <a name="unresponsiveness"></a>Falta
O VS deixa de responder por um longo período de tempo.

**Inresponsiva diretamente reproduzível**

Conforme descrito na seção correspondente sobre falhas, para problemas que podem ser facilmente reproduzidos, vistos em vários computadores e podem ser demonstrados em um pequeno exemplo, os relatórios de comentários mais valiosos são aqueles que incluem etapas para reproduzir o problema e incluem código-fonte de exemplo que demonstra o problema.

**Falta de resposta desconhecida**

Se uma falta de resposta se manifestar de maneira imprevisível, na próxima ocorrência, inicie uma nova instância do Visual Studio e relate um problema dessa instância.
Na [tela "registro"](/visualstudio/ide/how-to-report-a-problem-with-visual-studio?view=vs-2019#record-a-repro), certifique-se de selecionar a sessão do Visual Studio que não está respondendo.

Se a instância do Visual Studio que não está respondendo foi iniciada no modo de administrador, a segunda instância também precisaria ser iniciada no modo de administrador.

>[!NOTE] 
> **Comentários mais valiosos:** Para esse caso, os comentários mais valiosos são o despejo de heap capturado no momento da falta de resposta.

## <a name="slowness-and-high-cpu-issues"></a>Lentidão e problemas de CPU alta

O que torna um problema de uso de CPU lentidão ou alto mais acionável é um rastreamento de desempenho capturado enquanto a operação lenta ou o evento de CPU alto está em andamento.

>[!NOTE] 
> Quando possível, isole cada cenário em um relatório de comentários separado e específico.
Por exemplo, se a digitação e a navegação forem lentas, siga as etapas abaixo uma vez por problema. Isso ajuda a equipe de produto a isolar a causa de problemas específicos.

Para obter melhores resultados na captura do desempenho, siga estas etapas:

1.  Se ainda não estiver em execução, tenha uma cópia do Visual Studio aberta onde você irá reproduzir o problema

    -   Configure tudo para reproduzir o problema. Por exemplo, se você precisar que um projeto específico seja carregado com um arquivo específico aberto, certifique-se de que ambas as etapas sejam concluídas antes de continuar.

    -   Se você *não* estiver relatando um problema específico para carregar uma solução, tente aguardar 5-10 minutos (ou mais, dependendo do tamanho da solução) depois de abrir a solução antes de gravar o rastreamento de desempenho. O processo de carregamento da solução produz uma grande quantidade de dados, portanto, aguardando alguns minutos nos ajuda a concentrar-se no problema específico que você está relatando.

2.  Iniciar uma segunda cópia do Visual Studio sem *uma solução aberta*

3.  Na nova cópia do Visual Studio, abra o **relatório uma ferramenta de problema**

4.  Siga as etapas em [como relatar um problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017) até chegar à etapa "fornecer um rastreamento e despejo de heap (opcional)".

5.  Opte por registrar a primeira cópia do Visual Studio (a ocorrência de um problema de desempenho) e iniciar a gravação.

    -   O aplicativo do gravador de etapas será exibido e começará a gravar.

    -   **Durante a gravação,** execute a ação problemática na primeira cópia do Visual Studio. É difícil para nós corrigir problemas de desempenho específicos se eles não aparecerem dentro do tempo registrado.

    -   Se a ação for menor que 30 segundos e puder ser repetida com facilidade, repita a ação para demonstrar mais o problema.

    -   Na maioria dos casos, um rastreamento de 60 segundos é suficiente para demonstrar os problemas, especialmente se a ação problemática duração (ou foi repetida) por mais de 30 segundos. A duração pode ser ajustada conforme necessário para capturar o comportamento que você gostaria de corrigir.

6.  Clique em "parar registro" no gravador de etapas assim que a operação lenta ou o evento de CPU alto que você deseja relatar for concluído. Pode levar alguns minutos para processar o rastreamento de desempenho.

7.  Depois de concluído, haverá vários anexos para seus comentários. Anexe qualquer arquivo adicional que possa ajudar a reproduzir o problema (um projeto de exemplo, capturas de tela, vídeos, etc.).

8.  Envie os comentários.

Durante a gravação de um rastreamento de desempenho, se a operação lenta ou a alta CPU que você está relatando chegar a um fim, pare imediatamente a gravação. Se muitas informações forem coletadas, as informações mais antigas serão substituídas. Se o rastreamento não for interrompido em breve (dentro de alguns segundos) após a operação interessante, os dados de rastreamento úteis serão substituídos.

Não anexe diretamente rastreamentos de desempenho a itens de comentários existentes no site da comunidade de desenvolvedores. A solicitação/fornecimento de informações adicionais é um fluxo de trabalho com suporte no relatório interno de uma ferramenta problemática do Visual Studio. Se um rastreamento de desempenho for necessário para resolver um item de comentário anterior, definiremos o estado do item de comentário como "precisa de mais informações", que pode ser respondida da mesma maneira que relatar um novo problema. Para obter instruções detalhadas, consulte a [seção "precisar de mais informações"](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017?view=vs-2017#when-further-information-is-needed-need-more-info) em relatar um documento da ferramenta de problema.

> [!NOTE] 
> **Comentários mais valiosos:** Para quase todos os problemas de CPU lentidão/alta, os comentários mais valiosos são uma descrição de alto nível do que você estava tentando fazer, juntamente com o rastreamento de desempenho ( \*.etl.zip) que captura o comportamento durante esse tempo.

**Rastreamentos de desempenho avançados**

Os recursos de coleta de rastreamento no relatório-uma ferramenta de problema são suficientes para a maioria dos cenários. Mas há ocasiões em que mais controle sobre a coleta de rastreamento é necessário (por exemplo, Trace com um tamanho de buffer maior), caso em que PerfView é uma ótima ferramenta a ser usada. As etapas para registrar manualmente o rastreamento de desempenho usando a ferramenta PerfView podem ser encontradas na página [gravando rastreamentos de desempenho com Perfview](https://github.com/dotnet/roslyn/wiki/Recording-performance-traces-with-PerfView) .

## <a name="out-of-process-issues"></a>Problemas fora do processo

> [!NOTE]
> A partir do Visual Studio 2019 versão 16,3, os logs fora do processo são anexados automaticamente aos comentários enviados usando o relatório uma ferramenta problemática. No entanto, se o problema for reproduzido diretamente, seguir as etapas a seguir ainda poderá ajudar a adicionar informações adicionais para ajudar a diagnosticar melhor o problema.

Há vários processos de satélite que são executados paralelamente ao Visual Studio e fornecem diversos recursos de fora do processo principal do Visual Studio. Se ocorrer um erro em um desses processos de satélite, ele geralmente é visto no lado do Visual Studio como um ' StreamJsonRpc. RemoteInvocationException ' ou um ' StreamJsonRpc. ConnectionLostException '.

O que torna esses tipos de problemas mais acionáveis é fornecer logs adicionais que podem ser coletados seguindo estas etapas:

1.  Se esse for um problema diretamente reproduzível, comece excluindo a pasta **% Temp%/servicehub/logs** Se você não puder reproduzir esse problema, mantenha essa pasta intacta e ignore os seguintes marcadores:

    -   Definir a variável de ambiente global **ServiceHubTraceLevel** como **All**
    -   Reproduza o problema.

2.  Baixe a ferramenta de coleta de log de Microsoft Visual Studio e .NET Framework [aqui](https://www.microsoft.com/download/details.aspx?id=12493).
3.  Execute a ferramenta. Isso gera um arquivo zip para **% Temp%/vslogs.zip**. Anexe esse arquivo aos seus comentários.

## <a name="see-also"></a>Veja também

* [Opções de comentários do Visual Studio](../ide/feedback-options.md)
* [Relatar um problema com o Visual Studio para Mac](/visualstudio/mac/report-a-problem)
* [Relatar um problema com C++](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/)
* [Privacidade de dados da Comunidade de Desenvolvedores](developer-community-privacy.md)
