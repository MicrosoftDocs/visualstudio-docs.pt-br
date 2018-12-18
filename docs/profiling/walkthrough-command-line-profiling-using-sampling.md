---
title: 'Passo a passo: Criação de perfil de linha de comando usando amostragem | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
- performance tools, command-line tools
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: db4b47582d03a7f040850dd69e61d5fee2b80020
ms.sourcegitcommit: 1b9c1e333c2f096d35cfc77e846116f8e5054557
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34815250"
---
# <a name="walkthrough-command-line-profiling-using-sampling"></a>Passo a passo: criação de perfil de linha de comando usando amostragem

Este passo a passo demonstra como criar um perfil de um aplicativo usando ferramentas de linha de comando e amostragem para identificar problemas de desempenho.

Neste passo a passo, você passará pelo processo de criação de perfil de um aplicativo gerenciado usando ferramentas de linha de comando e amostragem para isolar e identificar problemas de desempenho no aplicativo.

Neste passo a passo, você seguirá estas etapas:

- Crie o perfil de um aplicativo usando ferramentas de linha de comando e amostragem.
- Analise os resultados da criação de perfil amostrada para localizar e corrigir problemas de desempenho.

## <a name="prerequisites"></a>Pré-requisitos

- Compreensão intermediária de [!INCLUDE[csharp_current_short](../misc/includes/csharp_current_short_md.md)]
- Compreensão intermediária para trabalhar com ferramentas de linha de comando
- Uma cópia de [amostra do PeopleTrax](../profiling/peopletrax-sample-profiling-tools.md)
- Para trabalhar com as informações fornecidas pela criação de perfil, é bom ter as informações de símbolo de depuração disponíveis.

## <a name="command-line-profiling-using-the-sampling-method"></a>Criação de perfil de linha de comando usando o método de amostragem

A amostragem é um método de criação de perfil pelo qual um processo específico é monitorado periodicamente para determinar a função ativa. Os dados resultantes fornecem uma contagem da frequência da função na parte superior da pilha de chamadas, quando o processo foi amostrado.

> [!NOTE]
> As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do Visual Studio. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). O PeopleTrax é um aplicativo de 32 bits.

### <a name="to-profile-the-peopletrax-application-by-using-the-sampling-method"></a>Para criar o perfil do aplicativo PeopleTrax usando o método de amostragem

1. Instale o aplicativo de exemplo PeopleTrax e compile a versão de lançamento do aplicativo.

2. Abra uma janela de prompt de comando e adicione o diretório Ferramentas de criação de perfil à variável de ambiente Path local.

3. Altere o diretório de trabalho para o diretório que contém os binários do PeopleTrax.

4. Digite o comando a seguir para definir as variáveis de ambiente apropriadas:

    ```cmd
    VSPerfCLREnv /sampleon
    ```

5. Inicie a criação de perfil executando *VSPerfCmd.exe*, que é a ferramenta de linha de comando que controla o criador de perfil. O comando a seguir inicia o aplicativo e o criador de perfil no modo de amostragem:

    ```cmd
    VsPerfCmd /start:sample /output:PeopleTraxReport.vsp /launch:PeopleTrax.exe
    ```

     O processo do criador de perfil é iniciado e anexado ao processo *PeopleTrax.exe*. O processo do criador de perfil começa a gravar os dados de criação de perfil coletados no arquivo de relatório.

6. Clique em **Get People**.

7. Clique em **ExportData**.

     O bloco de notas é aberto e exibe um novo arquivo que contém os dados exportados do **PeopleTrax**.

8. Feche o bloco de notas e, em seguida, feche o aplicativo **PeopleTrax**.

9. Desligue o criador de perfil. Digite o seguinte comando:

    ```cmd
    VSPerfCmd /shutdown
    ```

10. Use o comando a seguir para redefinir as variáveis de ambiente:

    ```cmd
    VSPerfCLREnv /sampleoff
    ```

11. Os dados de criação de perfil são armazenados no arquivo .*vsp*. Analise os resultados usando um dos seguintes métodos:

    - Abra o arquivo .*vsp* no IDE do Visual Studio.

         – ou —

    - Gere um arquivo de valores separados por vírgula (.*csv*) usando a ferramenta de linha de comando *VSPerfReport.exe*. Para gerar relatórios de uso fora do IDE [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], use o seguinte comando:

        ```cmd
        VSPerfReport <dir> PeopleTraxReport.vsp /output:<dir> /summary:all
        ```

## <a name="see-also"></a>Consulte também

[Visão geral da sessão de desempenho](../profiling/performance-session-overview.md)  
[Criar perfil da linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)  
[VSPerfCmd](../profiling/vsperfcmd.md)  
[Noções básicas sobre valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)  
[Exibições de relatório de desempenho](../profiling/performance-report-views.md)