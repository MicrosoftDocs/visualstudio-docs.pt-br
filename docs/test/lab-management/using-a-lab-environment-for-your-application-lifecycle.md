---
title: Usar um ambiente de laboratório para DevOps
description: Saiba mais sobre os ambientes de laboratório e como usar a nuvem com Azure Pipelines ou Team Foundation Server compilação e versão.
ms.custom: SEO-VS-2020
ms.date: 05/02/2017
ms.topic: how-to
helpviewer_keywords:
- lab environment, test lab
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: a16b8df2539272f96f0211fdf08e32fe4e4eaac8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887816"
---
# <a name="use-a-lab-environment-for-your-devops"></a>Usar um ambiente de laboratório para suas operações de desenvolvimento

Um ambiente de laboratório é uma coleção de computadores virtuais e físicos que você pode usar para desenvolver e testar aplicativos. Um ambiente de laboratório pode conter várias funções necessárias para testar aplicativos com camadas múltiplas, como estações de trabalho, servidores de Web e servidores de banco de dados. Além disso, você pode usar um fluxo de trabalho compilação-implantação-teste com seu ambiente de laboratório para automatizar o processo de compilação, implantação e execução de testes automatizados em seu aplicativo.

* **Usar um plano de teste para executar testes automáticos** − Você pode executar uma coleção de testes automatizados, chamados de *plano de teste* e exibir o processo usando.

* **Usar um fluxo de trabalho compilar-implantar-testar** − Você pode usar um fluxo de trabalho compilar-implantar-testar para testar aplicativos com camadas múltiplas automaticamente. Um exemplo típico é um fluxo de trabalho que começa com uma compilação, implanta os arquivos de compilação nos computadores apropriados em um ambiente de laboratório, em seguida, executa testes automáticos. Além disso, você pode programar seu fluxo de trabalho para ser executado em intervalos específicos.

* **Colecionar dados de diagnóstico de todos os computadores, até durante o teste manual** − Você pode colecionar dados de diagnóstico de vários computadores simultaneamente. Por exemplo, durante uma única execução de teste, você pode coletar IntelliTrace, impacto de teste e outras formas de dados de um servidor Web, um servidor de banco de dados e um cliente.

Aqui estão exemplos de topologias comuns de ambientes de laboratório:

| Topologia | Descrição |
|---|---|
|![Topologia apenas do servidor](../media/topology_backend.png)| Este ambiente de laboratório tem uma *topologia de servidor*, frequentemente usada para executar testes manuais em aplicativos de servidor e permite que os testadores usem seus próprios computadores cliente para verificar bugs no ambiente. Em uma topologia back-end, seu ambiente de laboratório contém apenas servidores. Ao usar esse tipo de topologia, geralmente você se conecta aos servidores no ambiente de laboratório usando um computador cliente que não é parte dele.|
|![Ambiente de laboratório de nuvem](../media/topology_cloud.png)| Esse ambiente de laboratório fornece funcionalidades e recursos semelhantes que a _topologia de rede_, mas remove a necessidade de máquinas virtuais ou computadores físicos em execução em um ambiente local, o que pode reduzir o tempo de configuração, simplificar a manutenção e minimizar o custo. Configurar vários sites e máquinas virtuais, junto o serviço de rede personalizado, é rápido e fácil em um ambiente de nuvem como o Microsoft Azure.|
|![Ambiente de laboratório de cliente-servidor](../media/topology_clientserver.png)| Este ambiente de laboratório te uma *topologia cliente/servidor*, frequentemente usada para testar um aplicativo com componentes de servidor e de cliente. Em uma topologia cliente/servidor, todos os computadores cliente e servidor usados para testar seu aplicativo estão em seu ambiente de laboratório. Quando você usa essa topologia, pode coletar dados de teste de cada computador que impacta seus testes.|

:::row:::
    :::column:::
        ![ícone de câmera para vídeo](../../install/media/video-icon.png)
    :::column-end:::
    :::column:::
        [Assistir a um vídeo](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Managing-lab-environments-for-testing) sobre como gerenciar ambientes de laboratório para teste.
    :::column-end:::
:::row-end:::

## <a name="use-the-cloud-with-azure-pipelines-or-team-foundation-server-build-and-release"></a>Usar a nuvem com o Azure Pipelines ou o Team Foundation Server Build and Release

Você pode executar testes automatizados e a automação de compilar-implantar-testar usando as funcionalidades de [compilação e lançamento](/azure/devops/pipelines/index?view=vsts&preserve-view=true) do TFS (Team Foundation Server) e do Azure Test Plans. Alguns dos benefícios são:

* Não é necessário ter um Controlador de Build ou um Controlador de Teste.
* O Agente de Teste é instalado por meio de uma tarefa como parte do build ou da versão.
* É fácil personalizar as etapas de implantação. Você não está mais restrito a usar um único script. Você também pode aproveitar as várias tarefas que estão disponíveis no produto, bem como no Visual Studio Marketplace.
* Você não precisa manter conjuntos de testes. Você pode executar os testes diretamente dos binários.
* Você obtém uma experiência de relatório embutido avançada para os testes executados dentro de cada build ou versão.
* Você pode controlar quais ativos (versão, build, itens de trabalho, confirmações) atualmente estão implantadas e testadas em cada ambiente.
* Você pode personalizar e estender a automação para implantar facilmente em vários ambientes de teste e até mesmo na produção.
* Você pode agendar a automação para ocorrer sempre que houver um check-in ou confirmação ou em um momento específico todos os dias.

Para saber mais, veja [Use o Build ou o Release Management](use-build-or-rm-instead-of-lab-management.md).

::: moniker range="vs-2017"
## <a name="use-the-visual-studio-lab-management-features-of-microsoft-test-manager"></a>Usar os recursos do Lab Management do Visual Studio do Microsoft Test Manager

Crie e gerencie ambientes de laboratório com as funcionalidades do Lab Management do Visual Studio do Microsoft Test Manager ao usar o Visual Studio Enterprise Edition.

O Lab Management instala automaticamente agentes de teste em cada computador do seu ambiente.

Se utilizar o Lab Management junto ao System Center Virtual Machine Manager (SCVMM), você pode obter esses benefícios ao usar ambientes de laboratório:

* **Reproduzir rapidamente as configurações do computador** − Você pode armazenar as coleções das máquinas virtuais que são configuradas para recriar ambientes típicos de produção. Assim, você pode aplicar cada execução de teste em uma nova cópia de um ambiente armazenado.

* **Reproduzir as condições exatas de um bug** -quando uma execução de teste falhar, você poderá armazenar uma cópia do estado do seu ambiente de laboratório e acessá-la de seus resultados de compilação ou de um item de trabalho.

* **Executar várias cópias de um ambiente de laboratório ao mesmo tempo** – Você pode executar várias cópias de seu ambiente de laboratório ao mesmo tempo sem conflitos de nome.

### <a name="standard-environments-and-scvmm-environments"></a>Ambientes padrão e SCVMM

Há dois tipos de ambientes de laboratório que você pode criar com o Lab Management do Visual Studio: **ambientes padrão** e **ambientes do SCVMM**. Entretanto, as capacidades de cada tipo de ambiente são diferentes.

**Ambientes padrão:** podem conter uma combinação de máquinas virtuais e físicas. Você também pode adicionar máquinas virtuais em um ambiente padrão que é gerenciado por estruturas de virtualização de terceiros. Além disso, ambientes padrão não precisam de recursos de servidor adicional, como um servidor SCVMM.

**Ambientes SCVMM:** podem conter apenas computadores virtuais gerenciados pelo SCVMM (System Center Virtual Machine Manager), ou seja, as máquinas virtuais em ambientes SCVMM somente podem executar a estrutura de virtualização Hyper-V. Entretanto, ambientes SCVMM fornecem os seguintes recursos de automação e gerenciamento, que não estão disponíveis nos ambientes padrão:

- **Instantâneos do ambiente:** instantâneos de ambiente contêm o estado de um ambiente de laboratório, para que você possa restaurar rapidamente um ambiente limpo ou salvar o estado de um ambiente que foi modificado. Você também pode usar um fluxo de trabalho compilar/implantar/testar para automatizar o processo de salvar e restaurar instantâneos de ambiente.

- **Ambientes armazenados:** você pode armazenar uma cópia de um ambiente SCVMM e, em seguida, implantar várias cópias desse ambiente.

- **Isolamento de rede:** o isolamento de rede permite executar simultaneamente várias cópias idênticas de um ambiente SCVMM sem conflitos com o nome do computador.

- **Modelos de máquina virtual:** um modelo de máquina virtual é uma máquina virtual que teve seu nome e outros identificadores removidos. Quando um modelo de VM é implantado em um ambiente SCVMM, o Microsoft Test Manager gera novos identificadores. Isso permite implantar várias cópias de uma máquina virtual em um mesmo ambiente ou vários ambientes. Em seguida, executar as máquinas virtuais simultaneamente.

- **Máquinas Virtuais Armazenadas:** uma máquina virtual armazenada em sua biblioteca de projeto que inclui identificadores exclusivos.

> [!NOTE]
> O Lab Management não dá suporte ao SCVMM 2016.

Para saber mais sobre SCVMM, veja [Virtual Machine Manager](/azure/devops/pipelines/?view=vsts&preserve-view=true).

Ambientes padrão e SCVMM oferecem suporte a vários dos mesmos recursos. No entanto, há duas diferenças importantes a se considerar. A tabela a seguir compara os recursos disponíveis para ambientes padrão e SCVMM.

|Funcionalidade|Ambiente SCVMM|Ambientes padrão|
|-|------------------------|-|
|Testes.|||
|Executar testes manuais|Suportado|Suportado|
|Executar IU codificado e outros testes automáticos|Suportado|Suportado|
|Arquivo com muitos bugs usando adaptadores de diagnóstico|Suportado|Suportado|
|**Compilar implantação**|||
|Fluxos de trabalho compilar/implantar/testar automáticos|Suportado|Suportado|
|**Criação e gerenciamento de ambiente**|||
|Usar máquinas físicas, além de virtuais|Sem suporte|Suportado|
|Usar máquinas virtuais de terceiros|Sem suporte|Suportado|
|Instalar automaticamente agentes de teste em computadores com ambiente de laboratório|Suportado|Suportado|
|Salvar e implantar o estado de um ambiente de laboratório usando instantâneos de ambiente|Suportado|Sem suporte|
|Criar ambientes de laboratório a partir de modelos VM|Suportado|Sem suporte|
|Ambiente de início/parada/instantâneo|Suportado|Sem suporte|
|Conecte-se ao ambiente usando o Visualizador de Ambiente|Suportado|Suportado|
|Executa várias cópias de um ambiente ao mesmo tempo usando isolamento de rede|Suportado|Sem suporte|

### <a name="lab-management-concepts"></a>Conceitos de Lab Management

Aqui estão alguns dos conceitos adicionais com que deve familiarizar-se antes de continuar:

|Termo|Descrição|
|-|-----------------|
|Centro de laboratório|A área do Microsoft Test Manager em que você cria e gerencia ambientes de laboratório.|
|Laboratório de projeto do Azure DevOps|A coleção de ambientes de laboratório que foi configurada para que você possa conectar-se a ela e executar suas máquinas virtuais.|
|Biblioteca de projeto do Azure DevOps|Um arquivo de máquinas virtuais armazenadas, modelos e ambientes de laboratório armazenados foi importado em um grupo de hosts do seu projeto. Você pode usar os itens em sua biblioteca com ambientes SCVMM; entretanto, você não pode adicioná-los diretamente em um ambiente padrão. Você não pode executar os itens em sua biblioteca; ao invés disso, você os utiliza para implantar um novo ambiente.|
|Ambiente implantado|Um ambiente de laboratório foi implantado pelo seu laboratório de projeto para que você possa se conectar a ele e executar seus computadores.|

Para saber mais sobre o Lab Management, veja:

* [Planejar seu laboratório](/previous-versions/ff756575(v=vs.140))
* [Administrar seu laboratório](/previous-versions/dd936084(v=vs.140))
* [Configurar para ambientes SCVMM](/previous-versions/dd380687(v=vs.140))
* [Gerenciar permissões](/previous-versions/dd380760(v=vs.140))
* [Alterar a configuração](/previous-versions/ee704508(v=vs.140))
* [Solução de problemas](/previous-versions/ee853230(v=vs.140))

Para saber mais sobre como configurar ambientes, veja:

* [Ambientes de nuvem de build e de lançamento](use-build-or-rm-instead-of-lab-management.md)
* [Ambientes de laboratório padrão](/previous-versions/ee390842(v=vs.140))
* [Ambientes SCVMM (virtuais)](/previous-versions/ee943322(v=vs.140))
* [Criando e usando um ambiente de rede isolado](/previous-versions/ee518924(v=vs.140))
::: moniker-end

## <a name="see-also"></a>Confira também

* [Instalar e configurar agentes de teste](../../test/lab-management/install-configure-test-agents.md)
* [Guia do Lab Management do Visual Studio](/archive/blogs/visualstudioalmrangers/library-of-tooling-and-guidance-solutions-aka-msvsarsolutions)
* [Blog do Microsoft DevOps](https://devblogs.microsoft.com/devops/)