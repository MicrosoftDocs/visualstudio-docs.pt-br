---
title: Guia do administrador do Visual Studio
titleSuffix: ''
description: Saiba mais sobre como implantar o Visual Studio em um ambiente corporativo.
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: overview
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: ba41c545c2af2e0490ef0410fde7849706123940
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306703"
---
# <a name="visual-studio-administrator-guide"></a>Guia do administrador do Visual Studio

Em ambientes empresariais, os administradores do sistema normalmente implantam instalações para usuários finais de um compartilhamento de rede ou usando software de gerenciamento de sistemas. Projetamos o mecanismo de instalação do Visual Studio para dar suporte à implantação corporativa, dando aos administradores de sistema a capacidade de criar um local de instalação de rede, pré-configurar padrões de instalação, implantar chaves de produto durante o processo de instalação e gerenciar atualizações de produto depois de uma implementação com êxito.

Este guia do administrador fornece orientações com base em cenários para implantações corporativas em ambientes de rede.

## <a name="before-you-begin"></a>Antes de começar

Antes de implantar o Visual Studio em sua organização, há algumas decisões a serem tomadas e tarefas a concluir:

::: moniker range=">=vs-2019"

* Verifique se cada computador de destino atende aos [requisitos mínimos de instalação](/visualstudio/releases/2019/system-requirements/).

::: moniker-end

::: moniker range="vs-2017"

* Verifique se cada computador de destino atende aos [requisitos mínimos de instalação](/visualstudio/productinfo/vs2017-system-requirements-vs/).

::: moniker-end

* Decida sobre suas necessidades de manutenção.

  Se sua empresa precisa ficar em um conjunto de recursos por mais tempo, mas ainda deseja atualizações de manutenção regulares, você deve planejar usar uma linha de base de manutenção. Para obter mais informações, consulte a seção Opções de suporte para clientes Enterprise e ***Professional*** da página ciclo de vida e manutenção do produto do [Visual Studio,](/visualstudio/releases/2019/servicing#support-options-for-enterprise-and-professional-customers) bem como a página Atualizar [Visual Studio](update-servicing-baseline.md) em uma página de linha de base de serviço.

* Escolha o modelo de atualização.

  De onde você deseja que os máquinas cliente individuais recebam as atualizações do produto? Especificamente, decida se deseja que o cliente receba atualizações da Internet ou de um compartilhamento local de toda a empresa. Em seguida, se você escolheu usar um compartilhamento local, decida se os usuários individuais podem atualizar seus próprios clientes ou se você deseja que um administrador atualize os clientes por meio de programação. É melhor se essas decisões foram tomadas antes que a instalação original ocorra no computador cliente. Para obter mais informações, consulte [Criar uma instalação baseada em rede do Visual Studio](../install/create-a-network-installation-of-visual-studio.md).

  É possível atualizar um layout de instalação de rede do Visual Studio com as atualizações mais recentes do produto para que ele possa ser usado como um ponto de instalação para a atualização mais recente do Visual Studio e também para manter instalações que já estão implantadas nas estações de trabalho cliente. Para obter mais informações, [consulte Atualizar uma instalação baseada em rede do Visual Studio](../install/update-a-network-installation-of-visual-studio.md).

  As organizações que utilizam ferramentas de implantação empresarial podem aproveitar o fato de que Visual Studio atualizações estão disponíveis no catálogo Microsoft Update e Windows Server Update Services. Para obter mais informações, consulte [Habilitando atualizações de administrador](../install/enabling-administrator-updates.md) [e Aplicando atualizações de administrador.](../install/applying-administrator-updates.md)

  Para computadores que não estão conectados à Internet, a criação de um layout mínimo é a maneira mais fácil e rápida de atualizar suas instâncias Visual Studio offline. Para obter mais informações, consulte [Atualizar Visual Studio usando um layout offline mínimo.](update-minimal-layout.md)

::: moniker range=">=vs-2019"

* Decida quais [cargas de trabalho e componentes](workload-and-component-ids.md?view=vs-2019&preserve-view=true) sua empresa necessita.

* Decida se usará um [arquivo de resposta](automated-installation-with-response-file.md?view=vs-2019&preserve-view=true) (que simplifica o gerenciamento detalhes no arquivo de script).

::: moniker-end

::: moniker range="vs-2017"

* Decida quais [cargas de trabalho e componentes](workload-and-component-ids.md?view=vs-2017&preserve-view=true) sua empresa necessita.

* Decida se usará um [arquivo de resposta](automated-installation-with-response-file.md?view=vs-2017&preserve-view=true) (que simplifica o gerenciamento detalhes no arquivo de script).

::: moniker-end

* Decida se você deseja habilitar a Política de Grupo e se deseja configurar o Visual Studio para desabilitar os comentários do cliente em computadores individuais.

::: moniker range=">=vs-2019"

## <a name="step-1---download-visual-studio-product-files"></a>Etapa 1 – baixar os arquivos de produto do Visual Studio

* [Selecione as cargas de trabalho e os componentes](workload-and-component-ids.md?view=vs-2019&preserve-view=true) que deseja instalar.

* [Crie um compartilhamento de rede para os arquivos de produto do Visual Studio](create-a-network-installation-of-visual-studio.md?view=vs-2019&preserve-view=true).

## <a name="step-2---build-an-installation-script"></a>Etapa 2 – criar um script de instalação

* Compile um script de instalação que use [parâmetros de linha de comando](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019&preserve-view=true) para controlar a instalação.

  >[!NOTE]
  > Você pode simplificar scripts usando um [arquivo de resposta](automated-installation-with-response-file.md?view=vs-2019&preserve-view=true). É preciso que você crie um arquivo de resposta que contenha sua opção de instalação padrão.

* (Opcional) [Aplique uma chave do produto de licença de volume](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2019&preserve-view=true) como parte do script de instalação para que os usuários não precisem ativar o software separadamente.

* (Opcional) Atualize o layout de rede para [controlar o período e o local de origem em que as atualizações de produto serão entregues aos usuários finais](controlling-updates-to-visual-studio-deployments.md?view=vs-2019&preserve-view=true).

* (Opcional) Defina políticas de registro que afetam a implantação do Visual Studio, como onde alguns pacotes compartilhados com outras versões ou instâncias são instalados, [onde os pacotes são armazenados em cache](set-defaults-for-enterprise-deployments.md?view=vs-2019&preserve-view=true) ou [se os pacotes são armazenados em cache](disable-or-move-the-package-cache.md?view=vs-2019&preserve-view=true).

* (Opcional) Defina a Política de Grupo. Você também pode [configurar o Visual Studio para desabilitar os comentários do cliente](../ide/visual-studio-experience-improvement-program.md) em computadores individuais.

## <a name="step-3---deploy-updates"></a>Etapa 3 – Implantar atualizações

Use a tecnologia de implantação de sua escolha para executar o script nas estações de trabalho do desenvolvedor de destino.

* [Atualize seu local de rede com as atualizações mais recentes](update-a-network-installation-of-visual-studio.md?view=vs-2019&preserve-view=true) do Visual Studio ao executar o comando usado na etapa 1 regularmente para adicionar componentes atualizados.

  Você pode atualizar o Visual Studio usando um script de atualização. Para fazer isso, use o [`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019&preserve-view=true) parâmetro de linha de comando.

  Você pode implantar Visual Studio do Windows Server Update Services ou do catálogo Microsoft Update com ferramentas como System Center Gerenciador de Configurações.  Consulte [Aplicando atualizações de administrador para](applying-administrator-updates.md) obter mais informações. 

## <a name="step-4---optional-use-visual-studio-tools-to-verify-installation"></a>Etapa 4 – (Opcional) Usar ferramentas Visual Studio para verificar a instalação

Temos várias ferramentas disponíveis para ajudar você a [detectar e gerenciar instâncias do Visual Studio instaladas](tools-for-managing-visual-studio-instances.md?view=vs-2019&preserve-view=true) em computadores cliente.

## <a name="advanced-configuration"></a>Configuração avançada

Por padrão, a instalação Visual Studio habilita a inclusão de tipo personalizado em pesquisas do Bing na lista de erros F1 e links de código. Você pode configurar o Visual Studio para desabilitar o mecanismo de pesquisa de incluir qualquer tipo de usuário personalizado alterando o valor da seguinte chave do Registro por política:

**"PutCustomTypeInBingSearch" DWORD 0**

O registro está localizado no diretório *Software\Microsoft\VisualStudio\16.0_{InstanceId}\Roslyn\Internal\Diagnostics do hive do registro \* privado. Para obter instruções sobre como abrir o hive do Registro, consulte [editando](tools-for-managing-visual-studio-instances.md?view=vs-2019&preserve-view=true#editing-the-registry-for-a-visual-studio-instance)o registro para uma instância Visual Studio .

::: moniker-end

::: moniker range="vs-2017"

## <a name="step-1---download-visual-studio-product-files"></a>Etapa 1 – baixar os arquivos de produto do Visual Studio

* [Selecione as cargas de trabalho e os componentes](workload-and-component-ids.md?view=vs-2017&preserve-view=true) que deseja instalar.

* [Crie um compartilhamento de rede para os arquivos de produto do Visual Studio](create-a-network-installation-of-visual-studio.md?view=vs-2017&preserve-view=true).

## <a name="step-2---build-an-installation-script"></a>Etapa 2 – criar um script de instalação

* Compile um script de instalação que use [parâmetros de linha de comando](use-command-line-parameters-to-install-visual-studio.md?view=vs-2017&preserve-view=true) para controlar a instalação.

  >[!NOTE]
  > Você pode simplificar scripts usando um [arquivo de resposta](automated-installation-with-response-file.md?view=vs-2017&preserve-view=true). É preciso que você crie um arquivo de resposta que contenha sua opção de instalação padrão.

* (Opcional) [Aplique uma chave do produto de licença de volume](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2017&preserve-view=true) como parte do script de instalação para que os usuários não precisem ativar o software separadamente.

* (Opcional) Atualize o layout de rede para [controlar o período e o local de origem em que as atualizações de produto serão entregues aos usuários finais](controlling-updates-to-visual-studio-deployments.md?view=vs-2017&preserve-view=true).

* (Opcional) Defina políticas de registro que afetam a implantação do Visual Studio, como onde alguns pacotes compartilhados com outras versões ou instâncias são instalados, [onde os pacotes são armazenados em cache](set-defaults-for-enterprise-deployments.md?view=vs-2019&preserve-view=true) ou [se os pacotes são armazenados em cache](disable-or-move-the-package-cache.md?view=vs-2017&preserve-view=true).

* (Opcional) Defina a Política de Grupo. Você também pode [configurar o Visual Studio para desabilitar os comentários do cliente](../ide/visual-studio-experience-improvement-program.md) em computadores individuais.

## <a name="step-3---deploy-updates"></a>Etapa 3 – Implantar atualizações

Use a tecnologia de implantação de sua escolha para executar o script nas estações de trabalho do desenvolvedor de destino.

* [Atualize seu local de rede com as atualizações mais recentes](update-a-network-installation-of-visual-studio.md?view=vs-2017&preserve-view=true) do Visual Studio ao executar o comando usado na etapa 1 regularmente para adicionar componentes atualizados.

  Você pode atualizar o Visual Studio usando um script de atualização. Para fazer isso, use o [`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019&preserve-view=true) parâmetro de linha de comando.

  Você pode implantar Visual Studio do Windows Server Update Services ou do catálogo Microsoft Update com ferramentas como System Center Gerenciador de Configurações. Para obter mais informações, [consulte Aplicando atualizações de administrador.](applying-administrator-updates.md)

## <a name="step-4---optional-use-visual-studio-tools-to-verify-installation"></a>Etapa 4 – (Opcional) Usar ferramentas Visual Studio para verificar a instalação

Temos várias ferramentas disponíveis para ajudar você a [detectar e gerenciar instâncias do Visual Studio instaladas](tools-for-managing-visual-studio-instances.md?view=vs-2017&preserve-view=true) em computadores cliente.

## <a name="advanced-configuration"></a>Configuração avançada

Por padrão, a instalação Visual Studio habilita a inclusão de tipo personalizado em pesquisas do Bing na lista de erros F1 e links de código. Você pode configurar o Visual Studio para desabilitar o mecanismo de pesquisa de incluir qualquer tipo de usuário personalizado alterando o valor da seguinte chave do Registro por política:

**"PutCustomTypeInBingSearch" DWORD 0**

O registro está localizado no `Software\Microsoft\VisualStudio\15.0_{InstanceId}\Roslyn\Internal\Diagnostics\` diretório do hive do registro privado. Para obter instruções sobre como abrir o hive do Registro, consulte [editando](tools-for-managing-visual-studio-instances.md?view=vs-2017&preserve-view=true#editing-the-registry-for-a-visual-studio-instance)o registro para uma instância Visual Studio .

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Habilitando atualizações de administrador](enabling-administrator-updates.md)
* [Aplicando atualizações de administrador](applying-administrator-updates.md)
* [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md)
* [Instalar os certificados necessários para instalação offline do Visual Studio](install-certificates-for-visual-studio-offline.md)
* [Importar ou exportar configurações de instalação](import-export-installation-configurations.md)
* [Arquivos de instalação do Visual Studio](https://devblogs.microsoft.com/setup/tag/vs2017/)
* [Visual Studio ciclo de vida e manutenção do produto](/visualstudio/releases/2019/servicing/)
* [Configurações de carregamento automático síncrono](../extensibility/synchronously-autoloaded-extensions.md)
