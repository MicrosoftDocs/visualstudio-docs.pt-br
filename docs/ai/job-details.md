---
title: Exibir trabalhos recentes
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: 2e404d6a258ebb480b3eb02e615097872714db03
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371541"
---
# <a name="view-recent-job-performance-and-details"></a>Exibir detalhes e desempenho do trabalho recentes

Depois que os trabalhos forem enviados, será possível exibir a lista de trabalhos para ver seus status, duração e mais.

1. No **Gerenciador de Servidores**, expanda o contexto de computação específico.
2. Clique duas vezes em **Trabalhos**.
3. Você verá a lista de trabalhos enviados para esse contexto de computação.
4. Selecione um **trabalho** específico na lista para exibir detalhes.

![monitorar trabalhos](media/job-details/monitor-jobs.png)

> O histórico de trabalhos enviado para VMs Linux é armazenado na VM no diretório /tmp. Portanto, sempre que ela for reinicializada, o histórico de trabalhos será limpo. Para obter um registro permanente do seu histórico de trabalhos, configure a VM como um contexto de computação no Azure Machine Learning. Em seguida, envie um trabalho para o Azure Machine Learning (selecionando sua VM como o contexto de computação).
