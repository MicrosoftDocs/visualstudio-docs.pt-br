---
title: Shells de linha de comando & prompt para desenvolvedores
description: Inicie nas ferramentas > menu linha de comando. O Visual Studio Prompt de Comando do Desenvolvedor, o PowerShell do desenvolvedor e o terminal permitem que você use as ferramentas do .NET e do C++ com mais facilidade.
ms.date: 04/11/2021
ms.custom: contperf-fy21q4
helpviewer_keywords:
- Visual Studio command prompt
- command prompt, Visual Studio
- Developer Command Prompt
- Developer PowerShell
- Visual Studio terminal
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
no-loc: cmdlet
ms.openlocfilehash: 57cbc93f4b6e8cf64dd5149462788e0cde833350
ms.sourcegitcommit: 52b093e000334f53d87c6165d1418347e4f45dec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2021
ms.locfileid: "107221725"
---
# <a name="visual-studio-developer-command-prompt-and-developer-powershell"></a>PowerShell de Prompt de Comando do Desenvolvedor e desenvolvedor do Visual Studio

O Visual Studio 2019 inclui dois shells de linha de comando para desenvolvedores:

- **Visual Studio prompt de comando do desenvolvedor** -um prompt de comando padrão com determinadas variáveis de ambiente definido para facilitar o uso das ferramentas de desenvolvedor de linha de comando. Disponível desde o Visual Studio 2015.

- **Visual Studio Developer PowerShell** – mais potente do que um prompt de comando. Por exemplo, você pode passar a saída de um comando (conhecido como um *cmdlet* ) para outro cmdlet . Este Shell tem as mesmas variáveis de ambiente definidas como Prompt de Comando do Desenvolvedor. Disponível desde o Visual Studio 2019.


:::image type="content" source="media/developer-command-prompt-for-vs/command-prompt.png" alt-text="Prompt de Comando do Desenvolvedor para Visual Studio mostrando a ferramenta CLRVer":::

A partir do Visual Studio 2019 versão 16,5, o Visual Studio inclui um **terminal** integrado que pode hospedar qualquer um desses shells (prompt de comando do desenvolvedor e o PowerShell do desenvolvedor). Você também pode abrir várias guias de cada shell. O terminal do Visual Studio é criado com base no [terminal do Windows](/windows/terminal/). Para abrir o terminal no Visual Studio, escolha **Exibir**  >  **terminal**.

:::image type="content" source="media/developer-command-prompt-for-vs/vs-terminal.png" alt-text="Terminal do Visual Studio mostrando várias guias":::

Quando você abre um dos shells do desenvolvedor do Visual Studio, seja como um aplicativo separado ou na janela do terminal, ele é aberto no diretório da sua solução atual (se você tiver uma solução carregada). Esse comportamento torna conveniente executar comandos na solução ou em seus projetos.

Ambos os shells têm variáveis de ambiente específicas definidas que permitem que você use ferramentas de desenvolvedor de linha de comando mais facilmente. Depois de abrir um desses shells, você pode inserir os comandos para diferentes utilitários sem precisar saber onde eles estão localizados. 

|Comandos populares|Descrição|
|--|--|
|[`MSBuild`](../../msbuild/msbuild-command-line-reference.md)|Compilar um projeto ou solução|
|[`clrver`](/dotnet/framework/tools/clrver-exe-clr-version-tool)| Uma [.NET Framework ferramentas](/dotnet/framework/tools/index) para CLR.|
|[`ildasm`](/dotnet/framework/tools/ildasm-exe-il-disassembler)|Uma [ferramenta de .NET Framework](/dotnet/framework/tools/index) para o desmontador.|
|[`dotnet`](/dotnet/core/tools/dotnet)|Um [comando da CLI do .net](/dotnet/core/tools/index)|
|[`dotnet run`](/dotnet/core/tools/dotnet-run)|Um [comando da CLI do .net](/dotnet/core/tools/index)|
|[`CL`](/cpp/build/reference/compiler-command-line-syntax)|Ferramenta de compilação C/C++|
|[`NMAKE`](/cpp/build/reference/running-nmake)|Ferramenta de compilação C/C++|
|[`LIB`](/cpp/build/reference/lib-reference)| Ferramenta de Build do C/C++|
|[`DUMPBIN`](/cpp/build/reference/dumpbin-reference)| Ferramenta de Build do C/C++|


## <a name="start-in-visual-studio"></a>Iniciar no Visual Studio

Siga estas etapas para abrir o Prompt de Comando do Desenvolvedor ou o PowerShell do desenvolvedor no Visual Studio:

1. Abra o Visual Studio.

1. Na barra de menus, escolha **ferramentas**  >  **linha de comando**  >  **prompt de comando do desenvolvedor** ou **desenvolvedor PowerShell**.

   ![Item de menu do prompt de comando no Visual Studio](./media/developer-command-prompt-for-vs/vs-menu.png)

## <a name="start-from-windows-menu"></a>Iniciar no menu do Windows

Outra maneira de iniciar os shells é a partir do menu iniciar. Você pode ter vários prompts de comando, dependendo da versão do Visual Studio e de quaisquer SDKs e cargas de trabalho adicionais instalados. 

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

## <a name="start-from-file-browser"></a>Iniciar no navegador de arquivos 

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

## <a name="see-also"></a>Veja também

- [PowerShell para desenvolvedores](https://devblogs.microsoft.com/visualstudio/the-powershell-you-know-and-love-now-with-a-side-of-visual-studio/)
- [Diga Olá para o novo terminal do Visual Studio](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/)
- [Terminal do Windows](/windows/terminal/)
- [Ferramentas do .NET Framework](/dotnet/framework/tools/index)
- [Gerenciar ferramentas externas](../managing-external-tools.md)
- [Usar o conjunto de ferramentas do Microsoft C++ na linha de comando](/cpp/build/building-on-the-command-line)
