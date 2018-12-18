---
title: Criando perfil em clusters HPC (computação de alto desempenho) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.hpc.wizard.exeoptions
- vs.performance.hpc.wizard.summary
- vs.performance.hpc.wizard.startoptions
- vs.performance.hpc.wizard.intro
- vs.performance.hpc.property.basic
- vs.performance.hpc.wizard.application
- vs.performance.hpc.wizard.clusteroptions
- vs.performance.hpc.property.advanced
helpviewer_keywords:
- profililng tools,HPC
- HPC profiling
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: aefdd145abce513e5311d4572a9da64105226b3b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49842366"
---
# <a name="profile-on-hpc-high-performance-computing-clusters"></a>Criar perfil em clusters HPC (computação de alto desempenho)

Você pode criar um perfil em nós de computação de clusters do Microsoft Windows HPC usando o método de amostragem das Ferramentas de Criação de Perfil do Visual Studio. Para obter mais informações sobre HPC, consulte [Windows HPC](https://azure.microsoft.com/solutions/big-compute/) no site da Microsoft.

## <a name="prerequisites"></a>Pré-requisitos

Para criar o perfil em um nó de computação do HPC, faça o seguinte:

- Instale o Microsoft HPC Pack 2008 no mesmo computador onde está o Visual Studio. O computador não precisa fazer parte do cluster de HPC. Você pode instalar o HPC Pack por meio do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=177414).

- Instale o [!INCLUDE[net_v40_long](../code-quality/includes/net_v40_long_md.md)] e a versão autônoma das Ferramentas de Criação de Perfil do nó de computação do HPC. Programas de instalação estão disponíveis para ambos o [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] e o criador de perfil autônomo na mídia de instalação do Visual Studio. **Observação** Você deve reiniciar a computação depois de ter instalado [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] e antes de instalar as ferramentas de criação de perfil.

  Para instalar o [!INCLUDE[net_v40_long](../code-quality/includes/net_v40_long_md.md)] e as Ferramentas de Criação de perfil autônomas em um nó de computação do HPC ativo e habilitar a criação de perfil no computador do cluster, execute estas etapas:

1. Abra a janela de prompt de comando que é instalada com o HPC pack.

2. Digite os seguintes comandos no prompt de comando:

    1. `clusrun /all /scheduler:` *%HeadNode% %FxPath%* `/q /norestart`

    2. `clusrun /all /scheduler:` *%HeadNode%* `shutdown /r /t 0 /d u:4:2 /c "Microsoft .NET Framework install required restart"`

    3. `clusrun /all /scheduler:` *%HeadNode% %ProfilerPath%* `/q /norestart`

| | |
|------------------| - |
| *%HeadNode%* | Nome do nó principal do cluster. |
| *%FxPath%* | Caminho para o instalador de [!INCLUDE[net_v40_long](../code-quality/includes/net_v40_long_md.md)]. Na mídia de instalação do Visual Studio, o caminho é: WCU\dotNetFramework\dotNetFx40_Full_x86_x64.exe |
| *%ProfilerPath%* | Caminho para a versão autônoma do instalador das Ferramentas de Criação de Perfil. Na mídia de instalação do Visual Studio, o caminho é: Standalone Profiler\x64\vs_profiler.exe |

## <a name="profile-on-an-hpc-compute-node"></a>Criar perfil um nó de computação HPC

Você pode configurar uma sessão de criação de perfil usando o Assistente de Desempenho HPC para especificar as informações de destino e de cluster HPC. Você pode definir outras opções nas páginas de propriedade de sessão de desempenho. As Ferramentas de Criação de Perfil implantam automaticamente os binários de destino e iniciam o criador de perfil e o aplicativo do HPC.

1. No menu **Analisar**, clique em **Inicializar o Assistente de Desempenho HPC**. Se o comando não estiver disponível, verifique se você tem os pré-requisitos listados acima.

2. Clique em **Avançar** na primeira página do assistente.

3. Na segunda página do assistente, selecione o aplicativo que você deseja analisar.

   - Para analisar um projeto que está aberto no momento no [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)], selecione a opção **Um ou mais projetos disponíveis** e, em seguida, selecione o nome do projeto na lista.

   - Para analisar um binário que não está em um projeto aberto, selecione a opção **Um executável (arquivo .EXE)**.

4. Clique em **Avançar**.

5. Na terceira página do assistente:

    - Se você estiver criando o perfil de um executável que não está em um projeto aberto, especifique o caminho para o arquivo binário em **Qual é o caminho completo para o executável**.

    - Se você está criando o perfil de um executável que não está em um projeto aberto, poderá especificar quaisquer argumentos de linha de comando para passar para o processo em **Argumentos de linha de comando**.

    - Em **Diretório de trabalho remoto**, especifique o caminho para a pasta que é usada pelas instâncias do processo individual de nós de computação.

    - Em **Local de implantação**, especifique o caminho para o diretório HPC server usa para imagens do estágio de implantação.

6. Clique em **Avançar**.

7. Na quarta página do assistente:

    - Na lista **Nó Principal**, clique no computador que atua como o nó principal do HPC na criação de perfil. O nó principal pode ser "localhost", que permite analisar o computador local sem a necessidade de um cluster.

    - Na lista **Número de processos**, clique no número de instâncias do aplicativo a ser executado.

    - Da lista **Opções de criação de perfil**, selecione o destino de criação de perfil.

         Para analisar um processo específico no cluster, selecione a opção **Perfil na classificação** e, em seguida, selecione a classificação do processo na lista suspensa.

         Para analisar processos que são executados em um nó específico no cluster de HPC, selecione a opção **Perfil no nó** e, em seguida, selecione o nó da lista suspensa.

8. Clique em **Avançar**.

9. Na quinta página do assistente, você pode escolher iniciar imediatamente o criador de perfil e o processo de criação de perfil ou iniciar a criação de perfil posteriormente usando o Gerenciador de Desempenho.

    - Selecione **Inicializar a criação de perfil após a conclusão do assistente** para iniciar a criação de perfil imediatamente ou desmarque a caixa de seleção para iniciar a criação de perfil manualmente.

10. Clique em **Finalizar**.

## <a name="set-hpc-profiling-properties-by-using-performance-session-property-pages"></a>Configurar as propriedades de criação de perfil HPC usando páginas de propriedade da sessão de desempenho

Você pode alterar as propriedades de sessão de desempenho definidas no Assistente de criação de perfil HPC na página Propriedades de inicialização do HPC da página de propriedades de sessão de desempenho. Defina as opções adicionais na página Propriedades Avançadas do HPC.

### <a name="to-open-the-performance-session-property-pages"></a>Para abrir as páginas de propriedade de sessão de desempenho

1. Se necessário, abra o arquivo de sessão de desempenho (.psess) no Gerenciador de Desempenho. No menu **Arquivo**, clique em **Abrir** e localize o arquivo.

2. No Gerenciador de Desempenho, clique com o botão direito do mouse no nome da sessão de desempenho e clique em **Propriedades**.

3. Na caixa de diálogo Páginas de Propriedade, use um dos seguintes métodos:

    - Clique em **Geral** e, em seguida, selecione **Coletar no Cluster HPC** para ativar a criação de perfil do HPC ou desmarque a caixa de seleção para desabilitar a criação de perfil do HPC.

    - Clique em **Propriedades de Inicialização do HPC** para alterar as propriedades que iniciam o aplicativo HPC.

    - Clique em **Propriedades Avançadas do HPC** para definir opções adicionais

### <a name="hpc-launch-properties"></a>Propriedades de inicialização do HPC

|Propriedade|Descrição|
|--------------|-----------------|
|**Nó principal**|Especifica o computador que atua como o nó principal do HPC na criação de perfil.|
|**Número de processos**|Especifica o número de instâncias do aplicativo a serem executadas no aplicativo analisado.|
|**Perfil na classificação**|Para analisar um processo específico no cluster, selecione a opção **Perfil na classificação** e, em seguida, selecione a classificação do processo na lista suspensa.|
|**Perfil no nó**|Para analisar processos que são executados em um nó específico no cluster de HPC, selecione a opção **Perfil no nó** e, em seguida, selecione o nó da lista suspensa.|
|**Diretório de trabalho remoto**|Especifica o caminho para a pasta que é usada pelas instâncias do processo individual de nós de computação.|
|**Local de implantação**|Especifica o caminho para o diretório HPC server usa para imagens do estágio de implantação.|

### <a name="advanced-properties"></a>Propriedades avançadas

| Propriedade | Descrição |
|---------------------------------------| - |
| **Nome do projeto** | O nome do projeto ou solução [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] atual. |
| **Limpar quando o criador de perfil é interrompido** | Quando verdadeiro, remove os binários que foram implantados para o diretório de execução. Arquivos e diretórios criados pelo programa de usuário não são removidos nesta etapa. Se o diretório de execução e o diretório de implantação foram criadas pelo IDE, o IDE tenta removê-los, mas não o fará se eles tiverem arquivos não implantados pelo IDE. |
| **Arquivos adicionais a serem implantados** | Especifica uma lista separada por ponto e vírgula de arquivos adicionais para implantar em um nó de computação. Você pode clicar no botão de reticências (**...**) para selecionar vários arquivos usando uma caixa de diálogo. |
| **Comando Mpiexec** | Especifica o aplicativo que inicia o aplicativo MPI. O valor padrão é **mpiexec.exe** |
| **Argumentos Mpiexec** | Especifica os argumentos para passar para o comando mpiexec.exe. |
| **Nós solicitados no cluster** | Especifica o número de nós no cluster no qual executar o aplicativo. |
| **Implantar arquivos CRT** | Se for true, implanta o tempo de execução C/C++ no cluster. |
| **Script de pré-perfil** | Especifica o caminho e o nome de arquivo de um script a ser executado no computador de desenvolvimento local antes de iniciar a sessão de criação de perfil. |
| **Argumentos do script pré-perfil** | Especifica os argumentos que serão passados para o script pré-perfil. |
| **Script pré-perfil** | Especifica o caminho e o nome de arquivo de um script a ser executado no computador de desenvolvimento local depois de iniciar a sessão de criação de perfil. |
| **Argumentos do script pós-perfil** | Especifica os argumentos que serão passados para o script pós-perfil. |

