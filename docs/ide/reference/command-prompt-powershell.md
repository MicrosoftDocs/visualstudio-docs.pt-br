---
title: Shells de linha de comando & prompt para desenvolvedores
description: Inicie em Ferramentas > menu Linha de Comando. Visual Studio Prompt de Comando do Desenvolvedor, o PowerShell do desenvolvedor e o terminal permitem que você use ferramentas do .NET e do C++ com mais facilidade.
author: TerryGLee
ms.author: tglee
ms.date: 06/11/2021
ms.topic: reference
ms.custom: contperf-fy21q4
helpviewer_keywords:
- Visual Studio command prompt
- command prompt, Visual Studio
- Developer Command Prompt
- Developer PowerShell
- Visual Studio terminal
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
no-loc: cmdlet
ms.openlocfilehash: fef783475304bb1faa1788bde591a22ed610d528
ms.sourcegitcommit: e7629e132a4d2fad6bb5869e4d68d9dbeeae9631
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2021
ms.locfileid: "113649167"
---
# <a name="visual-studio-developer-command-prompt-and-developer-powershell"></a>Visual Studio Prompt de Comando do Desenvolvedor e o PowerShell para desenvolvedores

Visual Studio 2019 inclui dois shells de linha de comando para desenvolvedores:

- **Visual Studio Prompt de Comando do Desenvolvedor** - um prompt de comando padrão com determinadas variáveis de ambiente definidas para facilitar o uso de ferramentas de desenvolvedor de linha de comando. Disponível desde Visual Studio 2015.

- **Visual Studio PowerShell para Desenvolvedores** – mais eficiente do que um prompt de comando. Por exemplo, você pode passar a saída de um comando (conhecido como *cmdlet* um ) para outro cmdlet . Esse shell tem as mesmas variáveis de ambiente definidas como Prompt de Comando do Desenvolvedor. Disponível desde Visual Studio 2019.

:::image type="content" source="media/developer-command-prompt-for-vs/command-prompt.png" alt-text="Prompt de Comando do Desenvolvedor para Visual Studio a ferramenta clrver":::

A partir do Visual Studio 2019 versão 16.5, o Visual Studio inclui um **terminal** integrado que pode hospedar qualquer um desses shells (Prompt de Comando do Desenvolvedor e PowerShell para desenvolvedores). Você também pode abrir várias guias de cada shell. O Visual Studio terminal é criado sobre [Terminal do Windows](/windows/terminal/). Para abrir o terminal no Visual Studio, escolha **Exibir**  >  **Terminal**.

:::image type="content" source="media/developer-command-prompt-for-vs/vs-terminal.png" alt-text="Visual Studio terminal mostrando várias guias":::

Quando você abre um dos shells de desenvolvedor do Visual Studio, como um aplicativo separado ou na janela Terminal, ele é aberto no diretório da solução atual (se você tiver uma solução carregada). Esse comportamento torna conveniente executar comandos na solução ou em seus projetos.

Ambos os shells têm variáveis de ambiente específicas definidas que permitem que você use ferramentas de desenvolvedor de linha de comando com mais facilidade. Depois de abrir um desses shells, você pode inserir os comandos para utilitários diferentes sem precisar saber onde eles estão localizados. 

|Comandos populares|Descrição|
|--|--|
|[`MSBuild`](../../msbuild/msbuild-command-line-reference.md)|Criar um projeto ou solução|
|[`clrver`](/dotnet/framework/tools/clrver-exe-clr-version-tool)| Uma [.NET Framework para](/dotnet/framework/tools/index) CLR|
|[`ildasm`](/dotnet/framework/tools/ildasm-exe-il-disassembler)|Uma [.NET Framework para](/dotnet/framework/tools/index) desmontagem|
|[`dotnet`](/dotnet/core/tools/dotnet)|Um [comando da CLI do .NET](/dotnet/core/tools/index)|
|[`dotnet run`](/dotnet/core/tools/dotnet-run)|Um [comando da CLI do .NET](/dotnet/core/tools/index)|
|[`CL`](/cpp/build/reference/compiler-command-line-syntax)|Ferramenta de compilação C/C++|
|[`NMAKE`](/cpp/build/reference/running-nmake)|Ferramenta de compilação C/C++|
|[`LIB`](/cpp/build/reference/lib-reference)| Ferramenta de build C/C++|
|[`DUMPBIN`](/cpp/build/reference/dumpbin-reference)| Ferramenta de build C/C++|


## <a name="start-in-visual-studio"></a>Iniciar em Visual Studio

Siga estas etapas para abrir o Prompt de Comando do Desenvolvedor ou o Developer PowerShell de dentro Visual Studio:

1. Abra o Visual Studio.

1. Na barra de menus, escolha Ferramentas linha **de comando Prompt de Comando do Desenvolvedor** desenvolvedor do  >    >   **PowerShell**.

   ![Item de menu do prompt de comando no Visual Studio](./media/developer-command-prompt-for-vs/vs-menu.png)

## <a name="start-from-windows-menu"></a>Iniciar do Windows menu

Outra maneira de iniciar os shells é a partir do menu Iniciar. Você pode ter vários prompts de comando, dependendo da versão do Visual Studio e quaisquer SDKs e cargas de trabalho adicionais que você instalou. 

### <a name="windows-10"></a>Windows 10

1. Selecione **Iniciar** ![ Windows tecla de logotipo no teclado.](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png) e role até a letra **V.**

1. Expanda **a Visual Studio 2019.**

1. Escolha **Prompt de Comando do Desenvolvedor para VS 2019** ou **PowerShell para Desenvolvedor para VS 2019.**

   Como alternativa, você pode começar a digitar o nome do shell na caixa de pesquisa na barra de tarefas e escolher o resultado que deseja, pois a lista de resultados começa a exibir as correspondeções de pesquisa.

   ![Gif animado mostrando o comportamento de pesquisa Windows 10](./media/developer-command-prompt-for-vs/windows-10-search.gif)

### <a name="windows-81"></a>Windows 8.1

1. Vá para a tela **Inicial** pressionando a tecla do logotipo do Windows ![tecla do logotipo do Windows no teclado.](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png) no seu teclado, por exemplo.

1. Na tela **Iniciar,** pressione **Ctrl** Tab para abrir a lista +  **Aplicativos** e pressione **V**. Isso abrirá uma lista que inclui todos os prompts de Visual Studio instalados.

1. Escolha **Prompt de Comando do Desenvolvedor para VS 2019** ou **PowerShell para Desenvolvedor para VS 2019.**

### <a name="windows-7"></a>Windows 7

1. Escolha **Iniciar** e, em seguida, **expanda Todos os Programas.**

1. Escolha **Visual Studio 2019**  >  **Ferramentas do Visual Studio** Prompt de Comando do Desenvolvedor vs  >  **2019** ou PowerShell para desenvolvedor para **VS 2019.**

   ![Windows 7 menu Iniciar com o prompt de comando realçada](./media/developer-command-prompt-for-vs/windows-7-menu.png)

Se você tiver outros SDKs instalados, como o [SDK do Windows 10](https://developer.microsoft.com/windows/downloads/windows-10-sdk) ou versões [anteriores,](https://developer.microsoft.com/windows/downloads/sdk-archive)poderá ver prompts de comando adicionais. Consulte a documentação das ferramentas individuais para determinar qual versão do prompt de comando você deve usar.

## <a name="start-from-file-browser"></a>Iniciar no navegador de arquivos 

Normalmente, os atalhos para os shells instalados são colocados na pasta **Menu** Iniciar do Visual Studio, como *em %ProgramData%\Microsoft\Windows\Menu Iniciar\Programas\Visual Studio 2019\Ferramentas do Visual Studio*. Mas se a pesquisa pelo prompt de comando não produzir os resultados esperados, você poderá tentar localizar manualmente os arquivos em seu computador.

### <a name="developer-command-prompt"></a>Prompt de Comando do Desenvolvedor

Pesquise o nome do arquivo de prompt de comando, que éVsDevCmd.batou acesse *a* pasta Ferramentas do Visual Studio, como *%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools* (alterações de caminho de acordo com sua versão, edição e local de instalação do Visual Studio).

Depois de localizar o arquivo de prompt de comando, abra-o inserindo o seguinte comando em uma janela de prompt de comando regular:

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

Ou digite o seguinte comando na caixa Windows **caixa de diálogo** Executar:

```cmd
%comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

> [!TIP]
> Você precisará editar o caminho para corresponder à sua Visual Studio instalação.

### <a name="developer-powershell"></a>PowerShell para desenvolvedores

Pesquise um arquivo de script do PowerShell chamadoLaunch-VsDevShell.ps1ou acesse *a* pasta Ferramentas do Visual Studio, como *%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools.* (O caminho muda de acordo com sua versão Visual Studio, edição e local de instalação.) Depois de localizar o arquivo do PowerShell, execute-o inserindo o seguinte comando em um prompt Windows PowerShell ou PowerShell 6:

```powershell
& 'C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\Launch-VsDevShell.ps1'
```

Por padrão, o PowerShell do desenvolvedor que é lançado é configurado para a instalação Visual Studio cujo caminho de instalação oLaunch-VsDevShell.ps1 *arquivo* está localizado.

> [!TIP]
> A [política de execução](/powershell/module/microsoft.powershell.core/about/about_execution_policies) deve ser definida para que o seja cmdlet executado.

## <a name="see-also"></a>Confira também

- [Terminal do Windows](/windows/terminal/)
- [Ferramentas do .NET Framework](/dotnet/framework/tools/index)
- [Usar o pacote de ferramentas do Microsoft C++ na linha de comando](/cpp/build/building-on-the-command-line)
- [Visual Studio Code usuários](https://code.visualstudio.com/docs/cpp/config-msvc#:~:text=To%20open%20the%20Developer%20Command,item%20to%20open%20the%20prompt.)
