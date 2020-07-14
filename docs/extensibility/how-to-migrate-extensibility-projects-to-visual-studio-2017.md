---
title: 'Como: migrar projetos de extensibilidade para o Visual Studio 2017 | Microsoft Docs'
ms.date: 11/09/2016
ms.topic: how-to
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 37f7259c1133ea51e004b5f6b2061427ff71dea0
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905841"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>Como migrar projetos de extensibilidade para o Visual Studio 2017

Este documento explica como atualizar projetos de extensibilidade para o Visual Studio 2017. Além de descrever como atualizar os arquivos de projeto, ele também descreve como atualizar a partir da versão 2 do manifesto de extensão (VSIX v2) para o novo formato de manifesto do VSIX da versão 3 (VSIX v3).

## <a name="install-visual-studio-2017-with-required-workloads"></a>Instalar o Visual Studio 2017 com cargas de trabalho necessárias

Verifique se a instalação inclui as seguintes cargas de trabalho:

* Desenvolvimento para área de trabalho com .NET
* Desenvolvimento de extensões do Visual Studio

## <a name="open-vsix-solution-in-visual-studio-2017"></a>Abrir a solução VSIX no Visual Studio 2017

Todos os projetos VSIX exigirão uma atualização unidirecional de uma versão principal para o Visual Studio 2017.

O arquivo de projeto (por exemplo **. csproj*) será atualizado:

* MinimumVisualStudioVersion-agora definido como 15,0
* OldToolsVersion (se houver anteriormente) – agora definido como 14,0

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>Atualizar o pacote NuGet Microsoft. VSSDK. BuildTools

> [!Note]
> Se sua solução não referencia o pacote NuGet Microsoft. VSSDK. BuildTools, você pode ignorar esta etapa.

Para criar sua extensão no novo VSIX v3 (versão 3), sua solução precisará ser criada com as novas ferramentas de Build do VSSDK. Isso será instalado com o Visual Studio 2017, mas sua extensão do VSIX V2 pode estar mantendo uma referência a uma versão mais antiga por meio do NuGet. Nesse caso, será necessário instalar manualmente uma atualização do pacote NuGet Microsoft. VSSDK. BuildTools para sua solução.

Para atualizar as referências do NuGet para Microsoft. VSSDK. BuildTools:

* Clique com o botão direito do mouse na solução e escolha **gerenciar pacotes NuGet para solução**.
* Navegue até a guia **atualizações** .
* Selecione **Microsoft. VSSDK. BuildTools (versão mais recente)**.
* Pressione **Atualizar**.

![Ferramentas de Build do VSSDK](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>Fazer alterações no manifesto de extensão do VSIX

Para garantir que a instalação do Visual Studio do usuário tenha todos os assemblies necessários para executar a extensão, especifique todos os componentes ou pacotes de pré-requisito no arquivo de manifesto de extensão. Quando um usuário tenta instalar a extensão, o VSIXInstaller verificará se todos os pré-requisitos estão instalados. Se alguns estiverem ausentes, o usuário será solicitado a instalar os componentes ausentes como parte do processo de instalação da extensão.

> [!Note]
> No mínimo, todas as extensões devem especificar o componente do editor de núcleo do Visual Studio como um pré-requisito.

* Edite o arquivo de manifesto de extensão (normalmente chamado de *Source. Extension. vsixmanifest*).
* Verifique se `InstallationTarget` inclui 15,0.
* Adicione os pré-requisitos de instalação necessários (conforme mostrado no exemplo abaixo).
  * Recomendamos que você especifique apenas IDs de componente para pré-requisitos de instalação.
  * Consulte a seção no final deste documento para obter [instruções sobre como identificar IDs de componentes](#find-component-ids).

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

### <a name="option-use-the-designer-to-make-changes-to-the-vsix-extension-manifest"></a>Opção: Use o designer para fazer alterações no manifesto de extensão do VSIX

Em vez de editar diretamente o XML do manifesto, você pode usar a nova guia **pré-requisitos** no designer de manifesto para selecionar os pré-requisitos e o XML será atualizado para você.

> [!Note]
> O designer de manifesto só permitirá que você selecione componentes (não cargas de trabalho ou pacotes) que estão instalados na instância atual do Visual Studio. Se você precisar adicionar um pré-requisito para uma carga de trabalho, um pacote ou um componente que não esteja instalado no momento, edite o XML do manifesto diretamente.

* Arquivo Open *Source. Extension. vsixmanifest [Design]* .
* Selecione a guia **pré-requisitos** e pressione o botão **novo** .

   ![Designer de manifesto VSIX](media/vsix-manifest-designer.png)

* A janela **Adicionar novo pré-requisito** será aberta.

   ![Adicionar pré-requisito do VSIX](media/add-vsix-prerequisite.png)

* Clique na lista suspensa para **nome** e selecione o pré-requisito desejado.
* Atualize a versão, se necessário.

   > [!Note]
   > O campo versão será preenchido previamente com a versão do componente atualmente instalado, com um intervalo abrangendo até (mas não incluindo) a próxima versão principal do componente.

   ![Adicionar pré-requisito Roslyn](media/add-roslyn-prerequisite.png)

* Pressione **OK**.

## <a name="update-debug-settings-for-the-project"></a>Atualizar configurações de depuração para o projeto

Se você quiser depurar sua extensão em uma instância experimental do Visual Studio, certifique-se de que a ação configurações do projeto para início da **depuração**  >  **Start action** tenha o **Iniciar programa externo:** valor definido para o arquivo de *devenv.exe* da instalação do Visual Studio 2017.

Ele pode ser semelhante a: *C:\Program Files (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\devenv.exe*

![Iniciar programa externo](media/start-external-program.png)

> [!Note]
> A ação iniciar depuração normalmente é armazenada no arquivo *. csproj. User* . Esse arquivo geralmente é incluído no arquivo *. gitignore* e, portanto, não é normalmente salvo com outros arquivos de projeto quando confirmado no controle do código-fonte. Dessa forma, se você tiver recebido sua solução para o controle do código-fonte, é provável que o projeto não tenha nenhum valor definido para iniciar a ação. Novos projetos VSIX criados com o Visual Studio 2017 terão um arquivo *. csproj. User* criado com os padrões que apontam para o diretório de instalação atual do Visual Studio. No entanto, se você estiver migrando uma extensão do VSIX v2, é provável que o arquivo *. csproj. User* contenha referências ao diretório de instalação anterior da versão do Visual Studio. Definir o **valor para**  >  **iniciar a ação de início** permitirá que a instância experimental correta do Visual Studio seja iniciada quando você tentar depurar a extensão.

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>Verificar se a extensão foi compilada corretamente (como um VSIX v3)

* Compile o projeto VSIX.
* Descompacte o VSIX gerado.
  * Por padrão, o arquivo VSIX reside dentro de *bin/Debug* ou *bin/Release* como *[YourCustomExtension]. vsix*.
  * Renomeie *. vsix* para *. zip* para exibir facilmente o conteúdo.
* Verifique a existência de três arquivos:
  * *extensão. vsixmanifest*
  * *manifest.jsem*
  * *catalog.jsem*

## <a name="check-when-all-required-prerequisites-are-installed"></a>Verificar quando todos os pré-requisitos necessários estão instalados

Teste se o VSIX é instalado com êxito em um computador com todos os pré-requisitos necessários instalados.

> [!Note]
> Antes de instalar qualquer extensão, desative todas as instâncias do Visual Studio.

Tentativa de instalar a extensão:

* No Visual Studio 2017

![Instalador do VSIX no Visual Studio 2017](media/vsixinstaller-vs-2017.png)

* Opcional: verificar as versões anteriores do Visual Studio.
  * Comprova a compatibilidade com versões anteriores.
  * Deve funcionar para o Visual Studio 2012, Visual Studio 2013, Visual Studio 2015.
* Opcional: Verifique se o verificador de versão do instalador VSIX oferece uma opção de versões.
  * Inclui versões anteriores do Visual Studio (se instaladas).
  * Inclui o Visual Studio 2017.

Se o Visual Studio foi aberto recentemente, você poderá ver uma caixa de diálogo como esta:

![processos em execução do vs](media/vs-running-processes.png)

Aguarde até que os processos sejam desligados ou encerre manualmente as tarefas. Você pode encontrar os processos pelo nome listado ou com o PID listado em parênteses.

> [!Note]
> Esses processos não serão desligados automaticamente enquanto uma instância do Visual Studio estiver em execução. Verifique se você desligou todas as instâncias do Visual Studio no computador, incluindo as de outros usuários, e continue a tentar novamente.

## <a name="check-when-missing-the-required-prerequisites"></a>Verificar quando falta os pré-requisitos necessários

* Tente instalar a extensão em um computador com o Visual Studio 2017 que não contenha todos os componentes definidos nos pré-requisitos (acima).
* Verifique se a instalação identifica o componente/s ausentes e os lista como um pré-requisito no VSIXInstaller.
* Observação: a elevação será necessária se algum pré-requisito precisar ser instalado com a extensão.

![vsixinstaller de pré-requisito ausente](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>Decidir sobre componentes

Ao pesquisar suas dependências, você verá que uma dependência pode ser mapeada para vários componentes. Para determinar quais dependências você deve especificar como seu pré-requisito, sugerimos que você escolha um componente que tenha uma funcionalidade semelhante à sua extensão e também considere os usuários e que tipo de componentes eles provavelmente teriam instalado ou não se lembrarão da instalação. Também sugerimos a criação de suas extensões de uma maneira em que os pré-requisitos necessários satisfaçam apenas o mínimo que permitirá que sua extensão seja executada e que os recursos adicionais os tenham inativo se determinados componentes não forem detectados.

Para fornecer mais orientações, identificamos alguns tipos de extensão comuns e seus pré-requisitos sugeridos:

Tipo de extensão | Nome de exibição | ID
--- | --- | ---
Editor | Editor do Visual Studio Core | Microsoft.VisualStudio.Component.CoreEditor
Roslyn | C# e Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | Núcleo da carga de trabalho de área de trabalho gerenciada | Microsoft.VisualStudio.Component.ManagedDesktop.Core
Depurador | Depurador Just-In-Time | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>Localizar IDs de componente

A lista de componentes classificados pelo produto Visual Studio é a [carga de trabalho do visual studio 2017 e as IDs de componentes](/visualstudio/install/workload-and-component-ids?view=vs-2019). Use essas IDs de componente para suas IDs de pré-requisito em seu manifesto.

Se você não tiver certeza de qual componente contém um binário específico, baixe o [componente > planilha de mapeamento binário](https://aka.ms/vs2017componentid-binaries).

### <a name="vs2017-componentbinarymappingxlsx"></a>vs2017-ComponentBinaryMapping.xlsx

Há quatro colunas na planilha do Excel: **nome do componente**, **ComponentID**, **versão**e **nomes binários/de arquivo**.  Você pode usar os filtros para pesquisar e localizar componentes e binários específicos.

Para todas as suas referências, primeiro determine quais estão no componente principal do editor (Microsoft. VisualStudio. Component. CoreEditor).  No mínimo, exigimos que o componente principal do editor seja especificado como um pré-requisito para todas as extensões. Das referências que são deixadas que não estão no editor principal, adicione filtros na seção **nomes de binários/arquivos** para localizar componentes que tenham qualquer um dos subconjuntos dessas referências.

Exemplos:

* Se você tiver uma extensão de depurador e souber que seu projeto tem uma referência a *VSDebugEng.dll* e *VSDebug.dll*, clique no botão de filtro no cabeçalho **nomes de binários/arquivos** .  Pesquise "VSDebugEng.dll" e selecione *OK*.  Em seguida, clique no botão de filtro no cabeçalho **nomes de binários/arquivos** novamente e pesquise por "VSDebug.dll".  Marque a caixa de seleção **Adicionar seleção atual para filtrar** e selecione **OK**.  Agora, examine o **nome do componente** para encontrar um componente mais relacionado ao seu tipo de extensão. Neste exemplo, você escolheria o depurador just-in-time e o adicionaria ao seu vsixmanifest.
* Se você souber que seu projeto lida com elementos do depurador, poderá pesquisar "Debugger" na caixa de pesquisa de filtro para ver quais componentes contêm o depurador em seu nome.

## <a name="specify-a-visual-studio-2017-release"></a>Especificar uma versão 2017 do Visual Studio

Se sua extensão exigir uma versão específica do Visual Studio 2017, por exemplo, depende de um recurso lançado em 15,3, você deve especificar o número de Build em seu **INSTALLATIONTARGET**VSIX. Por exemplo, a versão 15,3 tem um número de Build de ' 15.0.26730.3 '. Você pode ver o mapeamento de liberações para criar números [aqui](../install/visual-studio-build-numbers-and-release-dates.md). O uso do número de versão ' 15,3 ' não funcionará corretamente.

Se sua extensão exigir 15,3 ou superior, você declararia a **versão InstallationTarget** como [15.0.26730.3, 16,0):

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```
