---
title: Testando o desempenho de um serviço de nuvem | Microsoft Docs
description: Testar o desempenho de um serviço de nuvem usando o criador de perfil do Visual Studio
author: mikejo5000
manager: douge
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.topic: conceptual
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.openlocfilehash: 25b60e5e4072a0523d17082a5c5646e5bb1ade6a
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001155"
---
# <a name="testing-the-performance-of-a-cloud-service"></a>Testando o desempenho de um serviço de nuvem
## <a name="overview"></a>Visão geral
Você pode testar o desempenho de um serviço de nuvem das seguintes maneiras:

* Use o diagnóstico do Azure para coletar informações sobre solicitações e conexões e para examinar estatísticas de site que mostram o serviço de desempenho da perspectiva do cliente. Para obter uma introdução, consulte [Configurando o diagnóstico para serviços de nuvem do Azure e máquinas virtuais](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Use o criador de perfil do Visual Studio para obter uma análise detalhada dos aspectos computacionais de como o serviço é executado. Conforme descrito neste tópico, você pode usar o criador de perfil para medir o desempenho como um serviço é executado no Azure. Para obter informações sobre como usar o criador de perfil para medir o desempenho como um serviço é executado localmente em um emulador de computação, consulte [testando o desempenho de um serviço de nuvem de Azure localmente no emulador de computação usando o Visual Profiler Studio](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Escolhendo um método de teste de desempenho
### <a name="use-azure-diagnostics-to-collect"></a>Use o diagnóstico do Azure para coletar:
* Estatísticas em páginas da web ou serviços, como solicitações e conexões.
* Estatísticas sobre funções, como a frequência com que uma função é reiniciada.
* Em geral, informações sobre o uso de memória, como a porcentagem de tempo que leva o coletor de lixo ou a memória conjunto de uma função em execução.

### <a name="use-the-visual-studio-profiler-to"></a>Use o criador de perfil do Visual Studio para:
* Determine quais funções demoram mais.
* Medir quanto tempo leva cada parte de um programa de computação intensivo.
* Compare relatórios de desempenho detalhados para duas versões de um serviço.
* Analise a alocação de memória em mais detalhes e o nível de alocações de memória individuais.
* Analise problemas de simultaneidade em código multithread.

Quando você usa o criador de perfil, você pode coletar dados quando um serviço de nuvem é executado localmente ou no Azure.

### <a name="collect-profiling-data-locally-to"></a>Colete dados de perfil localmente para:
* Teste o desempenho de uma parte de um serviço de nuvem, como a execução da função de trabalho específica, que não exige uma carga simulada realística.
* Teste o desempenho de um serviço de nuvem isoladamente, em condições controladas.
* Teste o desempenho de um serviço de nuvem antes de implantá-lo para o Azure.
* Teste o desempenho de um serviço de nuvem em particular, sem afetar as implantações existentes.
* Teste o desempenho do serviço sem incorrer em encargos para execução no Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Colete dados de criação de perfil no Azure para:
* Teste o desempenho de um serviço de nuvem sob uma carga real ou simulada.
* Use o método de instrumentação de coletar dados de criação de perfil, como este tópico descreve posteriormente.
* Teste o desempenho do serviço no mesmo ambiente, como quando o serviço é executado na produção.

Você geralmente simula uma carga para serviços de nuvem de teste em normal ou condições de tensão.

## <a name="profiling-a-cloud-service-in-azure"></a>Criação de perfil de um serviço de nuvem no Azure
Quando você publica seu serviço de nuvem do Visual Studio, você pode criar o perfil de serviço e especifique as configurações de criação de perfil que fornecem as informações que você deseja. Uma sessão de criação de perfil é iniciada para cada instância de uma função. Para obter mais informações sobre como publicar seu serviço do Visual Studio, consulte [publicando em um serviço de nuvem do Azure do Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx).

Para saber mais sobre a criação de perfil de desempenho no Visual Studio, consulte [guia do Iniciante à criação de perfil de desempenho](https://msdn.microsoft.com/library/azure/ms182372.aspx) e [analisando o desempenho do aplicativo usando ferramentas de criação de perfil](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> Você pode habilitar o IntelliTrace ou a criação de perfil quando você publica seu serviço de nuvem. Não é possível habilitar ambos.
> 
> 

### <a name="profiler-collection-methods"></a>Métodos de coleta do Profiler
Você pode usar diferentes métodos de coleção para a criação de perfil, com base em seus problemas de desempenho:

* **Amostragem de CPU** -esse método coleta estatísticas de aplicativo que são úteis para análise inicial de problemas de utilização de CPU. Amostragem de CPU é o método sugerido para iniciar a maioria das investigações de desempenho. Há um impacto baixo do aplicativo que você está criando o perfil quando você coleta dados de amostragem de CPU.
* **Instrumentação** -esse método coleta dados detalhados que são úteis para análise concentrada e para analisar problemas de desempenho de entrada/saída. O método de instrumentação registra cada entrada, saída e a chamada de função das funções em um módulo durante uma geração de perfil. Este método é útil para coletar informações detalhadas de tempo sobre uma seção do seu código e para compreender o impacto das operações de entrada e saída sobre o desempenho do aplicativo. Esse método está desabilitado para um computador executando um sistema operacional de 32 bits. Essa opção está disponível somente ao executar o serviço de nuvem no Azure, não localmente no emulador de computação.
* **Alocação de memória .NET** -esse método coleta dados de alocação de memória do .NET Framework usando o método de criação de perfil de amostragem. Os dados coletados incluem o número e tamanho dos objetos alocados.
* **Simultaneidade** -esse método coleta dados de contenção de recursos e dados de execução de thread e processo úteis na análise de aplicativos multi-threaded e multiprocessados. O método de simultaneidade coleta dados para cada evento que bloqueia a execução de seu código, como quando um thread aguarda bloqueia o acesso a um recurso de aplicativo para ser liberado. Esse método é útil para analisar aplicativos multi-threaded.
* Você também pode habilitar **Tier Interaction Profiling**, que fornece informações adicionais sobre os tempos de execução do ADO.NET síncronas chamadas em funções de aplicativos de várias camadas que se comunicam com um ou mais bancos de dados. Você pode coletar dados de interação de camadas com qualquer um dos métodos de criação de perfil. Para obter mais informações sobre a criação de perfil de interação de camadas, consulte [exibição de interações de camada](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Definindo configurações de criação de perfil
A ilustração a seguir mostra como definir as configurações de criação de perfil na caixa de diálogo Publicar aplicativo do Azure.

![Configurar as configurações de criação de perfil](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> Para habilitar o **Habilitar criação de perfil** caixa de seleção, você deve ter o criador de perfil instalado no computador local que você está usando para publicar seu serviço de nuvem. Por padrão, o criador de perfil é instalado quando você instala o Visual Studio.
> 
> 

### <a name="to-configure-profiling-settings"></a>Para definir configurações de criação de perfil
1. No Gerenciador de soluções, abra o menu de atalho do seu projeto do Azure e, em seguida, escolha **publicar**. Para obter etapas detalhadas sobre como publicar um serviço de nuvem, consulte [publicando um serviço de nuvem usando as ferramentas do Azure](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. No **publicar aplicativo do Azure** caixa de diálogo, escolheu o **configurações avançadas** guia.
3. Para habilitar a criação de perfil, selecione o **Habilitar criação de perfil** caixa de seleção.
4. Para configurar suas configurações de perfil, escolha o **configurações** hiperlink. Caixa de diálogo Configurações de criação de perfil é exibido.
5. Dos **qual método de criação de perfil você gostaria de usar** botões de opção, escolha o tipo de criação de perfil que você precisa.
6. Para coletar a dados de criação de perfil de interação de camadas, selecione a **habilitar Tier Interaction Profiling** caixa de seleção.
7. Para salvar as configurações, escolha o **Okey** botão.
   
    Quando você publica esse aplicativo, essas configurações são usadas para criar a sessão de criação de perfil para cada função.

## <a name="viewing-profiling-reports"></a>Exibindo relatórios de criação de perfil
Uma sessão de criação de perfil é criada para cada instância de uma função no serviço de nuvem. Para exibir seus relatórios de criação de perfil de cada sessão do Visual Studio, você pode exibir a janela do Gerenciador de servidores e, em seguida, escolha o nó de computação do Azure para selecionar uma instância de uma função. Em seguida, você pode exibir o relatório de criação de perfil, conforme mostrado na ilustração a seguir.

![Exibir relatório de criação de perfil do Azure](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="to-view-profiling-reports"></a>Para exibir relatórios de criação de perfil
1. Para exibir a janela do Gerenciador de servidores no Visual Studio, na barra de menus, escolha Exibir, Gerenciador de servidores.
2. Escolha o nó de computação do Azure e, em seguida, escolha o nó de implantação do Azure para o serviço de nuvem que você selecionou para o perfil ao publicar no Visual Studio.
3. Para exibir relatórios de criação de perfil para uma instância, escolha a função no serviço, abra o menu de atalho para uma instância específica e, em seguida, escolha **Exibir relatório de criação de perfil**.
   
    O relatório, um arquivo. vsp, agora é baixado do Azure e o status do download é exibido no Log de atividades do Azure. Quando o download for concluído, o relatório de criação de perfil aparece em uma guia no editor do Visual Studio denominada <Role name> *<Instance Number>* <identifier>. vsp. Dados de resumo para o relatório é exibido.
4. Para exibir os diferentes modos de exibição do relatório, na lista exibição atual, escolha o tipo de exibição que você deseja usar. Para obter mais informações, consulte [exibições de relatório das ferramentas de criação de perfil](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Próximas etapas
[Depurando serviços de nuvem](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Publicando em um serviço de nuvem do Azure do Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

