---
title: Exemplos de parâmetro de linha de comando para instalação
description: Personalize esses exemplos para criar sua própria instalação de linha de comando do Visual Studio.
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 837F31AA-F121-46e9-9996-F8BCE768E579
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 5685de34235dcd9b903cbf5be6371ebf3f1e84c3
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307538"
---
# <a name="command-line-parameter-examples-for-visual-studio-installation"></a>Exemplos de parâmetros de linha de comando para a instalação do Visual Studio

Para ilustrar como [usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md), aqui estão vários exemplos que podem ser personalizados para atender às suas necessidades.

Em cada exemplo, `vs_enterprise.exe`, `vs_professional.exe` e `vs_community.exe` representam a respectiva edição do bootstrapper do Visual Studio, que é o arquivo pequeno (aproximadamente 1 MB) que inicia o processo de download. Se você estiver usando uma edição diferente, substitua o nome do bootstrapper adequado.

> [!NOTE]
> Todos os comandos exigem elevação administrativa e um prompt do Controle de Conta de Usuário será exibido se o processo não for iniciado em um prompt elevado.
>
> [!NOTE]
> Você pode usar o caractere `^` no final de uma linha de comando para concatenar várias linhas em um único comando. Como alternativa, é possível simplesmente colocar essas linhas juntas em uma única linha. No PowerShell, o equivalente é o caractere de acento grave (`` ` ``).

Para listas de cargas de trabalho e componentes que você pode instalar usando a linha de comando, confira a página [IDs de carga de trabalho e de componente do Visual Studio](workload-and-component-ids.md).

## <a name="using---installpath"></a>Usando --installPath

* Instale uma instância mínima do Visual Studio, com nenhum prompt interativo, com exceção do progresso, exibido:

  ```shell
   vs_enterprise.exe --installPath C:\minVS ^
   --add Microsoft.VisualStudio.Workload.CoreEditor ^
   --passive --norestart
  ```

* Atualize uma instância do Visual Studio usando a linha de comando, sem a exibição de prompts interativos, com exceção do progresso:

   ```shell
   vs_enterprise.exe --update --quiet --wait
   vs_enterprise.exe update --wait --passive --norestart --installPath "C:\installPathVS"
   ```

  > [!NOTE]
  > Ambos os comandos são aconselhados. O primeiro comando atualiza o Instalador do Visual Studio. O segundo comando atualiza a instância do Visual Studio. Para evitar uma caixa de diálogo Controle de Conta de Usuário, execute o prompt de comando como Administrador.

* Instale silenciosamente, uma instância da área de trabalho do Visual Studio com o pacote de idioma francês, retornando somente quando o produto estiver instalado.

  ```shell
   vs_enterprise.exe --installPath C:\desktopVS ^
   --addProductLang fr-FR ^
   --add Microsoft.VisualStudio.Workload.ManagedDesktop ^
   --includeRecommended --quiet --wait
  ```

## <a name="using---wait"></a>Em uso – Aguarde

* Use scripts ou arquivos em lotes para aguardar o instalador do Visual Studio ser concluído antes da execução do próximo comando. Para arquivos em lotes, uma variável de ambiente conterá `%ERRORLEVEL%` o valor de retorno do comando, conforme documentado na página [usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md) . Alguns utilitários de comando requerem parâmetros adicionais para aguardar a conclusão e obter o valor retornado do instalador. Veja a seguir um exemplo dos parâmetros adicionais usados com o comando de script do PowerShell "Start-Process":

   ```shell
   start /wait vs_professional.exe --installPath "C:\VS" --passive --wait > nul
   echo %errorlevel%
   ```

   ```powershell
   $process = Start-Process -FilePath vs_enterprise.exe -ArgumentList "--installPath", "C:\VS", "--passive", "--wait" -Wait -PassThru
   Write-Output $process.ExitCode 
   ```

   ou

   ```powershell
    $startInfo = New-Object System.Diagnostics.ProcessStartInfo
    $startInfo.FileName = "vs_enterprise.exe"
    $startInfo.Arguments = "--all --quiet --wait"
    $process = New-Object System.Diagnostics.Process
    $process.StartInfo = $startInfo
    $process.Start()
    $process.WaitForExit()
   ```

* O primeiro "--wait" é usado pelo Visual Studio Installer, e o segundo "-Wait" é usado pelo "Start-Process" para aguardar a conclusão. O parâmetro "-PassThru" é usado pelo "Start-Process" para usar o código de saída do instalador para seu valor retornado.

## <a name="using---layout"></a>Usando --layout

* Baixe o editor de núcleo do Visual Studio (a configuração mínima do Visual Studio). Inclua apenas o pacote de idiomas em inglês:

  ```shell
   vs_community.exe --layout C:\VS ^
   --lang en-US ^
   --add Microsoft.VisualStudio.Workload.CoreEditor
  ```

* Baixe as cargas de trabalho do .NET desktop e do .NET web juntamente com todos os componentes recomendados e com a extensão do GitHub. Inclua apenas o pacote de idiomas em inglês:

  ```shell
   vs_community.exe --layout C:\VS ^
   --lang en-US ^
   --add Microsoft.VisualStudio.Workload.NetWeb ^
   --add Microsoft.VisualStudio.Workload.ManagedDesktop ^
   --add Component.GitHub.VisualStudio ^
   --includeRecommended
  ```

## <a name="using---all"></a>Usando --all

* Inicie uma instalação interativa de todas as cargas de trabalho e componentes que estão disponíveis no Visual Studio Enterprise Edition:

   ```shell
   vs_enterprise.exe --all
   ```

## <a name="using---includerecommended"></a>Usando --includeRecommended

* Instale uma segunda instância nomeada do Visual Studio Professional em um computador com o Visual Studio Community Edition já instalado, com suporte para o desenvolvimento do Node.js:

   ```shell
   vs_professional.exe --installPath C:\VSforNode ^
   --add Microsoft.VisualStudio.Workload.Node --includeRecommended --nickname VSforNode
  ```

## <a name="using---remove"></a>Usando --remove

::: moniker range="vs-2017"

* Remova o componente Ferramentas de Criação de Perfil da instância do Visual Studio instalada por padrão:

  ```shell
   vs_enterprise.exe modify ^
   --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" ^
   --remove Microsoft.VisualStudio.Component.DiagnosticTools ^
   --passive
  ```

::: moniker-end

::: moniker range="vs-2019"

* Remova o componente Ferramentas de Criação de Perfil da instância do Visual Studio instalada por padrão:

  ```shell
   vs_enterprise.exe modify ^
   --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" ^
   --remove Microsoft.VisualStudio.Component.DiagnosticTools ^
   --passive
  ```

::: moniker-end

::: moniker range=">=vs-2022"

* Remova o componente Ferramentas de Criação de Perfil da instância do Visual Studio instalada por padrão:

  ```shell
   vs_enterprise.exe modify ^
   --installPath "C:\Program Files\Microsoft Visual Studio\2022\Enterprise" ^
   --remove Microsoft.VisualStudio.Component.DiagnosticTools ^
   --passive
  ```

::: moniker-end

## <a name="using---path"></a>Usando --path

::: moniker range="vs-2017"

Esses parâmetros de linha de comando são **novos no 15.7**. Para obter mais informações sobre eles, consulte a página [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

::: moniker-end

* Usando os caminhos de instalação, de cache e compartilhados:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path cache="C:\VS\cache" --path shared="C:\VS\shared"`

* Usando somente os caminhos de instalação e de cache:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path cache="C:\VS\cache"`

* Usando somente os caminhos de instalação e compartilhados:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path shared="C:\VS\shared"`

* Usando somente o caminho de instalação:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS"`

## <a name="using-export"></a>Usando a exportação

::: moniker range="vs-2017"

Este comando da linha de comando é uma **novidade na versão 15.9**. Para saber mais sobre ela, confira a página [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

::: moniker-end

* Usando a exportação para salvar a seleção de uma instalação:

  ```shell
  "C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe" export --installPath "C:\VS" --config "C:\.vsconfig"
  ```

* Usando a exportação para salvar a seleção personalizada do zero:

  ```shell
  "C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe" export --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeRecommended --config "C:\.vsconfig"
  ```

## <a name="using---config"></a>Usando --config

::: moniker range="vs-2017"

Esse parâmetro de linha de comando é uma **novidade na versão 15.9**. Para saber mais sobre ela, confira a página [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

::: moniker-end

* Usando --config para instalar os componentes e cargas de trabalho de um arquivo de configuração de instalação salvo anteriormente:

  ```shell
  vs_enterprise.exe --config "C:\.vsconfig" --installPath "C:\VS"
  ```

* Usando --config para adicionar os componentes e cargas de trabalho a uma instalação existente:

  ```shell
  vs_enterprise.exe modify --installPath "C:\VS" --config "C:\.vsconfig"
  ```

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Criar uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)
* [IDs de carga de trabalho e de componente do Visual Studio](workload-and-component-ids.md)
