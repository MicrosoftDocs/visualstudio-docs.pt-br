---
title: Incluindo um pacote NuGet no projeto
description: Este documento aborda como incluir um pacote NuGet em um projeto Xamarin. Ele explica a descoberta e download de um pacote, apresentando também os recursos de integração do IDE.
author: conceptdev
ms.author: crdun
ms.date: 04/14/2017
ms.assetid: 5C800815-0B13-4B27-B017-95FCEF1A0EA2
ms.openlocfilehash: 0a98425ba12ae7aba16a2bc6ffa29e701c1b9f11
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948616"
---
# <a name="include-a-nuget-package-in-your-project"></a>Incluir um pacote NuGet em seu projeto

O NuGet é o gerenciador de pacotes mais popular para desenvolvimento .NET e é interno no Visual Studio para Mac e no Visual Studio no Windows. Você pode pesquisar e adicionar pacotes aos seus projetos Xamarin.iOS e Xamarin.Android usando um dos IDE.

Este artigo descreve como incluir um pacote NuGet em um projeto e demonstra a cadeia de ferramentas que facilita esse processo.

## <a name="nuget-in-visual-studio-for-mac"></a>NuGet no Visual Studio para Mac

Para demonstrar a funcionalidade do pacote NuGet, primeiro veremos como criar um aplicativo e como adicionar um pacote nele. Em seguida, abordaremos os recursos do IDE que ajudam a gerenciar pacotes.

## <a name="create-a-new-project"></a>Criar um novo projeto

Primeiro, crie um projeto chamado `HelloNuget` conforme ilustrado abaixo. Este exemplo mostra o modelo de Aplicativo de exibição única do iOS, mas funcionaria com qualquer tipo de projeto compatível:

![Criar novo projeto do iOS](media/nuget-walkthrough-NewProject.png)

## <a name="adding-a-package"></a>Adicionar um pacote

Com o projeto aberto no Visual Studio para Mac, clique com o botão direito do mouse na pasta **Pacotes** no **Painel de Soluções** e selecione **Adicionar Pacotes**:

![Ação de contexto Adicionar novo pacote NuGet](media/nuget-walkthrough-PackagesMenu.png)

Isso inicia a janela **Adicionar Pacotes**. Verifique se a lista suspensa Origem está definida como `nuget.org`:

![Lista suspensa Origem](media/nuget-walkthrough-Source.png)

Quando a janela é aberta, ela carrega uma lista de pacotes da origem de pacote padrão: nuget.org. Os primeiros resultados serão semelhantes a estes:

![Listar pacotes NuGet](media/nuget-walkthrough-AddPackages1.png)

Use a caixa de pesquisa no canto superior direito para localizar um pacote específico, como o `azure`. Quando você encontrar um pacote que deseja usar, selecione-o e clique no botão **Adicionar pacote** para iniciar a instalação.

[Adicionar o pacote Azure NuGet](media/nuget-walkthrough-AddPackages2.png)

Depois que o pacote for baixado, ele será adicionado ao seu projeto. A solução mudará da seguinte maneira:

* O nó **Referências** conterá uma lista de todos os assemblies que fazem parte de um pacote NuGet.
* O nó **Pacotes** exibe cada pacote NuGet que você baixou. Você pode atualizar ou remover um pacote da lista.
* Um arquivo **packages.config** será adicionado ao projeto. Esse arquivo XML é usado pelo IDE para controlar quais versões do pacote são referenciada neste projeto. Esse arquivo não deve ser editado manualmente e deve ser mantido no controle de versão. Observe que é possível usar um arquivo project.json em vez de um arquivo packages.config. O arquivo project.json é um formato de arquivo de pacote novo introduzido com o NuGet 3, que dá suporte à restauração transitiva. Informações mais detalhadas sobre o project.json podem ser encontradas na [Documentação do NuGet](http://docs.microsoft.com/NuGet/Schema/Project-Json). O arquivo project.json precisa ser adicionado manualmente e o projeto fechado e reaberto para que o arquivo possa ser usado no Visual Studio para Mac.

## <a name="using-nuget-packages"></a>Usando pacotes NuGet

Depois que o pacote NuGet for adicionado e as referências de projeto forem atualizadas, você poderá programar as APIs como faria com qualquer referência de projeto.

Verifique se você adicionou as diretivas `using` necessárias na parte superior do arquivo:

```csharp
using Newtonsoft.Json;
```

A maioria dos NuGet fornecem informações adicionais, como um LEIAME ou um link da página do Projeto para a fonte do Nuget. Normalmente, um link para isso é encontrado na sinopse do pacote na página Adicionar pacotes:

[Link Exibir de página do projeto](media/nuget-walkthrough-project-page.png)

<a name="Package_Updates" class="injected"></a>

## <a name="package-updates"></a>Atualizações de Pacote

As atualizações de pacote podem ser feitas ao mesmo tempo, clicando com o botão direito do mouse no nó **Pacotes** ou individualmente em cada componente.

Clique com o botão direito do mouse em **Pacotes** para acessar o menu de contexto:

![Menu Pacotes](media/nuget-walkthrough-PackagesMenu.png)

*   **Adicionar pacotes** –Abre a janela para adicionar mais pacotes ao projeto.
*   **Atualizar** – Verifica o servidor de origem de cada pacote e baixa as versões mais recentes.
*   **Restaurar** – Baixa todos os pacotes ausentes (sem atualizar os pacotes existentes para as versões mais recentes).

As opções Atualizar e Restaurar também estão disponíveis no nível da Solução, afetando todos os projetos na solução.

Também é possível clicar com o botão direito do mouse em pacotes individuais para acessar um menu de contexto:

![Menu Pacotes](media/nuget-walkthrough-PackageMenu.png)

*   **Número de versão** – O número de versão é um item de menu desabilitado, sendo informado apenas para fins informativos.
*   **Atualizar** – Verifica o servidor de origem e baixa uma versão mais recente (se houver).
*   **Remover** – Remove o pacote desse projeto e os assemblies relevantes das Referências do projeto.

## <a name="adding-package-sources"></a>Adicionando origens de pacotes

Os pacotes disponíveis para instalação são recuperados inicialmente de nuget.org. No entanto, você pode adicionar outros locais de pacotes para o Visual Studio para Mac. Isso pode ser útil para testar seus próprios pacotes NuGet em desenvolvimento ou para usar um servidor NuGet privado dentro de sua empresa ou organização.

No Visual Studio para Mac, navegue até **Visual Studio > Preferências > NuGet > Origens** para exibir e editar a lista de origens de pacote. Observe que as origens podem ser um servidor remoto (especificado por uma URL) ou um diretório local.

![Origens dos pacotes](media/nuget-walkthrough-PackageSource.png)

Clique em **Adicionar** para configurar uma nova origem. Insira um nome amigável e a URL (ou caminho de arquivo) para a origem do pacote. Se a origem for um servidor Web seguro, insira também o nome de usuário e a senha, caso contrário, deixe essas entradas em branco:

![Adicionar origens de pacotes](media/nuget-walkthrough-PackageSource2.png)

É possível selecionar diferentes origens ao procurar pacotes:

![Adicionar origens de pacotes](media/nuget-walkthrough-PackageSource3.png)

## <a name="version-control"></a>Controle de versão

A documentação do NuGet aborda como [usar NuGet sem confirmar pacotes no controle do código-fonte](/nuget/consume-packages/packages-and-source-control). Se você preferir não armazenar binários e informações não usadas no controle do código-fonte, configure o Visual Studio para Mac para restaurar automaticamente os pacotes do servidor. Isso significa que, quando um desenvolvedor recuperar o projeto do controle do código-fonte pela primeira vez, o Visual Studio para Mac baixará e instalará os pacotes necessários automaticamente.

![Restaurar os pacotes automaticamente](media/nuget-walkthrough-AutoRestore.png)

Consulte a documentação do controle do código-fonte específico para ver detalhes sobre como excluir o diretório `packages` do rastreamento.

## <a name="see-also"></a>Consulte também

* [Instalar e usar um pacote no Visual Studio (no Windows)](/nuget/quickstart/install-and-use-a-package-in-visual-studio)
