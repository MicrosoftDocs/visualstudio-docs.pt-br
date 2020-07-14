---
title: Importar ou exportar configurações de instalação
titleSuffix: ''
description: Saiba como exportar sua configuração de instalação para um arquivo .vsconfig para compartilhar com outras pessoas e como importá-lo para clonar.
ms.date: 05/18/2019
ms.topic: how-to
f1_keywords:
- vs.about
helpviewer_keywords:
- import installation configuration
- export installation configuration
- install Visual Studio
- Visual Studio installer
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 4dcad21ce0a77e18bed0b077f731a509916e9e63
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418815"
---
# <a name="import-or-export-installation-configurations"></a>Importar ou exportar configurações de instalação

Você pode configurar o Visual Studio em sua organização usando arquivos de configuração de instalação. Para fazer isso, basta exportar as informações de componente e da carga de trabalho para um arquivo .vsconfig usando o instalador do Visual Studio. Em seguida, você pode importar a configuração em instalações novas ou existentes e compartilhá-la com outras pessoas.

Veja como.

::: moniker range="vs-2017"

> [!NOTE]
> Essa funcionalidade está disponível apenas no Visual Studio 2017 versão 15.9 e posteriores.

::: moniker-end

## <a name="export-a-configuration"></a>Exportar uma configuração

Você pode optar por exportar um arquivo de configuração de instalação de uma instância instalada anteriormente do Visual Studio ou de uma que você está instalando.

1. Abra o Instalador do Visual Studio.

1. No cartão do produto, escolha o botão **Mais** e selecione **Exportar configuração**.

   ![Exportar configuração do cartão de produto no instalador do Visual Studio](../install/media/vs-2019/vs-installer-export-config.png)

1. Procure ou digite o local no qual deseja salvar seu arquivo .vsconfig e, em seguida, escolha **Examinar detalhes**.

   ![Exportar a configuração do instalador do Visual Studio](../install/media/vs-2019/export-configuration-confirmation.png)

1. Verifique se você tem as cargas de trabalho e os componentes que deseja, e escolha **Exportar**.

## <a name="import-a-configuration"></a>Importar uma configuração

Quando estiver pronto para importar um arquivo de configuração de instalação, siga estas etapas.

1. Abra o Instalador do Visual Studio.

1. No cartão do produto, escolha o botão **Mais** e selecione **Importar configuração**.

1. Localize o arquivo .vsconfig que você deseja importar e, em seguida, escolha **Examinar detalhes**.

1. Verifique se você tem as cargas de trabalho e os componentes que deseja e escolha **Fechar**.

::: moniker range="vs-2019"

## <a name="automatically-install-missing-components"></a>Instalar automaticamente os componentes ausentes

**Novo no Visual Studio 2019**: quando você salva um arquivo. vsconfig no diretório raiz da solução e, em seguida, abre uma solução, o Visual Studio detecta automaticamente quais componentes estão ausentes e solicita que você os instale.

![O Gerenciador de Soluções sugere os componentes adicionais](../install/media/vs-2019/solution-explorer-config-file.png)

Você também pode gerar um arquivo .vsconfig diretamente no Gerenciador de Soluções.

1. Clique com botão direito do mouse no seu arquivo de solução.

1. Escolha **Adicionar** > **Arquivo de configuração de instalação**.

1. Confirme o local no qual deseja salvar o arquivo .vsconfig e escolha **Revisar detalhes**.

1. Verifique se você tem as cargas de trabalho e os componentes que deseja, e escolha **Exportar**.

::: moniker-end

> [!NOTE]
> Confira mais informações na postagem do blog [Configurar o Visual Studio em sua organização com .vsconfig](https://devblogs.microsoft.com/setup/configure-visual-studio-across-your-organization-with-vsconfig/).

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Veja também

* [Criar uma instalação de rede do Visual Studio](create-a-network-installation-of-visual-studio.md)
* [Atualizar uma instalação em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)
* [Controlar atualizações de implantações do Visual Studio](controlling-updates-to-visual-studio-deployments.md)
* [Definir padrões para implantações empresariais](set-defaults-for-enterprise-deployments.md)
