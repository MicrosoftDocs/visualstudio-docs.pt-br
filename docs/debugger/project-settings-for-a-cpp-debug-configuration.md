---
title: Configurações do projeto para uma configuração de depuração do C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2018
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- VC.Project.VCDebugSettings.WebBrowser.DebuggerType
- VC.Project.IVCGPUDebugPageObject.EnvironmentMerge
- VC.Project.VCDebugSettings.SymbolPath
- VC.Project.IVCClusterDebugPageObject.ApplicationCommand
- VC.Project.IVCRemoteDebugPageObject.WorkingDirectory
- VC.Project.VCDebugSettings.DebuggerType
- VC.Project.IVCLocalDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCRemoteDebugPageObject.SQLDebugging
- VC.Project.IVCRemoteDebugPageObject.Remote
- VC.Project.IVCGPUDebugPageObject.CommandArguments
- VC.Project.VCDebugSettings.CommandArguments
- VC.Project.IVCClusterDebugPageObject.MPIRunWorkingDirectory
- VC.Project.IVCLocalDebugPageObject.SQLDebugging
- VC.Project.IVCWebSvcDebugPageObject.HttpUrl
- VC.Project.IVCLocalDebugPageObject.WorkingDirectory
- VC.Project.IVCLocalDebugPageObject.CommandArguments
- VC.Project.IVCClusterDebugPageObject.MPIRunCommand
- VC.Project.IVCGPUDebugPageObject.WorkingDirectory
- VC.Project.IVCWebSvcDebugPageObject.DebuggerType
- VC.Project.IVCRemoteDebugPageObject.CommandArguments
- VC.Project.IVCRemoteDebugPageObject.DebuggerType
- VC.Project.IVCLocalDebugPageObject.GPUBreakOnAllThreads
- VC.Project.IVCRemoteDebugPageObject.RemoteMachine
- VC.Project.IVCClusterDebugPageObject.MPIRunArguments
- VC.Project.IVCClusterDebugPageObject.MPIAcceptFilter
- VC.Project.IVCGPUDebugPageObject.RemoteConnection
- VC.Project.VCDebugSettings.PDBPath
- VC.Project.IVCRemoteDebugPageObject.DeploymentDirectory
- VC.Project.VCDebugSettings.SQLDebugging
- VC.Project.VCDebugSettings.RemoteCommand
- VC.Project.IVCClusterDebugPageObject.ShimCommand
- VC.Project.IVCLocalDebugPageObject.Command
- VC.Project.IVCRemoteDebugPageObject.GPUBreakOnAllThreads
- VC.Project.IVCLocalDebugPageObject.Attach
- VC.Project.VCDebugSettings.Command
- VC.Project.IVCRemoteDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCRemoteDebugPageObject.RemoteCommand
- VC.Project.IVCClusterDebugPageObject.ApplicationArguments
- VC.Project.IVCLocalDebugPageObject.Environment
- VC.Project.IVCGPUDebugPageObject.DeploymentDirectory
- VC.Project.IVCLocalDebugPageObject.EnvironmentMerge
- VC.Project.VCDebugSettings.Environment
- VC.Project.IVCGPUDebugPageObject.BreakpointBehavior
- VC.Project.IVCLocalDebugPageObject.DebuggerType
- VC.Project.VCDebugSettings.WebBrowser.WebBrowserDebuggerHttpUrl
- VC.Project.IVCWebSvcDebugPageObject.SQLDebugging
- VC.Project.IVCGPUDebugPageObject.AcceleratorType
- VC.Project.IVCGPUDebugPageObject.Environment
- VC.Project.VCDebugSettings.RemoteMachine
- VC.Project.IVCGPUDebugPageObject.AdditionalFilesToDeploy
- VC.Project.VCDebugSettings.WorkingDirectory
- vs.debug.builds
- VC.Project.VCDebugSettings.Attach
- VC.Project.VCDebugSettings.HttpUrl
- VC.Project.IVCClusterDebugPageObject.MPIAcceptMode
- VC.Project.IVCGPUDebugPageObject.Attach
- VC.Project.IVCRemoteDebugPageObject.AdditionalFiles
- VC.Project.IVCGPUDebugPageObject.Command
- VC.Project.VCDebugSettings.Remote
- VC.Project.IVCRemoteDebugPageObject.Attach
- VC.Project.VCDebugSettings.EnvironmentMerge
- VC.Project.IVCGPUDebugPageObject.MachineName
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- DEBUG linker option
- -PDB linker option
- -Zl compiler option [C++]
- /DEBUG linker option
- /PDBSTRIPPED linker option
- /MAPINFO linker option
- -Zd compiler option [C++]
- -DEBUG linker option
- MAPINFO linker option
- /ZI compiler option [C++]
- ZI compiler option [C++]
- Z7 compiler option [C++]
- debugging [C++], debugger settings
- project settings [Visual Studio], debug configurations
- mapfiles, project settings
- debug configurations, C++
- project settings [Visual Studio]
- /PDB linker option
- -PDBSTRIPPED linker option
- debug builds, project settings
- PDB linker option
- projects [Visual Studio], debug configurations
- project configurations, debug
- Zd compiler option [C++]
- MAP linker option
- /Z7 compiler option [C++]
- .pdb files, debug build project settings
- -MAP linker option
- -MAPINFO linker option
- /Zd compiler option [C++]
- PDBSTRIPPED linker option
- -Z7 compiler option [C++]
- pdb files, debug build project settings
- /MAP linker option
ms.assetid: 860c7f13-a108-4fe5-8fca-d235cd3ca1cb
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: b333dca8f717cbd8e1172ed00b4a044aafeed857
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389650"
---
# <a name="project-settings-for-a-c-debug-configuration"></a>Configurações do projeto para uma configuração de depuração do C++
Você pode alterar as configurações de projeto para uma configuração de depuração C ou Visual C++ na **páginas de propriedades** caixa de diálogo, conforme discutido na [como: definir a depuração e configurações de versão](../debugger/how-to-set-debug-and-release-configurations.md). As tabelas a seguir mostram como localizar configurações relacionadas ao depurador na caixa de diálogo **Páginas de Propriedades**.  
  
> [!NOTE]
>  As configurações de projeto de depuração na **propriedades de configuração/depuração** categoria são diferentes para aplicativos UWP e componentes que são escritos em C++. Ver [iniciar uma sessão de depuração (VB, c#, C++ e XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md).  
  
 Cada configuração de propriedade de depuração é automaticamente gravada e salva no arquivo "por usuário" (. vcxproj) para sua solução quando você salvar sua solução.  

 Especifique qual depurador usar a **depurador a iniciar** caixa de listagem, conforme descrito na tabela a seguir. Sua escolha afetará as propriedades visíveis.  
    
## <a name="configuration-properties-folder-debugging-category"></a>A pasta propriedades de configuração (categoria de depuração)  
  
| **Configuração** | **Descrição** |
| - | - |
| **Depurador a ser inicializado** | Especifica o depurador para executar, com as seguintes opções:<br /><br /> -   **Depurador Local do Windows**<br />-   **Depurador Remoto do Windows**<br />-   **Depurador do Navegador da Web**<br />-   **Depurador de Serviço Web** |
| **Comando** (Depurador Local do Windows) | Especifica o comando para iniciar o programa que você está depurando no computador local. |
| **Comando Remoto** (Depurador Remoto do Windows) | O caminho para o .exe no computador remoto. Digite o caminho exatamente como você o digitaria no computador remoto. |
| **Argumentos do comando** (Depurador Local do Windows)<br /><br /> **Argumentos do comando remoto** (depurador remoto do Windows) | – Especifica argumentos para o comando especificado anteriormente.<br /><br /> Você pode usar os seguintes operadores de redirecionamento nesta caixa:<br /><br /> < `file`<br /> Lê o stdin do arquivo.<br /><br /> > `file`<br /> Grava stdout no arquivo.<br /><br /> >> `file`<br /> Acrescenta o stdout ao arquivo.<br /><br /> 2> `file`<br /> Grava stderr no arquivo.<br /><br /> 2 >> `file`<br /> Acrescenta o stderr ao arquivo.<br /><br /> 2> &1<br /> Envia a saída de stderr (2) para a mesma localidade que o stdout (1).<br /><br /> 1> &2<br /> Envia a saída de stdout (1) para a mesma localidade que o stderr (2).<br /><br /> Na maioria dos casos, esses operadores serão aplicáveis somente para aplicativos de console. |
| **Diretório de Trabalho** | Especifica o diretório de trabalho do programa que está sendo depurado, relativo ao diretório do projeto onde o EXE está localizado. Se você deixar isso em branco, o diretório de trabalho será o diretório do projeto. Para depuração remota, o diretório do projeto está no servidor remoto. |
| **Anexar** (Depurador Local do Windows e Depurador Remoto do Windows) | Especifica se inicia ou anexa ao aplicativo. A configuração padrão é Não. |
| **Nome do Servidor Remoto** (Depurador Remoto do Windows) | Especifica o nome de um computador (diferente do seu) no qual você deseja depurar um aplicativo.<br /><br /> A macro de build RemoteMachine é definida com o valor desta propriedade; para obter mais informações, confira [Macros para comandos e propriedades de compilação](/cpp/ide/common-macros-for-build-commands-and-properties). |
| **Conexão** (Depurador Remoto do Windows) | Permite que você alterne entre tipos de conexão padrão e sem autenticação para depuração remota. Especifique um nome do computador remoto na caixa de **Nome do Servidor Remoto**. Tipos de conexão incluem o seguinte:<br /><br /> -   **Remoto sem Autenticação do Windows**<br />-   **Remoto Sem Autenticação**<br /><br /> **Observação** Depuração remota sem a autenticação pode deixar o computador remoto vulnerável às violações de segurança. O modo de Autenticação do Windows é mais seguro.<br /><br /> Para obter mais informações, confira [Configuração de depuração remota](../debugger/remote-debugging.md). |
| **URL HTTP** (depurador de serviço Web e depurador de navegador da Web) | Especifica a URL no qual o projeto que você está depurar está localizado. |
| **Tipo de Depurador** | Especifica o tipo de depurador a ser usado: **Somente Nativo**, **Somente Gerenciado**, **Somente GPU**, **Misto**, **Automático** (padrão) ou **Script**.<br /><br /> -   **Apenas Nativo** é para código C++ não gerenciado.<br />-   **Gerenciado Somente** é para código executado no Common Language Runtime (código gerenciado).<br />-   **Misto** invoca depuradores para código gerenciado e não gerenciado.<br />-   **Automático** determina o tipo do depurador com base no compilador e as informações de EXE.<br />-   **Script** chama um depurador para scripts.<br />-   **Somente GPU** é para o código C++ AMP que é executado em um dispositivo GPU ou no rasterizador de referência de DirectX. Ver [código de depuração de GPU](../debugger/debugging-gpu-code.md). |
| **Ambiente** (Local do Windows e depurador remoto do Windows) | Especifica variáveis de ambiente para o programa que você está depurando. Use a sintaxe de variável de ambiente padrão (por exemplo, `PATH="%SystemRoot%\..."`). Essas variáveis substituem o ambiente do sistema ou são mescladas com o ambiente do sistema, dependendo da configuração de **Ambiente de Mesclagem**. Quando você clique na coluna de configurações, um "Editar..." é exibida. Selecione o link para editar as variáveis de ambiente. |
| **Ambiente de Mesclagem** (Depurador Local do Windows) | Determina se as variáveis que são especificadas na caixa **Ambiente** serão mescladas com o ambiente definido pelo sistema operacional. A configuração padrão é Sim. |
| **Depuração de SQL** (todos, com exceção do Depurador do Conjunto de MPI) | Permite a depuração de procedimentos SQL do seu aplicativo [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)]. A configuração padrão é Não. |
| **Tipo de Acelerador de Depuração** (somente depuração de GPU) | Especifica o dispositivo GPU a ser usado para depuração. A instalação de drivers de dispositivo para dispositivos compatíveis com GPU adicionará outras opções. A configuração padrão é **GPU – Emulador de Software**. |
| **Comportamento de ponto de interrupção padrão GPU** (somente depuração de GPU) | Especifica se um evento de ponto de interrupção deve ser gerado para cada thread em um warp SIMD. A configuração padrão é gerar o evento do ponto de interrupção apenas uma vez por encurvamento. |
| **Acelerador Padrão de Amp** | Especifica o acelerador padrão de AMP ao depurar o código de GPU. Escolha **Acelerador de software WARP** para investigar se um problema é causado por hardware ou por um driver em vez de por seu código. |
| **Diretório de Implantação** (Depurador Remoto do Windows) | Especifica o caminho no computador remoto onde a saída do projeto será copiada antes da inicialização. O caminho pode ser um compartilhamento de rede no computador remoto, ou pode ser um caminho para uma pasta no computador remoto. A configuração padrão está vazia, o que significa que a saída do projeto não é copiada para um compartilhamento de rede. Para habilitar a implantação de arquivos, você também deve marcar a caixa de seleção **Implantar** na caixa de diálogo Configuration Manager. Para obter mais informações, consulte [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md). |
| **Arquivos adicionais para implantar** (depurador remoto do Windows) | Se a propriedade de diretório de implantação é definida, isso é uma lista delimitada por ponto e vírgula de arquivos adicionais para copiar para diretório de implantação. A configuração padrão está vazia, o que significa que nenhum arquivo adicional é copiado para o diretório de implantação. Para habilitar a implantação de arquivos, você também deve marcar a caixa de seleção **Implantar** na caixa de diálogo Configuration Manager. Para obter mais informações, consulte [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md). |
| **Implantar Bibliotecas de Tempo de Execução de Depuração do Visual C++** (Depurador Remoto do Windows) | Se a propriedade do diretório de implantação estiver definida, isso especifica se as bibliotecas em tempo de execução de depuração do Visual C++ da plataforma atual devem ser copiadas para o compartilhamento de rede. A configuração padrão é Sim. |
  
## <a name="cc-folder-general-category"></a>Pasta C/C++ (Categoria geral)  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Formato de Informação de Depuração** ([/Z7, /Zd, Zi, /ZI](/cpp/build/reference/z7-zi-zi-debug-information-format))|Especifica o tipo de informação de depuração a ser criada para o projeto.<br /><br /> A opção padrão (/ZI) cria um banco de dados (PDB) do programa no formato Editar e Continuar compatível. Para obter mais informações, confira [/Z7, /Zd, /Zi, /ZI (formato de informação de depuração)](/cpp/build/reference/z7-zi-zi-debug-information-format).|  
  
## <a name="cc-folder-optimization-category"></a>Pasta C/C++ (Categoria de otimização)  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Optimization**|Especifica se o compilador deve otimizar o código que produz. A otimização altera o código que é executado. O código otimizado não corresponde mais ao código-fonte, o que simplifica a depuração mais difícil.<br /><br /> A opção padrão (**Desabilitado (/0d)**) suprime a otimização. Você pode desenvolver com a otimização suprimida e, em seguida, habilitá-la quando você criar a versão de produção do seu código.|  
  
## <a name="linker-folder-debugging-category"></a>Pasta do vinculador (categoria de depuração)  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Gerar informações de depuração** ([/DEBUG](/cpp/build/reference/debug-generate-debug-info))|Informe ao vinculador para incluir informações de depuração, que terá o formato especificado por [/Z7, por /Zd, por Zi ou por /ZI](/cpp/build/reference/z7-zi-zi-debug-information-format).|  
|**Gerar arquivo de banco de dados de programa** ([/PDB:name](/cpp/build/reference/pdb-use-program-database))|Especifique o nome de um arquivo de banco de dados (PDB) do programa nesta caixa. Você deve selecionar ZI ou /Zi para obter o formato de informações de depuração.|  
|**Segmentar Símbolos Privados** ([/PDBSTRIPPED:filename](/cpp/build/reference/pdbstripped-strip-private-symbols))|Especifique o nome de um arquivo de PDB nesta caixa, caso não queira incluir símbolos particulares no arquivo de PDB. Esta opção cria um segundo arquivo PDB quando você compila a imagem do programa com qualquer opção do compilador ou vinculador opções que geram um arquivo PDB, como /DEBUG, / Z7, /Zd. Ou /Zi. Este segundo arquivo PDB omite os símbolos que você não desejaria enviar aos seus clientes. Para obter mais informações, confira [/PDBSTRIPPED (Remover símbolos privados)](/cpp/build/reference/pdbstripped-strip-private-symbols).|  
|**Gerar arquivo de mapa** ([/MAP](/cpp/build/reference/map-generate-mapfile))|Informe ao vinculador para gerar um arquivo de mapa durante a vinculação. A configuração padrão é Não. Para obter mais informações, consulte [/MAP (Gerar Mapfile)](/cpp/build/reference/map-generate-mapfile).|  
|**Nome do arquivo do mapa** ([/Map:](/cpp/build/reference/map-generate-mapfile)*nome*)|Se você escolher Gerar Arquivo de Mapa, poderá especificar o arquivo de mapa nesta caixa. Para obter mais informações, consulte [/MAP (Gerar Mapfile)](/cpp/build/reference/map-generate-mapfile).|  
|**Exportações de Mapa** ([/MAPINFO:EXPORTS](/cpp/build/reference/mapinfo-include-information-in-mapfile))|Inclui funções exportadas no arquivo de mapa. A configuração padrão é Não. Para obter mais informações, consulte [/MAPINFO (incluir informações em Mapfile)](/cpp/build/reference/mapinfo-include-information-in-mapfile).|  
|**Assembly Depurável** ([/ASSEMBLYDEBUG](/cpp/build/reference/mapinfo-include-information-in-mapfile))|Especifica configurações para a opção de /ASSEMBLYDEBUG de vinculador. Os possíveis valores são:<br /><br /> -   **Nenhum atributo depurável emitido**.<br />-   **Acompanhamento de tempo de execução e desabilitação de otimizações (/ASSEMBLYDEBUG)**. Essa é a configuração padrão,<br />-   **Nenhum acompanhamento em tempo de execução e otimizações habilitadas (/ASSEMBLYDEBUG:DISABLE)**.<br />-   **\<herdar do pai ou padrões de projeto>**.<br />– Para obter mais informações, confira [/ASSEMBLYDEBUG (Adicionar DebuggableAttribute)](/cpp/build/reference/assemblydebug-add-debuggableattribute).|  
  
 Você pode alterar essas configurações na pasta Propriedades de Configuração (categoria Depuração) programaticamente usando a interface Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings>.

## <a name="other-project-settings"></a>Outras configurações do projeto

Para depurar os tipos de projeto, como bibliotecas estáticas e DLLs, seu projeto do Visual Studio deve ser capaz de encontrar os arquivos corretos. Quando o código-fonte estiver disponível, você pode adicionar bibliotecas estáticas e DLLs como projetos separados para a mesma solução, para facilitar a depuração. Para obter informações sobre como criar esses tipos de projeto, consulte [criando e usando uma biblioteca de vínculo dinâmico (DLL)](/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp) e [criando um uma biblioteca estática usando](/cpp/windows/walkthrough-creating-and-using-a-static-library-cpp). Com o código-fonte disponível, você também pode criar um novo projeto do Visual Studio escolhendo **arquivo** > **New** > **projeto de código existente**.

Para depurar DLLs que são externas ao seu projeto, consulte [projetos de DLL de depuração](../debugger/debugging-dll-projects.md#vxtskdebuggingdllprojectsexternal). Se você precisar depurar o seu próprio projeto DLL, mas não tem acesso ao projeto para o aplicativo de chamada, consulte [como depurar de um projeto de DLL](../debugger/how-to-debug-from-a-dll-project.md).
  
## <a name="see-also"></a>Consulte também  
 [Depurando código nativo](../debugger/debugging-native-code.md)   
 [Configurações e preparação do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Criar e gerenciar projetos do Visual C++](/cpp/ide/creating-and-managing-visual-cpp-projects)   
 [/ASSEMBLYDEBUG (adicionar DebuggableAttribute)](/cpp/build/reference/assemblydebug-add-debuggableattribute)   
 [Macros comuns para comandos e propriedades de build](/cpp/ide/common-macros-for-build-commands-and-properties)