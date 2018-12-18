---
title: Opções de linha de comando devenv do Visual Studio
ms.date: 02/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- switches, Devenv
- command-line switches, Devenv
- command line [Visual Studio], switches
- Devenv
ms.assetid: e12bc6ed-74fd-4bea-8d7c-89b99c20bad8
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 818bbb38fab706dde2f4d36d5a534e0a351a6450
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948888"
---
# <a name="devenv-command-line-switches"></a>Opções de linha de comando do Devenv

O Devenv permite definir várias opções para o IDE (ambiente de desenvolvimento integrado), assim como criar, depurar e implantar projetos com base na linha de comando. Use essas opções para executar o IDE com base em um script ou um arquivo .bat, por exemplo, um script de build noturno ou para iniciar o IDE em uma configuração específica.

> [!NOTE]
> Para tarefas relacionadas ao build, é recomendável usar o MSBuild em vez do devenv. Para obter mais informações, consulte [Referência de linha de comando do MSBuild](../../msbuild/msbuild-command-line-reference.md).

## <a name="devenv-switch-syntax"></a>Sintaxe da opção do devenv

Os comandos que começam com `devenv` são manipuladas pelo utilitário do `devenv.com`, que fornece a saída por meio de fluxos de sistema padrão, como `stdout` e `stderr`. O utilitário determina o redirecionamento de E/S apropriado quando ele captura a saída, por exemplo, em um arquivo .txt.

Por outro lado, os comandos que começam com `devenv.exe` podem usar as mesmas opções, mas o utilitário `devenv.com` é ignorado. Usando `devenv.exe` diretamente impede que a saída seja exibida no console.

As regras de sintaxe para opções `devenv` são semelhantes às de outros utilitários de linha de comando do DOS. As regras de sintaxe a seguir se aplicam a todas as opções `devenv` e seus argumentos:

- Os comandos começam com `devenv`.

- As opções não diferenciam maiúsculas de minúsculas.

- Ao especificar uma solução ou um projeto, o primeiro argumento é o nome do arquivo de solução ou do arquivo de projeto, incluindo o caminho do arquivo.

- Se o primeiro argumento for um arquivo que não é uma solução ou um projeto, esse arquivo será aberto no editor apropriado, em uma nova instância do IDE.

- Ao fornecer um nome de arquivo de projeto em vez de um nome de arquivo de solução, um comando `devenv` pesquisa na pasta pai do arquivo de projeto um arquivo de solução que tem o mesmo nome. Por exemplo, o comando `devenv myproject1.vbproj /build` pesquisa na pasta pai um arquivo de solução chamado "myproject1.sln".

    > [!NOTE]
    > Apenas um arquivo de solução que referencia esse projeto deve ser localizado em sua pasta pai. Se a pasta pai não contiver nenhum arquivo de solução que referencie esse projeto ou se contiver dois ou mais arquivos de solução que a referenciem, então um arquivo de solução temporário será criado.

- Quando nomes de arquivo e caminhos de arquivo incluírem espaços, será necessário usar aspas duplas (""). Por exemplo, "c:\project um\\".

- Insira um caractere de espaço entre as opções e os argumentos na mesma linha. Por exemplo, o comando **devenv /log output.txt** abre o IDE e gera todas as informações de log dessa sessão para output.txt.

- Não é possível usar sintaxe de correspondência de padrões em comandos `devenv`.

## <a name="devenv-switches"></a>Opções do devenv

As seguintes opções de linha de comando exibem o IDE e realizam a tarefa descrita.

|Opção de linha de comando|Descrição|
| - |-----------------|
|[/Command](../../ide/reference/command-devenv-exe.md)|Inicia o IDE e executa o comando especificado.|
|[/DebugExe](../../ide/reference/debugexe-devenv-exe.md)|Carrega um executável C++ no controle do depurador. Essa opção não está disponível para os executáveis do Visual Basic ou do C++. Para obter mais informações, consulte [Automatically start a process in the debugger (Iniciar automaticamente um processo no depurador)](../../debugger/debug-multiple-processes.md#BKMK_Automatically_start_an_process_in_the_debugger).|
|[/LCID ou /l](../../ide/reference/lcid-devenv-exe.md)|Define o idioma padrão do IDE. Se a linguagem especificada não estiver incluída em sua instalação do Visual Studio, essa configuração será ignorada.|
|[/Log](../../ide/reference/log-devenv-exe.md)|Inicia o Visual Studio e registra toda a atividade no arquivo de log.|
|[/Run ou /r](../../ide/reference/run-devenv-exe.md)|Compila e executa a solução especificada.|
|[/Runexit](../../ide/reference/runexit-devenv-exe.md)|Compila e executa a solução especificada, minimiza o IDE quando a solução é executada e fecha o IDE depois que a solução termina a execução.|
|[/UseEnv](../../ide/reference/useenv-devenv-exe.md)|Faz com que o IDE use variáveis de ambiente PATH, INCLUDE e LIB para a compilação C++ em vez das configurações especificadas na seção Diretórios VC++ de opções **Projetos** na caixa de diálogo **Opções**. Essa opção é instalada com a carga de trabalho de **Desenvolvimento para desktop com C++**. Para obter mais informações, consulte [Configurando o caminho e variáveis de ambiente para Builds de linha de comando](/cpp/build/setting-the-path-and-environment-variables-for-command-line-builds).|
|[/Edit](../../ide/reference/edit-devenv-exe.md)|Abre os arquivos especificados em uma instância em execução deste aplicativo. Se não houver nenhuma instância em execução, uma nova instância será iniciada com um layout de janela simplificado.|
|[/SafeMode](../../ide/reference/safemode-devenv-exe.md)|Inicia o Visual Studio no modo de segurança e carrega somente o ambiente e os serviços padrão e as versões enviadas de pacotes de terceiros.|
|[/ResetSkipPkgs](../../ide/reference/resetskippkgs-devenv-exe.md)|Limpa todas as marcações SkipLoading que foram adicionadas aos VSPackages por usuários que desejam evitar carregar VSPackages com problemas.|
|[/Setup](../../ide/reference/setup-devenv-exe.md)|Força o Visual Studio a mesclar os metadados de recursos que descrevem menus, barras de ferramentas e grupos de comando de todos os VSPackages disponíveis. Você deve executar esse comando como administrador.|

As opções de linha de comando a seguir não exibem o IDE.

|Opção de linha de comando|Descrição|
| - |-----------------|
|[/?](../../ide/reference/q-devenv-exe.md)|Exibe ajuda para opções do devenv na **Janela do prompt de comando**.<br /><br /> `devenv /?`|
|[/Build](../../ide/reference/build-devenv-exe.md)|Cria a solução ou o projeto especificado de acordo com a configuração da solução especificada.<br /><br /> `devenv myproj.csproj /build`|
|[/Clean](../../ide/reference/clean-devenv-exe.md)|Exclui os arquivos criados pelo comando de build sem afetar os arquivos de origem.<br /><br /> `devenv myproj.csproj /clean`|
|[/Deploy](../../ide/reference/deploy-devenv-exe.md)|Compila a solução, juntamente com os arquivos necessários para a implantação, de acordo com a configuração de soluções.<br /><br /> `devenv myproj.csproj /deploy`|
|[/Diff](../../ide/reference/diff.md)|Compara dois arquivos. Assume quatro parâmetros: SourceFile, TargetFile, SourceDisplayName (opcional), TargetDisplayName (opcional).|
|[/Out](../../ide/reference/out-devenv-exe.md)|Permite que você especifique um arquivo para receber erros ao compilar.<br /><br /> `devenv myproj.csproj /build /out log.txt`|
|[/Project](../../ide/reference/project-devenv-exe.md)|O projeto a ser criado, limpo ou implantado. Será possível usar essa opção somente se você tiver fornecido também a opção /build, /rebuild, /clean ou /deploy.|
|[/ProjectConfig](../../ide/reference/projectconfig-devenv-exe.md)|Especifica a configuração de projeto a ser criada ou implantada. Será possível usar essa opção somente se você tiver fornecido a opção /project.|
|[/Rebuild](../../ide/reference/rebuild-devenv-exe.md)|Limpa e depois compila a solução ou o projeto especificado de acordo com a configuração da solução especificada.|
|[/ResetSettings](../../ide/reference/resetsettings-devenv-exe.md)|Restaura as configurações padrão do Visual Studio. Opcionalmente, redefine as configurações para o arquivo .vssettings especificado.|
|[/Upgrade](../../ide/reference/upgrade-devenv-exe.md)|Atualiza o arquivo de solução especificado e todos os seus arquivos de projeto ou o arquivo de projeto especificado, para os formatos do Visual Studio atuais para esses arquivos.|

## <a name="see-also"></a>Consulte também

* [Caixa de diálogo Geral, Ambiente, Opções](../../ide/reference/general-environment-options-dialog-box.md)
