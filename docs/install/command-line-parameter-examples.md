---
title: Exemplos de parâmetros de linha de comando para a instalação do Visual Studio
description: Personalize esses exemplos para criar sua própria instalação de linha de comando do Visual Studio.
ms.date: 11/14/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: 837F31AA-F121-46e9-9996-F8BCE768E579
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b40b228ce04a83622f739d22b15c9ab126aade3f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803806"
---
# <a name="command-line-parameter-examples-for-visual-studio-2017-installation"></a>Exemplos de parâmetros de linha de comando para a instalação do Visual Studio 2017

Para ilustrar como [usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md), aqui estão vários exemplos que podem ser personalizados para atender às suas necessidades.

Em cada exemplo, `vs_enterprise.exe`, `vs_professional.exe` e `vs_community.exe` representam a respectiva edição do bootstrapper do Visual Studio, que é o arquivo pequeno (aproximadamente 1 MB) que inicia o processo de download. Se você estiver usando uma edição diferente, substitua o nome do bootstrapper adequado.

> [!NOTE]
> Todos os comandos exigem elevação administrativa e um prompt do Controle de Conta de Usuário será exibido se o processo não for iniciado em um prompt elevado.
>
> [!NOTE]
>  Você pode usar o caractere `^` no final de uma linha de comando para concatenar várias linhas em um único comando. Como alternativa, é possível simplesmente colocar essas linhas juntas em uma única linha. No PowerShell, o equivalente é o caractere de acento grave (`` ` ``).

## <a name="using---installpath"></a>Usando --installPath

* Instale uma instância mínima do Visual Studio, com nenhum prompt interativo, com exceção do progresso, exibido:

  ```cmd
  vs_enterprise.exe --installPath C:\minVS ^
   --add Microsoft.VisualStudio.Workload.CoreEditor ^
   --passive --norestart
  ```

* Atualize uma instância do Visual Studio usando a linha de comando, sem a exibição de prompts interativos, com exceção do progresso:

  ```cmd
  vs_enterprise.exe --update --quiet --wait
  vs_enterprise.exe update --wait --passive --norestart --installPath "C:\installPathVS"
  ```

  > [!NOTE]
  > Os dois comandos são obrigatórios. O primeiro comando atualiza o Instalador do Visual Studio. O segundo comando atualiza a instância do Visual Studio. Para evitar uma caixa de diálogo Controle de Conta de Usuário, execute o prompt de comando como Administrador.

* Instale silenciosamente, uma instância da área de trabalho do Visual Studio com o pacote de idioma francês, retornando somente quando o produto estiver instalado.

  ```cmd
  vs_enterprise.exe --installPath C:\desktopVS ^
   --addProductLang fr-FR ^
   --add Microsoft.VisualStudio.Workload.ManagedDesktop ^
   --includeRecommended --quiet --wait
  ```

  > [!NOTE]
  > O parâmetro `--wait` é projetado para uso em um arquivo em lotes. Em um arquivo em lotes, a execução do próximo comando não continuará até que a instalação seja concluída. A variável de ambiente `%ERRORLEVEL%` contém o valor retornado do comando, conforme documentado na página [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

## <a name="using---layout"></a>Usando --layout

* Baixe o editor de núcleo do Visual Studio (a configuração mínima do Visual Studio). Inclua apenas o pacote de idiomas em inglês:

  ```cmd
  vs_community.exe --layout C:\VS2017
   --lang en-US ^
   --add Microsoft.VisualStudio.Workload.CoreEditor
  ```

* Baixe as cargas de trabalho do .NET desktop e do .NET web juntamente com todos os componentes recomendados e com a extensão do GitHub. Inclua apenas o pacote de idiomas em inglês:

  ```cmd
  vs_community.exe --layout C:\VS2017 ^
   --lang en-US ^
   --add Microsoft.VisualStudio.Workload.NetWeb ^
   --add Microsoft.VisualStudio.Workload.ManagedDesktop ^
   --add Component.GitHub.VisualStudio ^
   --includeRecommended
  ```

## <a name="using---includerecommended"></a>Usando --includeRecommended

* Inicie uma instalação interativa de todas as cargas de trabalho e componentes que estão disponíveis no Visual Studio 2017 Enterprise edition:

  ```cmd
  vs_enterprise.exe --all --includeRecommended --includeOptional
  ```

* Instale uma segunda instância nomeada do Visual Studio 2017 Professional em um computador com Visual Studio 2017 Community edition já instalado, com suporte para o desenvolvimento do Node.js:

  ```cmd
  vs_professional.exe --installPath C:\VSforNode ^
   --add Microsoft.VisualStudio.Workload.Node --includeRecommended --nickname VSforNode
  ```

## <a name="using---remove"></a>Usando --remove

* Remova o componente Ferramentas de Criação de Perfil da instância do Visual Studio instalada por padrão:

  ```cmd
  vs_enterprise.exe modify ^
   --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" ^
   --remove Microsoft.VisualStudio.Component.DiagnosticTools ^
   --passive
  ```

## <a name="using---path"></a>Usando --path

Esses parâmetros de linha de comando são **novos no 15.7**. Para obter mais informações sobre eles, consulte a página [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

* Usando os caminhos de instalação, de cache e compartilhados:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path cache="C:\VS\cache" --path shared="C:\VS\shared"`

* Usando somente os caminhos de instalação e de cache:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path cache="C:\VS\cache"`

* Usando somente os caminhos de instalação e compartilhados:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path shared="C:\VS\shared"`

* Usando somente o caminho de instalação:

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS"`

## <a name="using-export"></a>Usando a exportação

Este comando da linha de comando é uma **novidade na versão 15.9**. Para saber mais sobre ela, confira a página [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

* Usando a exportação para salvar a seleção de uma instalação:

```cmd
vs_enterprise.exe export --installPath "C:\VS" --config "C:\.vsconfig"
```

* Usando a exportação para salvar a seleção personalizada do zero:

```cmd
vs_enterprise.exe export --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeRecommended --config "C:\.vsconfig"
```

## <a name="using---config"></a>Usando --config

Esse parâmetro de linha de comando é uma **novidade na versão 15.9**. Para saber mais sobre ela, confira a página [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

* Usando --config para instalar os componentes e cargas de trabalho de um arquivo de configuração de instalação salvo anteriormente:

```cmd
vs_enterprise.exe --config "C:\.vsconfig" --installPath "C:\VS"
```

* Usando --config para adicionar os componentes e cargas de trabalho a uma instalação existente:

```cmd
vs_enterprise.exe modify --installPath "C:\VS" --config "C:\.vsconfig"
```


[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Criar uma instalação offline do Visual Studio 2017](create-an-offline-installation-of-visual-studio.md)
