---
title: Opções de linha de comando do Devenv | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- switches, Devenv
- builds [Team System], command-line
- applications [Visual Studio], executing
- compiling source code, Devenv
- command-line switches, Devenv
- command line [Visual Studio], switches
- Devenv
- environment, Devenv commands
- compilers, Devenv commands
- switches
- Devenv, syntax and list of switches
ms.assetid: e12bc6ed-74fd-4bea-8d7c-89b99c20bad8
caps.latest.revision: 36
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7ee1596cf59fb4ba9b21772cdabc0c875ef8779a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49215028"
---
# <a name="devenv-command-line-switches"></a>Opções de linha de comando do desenvolvedor
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
O Devenv permite definir várias opções para o IDE (ambiente de desenvolvimento integrado) e também criar, depurar e implantar projetos com base na linha de comando. Use essas opções para executar o IDE com base em um script ou um arquivo .bat, por exemplo, um script de build noturno ou para iniciar o IDE em uma configuração específica.  
  
> [!NOTE]
>  Para tarefas relacionadas ao build, agora é recomendável usar o MSBuild em vez do devenv. Para obter mais informações, consulte [Referência de linha de comando](../../msbuild/msbuild-command-line-reference.md).  
  
> [!NOTE]
>  É necessário executar o devenv como um administrador para usar as opções [/Setup (devenv.exe)](../../ide/reference/setup-devenv-exe.md) e [/InstallVSTemplates (devenv.exe)](../../ide/reference/installvstemplates-devenv-exe.md).  
  
## <a name="devenv-switch-syntax"></a>Sintaxe da opção do devenv  
 Por padrão, os comandos do devenv passam opções para o utilitário devenv.com.  
  
 O utilitário devenv.com fornece a entrega de saída por meio de fluxos de sistema padrão, como `stdout` e `stderr` e determina o redirecionamento de E/S apropriado quando ele captura a saída, por exemplo, para um arquivo .txt. Em vez disso, comandos que começam com `devenv.exe` podem usar as mesmas opções, mas eles as enviarão para o programa devenv.exe, ignorando o utilitário devenv.com.  
  
 As regras de sintaxe para opções `devenv` são semelhantes às de outros utilitários de linha de comando do DOS. As regras de sintaxe a seguir se aplicam a todas as opções `devenv` e seus argumentos:  
  
-   Os comandos começam com `devenv`.  
  
-   As opções não diferenciam maiúsculas de minúsculas.  
  
-   Ao especificar uma solução ou um projeto, o primeiro argumento é o nome do arquivo de solução ou do arquivo de projeto, incluindo o caminho do arquivo.  
  
-   Se o primeiro argumento for um arquivo que não é uma solução ou um projeto, esse arquivo será aberto no editor apropriado, em uma nova instância do IDE.  
  
-   Ao fornecer um nome de arquivo de projeto em vez de um nome de arquivo de solução, um comando `devenv` pesquisará na pasta pai do arquivo de projeto um arquivo de solução que tem o mesmo nome. Por exemplo, o comando `devenv /build myproject1.vbproj` pesquisará na pasta pai um arquivo de solução chamado "myproject1.sln".  
  
    > [!NOTE]
    >  Apenas um arquivo de solução que referencia esse projeto deve ser localizado em sua pasta pai. Se a pasta pai não contiver nenhum arquivo de solução que referencie esse projeto ou se a pasta pai contiver dois ou mais arquivos de solução que a referenciem, então um arquivo de solução temporário será criado, nomeado para esse projeto e o referenciará.  
  
-   Quando nomes de arquivo e caminhos de arquivo incluírem espaços, será necessário circunscrevê-los em aspas duplas (""). Por exemplo, "c:\project um\\".  
  
-   Insira um caractere de espaço entre as opções e os argumentos na mesma linha. Por exemplo, o comando **devenv /log output.txt** abre o IDE e gera todas as informações de log dessa sessão para output.txt.  
  
-   Não é possível usar sintaxe de correspondência de padrões em comandos `devenv`.  
  
## <a name="devenv-switches"></a>Opções do devenv  
 Use as seguintes opções de linha de comando para exibir o IDE e realizar a tarefa descrita.  
  
|Opção de linha de comando|Descrição|  
|-------------------------|-----------------|  
|[/Command (devenv.exe)](../../ide/reference/command-devenv-exe.md)|Inicia o IDE e executa o comando especificado.|  
|[/DebugExe (devenv.exe)](../../ide/reference/debugexe-devenv-exe.md)|Carrega um executável [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] no controle do depurador. Essa opção não está disponível para os executáveis [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ou [!INCLUDE[csprcs](../../includes/csprcs-md.md)]. Para obter mais informações, consulte [Automatically start a process in the debugger (Iniciar automaticamente um processo no depurador)](../../debugger/debug-multiple-processes.md#BKMK_Automatically_start_an_process_in_the_debugger).|  
|[/LCID (devenv.exe)](../../ide/reference/lcid-devenv-exe.md) or `/l`|Define o idioma padrão do IDE. Se a linguagem especificada não estiver incluída em sua instalação do Visual Studio, essa configuração será ignorada.|  
|[/Log (devenv.exe)](../../ide/reference/log-devenv-exe.md)|Inicia [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e registra toda a atividade no arquivo de log.|  
|[/Run (devenv.exe)](../../ide/reference/run-devenv-exe.md) ou `/r`|Compila e executa a solução especificada.|  
|[/Runexit (devenv.exe)](../../ide/reference/runexit-devenv-exe.md)|Compila e executa a solução especificada, minimiza o IDE quando a solução é executada e fecha o IDE depois que a solução termina a execução.|  
|[/UseEnv (devenv.exe)](../../ide/reference/useenv-devenv-exe.md)|Faz com que o IDE use variáveis de ambiente PATH, INCLUDE e LIB para a compilação [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] em vez das configurações especificadas na seção Diretórios VC++ de opções **Projetos** na caixa de diálogo **Opções**. Para obter mais informações, consulte [Configurar o caminho e variáveis de ambiente para Builds de linha de comando](http://msdn.microsoft.com/library/99389528-deb5-43b9-b99a-03c8773ebaf4)|  
|[/Edit (devenv.exe)](../../ide/reference/edit-devenv-exe.md)|Abre os arquivos especificados em uma instância em execução deste aplicativo. Se não houver nenhuma instância em execução, uma nova instância será iniciada com um layout de janela simplificado.|  
|[/ResetAddin (devenv.exe)](../../ide/reference/resetaddin-devenv-exe.md)|Inicia uma instância do IDE do Visual Studio sem carregar o suplemento especificado.|  
|[/SafeMode (devenv.exe)](../../ide/reference/safemode-devenv-exe.md)|Inicia [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] no modo de segurança e carrega somente o ambiente e os serviços padrão e as versões enviadas de pacotes de terceiros.|  
|[/ResetSkipPkgs (devenv.exe)](../../ide/reference/resetskippkgs-devenv-exe.md)|Limpa todas as marcações SkipLoading que foram adicionadas aos VSPackages por usuários que desejam evitar carregar VSPackages com problemas.|  
|[/Setup (devenv.exe)](../../ide/reference/setup-devenv-exe.md)|Força o Visual Studio a mesclar os metadados de recursos que descrevem menus, barras de ferramentas e grupos de comando de todos os VSPackages disponíveis.|  
  
 Use as seguintes opções de linha de comando para realizar a tarefa descrita. Essas opções de linha de comando não exibem o IDE.  
  
|Opção de linha de comando|Descrição|  
|-------------------------|-----------------|  
|[/? (devenv.exe)](../../ide/reference/q-devenv-exe.md)|Exibe ajuda para opções do devenv na **Janela do prompt de comando**.<br /><br /> **Devenv /?**|  
|[/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)|Cria a solução ou o projeto especificado de acordo com a configuração da solução especificada.<br /><br /> **Devenv myproj.csproj /build**|  
|[/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)|Exclui os arquivos criados pelo comando de build sem afetar os arquivos de origem.<br /><br /> **Devenv myproj.csproj /clean**|  
|[/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)|Compila a solução, juntamente com os arquivos necessários para a implantação, de acordo com a configuração de soluções.<br /><br /> **Devenv myproj.csproj /deploy**|  
|[/Diff](../../ide/reference/diff.md)|Compara dois arquivos.  Assume quatro parâmetros: SourceFile, TargetFile, SourceDisplayName(opcional),TargetDisplayName(opcional).|  
|[/InstallVSTemplates (devenv.exe)](../../ide/reference/installvstemplates-devenv-exe.md)|Registra modelos de item ou de projeto localizados em *\<VisualStudioInstallDir>* \Common7\IDE\ProjectTemplates ou *\<VisualStudioInstallDir>* \Common7\IDE\ItemTemplates para que eles possam ser acessados por meio das caixas de diálogo **Novo projeto** e **Adicionar novo item**.<br /><br /> **Devenv /InstallVSTemplates**|  
|[/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)|Permite que você especifique um arquivo para receber erros ao compilar.<br /><br /> **Devenv myproj.csproj /build /out log.txt**|  
|[/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md)|O projeto a ser criado, limpo ou implantado. Será possível usar essa opção somente se você tiver fornecido também a opção /build, /rebuild, /clean ou /deploy.|  
|[/ProjectConfig (devenv.exe)](../../ide/reference/projectconfig-devenv-exe.md)|Especifica a configuração de projeto a ser criada ou implantada. Será possível usar essa opção somente se você tiver fornecido a opção /project.|  
|[/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)|Limpa e depois compila a solução ou o projeto especificado de acordo com a configuração da solução especificada.|  
|[/ResetSettings (devenv.exe)](../../ide/reference/resetsettings-devenv-exe.md)|Restaura as configurações padrão do Visual Studio. Opcionalmente, redefine as configurações para o arquivo .vssettings especificado.|  
|[/Updateconfiguration (devenv.exe)](../../ide/reference/updateconfiguration-devenv-exe.md)|Notifica o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para mesclar os pacotes [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] no sistema e verificar o cache MEF para as alterações.|  
|[/Upgrade (devenv.exe)](../../ide/reference/upgrade-devenv-exe.md)|Atualiza o arquivo de solução especificado e todos os seus arquivos de projeto ou o arquivo de projeto especificado, para os formatos [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] atuais para esses arquivos.|  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Geral, Ambiente, Opções](../../ide/reference/general-environment-options-dialog-box.md)



