---
title: Configurações do projeto para uma configuração de depuração de C++ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
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
- FSharp
- VB
- CSharp
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
caps.latest.revision: 52
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ca9ff0678ba2c7abafa0d988efa09437ccd27dca
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687565"
---
# <a name="project-settings-for-a-c-debug-configuration"></a>Definições do projeto para uma configuração de depuração do C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode alterar as configurações de projeto para uma configuração de depuração C ou Visual C++ na **páginas de propriedades** caixa de diálogo, conforme discutido em [como: Definir as configurações de depuração e de versão](../debugger/how-to-set-debug-and-release-configurations.md). As tabelas a seguir mostram como localizar configurações relacionadas ao depurador na caixa de diálogo **Páginas de Propriedades**.  
  
> [!WARNING]
> As configurações de projeto de depuração na **propriedades de configuração/depuração** categoria para aplicativos da Windows Store e componentes que são escritos em C++ são diferentes. Ver [iniciar uma sessão de depuração (VB, c#, C++ e XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md) no Centro de desenvolvimento do Windows.  
  
 Especifique qual depurador usar a **depurador a iniciar** caixa de listagem. Sua escolha afetará as propriedades visíveis.  
  
 Cada configuração de propriedade de depuração é automaticamente gravada e salva no arquivo “por usuário” (.vcxproj.user) para sua solução sempre que você salve sua solução.  
  
### <a name="configuration-properties-folder-debugging-category"></a>A pasta propriedades de configuração (categoria de depuração)  
  
|**Configuração**|**Descrição**|  
|-----------------|---------------------|  
|**Depurador a ser inicializado**|Especifica o depurador para executar, com as seguintes opções:<br /><br /> -   **Depurador Local do Windows**<br />-   **Depurador Remoto do Windows**<br />-   **Depurador do Navegador da Web**<br />-   **Depurador de Serviço Web**|  
|**Comando** (Depurador Local do Windows)|Especifica o comando para iniciar o programa que você está depurando no computador local.|  
|**Comando Remoto** (Depurador Remoto do Windows)|O caminho para o .exe no computador remoto. Digite o caminho exatamente como você o digitaria no computador remoto.|  
|**Argumentos do comando** (Local do Windows e depurador remoto do Windows)|– Especifica argumentos para o comando especificado anteriormente.<br /><br /> Você pode usar os seguintes operadores de redirecionamento nesta caixa:<br /><br /> < `file`<br /> Lê o stdin do arquivo.<br /><br /> > `file`<br /> Grava stdout no arquivo.<br /><br /> >> `file`<br /> Acrescenta o stdout ao arquivo.<br /><br /> 2> `file`<br /> Grava stderr no arquivo.<br /><br /> 2>> `file`<br /> Acrescenta o stderr ao arquivo.<br /><br /> 2> &1<br /> Envia a saída de stderr (2) para a mesma localidade que o stdout (1).<br /><br /> 1> &2<br /> Envia a saída de stdout (1) para a mesma localidade que o stderr (2).<br /><br /> Na maioria dos casos, esses operadores serão aplicáveis somente para aplicativos de console.|  
|**Diretório de Trabalho**|Especifica o diretório de trabalho do programa que está sendo depurado, relativo ao diretório do projeto onde o EXE está localizado. Se você deixar isso em branco, o diretório de trabalho será o diretório do projeto. A depuração remota, o diretório do projeto será no servidor remoto.|  
|**Anexar** (Depurador Local do Windows e Depurador Remoto do Windows)|Especifica se inicia ou anexa ao aplicativo. A configuração padrão é Não.|  
|**Nome do Servidor Remoto** (Depurador Remoto do Windows)|Especifica o nome de um computador (diferente do seu) no qual você deseja depurar um aplicativo.<br /><br /> A macro de compilação RemoteMachine é definida como o valor dessa propriedade; Para obter mais informações, consulte [Macros para compilar comandos e propriedades](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b).|  
|**Conexão** (Depurador Remoto do Windows)|Permite que você alterne entre tipos de conexão padrão e sem autenticação para depuração remota. Especifique um nome do computador remoto na caixa de **Nome do Servidor Remoto**. Tipos de conexão incluem o seguinte:<br /><br /> -   **Remoto sem Autenticação do Windows**<br />-   **Remoto sem autenticação (somente nativo)**<br /><br /> **Observação** Depuração remota sem a autenticação pode deixar o computador remoto vulnerável às violações de segurança. O modo de Autenticação do Windows é mais seguro.<br /><br /> Para obter mais informações, consulte [configuração de depuração remota](../debugger/remote-debugging.md).|  
|**URL HTTP** (depurador de serviço Web e depurador de navegador da Web)|Especifica a URL no qual o projeto que você está depurar está localizado.|  
|**Tipo de Depurador**|Especifica o tipo de depurador a ser usado: **Somente nativo**, **gerenciado somente**, **somente GPU**, **misto**, **automático** (padrão), ou **Script**.<br /><br /> -   **Apenas Nativo** é para código C++ não gerenciado.<br />-   **Gerenciado Somente** é para código executado no Common Language Runtime (código gerenciado).<br />-   **Misto** invoca depuradores para código gerenciado e não gerenciado.<br />-   **Automático** determina o tipo do depurador com base no compilador e as informações de EXE.<br />-   **Script** chama um depurador para scripts.<br />-   **Somente GPU** é para o código C++ AMP que é executado em um dispositivo GPU ou no rasterizador de referência de DirectX. Ver [depurando código de GPU](../debugger/debugging-gpu-code.md).|  
|**Ambiente** (Depurador Local do Windows)|Especifica variáveis de ambiente para o programa que você está depurando. Use a sintaxe de variável de ambiente padrão (por exemplo, `PATH="%SystemRoot%\..."`). Essas variáveis substituem o ambiente do sistema ou são mescladas com o ambiente do sistema, dependendo da configuração de **Ambiente de Mesclagem**. Quando você clica na coluna de configurações, uma opção "Editar..." aparece. Clique nesse link para editar variáveis de ambiente.|  
|**Ambiente de Mesclagem** (Depurador Local do Windows)|Determina se as variáveis que são especificadas na caixa **Ambiente** serão mescladas com o ambiente definido pelo sistema operacional. A configuração padrão é Sim.|  
|**Depuração de SQL** (todos, com exceção do Depurador do Conjunto de MPI)|Permite a depuração de procedimentos SQL do seu aplicativo [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]. A configuração padrão é Não.|  
|**Tipo de Acelerador de Depuração** (somente depuração de GPU)|Especifica o dispositivo GPU a ser usado para depuração. A instalação de drivers de dispositivo para dispositivos compatíveis com GPU adicionará outras opções. A configuração padrão é “GPU - emulador de software.”|  
|**Comportamento de ponto de interrupção padrão GPU** (somente depuração de GPU)|Especifica se um evento de ponto de interrupção deve ser gerado para cada thread em um warp SIMD. A configuração padrão é gerar o evento do ponto de interrupção apenas uma vez por encurvamento.|  
|**1&gt;Acelerador padrão** (somente depuração de GPU)|Especifica o acelerador padrão de AMP ao depurar o código de GPU. Escolha **Acelerador de software WARP** para investigar se um problema é causado por hardware ou por um driver em vez de por seu código.|  
|**Diretório de Implantação** (Depurador Remoto do Windows)|Especifica o caminho no computador remoto onde a saída do projeto será copiada antes da inicialização. O caminho pode ser um compartilhamento de rede no computador remoto, ou pode ser um caminho para uma pasta no computador remoto. A configuração padrão está vazia, o que significa que a saída do projeto não é copiada para um compartilhamento de rede. Para habilitar a implantação de arquivos, você também deve marcar a caixa de seleção **Implantar** na caixa de diálogo Configuration Manager. Para obter mais informações, confira [Como: Criar e editar configurações](../ide/how-to-create-and-edit-configurations.md).|  
|**Arquivos adicionais para implantar** (depurador remoto do Windows)|Se a propriedade do diretório de implantação estiver definida, esta é uma lista delimitada por ponto-e-vírgula de arquivos adicionais a serem copiados para o diretório de implantação. A configuração padrão está vazia, o que significa que nenhum arquivo adicional é copiado para o diretório de implantação. Para habilitar a implantação de arquivos, você também deve marcar a caixa de seleção **Implantar** na caixa de diálogo Configuration Manager. Para obter mais informações, confira [Como: Criar e editar configurações](../ide/how-to-create-and-edit-configurations.md).|  
|**Implantar Bibliotecas de Tempo de Execução de Depuração do Visual C++** (Depurador Remoto do Windows)|Se a propriedade do diretório de implantação estiver definida, isso especifica se as bibliotecas em tempo de execução de depuração do Visual C++ da plataforma atual devem ser copiadas para o compartilhamento de rede. A configuração padrão é Sim.|  
  
### <a name="cc-folder-general-category"></a>Pasta C/C++ (Categoria geral)  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Formato de Informação de Depuração** ([/Z7, /Zd, Zi, /ZI](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8))|Especifica o tipo de informação de depuração a ser criada para o projeto.<br /><br /> A opção padrão (/ZI) cria um banco de dados (PDB) do programa no formato Editar e Continuar compatível. Para obter mais informações, consulte [/Z7, /Zd, /Zi, /ZI (formato de informações de depuração)](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8).|  
  
### <a name="cc-folder-optimization-category"></a>Pasta C/C++ (Categoria de otimização)  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Optimization**|Especifica se o compilador deve otimizar o código que produz. A otimização altera o código que é executado. O código otimizado não corresponde ao código-fonte. Portanto, a depuração é difícil.<br /><br /> A opção padrão (**desabilitado (/ 0d**) suprime a otimização. Você pode desenvolver com a otimização suprimida e, em seguida, habilitá-la quando você criar a versão de produção do seu código.|  
  
### <a name="linker-folder-debugging-category"></a>Pasta do vinculador (categoria de depuração)  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Gerar informações de depuração** ([/DEBUG](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103))|Informe ao vinculador para incluir informações de depuração, que terá o formato especificado por /Z7, por /Zd, por Zi, ou por /ZI.|  
|**Gerar arquivo de banco de dados de programa** ([/PDB:name](https://msdn.microsoft.com/library/d23db0ce-10cb-427a-bc60-d6b2a852723d))|Especifique o nome de um arquivo de PDB nesta caixa. Você deve selecionar ZI ou /Zi para obter o formato de informações de depuração.|  
|**Segmentar Símbolos Privados** ([/PDBSTRIPPED:filename](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55))|Especifique o nome de um arquivo de PDB nesta caixa, caso não queira incluir símbolos particulares no arquivo de PDB. Esta opção cria um segundo arquivo (PDB) de banco de dados do programa quando você compila a imagem do programa com qualquer uma das opções de compilador ou vinculador que gera um arquivo PDB, como /DEBUG, /Z7, /Zd. Ou /Zi. Este segundo arquivo PDB omite os símbolos que você não desejaria enviar aos seus clientes. Para obter mais informações, consulte [/PDBSTRIPPED (Remover Símbolos Privados)](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55).|  
|**Gerar arquivo de mapa** ([/MAP](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63))|Informe ao vinculador para gerar um arquivo de mapa durante a vinculação. A configuração padrão é Não. Para obter mais informações, consulte [/MAP (Gerar Mapfile)](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63).|  
|**Nome do arquivo do mapa** ([/Map:](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)*nome*)|Se você escolher Gerar Arquivo de Mapa, poderá especificar o arquivo de mapa nesta caixa. Para obter mais informações, consulte [/MAP (Gerar Mapfile)](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63).|  
|**Exportações de Mapa** ([/MAPINFO:EXPORTS](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b))|Inclui funções exportadas no arquivo de mapa. A configuração padrão é Não. Para obter mais informações, consulte [/MAPINFO (incluir informações em Mapfile)](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b).|  
|**Assembly Depurável** ([/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b))|Especifica configurações para a opção de /ASSEMBLYDEBUG de vinculador. Os valores possíveis são:<br /><br /> -   **Nenhum atributo depurável emitido**.<br />-   **Acompanhamento de tempo de execução e desabilitação de otimizações (/ASSEMBLYDEBUG)** . Essa é a configuração padrão,<br />-   **Nenhum acompanhamento em tempo de execução e otimizações habilitadas (/ASSEMBLYDEBUG:DISABLE)** .<br />-    **\<herdar do pai ou padrões de projeto>** .<br />– Para obter mais informações, confira [/ASSEMBLYDEBUG (Adicionar DebuggableAttribute)](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982).|  
  
 Você pode alterar essas configurações na pasta Propriedades de Configuração (categoria Depuração) programaticamente usando a interface Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings>.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código nativo](../debugger/debugging-native-code.md)   
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Criando e gerenciando projetos do Visual C++](https://msdn.microsoft.com/library/11003cd8-9046-4630-a189-a32bf3b88047)   
 [/ASSEMBLYDEBUG (adicionar DebuggableAttribute)](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)   
 [Macros comuns para compilar comandos e propriedades](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b)
