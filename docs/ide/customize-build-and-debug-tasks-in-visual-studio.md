---
title: Personalizar tarefas de build e depuração no Visual Studio usando tasks.vs.json e launch.vs.json
ms.date: 02/21/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- NMAKE [Visual Studio]
- makefiles [Visual Studio]
- customize codebases [Visual Studio]
- tasks.vs.json file [Visual Studio]
- launch.vs.json file [Visual Studio]
- vsworkspacesettings.json file [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3c4b915f632179ff118247e8c046ce980a824ea2
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34448081"
---
# <a name="customize-build-and-debug-tasks-for-open-folder-development"></a>Personalizar tarefas de compilação e depuração para desenvolvimento de "Pasta Aberta"

O Visual Studio sabe como executar várias linguagens e bases de código diferentes, mas não sabe como executar tudo. Se você [abrir uma pasta de código](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) no Visual Studio, e o Visual Studio souber como executar seu código, você poderá executá-lo imediatamente sem qualquer configuração adicional.

Se a base de código usar ferramentas de compilação personalizadas não reconhecidas pelo Visual Studio, será necessário fornecer alguns detalhes de configuração para executar e depurar o código no Visual Studio. Instrua o Visual Studio sobre como compilar seu código definindo *tarefas de compilação*. Você pode criar uma ou mais tarefas de compilação para especificar todos os itens que uma linguagem precisa para compilar e executar seu código. Você também pode criar tarefas arbitrárias que podem fazer quase tudo o que você deseja. Por exemplo, é possível criar uma tarefa para listar o conteúdo de uma pasta ou renomear um arquivo.

Personalizar sua base de código sem projeto usando os seguintes arquivos *.json*:

|Nome do arquivo|Finalidade|
|-|-|
|*tasks.vs.json*|Especifique os comandos de compilação personalizados e as opções do compilador, além de tarefas arbitrárias (sem relação com a compilação).<br>Acessados por meio do item de menu de contexto do **Gerenciador de Soluções**, **Configurar tarefas**.|
|*launch.vs.json*|Especifica argumentos de linha de comando para depuração.<br>Acessados por meio do item de menu de contexto do **Gerenciador de Soluções**, **Configurações de depuração e de inicialização**.|
|*VSWorkspaceSettings.json*|Configurações genéricas que podem afetar as tarefas e a inicialização. Por exemplo, a definição de `envVars` em *VSWorkspaceSettings.json* adiciona as variáveis de ambiente especificadas para executar os comandos externamente.<br>Crie esse arquivo manualmente.|

Esses arquivos *.json* estão localizados em uma pasta oculta chamada *.vs* na pasta raiz de sua base de código. Os arquivos *tasks.vs.json* e *launch.vs.json* são criados pelo Visual Studio conforme a necessidade quando você escolhe **Configurar Tarefas** ou **Configurações de Depuração e de Inicialização** em um arquivo ou pasta no **Gerenciador de Soluções**. Esses arquivos *.json* ficam ocultos porque a maioria dos usuários geralmente não deseja inclui-los no controle do código-fonte. No entanto, se você quiser a possibilidade de inclui-los no controle do código-fonte, arraste os arquivos para a raiz da base de código, onde eles ficarão visíveis.

> [!TIP]
> Para exibir arquivos ocultos no Visual Studio, escolha o botão **Mostrar Todos os Arquivos** na barra de ferramentas do **Gerenciador de Soluções**.

## <a name="define-tasks-with-tasksvsjson"></a>Definir tarefas com tasks.vs.json

Você pode automatizar os scripts de compilação, ou quaisquer outras operações externas nos arquivos existentes em seu espaço de trabalho atual, executando-os como tarefas diretamente no IDE. Você pode configurar uma nova tarefa clicando com o botão direito em um arquivo ou pasta e selecionando **Configurar Tarefas**.

![Menu Configurar Tarefas](../ide/media/customize-configure-tasks-menu.png)

Isso cria (ou abre) o arquivo *tasks.vs.json* na pasta *.vs*. Você pode definir uma tarefa de compilação ou tarefa arbitrária nesse arquivo e, depois, invocá-la usando o nome que você forneceu no menu de contexto **Gerenciador de Soluções**.

As tarefas personalizadas podem ser adicionadas a arquivos individuais ou a todos os arquivos de um tipo específico. Por exemplo, os arquivos do pacote NuGet podem ser configurados para terem uma tarefa “Restaurar Pacotes” ou todos os arquivos de origem podem ser configurados para terem uma tarefa de análise estática, como um linter para todos os arquivos *.js*.

### <a name="define-custom-build-tasks"></a>Definir tarefas de compilação personalizadas

Se a sua base de código usar ferramentas de compilação personalizadas não reconhecidas pelo Visual Studio, não será possível executar e depurar o código no Visual Studio antes de concluir algumas etapas de configuração. O Visual Studio fornece *tarefas de compilação*, nas quais você pode informar ao Visual Studio como compilar, recompilar e limpar seu código. O arquivo de tarefa de build *tasks.vs.json* associa o loop de desenvolvimento interno do Visual Studio às ferramentas de build personalizadas usadas pela base de código.

Considere uma base de código composta por um único arquivo em C# chamado *hello.cs*. O *makefile* de uma base de código como essa pode ter esta aparência:

```makefile
build: directory hello.exe

hello.exe: hello.cs
    csc -debug hello.cs /out:bin\hello.exe

clean:
    del bin\hello.exe bin\hello.pdb

rebuild: clean build

directory: bin

bin:
    md bin
```

Para um *makefile* que contém destinos de build, limpeza e recompilação, você pode definir o seguinte arquivo *tasks.vs.json*. Ele contém três tarefas de compilação para compilar, recompilar e limpar a base de código, usando NMAKE como a ferramenta de compilação.

```json
{
  "version": "0.2.1",
  "outDir": "\"${workspaceRoot}\\bin\"",
  "tasks": [
    {
      "taskName": "makefile-build",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "build",
      "command": "nmake",
      "args": [ "build" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    },
    {
      "taskName": "makefile-clean",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "clean",
      "command": "nmake",
      "args": [ "clean" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    },
    {
      "taskName": "makefile-rebuild",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "rebuild",
      "command": "nmake",
      "args": [ "rebuild" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    }
  ]
}
```

Depois de definir as tarefas de compilação no *tasks.vs.json*, ocorre a adição de outros itens de menu de contexto aos arquivos correspondentes no **Gerenciador de Soluções**. Neste exemplo, as opções "criar", "recriar" e "limpar" são adicionadas ao menu de contexto de quaisquer arquivos *makefile*.

![menu de contexto do makefile com compilação, recompilação e limpeza](media/customize-build-rebuild-clean.png)

> [!NOTE]
> Os comandos são exibidos no menu de contexto sob o comando **Configurar Tarefas** devido às configurações `contextType`. "compilar", "recompilar" e "limpar" são comandos de compilação, portanto, eles aparecem na seção de compilação no meio do menu de contexto.

Quando você seleciona uma dessas opções, a tarefa é executada. A saída é exibida na janela **Saída** e os erros de compilação são exibidos na **Lista de Erros**.

### <a name="define-arbitrary-tasks"></a>Definir tarefas arbitrárias

Você pode definir tarefas arbitrárias no arquivo *tasks.vs.json*, a fim de fazer quase tudo o que você quiser. Por exemplo, você pode definir uma tarefa para exibir o nome do arquivo selecionado atualmente na janela **Saída**, ou para listar os arquivos em um diretório especificado.

A exemplo a seguir mostra um arquivo *tasks.vs.json* que define uma única tarefa. Quando chamada, a tarefa exibe o nome do arquivo *.js* selecionado atualmente.

```json
{
  "version": "0.2.1",
  "tasks": [
    {
      "taskName": "Echo filename",
      "appliesTo": "*.js",
      "type": "default",
      "command": "${env.COMSPEC}",
      "args": [ "echo ${file}" ]
    }
  ]
}
```

- `taskName` especifica o nome que aparece no menu de contexto.
- `appliesTo` especifica em quais arquivos o comando pode ser executado.
- A propriedade `command` especifica o comando a ser invocado. Neste exemplo, a variável de ambiente `COMSPEC` é usada para identificar o interpretador de linha de comando, normalmente *cmd.exe*.
- A propriedade `args` especifica os argumentos a serem passados para o comando invocado.
- A macro `${file}` recupera o arquivo selecionado no **Gerenciador de Soluções**.

Depois de salvar *tasks.vs.json*, clique com o botão direito em qualquer arquivo *.js* na pasta e escolha **Ecoar nome de arquivo**. O nome do arquivo é exibido na janela **Saída**.

> [!NOTE]
> Se a sua base de código não contiver um arquivo *tasks.vs.json*, você poderá criar um escolhendo **Configurar Tarefas** no menu de atalho ou de contexto de um arquivo no **Gerenciador de Soluções**.

O exemplo a seguir define uma tarefa que lista os arquivos e subpastas do diretório *bin*.

```json
{
  "version": "0.2.1",
  "outDir": "\"${workspaceRoot}\\bin\"",
  "tasks": [
    {
      "taskName": "List Outputs",
      "appliesTo": "*",
      "type": "default",
      "command": "${env.COMSPEC}",
      "args": [ "dir ${outDir}" ]
    }
  ]
}
```

- `${outDir}` é uma macro personalizada definida primeiro antes do bloco `tasks`. Em seguida, ela é chamada na propriedade `args`.

Essa tarefa se aplica a todos os arquivos. Quando você abre o menu de contexto em qualquer arquivo no **Gerenciador de Soluções**, o nome da tarefa **Listar Saídas** aparece na parte inferior do menu. Quando você escolhe **Listar Saídas**, o conteúdo do diretório *bin* é listado na janela **Saída** no Visual Studio.

![Tarefa arbitrária no menu de contexto](../ide/media/customize-arbitrary-task-menu.png)

### <a name="settings-scope"></a>Escopo das configurações

Vários arquivos *tasks.vs.json* podem existir na raiz e em subdiretórios de uma base de código. Esse design permite que você tenha um comportamento diferente em subdiretórios diferentes da base de código. O Visual Studio agrega ou substitui as configurações em toda a base de código, priorizando arquivos na seguinte ordem:

- Arquivos de configuração no diretório *.vs* da pasta raiz.
- O diretório no qual uma configuração está sendo calculada.
- Diretório pai do diretório atual, até o diretório raiz.
- Arquivos de configuração no diretório raiz.

Essas regras de agregação se aplicam aos arquivos *tasks.vs.json* e *VSWorkspaceSettings.json*. Para saber mais sobre como as configurações em outro arquivo são agregadas, veja a seção correspondente desse arquivo neste artigo.

### <a name="properties-for-tasksvsjson"></a>Propriedades para tasks.vs.json

Esta seção descreve algumas das propriedades que você pode especificar em *tasks.vs.json*.

#### <a name="appliesto"></a>appliesTo

Você pode criar tarefas para qualquer arquivo ou pasta especificando seu nome no campo `appliesTo`, por exemplo `"appliesTo": "hello.js"`. As máscaras de arquivo a seguir podem ser usadas como valores:

|||
|-|-|
|`"*"`| a tarefa está disponível para todos os arquivos e pastas no espaço de trabalho|
|`"*/"`| a tarefa está disponível para todas as pastas no espaço de trabalho|
|`"*.js"`| a tarefa está disponível para todos os arquivos com a extensão *.js* no espaço de trabalho|
|`"/*.js"`| a tarefa está disponível para todos os arquivos com a extensão *.js* na raiz do espaço de trabalho|
|`"src/*/"`| a tarefa está disponível para todas as subpastas da pasta *src*|
|`"makefile"`| a tarefa está disponível para todos os arquivos *makefile* no espaço de trabalho|
|`"/makefile"`| a tarefa está disponível apenas para o *makefile* na raiz do espaço de trabalho|

#### <a name="macros-for-tasksvsjson"></a>Macros para tasks.vs.json

|||
|-|-|
|`${env.<VARIABLE>}`| Especifica qualquer variável de ambiente (por exemplo, ${env.PATH}, ${env.COMSPEC} e assim por diante) que esteja definida para o prompt de comando do desenvolvedor. Para saber mais, confira [Prompt de comando do desenvolvedor para Visual Studio](/dotnet/framework/tools/developer-command-prompt-for-vs).|
|`${workspaceRoot}`| O caminho completo para a pasta do espaço de trabalho (por exemplo, *C:\sources\hello*)|
|`${file}`| O caminho completo do arquivo ou pasta selecionado para execução dessa tarefa (por exemplo, *C:\sources\hello\src\hello.js*)|
|`${relativeFile}`| O caminho relativo até o arquivo ou pasta (por exemplo, *src\hello.js*)|
|`${fileBasename}`| O nome do arquivo sem o caminho ou extensão (por exemplo, *hello*)|
|`${fileDirname}`| O caminho completo até o arquivo, exceto o nome do arquivo (por exemplo, *C:\sources\hello\src*)|
|`${fileExtname}`| A extensão do arquivo selecionado (por exemplo, *.js*)|

## <a name="configure-debugging-with-launchvsjson"></a>Configurar a depuração com launch.vs.json

1. Para configurar sua base de código para depuração, no **Gerenciador de Soluções** escolha o item de menu **Configurações de Depuração e de Inicialização** no menu de contexto ou de atalho do seu arquivo executável.

   ![Menu de contexto Configurações de Depuração e Inicialização](media/customize-debug-launch-menu.png)

1. Na caixa de diálogo **Selecionar um Depurador**, escolha uma opção e, em seguida, escolha o botão **Selecionar**.

   ![Caixa de diálogo Selecionar um Depurador](media/customize-select-a-debugger.png)

   Se o arquivo *launch.vs.json* ainda não existir, ele será criado.

   ```json
   {
     "version": "0.2.1",
     "defaults": {},
     "configurations": [
       {
         "type": "default",
         "project": "bin\\hello.exe",
         "name": "hello.exe"
       }
     ]
   }
   ```

1. Em seguida, clique com o botão direito do mouse no **Gerenciador de Soluções** e escolha **Definir como Item de Inicialização**.

   O executável é definido como o item de inicialização para a sua base de código, e o título do botão **Iniciar** da depuração é alterado para refletir o nome do executável.

   ![Botão Início personalizado](media/customize-start-button.png)

   Quando você escolhe **F5**, o depurador é iniciado, e é interrompido em qualquer ponto de interrupção já criado. Todas as janelas conhecidas do depurador ficam disponíveis e funcionais.

### <a name="specify-arguments-for-debugging"></a>Especificar argumentos para depuração

Você pode especificar argumentos de linha de comando para passar para depuração no arquivo *launch.vs.json*. Adicione os argumentos à matriz `args`, conforme mostra o exemplo a seguir:

```json
{
  "version": "0.2.1",
  "defaults": {},
  "configurations": [
    {
      "type": "default",
      "project": "bin\\hello.exe",
      "name": "hello.exe"
    },
    {
      "type": "default",
      "project": "bin\\hello.exe",
      "name": "hello.exe a1",
      "args": [ "a1" ]
    }
  ]
}
```

Quando você salva esse arquivo, o nome da nova configuração aparece na lista suspensa de destino de depuração, e você pode selecioná-lo para iniciar o depurador. Você pode criar quantas configurações de depuração quiser.

![Lista suspensa de configurações de depuração](media/customize-debug-configurations.png)

> [!NOTE]
> A propriedade da matriz `configurations` em *launch.vs.json* é lida em dois locais de arquivo &mdash;o diretório raiz da base de código, e o diretório *.vs*. Se houver um conflito, a prioridade será dada ao valor em *.vs\launch.vs.json*.

## <a name="define-workspace-settings-in-vsworkspacesettingsjson"></a>Definir configurações de espaço de trabalho em VSWorkspaceSettings.json

Você pode especificar configurações genéricas que podem afetar as tarefas e iniciar no arquivo *VSWorkspaceSettings.json*. Por exemplo, se você definir `envVars` no *VSWorkspaceSettings.json*, o Visual Studio adicionará as variáveis de ambiente especificadas aos comandos executados externamente. Para usar esse arquivo, você deverá criá-lo manualmente.

## <a name="additional-settings-files"></a>Arquivos de configurações adicionais

Além dos três arquivos *.json* descritos neste tópico, o Visual Studio também lê configurações de alguns arquivos adicionais, se eles existirem em sua base de código.

### <a name="vscodesettingsjson"></a>.vscode\settings.json

O Visual Studio lê configurações limitadas de um arquivo chamado *settings.json*, se estiver em um diretório chamado *.vscode*. Essa funcionalidade é fornecida para bases de código desenvolvidas anteriormente no Visual Studio Code. Atualmente, a única configuração lida de *.vscode\settings.json* é `files.exclude`, que filtra os arquivos visualmente no Gerenciador de Soluções e algumas ferramentas de pesquisa.

Você pode ter quantos arquivos *.vscode\settings.json* quiser em sua base de código. As configurações lidas neste arquivo são aplicadas ao diretório pai do *.vscode* e em todos os subdiretórios.

### <a name="gitignore"></a>.gitignore

Os arquivos *.gitignore* são usados para informar ao Git quais arquivos ignorar; ou seja, de quais arquivos e diretórios você não quer fazer check-in. Os arquivos *.gitignore* são normalmente incluídos como parte de uma base de código, para que as configurações possam ser compartilhadas com todos os desenvolvedores da base de código. O Visual Studio lê padrões em arquivos *.gitignore* para filtrar itens visualmente e de algumas ferramentas de pesquisa.

As configurações lidas no arquivo *.gitignore* são aplicadas ao seu diretório pai e a todos os subdiretórios.

## <a name="see-also"></a>Consulte também

- [Desenvolver código sem projetos ou soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [Projetos de pasta aberta para C++](/cpp/ide/non-msbuild-projects)
- [Projetos CMake em C++](/cpp/ide/cmake-tools-for-visual-cpp)
- [Referência a NMAKE](/cpp/build/nmake-reference)
- [Recursos do Editor de Códigos](../ide/writing-code-in-the-code-and-text-editor.md)