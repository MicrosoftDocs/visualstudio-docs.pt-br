---
title: Instalar agentes e controladores de teste
ms.date: 04/17/2019
ms.topic: how-to
helpviewer_keywords:
- configure test agents, test lab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3c374951b4d4875e4e754035ac52afb7f8fc5a2e
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286889"
---
# <a name="install-test-agents-and-test-controllers"></a>Instalar agentes e controladores de teste

Para cenários de teste que usam o Visual Studio e o Azure Test Plans ou o TFS (Team Foundation Server), não é necessário ter um controlador de teste. O Agents para Visual Studio faz a orquestração comunicando-se com Azure Test Plans ou o TFS. Um cenário possível seria você executar testes contínuos para fluxos de trabalho de build e de lançamento no Azure Test Plans ou no TFS.

Você também pode considerar mais fácil usar [o gerenciamento de compilação ou lançamento](use-build-or-rm-instead-of-lab-management.md) em vez do gerenciamento de laboratório.

## <a name="system-requirements"></a>Requisitos do sistema

A seguinte tabela mostra os requisitos do sistema para instalação do controlador de teste ou do agente de teste para o Visual Studio:

| Item | Requisitos |
| ---- | ------------ |
| **Agente** | Windows 10<br />Windows 8, Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016 Standard e Datacenter<br />Windows Server 2012 R2 |
| **Controller** | Windows 10<br />Windows 8, Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016 Standard e Datacenter<br />Windows Server 2012 R2 |
| **.NET Framework** | .NET Framework 4.5 |

## <a name="install-the-test-controller-and-test-agents"></a>Instalar o controlador de teste e agentes de teste

Baixe agentes para o Visual Studio em [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/?q=agents). Procure *Agents para Visual Studio 2019* e selecione *Agente* ou *Controlador*, depois escolha *Download*. Execute o arquivo executável baixado para instalar o agente ou o controlador de teste.

Você pode baixar agentes para Visual Studio 2017, Visual Studio 2015 e Visual Studio 2013 pela página [downloads mais antigos](https://visualstudio.microsoft.com/vs/older-downloads/).

Esses instaladores estão disponíveis como arquivos ISO para a instalação fácil em máquinas virtuais.

::: moniker range="vs-2017"
## <a name="compatible-versions-of-tfs-microsoft-test-manager-the-test-controller-and-test-agent"></a>Versões compatíveis do TFS, do Microsoft Test Manager, do controlador de teste e do agente de teste

Você pode combinar versões diferentes do TFS, o Microsoft Test Manager, o controlador de teste e o agente de teste, conforme a tabela a seguir:

| TFS | Microsoft Test Manager com Central de Laboratório | Controller | Agente |
| --- | -------------------------------------- | ---------- | ----- |
| 2017: atualizar do 2015 ou nova instalação | 2017 | 2017 | 2017 |
| 2017: atualizar do 2015 ou nova instalação | 2017 | 2013 Atualização 5 | 2013 Atualização 5 |
| 2017: atualizar do 2015 ou nova instalação | 2015 | 2013 Atualização 5 | 2013 Atualização 5 |
| 2015: atualizar do 2013 | 2013 | 2013 |2013 |
| 2015: nova instalação | 2013 | 2013 | 2013 |
| 2015: atualizar do 2013 ou nova instalação | 2015 | 2013 | 2013 |
| 2013 | 2015 | 2013 | 2013 |
::: moniker-end

::: moniker range=">=vs-2019"
## <a name="compatible-versions-of-tfs-the-test-controller-and-test-agent"></a>Versões compatíveis do TFS, do controlador de teste e do agente de teste

Você pode misturar versões diferentes do TFS, do controlador de teste e do agente de teste, de acordo com a tabela a seguir:

| TFS | Controller | Agente |
| --- | -------------------------------------- | ---------- | ----- |
| 2017: atualizar do 2015 ou nova instalação | 2017 | 2017 |
| 2017: atualizar do 2015 ou nova instalação | 2013 Atualização 5 | 2013 Atualização 5 |
| 2017: atualizar do 2015 ou nova instalação | 2013 Atualização 5 | 2013 Atualização 5 |
| 2015: atualizar do 2013 | 2013 |2013 |
| 2015: nova instalação | 2013 | 2013 |
| 2015: atualizar do 2013 ou nova instalação | 2013 | 2013 |
| 2013 | 2013 | 2013 |
::: moniker-end

> [!NOTE]
> Os cenários do Lab Management no TFS 2018 e no Azure DevOps Services foram preteridos. Para obter mais informações, confira [Notas sobre a versão do TFS 2018](/visualstudio/releasenotes/tfs2018-relnotes#--removing-support-for-lab-center-and-automated-testing-flows-in-microsoft-test-manager).

## <a name="upgrade-from-visual-studio-2013-test-agents"></a>Atualizar de agentes de teste do Visual Studio 2013

É recomendável que você use agentes para Visual Studio em todos os novos cenários de teste automatizado. Você pode usar a tarefa de *Implantar Agentes de Teste* em um pipeline de build para baixar e instalar os agentes de teste em seu computador.

A tabela a seguir mostra os cenários com suporte do Agents para Visual Studio 2013 e as alternativas para o TFS (Team Foundation Server) 2015 e o Azure Test Plans:

| Cenários com suporte pelo Agents para Visual Studio 2013 | Alternativa no TFS e no Azure Test Plans |
| - | - |
| Fluxo de trabalho compilar-implantar-testar no Visual Studio | Os usuários podem usar um [pipeline de build](/azure/devops/pipelines/index?view=vsts) (não um build XAML) para compilar, implantar e testar os cenários no TFS. |
| Teste de carga (teste de desempenho) usando computadores remotos locais | Use o Test Controller e o Test Agents 2013 Atualização 5 para executar os testes de carga locais. |
| Execução remota de testes automatizados de Microsoft Test Manager (preterido no Visual Studio 2017) usando um ambiente de laboratório | Atualmente não há nenhuma alternativa para esse cenário. Recomendamos que você use a tarefa Executar Testes Funcionais nas definições de build e versão (não em um build XAML) para executar testes remotamente. |
| Desenvolvedores executando testes remotos no Visual Studio | Não tem mais suporte. |
