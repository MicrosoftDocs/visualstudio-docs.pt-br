---
title: Criar uma instalação offline
description: Saiba como instalar o Visual Studio offline quando você tiver uma conexão com a Internet não confiável ou largura de banda baixa.
ms.date: 4/16/2021
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- offline installation [Visual Studio]
- offline install [Visual Studio]
- layout [Visual Studio]
ms.assetid: f8625d5e-f6ea-4db0-83c0-619b77fab3cf
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: b10fc1adbb0b4a6e053549749ea90acf3919d0c6
ms.sourcegitcommit: 674d3fafa7c9e0cb0d1338027ef419a49c028c36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2021
ms.locfileid: "112602204"
---
# <a name="create-an-offline-installation-of-visual-studio"></a>Criar uma instalação offline do Visual Studio

::: moniker range="vs-2017"

Projetamos o Visual Studio 2017 para funcionar bem em uma variedade de configurações de rede e do computador. Embora seja recomendável que você experimente o [instalador do Visual Studio Web](https://visualstudio.microsoft.com/vs/older-downloads) &mdash; , que é um arquivo pequeno que permite que você se mantenha atualizado com todas as correções e recursos mais recentes &mdash; , entendemos que talvez você não consiga fazê-lo.

::: moniker-end

::: moniker range=">=vs-2019"

Criamos o Visual Studio 2019 e posteriores para funcionar bem em várias configurações de rede e de computador. Embora seja recomendável que você experimente o [instalador do Visual Studio Web](https://visualstudio.microsoft.com/downloads) &mdash; , que é um arquivo pequeno que permite que você se mantenha atualizado com todas as correções e recursos mais recentes &mdash; , entendemos que talvez você não consiga fazê-lo.

::: moniker-end

Por exemplo, você pode ter uma conexão com a Internet não confiável ou que tem largura de banda baixa. Se esse for o caso, você terá algumas opções: você poderá usar o recurso "Baixar tudo, depois instalar" para baixar os arquivos antes de instalar, ou você poderá usar a linha de comando para criar um cache local dos arquivos.

> [!NOTE]
> Se você for um administrador de empresas que deseja executar uma implantação do Visual Studio em uma rede de estações de trabalho cliente protegidas da Internet por firewall, confira nossas páginas [Criar uma instalação de rede do Visual Studio](../install/create-a-network-installation-of-visual-studio.md) e [Instalar os certificados necessários para a instalação offline do Visual Studio](../install/install-certificates-for-visual-studio-offline.md).

## <a name="use-the-download-all-then-install-feature"></a>Usar o recurso "baixar tudo, depois instalar"

::: moniker range="vs-2017"

[**Novidade na versão 15,8**](/visualstudio/releasenotes/vs2017-relnotes-v15.8#install): depois de baixar o instalador da Web, selecione a opção **baixar tudo e instalar** no instalador do Visual Studio. Em seguida, continue com a instalação.

   ![A opção "Baixar tudo, depois instalar"](media/download-all-then-install.png)

::: moniker-end

::: moniker range=">=vs-2019"

Depois de baixar o instalador da Web, selecione a nova opção **Baixar tudo, depois instalar** do Instalador do Visual Studio. Em seguida, continue com a instalação.

   ![A opção "Baixar tudo, depois instalar"](media/vs-2019/download-all-then-install-from-installer.png)

::: moniker-end

Criamos o recurso "Baixar tudo, depois instalar" para que você possa baixar o Visual Studio como uma instalação única, no mesmo computador em que você o baixar. Dessa maneira, você pode se desconectar com segurança da Web antes de instalar o Visual Studio.

> [!IMPORTANT]
> Não use o recurso "Baixar tudo, depois instalar" para criar um cache offline, que você pretende transferir para outro computador. Ele não foi desenvolvido para funcionar dessa maneira. <br><br>Se você quiser criar um cache offline no computador local que você pode usar para instalar o Visual Studio, consulte a seção [usar a linha de comando para criar um cache local](#use-the-command-line-to-create-a-local-cache) abaixo.  Como alternativa, a página [criar uma instalação de rede do Visual Studio](../install/create-a-network-installation-of-visual-studio.md) fornece informações sobre como criar um cache na rede.

## <a name="use-the-command-line-to-create-a-local-cache"></a>Use a linha de comando para criar um cache local
::: moniker range="vs-2017"

Depois de baixar um bootstrapper pequeno, use a linha de comando para criar um cache local. Em seguida, use o cache local para instalar o Visual Studio. (Esse processo substitui os arquivos ISO que estavam disponíveis para versões anteriores). 

::: moniker-end

::: moniker range=">=vs-2019"

Depois de baixar um arquivo bootstrapper pequeno, use a linha de comando para criar um cache local. Em seguida, use o cache local para instalar o Visual Studio.

::: moniker-end

### <a name="step-1---download-the-visual-studio-bootstrapper"></a>Etapa 1 – Baixar o bootstrapper do Visual Studio

Você deve ter uma conexão com a Internet para concluir esta etapa.

::: moniker range="vs-2017"

Para obter o bootstrapper mais recente para o Visual Studio 2017 versão 15,9, vá para a página [versões anteriores do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) e baixe um dos seguintes arquivos bootstrapper:

| Edition                                      | Nome de arquivo            |
|----------------------------------------------|---------------------|
| Visual Studio Professional 2017 versão 15,9 | vs_professional.exe |
| Visual Studio Enterprise 2017 versão 15,9   | vs_enterprise.exe   |
| Ferramentas de Build do Visual Studio 2017 versão 15,9  | vs_buildtools.exe   |

::: moniker-end

::: moniker range="vs-2019"

Comece baixando o bootstrapper do Visual Studio 2019 da [página de downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) ou da página de [versões do Visual Studio 2019](/visualstudio/releases/2019/history#installing-an-earlier-release) para a versão escolhida e a edição do Visual Studio. O seu arquivo de instalação &mdash; ou bootstrapper &mdash; será compatível ou ser semelhante a um dos seguintes:

| Edition                         | Arquivo                                                                                                                                                                                                                               |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Studio 2019 Community    | [vs_community.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)       |
| Visual Studio 2019 Professional | [vs_professional.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019) |
| Visual Studio 2019 Enterprise   | [vs_enterprise.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)     |
| Ferramentas de Build do Visual Studio 2019  | [vs_buildtools.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)     |

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
> Versões lançadas do Visual Studio 2022 ainda não estão disponíveis, os bootstrappers abaixo são para a versão de visualização do Visual Studio 2022.
>Comece baixando o bootstrapper do Visual Studio 2022 da [página de downloads do Visual Studio](https://aka.ms/vs2022preview).

| Edition                         | Baixar                                                            |
|---------------------------------|---------------------------------------------------------------------|
| Visual Studio 2022 Professional | [vs_professional.exe](https://aka.ms/vs/17/pre/vs_professional.exe) |
| Visual Studio 2022 Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/pre/vs_enterprise.exe)     |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>Se você tiver baixado um arquivo bootstrapper anteriormente e quiser verificar qual é a versão dele, veja como fazer isso. No Windows, abra o explorador de arquivos, clique com o botão direito do mouse no arquivo bootstrapper, escolha **Propriedades**, escolha a guia **detalhes** e, em seguida, exiba o número de **versão do produto** . Para corresponder esse número a uma versão do Visual Studio, consulte a página [números de compilação e datas de lançamento do Visual Studio](/visual-studio-build-numbers-and-release-dates.md) .

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>Se você tiver baixado anteriormente um arquivo bootstrapper e quiser verificar sua versão, veja como fazer isso. No Windows, abra o explorador de arquivos, clique com o botão direito do mouse no arquivo bootstrapper, escolha **Propriedades**, escolha a guia **detalhes** e, em seguida, exiba o número de **versão do produto** . Para corresponder esse número a uma versão do Visual Studio, consulte a página de [versões do visual studio 2019](/visualstudio/releases/2019/history) .

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>Se você tiver baixado anteriormente um arquivo bootstrapper e quiser verificar sua versão, veja como fazer isso. No Windows, abra o explorador de arquivos, clique com o botão direito do mouse no arquivo bootstrapper, escolha **Propriedades**, escolha a guia **detalhes** e, em seguida, exiba o número de **versão do produto** . Para corresponder esse número a uma versão do Visual Studio, consulte a página de [versões do visual studio 2022](/visualstudio/releases/2022/history) .

::: moniker-end

### <a name="step-2---create-a-local-install-cache"></a>Etapa 2 – Criar um cache local de instalação

Você deve ter uma conexão com a Internet para concluir esta etapa.

Abra um prompt de comando e use os parâmetros do bootstrapper, conforme definido na página [usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md) , para criar o cache de instalação local. Exemplos comuns usando o bootstrapper corporativo estão ilustrados abaixo e na página [exemplos de parâmetro de linha de comando](command-line-parameter-examples.md) . Você pode instalar um idioma diferente do inglês alterando `en-US` para uma localidade na [lista de localidades de idioma](#list-of-language-locales)e pode usar a [lista de componentes e cargas de trabalho](workload-and-component-ids.md) para personalizar ainda mais seu cache.

> [!TIP]
> Para evitar erro, certifique-se de que seu caminho de instalação completo seja menor do que 80 caracteres.

- Para .NET Web e desenvolvimento de área de trabalho do .NET, execute:

   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
    ```

- Para a área de trabalho do .NET e o desenvolvimento do Office, execute:

   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.Office --includeOptional --lang en-US
    ```

- Para desenvolvimento do C++ da área de trabalho, execute:

   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --lang en-US
    ```

- Para criar um layout local completo, somente em inglês, com todos os recursos (isso levará muito tempo, &mdash; temos _muitos_ recursos!), execute:

   ```shell
    vs_enterprise.exe --layout c:\vslayout --lang en-US
    ```

::: moniker range="vs-2017"

   > [!NOTE]
   > Um layout completo do Visual Studio exige no mínimo 35 GB de espaço em disco. Para obter mais informações, consulte [requisitos do sistema](/visualstudio/productinfo/vs2017-system-requirements-vs/). 

::: moniker-end

::: moniker range=">=vs-2019"

   > [!NOTE]
   > Um layout completo do Visual Studio requer um mínimo de 41 GB de espaço em disco. Para obter mais informações, consulte [requisitos do sistema](/visualstudio/releases/2019/system-requirements/).

::: moniker-end


### <a name="step-3---install-visual-studio-from-the-local-cache"></a>Etapa 3 – Instalar o Visual Studio do cache local
Quando você instala o Visual Studio de um cache de instalação local, o instalador do Visual Studio usa as versões armazenadas em cache local dos arquivos. Mas, se você selecionar componentes durante a instalação que não estão no cache, o instalador do Visual Studio tentará baixá-los da Internet. Para certificar-se de instalar apenas os arquivos que você baixou anteriormente, use as mesmas [Opções de linha de comando](use-command-line-parameters-to-install-visual-studio.md) que você usou para criar o cache de layout. 

Por exemplo, se você criou um cache de instalação local com o seguinte comando:

```shell
vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
```

Depois use este comando para executar a instalação:

```shell
c:\vslayout\vs_enterprise.exe --noweb --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional
```

> [!IMPORTANT]
> Se você estiver usando o Visual Studio Community, deverá ativá-lo fazendo logon no produto dentro de 30 dias após a instalação. A ativação requer uma conexão com a Internet.

> [!NOTE]
> Se você receber um erro de que uma assinatura é inválida, deverá [instalar certificados atualizados](install-certificates-for-visual-studio-offline.md). Abra a pasta Certificados no cache offline. Clique duas vezes em cada um dos arquivos de certificado e, em seguida, clique no assistente do Gerenciador de Certificados. Se for solicitado que você forneça uma senha, deixe-a em branco.

::: moniker range=">=vs-2019"
> [!TIP]
> Para instalações offline, se você receber uma mensagem de erro dizendo "um produto correspondente aos seguintes parâmetros não pode ser encontrado", certifique-se de estar usando a `--noweb` opção com a versão 16.3.5 ou posterior.

::: moniker-end

### <a name="list-of-language-locales"></a>Lista de localidades de idioma

| **Localidade de idioma** | **Idioma**          |
|---------------------|-----------------------|
| cs-CZ               | Tcheco                 |
| de-DE               | Alemão                |
| en-US               | Inglês               |
| es-ES               | Espanhol               |
| fr-FR               | Francês                |
| it-IT               | Italiano               |
| ja-JP               | Japonês              |
| ko-KR               | Coreano                |
| pl-PL               | Polonês                |
| pt-BR               | Português - Brasil   |
| ru-RU               | Russo               |
| tr-TR               | Turco               |
| zh-CN               | Chinês - Simplificado  |
| zh-TW               | Chinês - Tradicional |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

- [Criar uma instalação de rede do Visual Studio](../install/create-a-network-installation-of-visual-studio.md)
- [Atualizar uma instalação em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)
- [Instalar os certificados necessários para instalação offline do Visual Studio](../install/install-certificates-for-visual-studio-offline.md)
- [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
- [IDs de carga de trabalho e de componente do Visual Studio](workload-and-component-ids.md)
