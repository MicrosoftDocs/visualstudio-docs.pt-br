---
title: Shells de linha de comando para desenvolvedores
description: Saiba como localizar e usar o Prompt de Comando do Desenvolvedor para o Visual Studio, o PowerShell do desenvolvedor e o terminal do Visual Studio, que permitem usar as ferramentas do .NET e do C++ com mais facilidade.
ms.date: 03/04/2021
ms.custom: contperf-fy21q3
helpviewer_keywords:
- Visual Studio command prompt
- command prompt, Visual Studio
- Developer Command Prompt
- Developer PowerShell
- Visual Studio terminal
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
no-loc: cmdlet
ms.openlocfilehash: 406ef4e7d475df82a0e36732dd5e777959ea3b96
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249740"
---
# <a name="developer-command-prompt-and-developer-powershell"></a>Prompt de Comando do Desenvolvedor e o PowerShell para desenvolvedores

O Visual Studio 2019 inclui dois shells de linha de comando para desenvolvedores:

- **Prompt de comando do desenvolvedor para Visual Studio** -um prompt de comando padrão com determinadas variáveis de ambiente definido para facilitar o uso das ferramentas de desenvolvedor de linha de comando.
- **Developer PowerShell** – mais potente do que um prompt de comando. Por exemplo, você pode passar a saída de um comando (conhecido como um *cmdlet* ) para outro cmdlet . Este Shell tem as mesmas variáveis de ambiente definidas como Prompt de Comando do Desenvolvedor.

Ambos os shells têm variáveis de ambiente específicas definidas que permitem que você use ferramentas de desenvolvedor de linha de comando mais facilmente. Depois de abrir um desses shells, você pode inserir os comandos para diferentes utilitários sem precisar saber onde eles estão localizados. Os comandos que você pode executar incluem:

- [`MSBuild`](../../msbuild/msbuild-command-line-reference.md), para criar um projeto ou solução.
- [.NET Framework ferramentas](/dotnet/framework/tools/index), como [`clrver`](/dotnet/framework/tools/clrver-exe-clr-version-tool) e [`ildasm`](/dotnet/framework/tools/ildasm-exe-il-disassembler) .
- Ferramentas de compilação C/C++, como [`CL`](/cpp/build/reference/compiler-command-line-syntax) e [`NMAKE`](/cpp/build/reference/running-nmake) .
- Ferramentas de Build do C/C++ adicionais, como [`LIB`](/cpp/build/reference/lib-reference) e [`DUMPBIN`](/cpp/build/reference/dumpbin-reference) .
- [Comandos da CLI do .net](/dotnet/core/tools/index), como [`dotnet`](/dotnet/core/tools/dotnet) e [`dotnet run`](/dotnet/core/tools/dotnet-run) . (Esses comandos também estão disponíveis em um prompt de comando regular).

:::image type="content" source="media/developer-command-prompt-for-vs/command-prompt.png" alt-text="Prompt de Comando do Desenvolvedor para Visual Studio mostrando a ferramenta CLRVer":::

A partir do Visual Studio 2019 versão 16,5, o Visual Studio inclui um **terminal** integrado que pode hospedar qualquer um desses shells (prompt de comando do desenvolvedor e o PowerShell do desenvolvedor). Você também pode abrir várias guias de cada shell. O terminal do Visual Studio é criado com base no [terminal do Windows](/windows/terminal/). Para abrir o terminal no Visual Studio, escolha **Exibir**  >  **terminal**.

:::image type="content" source="media/developer-command-prompt-for-vs/vs-terminal.png" alt-text="Terminal do Visual Studio mostrando várias guias":::

Quando você abre um dos shells do desenvolvedor do Visual Studio, seja como um aplicativo separado ou na janela do terminal, ele é aberto no diretório da sua solução atual (se você tiver uma solução carregada). Esse comportamento torna conveniente executar comandos na solução ou em seus projetos.

## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)

## <a name="start-the-shell-from-inside-visual-studio"></a>Iniciar o Shell de dentro do Visual Studio

Siga estas etapas para abrir o Prompt de Comando do Desenvolvedor ou o PowerShell do desenvolvedor no Visual Studio:

1. Abra o Visual Studio.

1. Na barra de menus, escolha **ferramentas**  >  **linha de comando**  >  **prompt de comando do desenvolvedor** ou **desenvolvedor PowerShell**.

   ![Item de menu do prompt de comando no Visual Studio](./media/developer-command-prompt-for-vs/vs-menu.png)

## <a name="use-the-windows-start-menu"></a>Usar o menu Iniciar do Windows

Você pode ter vários prompts de comando, dependendo da versão do Visual Studio e de quaisquer SDKs e cargas de trabalho adicionais instalados. Se as etapas a seguir não funcionarem, você poderá tentar [localizar manualmente os arquivos em seu computador](#manually-locate-the-file) ou [iniciar o Shell de dentro do Visual Studio](#start-the-shell-from-inside-visual-studio).

### <a name="windows-10"></a>Windows 10

1. Selecione **Iniciar** ![ a tecla do logotipo do Windows no teclado.](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png) e role até a letra **V**.

1. Expanda a pasta do **Visual Studio 2019** .

1. Escolha **prompt de comando do desenvolvedor para o vs 2019** ou o **PowerShell para desenvolvedores para vs 2019**.

   Como alternativa, você pode começar a digitar o nome do Shell na caixa de pesquisa na barra de tarefas e escolher o resultado desejado, pois a lista de resultados começa a exibir as correspondências de pesquisa.

   ![GIF animado mostrando o comportamento de pesquisa no Windows 10](./media/developer-command-prompt-for-vs/windows-10-search.gif)

### <a name="windows-81"></a>Windows 8.1

1. Vá para a tela **Inicial** pressionando a tecla do logotipo do Windows ![tecla do logotipo do Windows no teclado.](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png) no seu teclado, por exemplo.

1. Na tela **Iniciar** , pressione a **tecla CTRL** +  para abrir a lista de **aplicativos** e, em seguida, pressione **V**. Isso abre uma lista que inclui todos os prompts de comando instalados do Visual Studio.

1. Escolha **prompt de comando do desenvolvedor para o vs 2019** ou o **PowerShell para desenvolvedores para vs 2019**.

### <a name="windows-7"></a>Windows 7

1. Escolha **Iniciar** e expanda **todos os programas**.

1. Escolha o **Visual Studio 2019**  >  **Ferramentas do Visual Studio**  >  **prompt de comando do desenvolvedor para vs 2019** ou **desenvolvedor PowerShell para vs 2019**.

   ![Menu Iniciar do Windows 7 com o prompt de comando realçado](./media/developer-command-prompt-for-vs/windows-7-menu.png)

Se você tiver outros SDKs instalados, como o [SDK do Windows 10](https://developer.microsoft.com/windows/downloads/windows-10-sdk) ou [versões anteriores](https://developer.microsoft.com/windows/downloads/sdk-archive), poderá ver prompts de comando adicionais. Consulte a documentação das ferramentas individuais para determinar qual versão do prompt de comando você deve usar.

## <a name="manually-locate-the-file"></a>Localizar o arquivo manualmente

Normalmente, os atalhos para os shells que você instalou são colocados na pasta do **menu iniciar** do Visual Studio, como no *%ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2019 \ Ferramentas do Visual Studio*. Mas se a pesquisa do prompt de comando não produzir os resultados esperados, você poderá tentar localizar manualmente os arquivos em seu computador.

### <a name="developer-command-prompt"></a>Prompt de Comando do Desenvolvedor

Procure o nome do arquivo de prompt de comando, que é *VsDevCmd.bat* ou vá para a pasta Ferramentas do Visual Studio, como *% ProgramFiles (x86)% \ Microsoft Visual Studio\2019\Community\Common7\Tools* (o caminho muda de acordo com sua versão, edição e local de instalação do Visual Studio).

Depois de localizar o arquivo de prompt de comando, abra-o inserindo o seguinte comando em uma janela de prompt de comando regular:

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

Ou digite o seguinte comando na caixa de diálogo **executar** do Windows:

```cmd
%comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

> [!TIP]
> Você precisará editar o caminho para corresponder à instalação do Visual Studio.

### <a name="developer-powershell"></a>PowerShell para desenvolvedores

Procure um arquivo de script do PowerShell chamado *Launch-VsDevShell.ps1* ou vá para a pasta Ferramentas do Visual Studio, como *% ProgramFiles (x86)% \ Microsoft Visual Studio\2019\Community\Common7\Tools*. (O caminho muda de acordo com a versão, edição e o local de instalação do Visual Studio.) Depois de localizar o arquivo do PowerShell, execute-o digitando o seguinte comando em um prompt do Windows PowerShell ou do PowerShell 6:

```powershell
& 'C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\Launch-VsDevShell.ps1'
```

Por padrão, o PowerShell de desenvolvedor que é iniciado é configurado para a instalação do Visual Studio cujo caminho de instalação no qual o arquivo de *Launch-VsDevShell.ps1* está localizado.

> [!TIP]
> A [política de execução](/powershell/module/microsoft.powershell.core/about/about_execution_policies) deve ser definida para que o cmdlet seja executado.

## <a name="see-also"></a>Confira também

- [PowerShell para desenvolvedores](https://devblogs.microsoft.com/visualstudio/the-powershell-you-know-and-love-now-with-a-side-of-visual-studio/)
- [Diga Olá para o novo terminal do Visual Studio](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/)
- [Terminal do Windows](/windows/terminal/)
- [Ferramentas do .NET Framework](/dotnet/framework/tools/index)
- [Gerenciar ferramentas externas](../managing-external-tools.md)
- [Usar o conjunto de ferramentas do Microsoft C++ na linha de comando](/cpp/build/building-on-the-command-line)
