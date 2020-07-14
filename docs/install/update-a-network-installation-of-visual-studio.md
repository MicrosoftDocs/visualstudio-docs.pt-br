---
title: Atualizar uma instalação baseada em rede
description: Saiba como atualizar uma instalação do Visual Studio baseada em rede usando o comando --layout
ms.date: 06/29/2020
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 1AF69C0E-0AC9-451B-845D-AE4EDBCEA65C
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: f54ee1191dd998d34e46a442debafc175ce98c8b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545425"
---
# <a name="update-a-network-based-installation-of-visual-studio"></a>Atualizar uma instalação em rede do Visual Studio

É possível atualizar um layout de instalação de rede do Visual Studio com as últimas atualizações de produto, para que ele possa ser usado como um ponto de instalação para a atualização mais recente do Visual Studio e também manter instalações que já estão implantadas em estações de trabalho do cliente.

## <a name="how-to-update-a-network-layout"></a>Como atualizar um layout de rede

> [!IMPORTANT]
> Essas instruções pressupõem que você criou anteriormente um layout de instalação de rede. Para obter mais informações sobre como fazer isso, consulte a página [criar uma instalação de rede do Visual Studio](create-a-network-installation-of-visual-studio.md) .

Para atualizar o compartilhamento de instalação de rede para que ele inclua as últimas atualizações, execute o comando `--layout` para baixar pacotes atualizados de forma incremental.

::: moniker range="vs-2017"

**Novo no 15,3**: se você selecionou um layout parcial quando [criou o layout de rede pela primeira vez](create-a-network-installation-of-visual-studio.md), essas configurações serão salvas. Comandos de layout futuros usam as opções anteriores e quaisquer novas opções que você especificar. Porém, se você está usando um layout de uma versão anterior, use os mesmos parâmetros de linha de comando utilizados ao criar o layout de instalação de rede pela primeira vez (em outras palavras, as mesmas cargas de trabalho e os mesmos idiomas) para atualizar o conteúdo.

::: moniker-end

::: moniker range="vs-2019"

Se você selecionou um layout parcial quando [criou o layout de rede pela primeira vez](create-a-network-installation-of-visual-studio.md), essas configurações serão salvas. Comandos de layout futuros usam as opções anteriores e quaisquer novas opções que você especificar.

::: moniker-end

Se você hospedar um layout em um compartilhamento de arquivos, deverá atualizar uma cópia privada do layout (por exemplo, c:\VSLayout) e, depois, depois que todo o conteúdo atualizado for baixado, copie-o para o compartilhamento de arquivos (por exemplo, \\ server\products\VS). Se você não fizer isso, haverá uma chance maior de que quaisquer usuários que executem a instalação enquanto o layout está sendo atualizado não consigam obter todo o conteúdo do layout, pois ele não estará completamente atualizado.

Vamos examinar alguns exemplos de como criar e, em seguida, atualizar um layout:

* Primeiro, aqui está um exemplo de como criar um layout com uma carga de trabalho apenas para inglês:

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
  ```

* Veja aqui como atualizar esse mesmo layout para uma versão mais recente. Você não precisa especificar parâmetros de linha de comando adicionais. As configurações anteriores foram salvas e serão usadas por quaisquer comandos de layout subsequentes nesta pasta de layout.

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout
  ```

* É assim que se atualiza o layout para uma versão mais recente de maneira autônoma. A operação de layout executa o processo de configuração em uma nova janela do console. A janela é deixada aberta para que os usuários possam ver o resultado final e um resumo dos erros que podem ter ocorrido. Se você estiver executando uma operação de layout de forma autônoma (por exemplo, se você tiver um script que é executado regularmente para atualizar seu layout para a versão mais recente), então, use o parâmetro `--passive` e o processo fechará automaticamente a janela.

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --passive
  ```

* Veja aqui como adicionar uma carga de trabalho e idioma traduzido adicionais.  (Esse comando adiciona a carga de trabalho de *desenvolvimento do Azure* .)  Agora, a área de trabalho gerenciada e o Azure estão incluídos nesse layout.  Os recursos de idioma para inglês e alemão também estão incluídos para todas essas cargas de trabalho.  Além disso, o layout é atualizado para a versão mais recente disponível.

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
  ```

    > [!IMPORTANT]
    > Uma operação de atualização não instala componentes opcionais recém-adicionados. Se você precisar dos componentes opcionais adicionados recentemente, remova os componentes opcionais antigos no `Layout.JSON` [arquivo de resposta](automated-installation-with-response-file.md) e inclua os componentes necessários na seção "Adicionar" de `Layout.JSON` . 
    >
    > **Solução alternativa**: execute uma operação de modificação separada após uma atualização para instalar os componentes ausentes.

* E, finalmente, eis aqui como adicionar uma carga de trabalho e um idioma traduzido adicionais sem atualizar a versão. (Esse comando adiciona o ASP.NET e a carga de trabalho de *desenvolvimento da Web* .)  Agora, a área de trabalho gerenciada, o Azure e o ASP.NET & as cargas de desenvolvimento da Web estão incluídas nesse layout. Os recursos de idioma para inglês, alemão e francês também estão incluídos para todas essas cargas de trabalho.  No entanto, o layout não foi atualizado para a versão mais recente disponível quando esse comando foi executado. Ele permanece com a versão existente.

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.NetWeb --lang fr-FR --keepLayoutVersion
  ```

## <a name="deploy-an-update-to-client-machines"></a>Implantar uma atualização em computadores cliente

Dependendo de como o ambiente de rede é configurado, uma atualização pode ser implantada por um administrador de empresa ou iniciada de um computador cliente.

* Os usuários podem atualizar uma instância do Visual Studio instalada de uma pasta de instalação offline:
  * Execute o instalador do Visual Studio.
  * Em seguida, clique em **Atualizar**.

::: moniker range="vs-2017"

* Os administradores podem atualizar implantações de cliente do Visual Studio sem qualquer interação do usuário com dois comandos separados:
  * Primeiro, atualize o Instalador do Visual Studio: <br>```vs_enterprise.exe --quiet --update```
  * Depois, atualize o aplicativo do Visual Studio em si: <br>```vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" --quiet --wait --norestart```

::: moniker-end

::: moniker range="vs-2019"

* Os administradores podem atualizar implantações de cliente do Visual Studio sem qualquer interação do usuário com dois comandos separados:
  * Primeiro, atualize o Instalador do Visual Studio: <br>```vs_enterprise.exe --quiet --update```
  * Depois, atualize o aplicativo do Visual Studio em si: <br>```vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" --quiet --wait --norestart```

::: moniker-end

> [!NOTE]
> Use o [comando vswhere.exe](tools-for-managing-visual-studio-instances.md) para identificar o caminho de instalação de uma instância existente do Visual Studio em um computador cliente.
>
> [!TIP]
> Para obter detalhes sobre como controlar quando as notificações de atualização são apresentadas aos usuários, confira [Controlar as atualizações nas implantações do Visual Studio com base em rede](controlling-updates-to-visual-studio-deployments.md).

## <a name="verify-a-layout"></a>Verificar um layout

Use `--verify` para executar a verificação no cache offline fornecido. Ele verifica se os arquivos de pacotes estão ausentes ou são inválidos. No final da verificação, imprime a lista de arquivos ausentes e arquivos inválidos.

```cmd
vs_enterprise.exe --layout <layoutDir> --verify
```

O vs_enterprise.exe pode ser invocado dentro do layoutDir.

> [!NOTE]
> Alguns arquivos de metadados importantes que são necessários para a opção `--verify` devem estar no cache offline do layout. Se esses arquivos de metadados estiverem ausentes, "--verify" não poderá ser executado e a instalação apresentará um erro. Se esse erro ocorrer, recrie um novo layout offline para uma pasta diferente (ou na mesma pasta de cache offline). Para fazer isso, execute o mesmo comando de layout que você usou para criar o layout offline inicial. Por exemplo, `vs_enterprise.exe --layout <layoutDir>`.

A Microsoft fornece atualizações para o Visual Studio periodicamente, portanto, o novo layout que você criar poderá não ser da mesma versão que o layout inicial.

> [!NOTE]
> A verificação funciona apenas para a versão mais recente de uma versão secundária específica do Visual Studio. Assim que uma nova versão é lançada, a verificação não funcionará para versões de nível de patch anteriores da mesma versão secundária.

## <a name="fix-a-layout"></a>Corrigir um layout

Use `--fix` para executar a mesma verificação que `--verify` e também tentar corrigir os problemas identificados. O processo `--fix` precisa de uma conexão de Internet, portanto, verifique se o computador está conectado à Internet antes de você invocar `--fix`.

```cmd
vs_enterprise.exe --layout <layoutDir> --fix
```

O vs_enterprise.exe pode ser invocado dentro do layoutDir.

## <a name="remove-older-versions-from-a-layout"></a>Remover versões mais antigas de um layout

Depois de executar atualizações de layout para um cache offline, a pasta de cache de layout pode ter alguns pacotes obsoletos que não são mais requeridos pela instalação do Visual Studio mais recente. Você pode usar a opção `--clean` para remover pacotes obsoletos de uma pasta de cache offline.

Para fazer isso, você precisará dos caminhos de arquivo para os manifestos de catálogo que contêm esses pacotes obsoletos. Você pode encontrar os que manifestos de catálogo em uma pasta "Arquivo morto" no cache de layout offline. Eles são salvos nela quando você atualiza um layout. Na pasta "Arquivo morto", há uma ou mais pastas chamadas "GUID", cada qual contendo um manifesto de catálogo obsoleto. O número de pastas "GUID" deve ser o mesmo que o número de atualizações feitas em seu cache offline.

Alguns arquivos são salvos dentro de cada pasta "GUID". Os dois arquivos mais interessantes são um arquivo "catalog.json" e um arquivo "version.txt". O arquivo "catalog.json" é o manifesto de catálogo obsoleto que você precisará passar para a opção `--clean`. O outro arquivo, version.txt, contém a versão deste manifesto de catálogo obsoleto. Com base no número de versão, você pode decidir se deseja remover pacotes obsoletos do manifesto de catálogo. Você pode fazer o mesmo ao percorrer as outras pastas "GUID". Depois de tomar a decisão sobre os catálogos que deseja limpar, execute o comando `--clean` fornecendo os caminhos de arquivos para esses catálogos.

Aqui estão alguns exemplos de como usar a opção --clean:

```cmd
vs_enterprise.exe --layout <layoutDir> --clean <file-path-of-catalog1> <file-path-of-catalog2> …
```

```cmd
vs_enterprise.exe --layout <layoutDir> --clean <file-path-of-catalog1> --clean <file-path-of-catalog2> …
```

Você também pode invocar vs_enterprise.exe dentro do &lt;layoutDir&gt;. Aqui está um exemplo:

```cmd
c:\VSLayout\vs_enterprise.exe --layout c:\VSLayout --clean c:\VSLayout\Archive\1cd70189-fc55-4583-8ad8-a2711e928325\Catalog.json --clean c:\VS2017Layout\Archive\d420889f-6aad-4ba4-99e4-ed7833795a10\Catalog.json
```

Quando você executa esse comando, a instalação analisa sua pasta de cache offline para localizar a lista de arquivos que ela removerá. Você terá a oportunidade de examinar os arquivos que serão excluídos e confirmar as exclusões.

## <a name="get-support-for-your-offline-installer"></a>Obtenha suporte para o instalador offline

Caso tenha um problema com a instalação offline, gostaríamos de saber a respeito. A melhor maneira de fazer isso é usando a ferramenta [Relatar um Problema](../ide/how-to-report-a-problem-with-visual-studio.md). Ao usar essa ferramenta, é possível enviar-nos a telemetria e os logs necessários para nos ajudar a diagnosticar e corrigir o problema.

Também oferecemos uma opção de suporte de [**chat ao vivo**](https://visualstudio.microsoft.com/vs/support/#talktous) (somente em inglês) para problemas relacionados à instalação.

Também temos outras opções de suporte disponíveis. Para obter uma lista, confira nossa página de [comentários](../ide/feedback-options.md).

## <a name="see-also"></a>Consulte também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Ferramentas para detectar e gerenciar instâncias do Visual Studio](tools-for-managing-visual-studio-instances.md)
* [Atualizações de controle para implantações do Visual Studio com base em rede](controlling-updates-to-visual-studio-deployments.md)
* [Ciclo de vida do produto Visual Studio e manutenção](/visualstudio/releases/2019/servicing/)
