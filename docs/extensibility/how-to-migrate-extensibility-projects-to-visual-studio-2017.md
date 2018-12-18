---
title: 'Como: migrar projetos de extensibilidade para o Visual Studio 2017 | Microsoft Docs'
ms.custom: ''
ms.date: 11/09/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 195d63e5ddb8b8536c1d0c1c4197270f5b3aa508
ms.sourcegitcommit: 331dbb12e11fcd7f5d15fab05f3c861e48126e43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51826811"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>Como: migrar projetos de extensibilidade para o Visual Studio 2017

Este documento explica como atualizar projetos de extensibilidade para o Visual Studio 2017. Além de descrever como atualizar os arquivos de projeto, ele também descreve como atualizar da versão do manifesto de extensão 2 (v2 VSIX) para o formato manifesto do VSIX do novo versão 3 (v3 VSIX).

## <a name="install-visual-studio-2017-with-required-workloads"></a>Instalar o Visual Studio 2017 com cargas de trabalho necessárias

Certifique-se de que sua instalação inclui as seguintes cargas de trabalho:

* Desenvolvimento de área de trabalho do .NET
* Desenvolvimento de extensões do Visual Studio

## <a name="open-vsix-solution-in-visual-studio-2017"></a>Abra a solução VSIX no Visual Studio 2017

Todos os projetos VSIX exigirá uma atualização unidirecional da versão principal para o Visual Studio 2017.

O arquivo de projeto (por exemplo **. csproj*) será atualizada:

* MinimumVisualStudioVersion - agora definido como 15.0
* OldToolsVersion (se existir anteriormente) – agora definido como 14.0

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>Atualizar o pacote Microsoft.VSSDK.BuildTools NuGet

>**Observação:** se sua solução não fizer referência para o pacote do Microsoft.VSSDK.BuildTools NuGet, você pode ignorar esta etapa.

A fim de criar sua extensão no VSIX v3 novo formato (versão 3), sua solução precisará ser criado com as novas ferramentas de VSSDK compilar. Isso será instalado com o Visual Studio 2017, mas sua extensão do VSIX v2 pode ser mantendo uma referência para uma versão mais antiga por meio do NuGet. Nesse caso, você precisará instalar manualmente uma atualização do pacote do Microsoft.VSSDK.BuildTools NuGet para sua solução.

Para atualizar as referências de NuGet para Microsoft.VSSDK.BuildTools:

* Clique com botão direito na solução e escolha **gerenciar pacotes NuGet para solução**.
* Navegue até a **atualizações** guia.
* Selecione **Microsoft.VSSDK.BuildTools (versão mais recente)**.
* Pressione **atualização**.

![Ferramentas de build do VSSDK](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>Fazer alterações no manifesto de extensão do VSIX

Para garantir que a instalação do usuário do Visual Studio tem todos os assemblies necessários para executar a extensão, especifique todos os componentes de pré-requisito ou pacotes no arquivo de manifesto de extensão. Quando um usuário tenta instalar a extensão, o VSIXInstaller verificará para ver se todos os pré-requisitos estão instalados. Se alguns estiverem ausentes, o usuário será solicitado para instalar os componentes ausentes como parte do processo de instalação da extensão.

>**Observação:** no mínimo, todas as extensões devem especificar o componente de editor de núcleo do Visual Studio como um pré-requisito.

* Edite o arquivo de manifesto de extensão (normalmente chamada de *vsixmanifest*).
* Certifique-se de `InstallationTarget` inclui 15.0.
* Adicione os pré-requisitos de instalação necessárias (conforme mostrado no exemplo a seguir).
  * É recomendável que você especificar somente IDs de componente os pré-requisitos de instalação.
  * Consulte a seção no final deste documento para [instruções sobre como identificar as IDs de componente](#find-component-ids).

Exemplo:

```xml
<PackageManifest>
 ...
    <Prerequisites>
        <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Component.DiagnosticTools" Version="[15.0.25814.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Shell.12.0" Version="[12.0]" />
    </Prerequisites>
 ...
</PackageManifest>
```

### <a name="option-use-the-designer-to-make-changes-to-the-vsix-extension-manifest"></a>Opção: Usar o designer para fazer alterações no manifesto de extensão do VSIX

Em vez de editar diretamente o XML do manifesto, você pode usar o novo **pré-requisitos** guia no Designer de manifesto para selecionar os pré-requisitos e o XML será atualizado para você.

>**Observação:** o Designer de manifesto só permitirá a seleção de componentes (não as cargas de trabalho ou pacotes) que estão instalados na instância atual do Visual Studio. Se você precisar adicionar um pré-requisito para uma carga de trabalho, pacote ou componente que não está instalado, edite o manifesto XML diretamente.

* Abra *vsixmanifest [Design]* arquivo.
* Selecione **pré-requisitos** guia e pressione **New** botão.

  ![Designer de manifesto do VSIX](media/vsix-manifest-designer.png)

* O **adicionar novo pré-requisito** janela será aberta.

  ![Adicionar o pré-requisito do vsix](media/add-vsix-prerequisite.png)

* Clique no menu suspenso **nome** e selecione o pré-requisito desejado.
* Atualize a versão, se necessário.

  >Observação: O campo de versão será preenchido previamente com a versão do componente instalado no momento, com um intervalo que abrange até (, mas não incluindo) a próxima versão principal do componente.

  ![Adicionar o pré-requisito de roslyn](media/add-roslyn-prerequisite.png)

* Pressione **Okey**.

## <a name="update-debug-settings-for-the-project"></a>Atualizar as configurações de depuração para o projeto

Se você deseja depurar sua extensão em uma instância experimental do Visual Studio, verifique se as configurações de projeto para **Debug** > **iniciar ação** tem o **iniciar externo programa:** valor definido o *devenv.exe* arquivo de sua instalação do Visual Studio 2017.

Ele pode parecer com: *C:\Program Files (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\devenv.exe*

![Iniciar programa externo](media/start-external-program.png)

>**Observação:** depurar iniciar ação normalmente é armazenada em de *. csproj* arquivo. Geralmente, esse arquivo é incluído na *. gitignore* de arquivo e, portanto, não é normalmente salva com outros arquivos de projeto quando o compromisso de controle de origem. Dessa forma, se você tiver extraída sua solução atualizada do controle de origem é provável que o projeto não terá nenhum valor definido para a ação inicial. Novos projetos VSIX criados com o Visual Studio 2017 terá um *. csproj* arquivo criado com os padrões que aponta para o diretório de instalação atual do Visual Studio. No entanto se você estiver migrando uma extensão do VSIX v2, é provável que o *. csproj* arquivo conterá as referências para o diretório de instalação da versão do Visual Studio anterior. Configurar o valor de **Debug** > **iniciar ação** permitirá que a instância experimental do Visual Studio correta iniciar quando você tenta depurar sua extensão.

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>Verifique que a extensão seja compilado corretamente (como um VSIX v3)

* Compile o projeto VSIX.
* Descompacte o VSIX gerado.
  * Por padrão, o arquivo VSIX reside dentro *bin/Debug* ou *bin/Release* como *VSIX [YourCustomExtension]*.
  * Renomeie *. VSIX* à *. zip* facilmente exibir o conteúdo.
* Verificar a existência dos três arquivos:
  * *vsixmanifest*
  * *manifest. JSON*
  * *Catalog. JSON*

## <a name="check-when-all-required-prerequisites-are-installed"></a>Verificar quando todos os pré-requisitos necessários são instalados

Teste o VSIX é instalado com êxito em um computador com os pré-requisitos necessários instalados.

>**Observação:** antes de instalar qualquer extensão, por favor, feche todas as instâncias do Visual Studio.

Tentativa de instalar a extensão:

* No Visual Studio 2017

![Instalador do VSIX no Visual Studio 2017](media/vsixinstaller-vs-2017.png)

* Opcional: Verifique as versões anteriores do Visual Studio.
  * Prova a compatibilidade com versões anteriores.
  * Deve funcionar para o Visual Studio 2012, Visual Studio 2013, Visual Studio 2015.
* Opcional: Verifique se o verificador de versão do instalador do VSIX oferece uma opção de versões.
  * Inclui as versões anteriores do Visual Studio (se instalado).
  * Inclui o Visual Studio 2017.

Se o Visual Studio recentemente foi aberto, você poderá ver uma caixa de diálogo como esta:

![VS processos em execução](media/vs-running-processes.png)

Aguarde até que os processos desligar ou encerrar manualmente as tarefas. Você pode encontrar os processos pelo nome do listados, ou com o PID listado entre parênteses.

>**Observação:** esses processos não serão automaticamente desligado enquanto uma instância do Visual Studio está em execução. Certifique-se de que você encerrou todas as instâncias do Visual Studio no computador - incluindo aqueles de outros usuários, e continuar tentar novamente.

## <a name="check-when-missing-the-required-prerequisites"></a>Verificar quando os pré-requisitos necessários ausentes

* Tentativa de instalar a extensão em um computador com o Visual Studio 2017 que não CONTÊM todos os componentes definidos em pré-requisitos (acima).
* Verifique se a instalação identifica o componente/s ausente e listá-los como um pré-requisito no VSIXInstaller.
* Observação: Elevação será necessária se todos os pré-requisitos precisam ser instalados com a extensão.

![pré-requisito ausente vsixinstaller](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>Decidir sobre componentes

Ao procurar por suas dependências, você encontrará que uma dependência poderia mapear para vários componentes. Para determinar quais dependências você deve especificar como o pré-requisito, sugerimos que você escolha um componente que tem uma funcionalidade semelhante a sua extensão e também considerar que os usuários e que tipo de componentes seria muito provavelmente tiverem instalado ou incomodaria a instalação. Também sugerimos a construção de suas extensões de uma forma em que os pré-requisitos necessários satisfazem apenas o mínimo que permitirá que a sua extensão executar e para recursos adicionais de peça fique inativo se certos componentes não são detectados.

Para fornecer mais orientações, identificamos alguns tipos comuns de extensão e seus pré-requisitos sugeridos:

Tipo de extensão | Nome de Exibição | Id
--- | --- | ---
Editor | Editor do Visual Studio Core  | Microsoft.VisualStudio.Component.CoreEditor
Roslyn | C# e Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | Núcleo da carga de trabalho de área de trabalho gerenciada | Microsoft.VisualStudio.Component.ManagedDesktop.Core
Depurador | Depurador Just-In-Time | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>Localizar IDs de componente

A lista de componentes, classificadas por produto do Visual Studio está em [IDs de carga de trabalho e de componente do Visual Studio 2017](https://aka.ms/vs2017componentIDs). Use essas IDs de componente para suas IDs de pré-requisito em seu manifesto.

Se você não tiver certeza de qual componente contenha um binário específico, baixe o [componente de planilha de mapeamento binário ->](https://aka.ms/vs2017componentid-binaries).

### <a name="vs2017-componentbinarymappingxlsx"></a>vs2017 ComponentBinaryMapping.xlsx

Há quatro colunas na planilha do Excel: **nome do componente**, **ComponentId**, **versão**, e **binário / nomes de arquivo**.  Você pode usar os filtros para pesquisar e localizar os binários e componentes específicos.

Para todas as suas referências, primeiro determine quais delas são no componente editor (Microsoft.VisualStudio.Component.CoreEditor) core.  No mínimo, exigimos o componente do editor de núcleo seja especificado como um pré-requisito para todas as extensões. De referências que são deixadas que não estão no editor de núcleo, adicione filtros na **binários / nomes de arquivos** seção para encontrar componentes que têm algum subconjunto essas referências.

Exemplos:

* Se você tiver uma extensão de depurador e saber que o projeto tem uma referência a *Vsdebugeng* e *VSDebug.dll*, clique no botão de filtro no **binários / nomes de arquivos**cabeçalho.  Pesquise por "Vsdebugeng" e selecione *Okey*.  Em seguida, clique no botão de filtro na **binários / nomes de arquivos** cabeçalho novamente e procure por "VSDebug.dll".  Marque a caixa de seleção **Adicionar seleção atual ao filtro** e selecione **Okey**.  Agora examine a **nome do componente** para localizar um componente que é mais relacionadas ao seu tipo de extensão. Neste exemplo, você pode escolher o Just-In-Time do depurador e adicioná-lo ao seu vsixmanifest.
* Se você souber que seu projeto lida com elementos do depurador, você pode pesquisar em "depurador" na caixa de pesquisa do filtro para ver quais componentes contêm o depurador em seu nome.

## <a name="specify-a-visual-studio-2017-release"></a>Especifique uma versão do Visual Studio 2017

Se sua extensão requer uma versão específica do Visual Studio 2017, por exemplo, ele depende de um recurso lançado no 15.3, você deve especificar o número de compilação no seu VSIX **InstallationTarget**. Por exemplo, a versão 15.3 tem um número de compilação de '15.0.26730.3'. Você pode ver o mapeamento de lançamentos para números de compilação [aqui](../install/visual-studio-build-numbers-and-release-dates.md). Usando o número de versão '15.3' não funcionará corretamente.

Se sua extensão requer 15.3 ou superior, você poderia declarar o **InstallationTarget versão** como [15.0.26730.3, 16.0):

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```
