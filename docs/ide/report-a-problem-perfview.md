---
description: PerfView é uma ferramenta que cria arquivos ETL (log de rastreamento de eventos) baseados em rastreamento de eventos para Windows) que podem ser úteis para solucionar alguns tipos de problemas com o Visual Studio.
title: Coletar um rastreamento ETL com PerfView
ms.date: 09/27/2019
ms.topic: how-to
helpviewer_keywords:
- perfview
- ETL Trace
author: corob-msft
ms.author: corob
manager: jmartens
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Use perfview.exe to collect ETL traces for troubleshooting issues with Visual Studio
ms.openlocfilehash: 81cf6469a14fb3559d37056ba5193d9018ccc1c8
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221061"
---
# <a name="collect-an-etl-trace-with-perfview"></a>Coletar um rastreamento ETL com PerfView

PerfView é uma ferramenta que cria arquivos ETL (log de rastreamento de eventos) com base no [Rastreamento de Eventos para Windows](/windows/desktop/ETW/event-tracing-portal) que pode ser útil na solução de alguns tipos de problemas do Visual Studio. Ocasionalmente, quando você relata algum problema, a equipe de produto pode solicitar que você execute o PerfView para coletar informações adicionais.

## <a name="install-perfview"></a>Instalar o PerfView

Baixe o PerfView do [GitHub](https://github.com/Microsoft/perfview/blob/master/documentation/Downloading.md).

## <a name="run-perfview"></a>Executar o PerfView

1. Clique com o botão direito do mouse em **PerfView.exe** no Windows Explorer e, como administrador, escolha **Executar como administrador**
1. No menu Coletar, escolha **Coletar**
1. Marque **Zip**, **Mesclar** e **Tempo de Thread**.
1. Aumente **MB Circular** para 1000.
1. Altere **Dir atual** para salvar os rastreamentos ETL em uma pasta especificada e altere o Arquivo de Dados, se você pretende coletar mais de uma vez.
1. Para iniciar a gravação de dados, selecione o botão **Iniciar a Coleta**.
1. Para interromper a gravação de dados, selecione o botão **Parar a Coleta**. O arquivo PrefView.etl.zip será salvo no diretório especificado.

O PerfView pode armazenar apenas os dados mais recentes que se encaixam em seu buffer. Portanto, tente interromper a coleta logo depois que o Visual Studio for iniciado para congelá-lo ou diminuí-lo. Não colete por mais de 30 segundos depois de alcançar um problema.

Para obter mais informações, assista ao [Tutorial do PerfView no Channel9](https://channel9.msdn.com/Series/PerfView-Tutorial/PerfView-Tutorial-1-Collecting-data-with-the-Run-command).
