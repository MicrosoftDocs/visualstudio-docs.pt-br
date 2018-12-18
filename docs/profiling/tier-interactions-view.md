---
title: Exibição de interações de camada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.tierinteraction
helpviewer_keywords:
- Tier Interactions view
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d92144a6b9bd94e23397a033fbbee45bd5aeed4a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49917759"
---
# <a name="tier-interactions-view"></a>Exibição de interações da camada

A criação de perfil de interação de camada fornece informações adicionais sobre os tempos de execução em funções de aplicativos de várias camadas que se comunicam com os bancos de dados por meio de [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)]. Os dados são coletados apenas para chamadas de função síncronas.

**Requisitos**

- Visual Studio Enterprise

A Exibição Interações exibe os dados de interação de camada em dois painéis:

- O painel principal é uma árvore hierárquica. A linha de nível superior contém os dados agregados das conexões de banco de dados de uma página [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ou um processo. Nós filho contêm dados agregados para as conexões de banco de dados do pai.

- Ao clicar em um nó de chamada de banco de dados no painel principal, os dados da instância da chamada de banco de dados são exibidos no painel de detalhes.

  A hora é exibida como o número de milissegundos ou o número de tiques do relógio da CPU. Para alterar a unidade de tempo exibida, clique no menu **Ferramentas**, clique em **Opções** e escolha uma das opções **Mostrar valores temporais como**.

## <a name="master-pane"></a>Painel principal

|Column|Descrição|
|------------|-----------------|
|**Nome**|- Para uma linha de nível superior, o nome do processo com perfil ou a página da Web.<br />- Para uma linha de conexão de banco de dados, o nome do servidor que hospeda o banco de dados.|
|**Banco de dados**|O nome do banco de dados (somente linhas de conexão de banco de dados).|
|**Contagem**|O número total de solicitações geradas pelo processo, pela página da Web ou pela conexão de banco de dados.|
|**Tempo total decorrido**|O tempo total gasto na execução de uma solicitação do processo, da página da Web ou da conexão de banco de dados.|
|**Tempo máximo decorrido**|O tempo máximo gasto na execução de uma solicitação do processo, da página da Web ou da conexão de banco de dados.|
|**Tempo mínimo decorrido**|O tempo mínimo gasto na execução de uma solicitação do processo, da página da Web ou da conexão de banco de dados.|
|**Tempo médio decorrido**|O tempo médio gasto na execução de uma solicitação do processo, da página da Web ou da conexão de banco de dados.|

## <a name="database-connection-details-pane"></a>Painel Detalhes de Conexão do Banco de Dados

|Column|Descrição|
|------------|-----------------|
|**Texto do comando**|A consulta SQL da solicitação.|
|**Contagem de consulta**|O número de vezes que a consulta foi executada.|
|**Tempo total decorrido**|O tempo total gasto na execução das instâncias da consulta.|
|**Tempo máximo decorrido**|O tempo máximo gasto na execução de uma instância da consulta.|
|**Tempo mínimo decorrido**|O tempo mínimo gasto na execução de uma instância da consulta.|
|**Tempo médio decorrido**|O tempo médio gasto na execução de uma instância da consulta.|