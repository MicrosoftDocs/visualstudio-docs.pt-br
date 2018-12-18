---
title: Instalar agentes e controladores de teste
ms.date: 10/24/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- configure test agents, test lab
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8055e1c11f38ab83ae9c3a0570064ca49158b886
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219023"
---
# <a name="install-test-agents-and-test-controllers"></a>Instalar agentes e controladores de teste

Para cenários de teste que usam o Visual Studio e o Azure Test Plans ou o TFS (Team Foundation Server), não é necessário ter um controlador de teste. O Agents para Visual Studio faz a orquestração comunicando-se com Azure Test Plans ou o TFS. Um cenário possível seria você executar testes contínuos para fluxos de trabalho de build e de lançamento no Azure Test Plans ou no TFS.

Você também pode considerar mais fácil usar [o gerenciamento de compilação ou lançamento](use-build-or-rm-instead-of-lab-management.md) em vez do gerenciamento de laboratório.

## <a name="system-requirements"></a>Requisitos do sistema

A tabela a seguir mostra os requisitos de sistema para instalar o controlador de teste ou agente de teste para o Visual Studio 2017:

| Item | Requisitos |
| ---- | ------------ |
| **Agente** | Windows 10<br />Windows 8, Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016 Standard e Datacenter<br />Windows Server 2012 R2 |
| **Controlador** | Windows 10<br />Windows 8, Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016 Standard e Datacenter<br />Windows Server 2012 R2 |
| **.NET Framework** | .NET Framework 4.5 |

## <a name="install-the-test-controller-and-test-agents"></a>Instalar o controlador de teste e agentes de teste

Você pode baixar agentes para Visual Studio 2017 em [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/?q=agents). Procure *Agents para Visual Studio 2017* e selecione *Agente* ou *Controlador*, em seguida, escolha *Download*. Execute o arquivo executável baixado para instalar o agente ou o controlador de teste.

Você pode baixar agentes para Visual Studio 2015 e Visual Studio 2013 pela página [downloads mais antigos](https://visualstudio.microsoft.com/vs/older-downloads/).

Esses instaladores estão disponíveis como arquivos ISO para a instalação fácil em máquinas virtuais.

## <a name="compatible-versions-of-tfs-microsoft-test-manager-the-test-controller-and-test-agent"></a>Versões compatíveis do TFS, do Microsoft Test Manager, do controlador de teste e do agente de teste

Você pode combinar versões diferentes do TFS, o Microsoft Test Manager, o controlador de teste e o agente de teste, conforme a tabela a seguir:

| TFS | Microsoft Test Manager com Central de Laboratório | Controlador | Agente |
| --- | -------------------------------------- | ---------- | ----- |
| 2017: atualizar do 2015 ou nova instalação | 2017 | 2017 | 2017 |
| 2017: atualizar do 2015 ou nova instalação | 2017 | 2013 Atualização 5 | 2013 Atualização 5 |
| 2017: atualizar do 2015 ou nova instalação | 2015 | 2013 Atualização 5 | 2013 Atualização 5 |
| 2015: atualizar do 2013 | 2013 | 2013 |2013 |
| 2015: nova instalação | 2013 | 2013 | 2013 |
| 2015: atualizar do 2013 ou nova instalação | 2015 | 2013 | 2013 |
| 2013 | 2015 | 2013 | 2013 |

> [!NOTE]
> Os cenários do Lab Management no TFS 2018 e no Azure DevOps Services foram preteridos. Para obter mais informações, confira [Notas sobre a versão do TFS 2018](/visualstudio/releasenotes/tfs2018-relnotes#--removing-support-for-lab-center-and-automated-testing-flows-in-microsoft-test-manager).

## <a name="upgrade-from-visual-studio-2013-test-agents"></a>Atualizar de agentes de teste do Visual Studio 2013

É recomendável que você use agentes para Visual Studio em todos os novos cenários de teste automatizado. Você pode usar a tarefa de *Implantar Agentes de Teste* em um pipeline de build para baixar e instalar os agentes de teste em seu computador.

A tabela a seguir mostra os cenários com suporte do Agents para Visual Studio 2013 e as alternativas para o TFS (Team Foundation Server) 2015 e o Azure Test Plans:

| Cenários com suporte pelo Agents para Visual Studio 2013 | Alternativa no TFS e no Azure Test Plans |
| - | - |
| Fluxo de trabalho compilar-implantar-testar no Visual Studio | Os usuários podem usar um [pipeline de build](/azure/devops/pipelines/index?view=vsts) (não um build XAML) para compilar, implantar e testar os cenários no TFS. |
| Teste de carga (teste de desempenho) usando computadores remotos locais | Use o Test Controller e o Test Agents 2013 Atualização 5 para executar os testes de carga locais. |
| Execução remota de testes automatizados do Microsoft Test Manager usando um ambiente de laboratório | Atualmente não há nenhuma alternativa para esse cenário. Recomendamos que você use a tarefa Executar Testes Funcionais nas definições de build e versão (não em um build XAML) para executar testes remotamente. |
| Desenvolvedores executando testes remotos no Visual Studio | Não há mais suporte. |
