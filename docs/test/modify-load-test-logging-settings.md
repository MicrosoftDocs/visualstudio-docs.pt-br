---
title: Configurações de registro em log de testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, logging, modifying
ms.assetid: 9649226a-857d-41ef-8ec7-047b6e498033
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 2adef763b46a00f380ef7fb0f9f2d0a3ecdcfb8b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49909686"
---
# <a name="modify-load-test-logging-settings"></a>Modificar configurações de registro em log de testes de carga

O resultado de teste de carga para o teste de carga concluído contém exemplos de contador de desempenho e informações de erros que foram coletados em um log periodicamente dos computadores em teste. Um grande número de exemplos de contador de desempenho podem ser coletados durante a execução de um teste de carga. A quantidade de dados de desempenho coletados depende da extensão da execução, do intervalo de amostragem, do número de computadores em teste, e do número de contadores para coletar. Para um teste de carga grande, a quantidade de dados de desempenho coletados pode ser facilmente vários gigabytes; portanto, você deverá considerar a possibilidade de modificar o modo como os dados são salvos com frequência no log. Consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

O *controlador de teste* armazena em spool todos os dados de exemplo do teste de carga em um log de banco de dados durante a execução do teste. Os dados adicionais, como detalhes dos erros e de medição de tempo, são carregados no banco de dados quando o teste é concluído.

|Tarefa|Tópicos associados|
|-|-----------------------|
|**Especificar a frequência de salvamento de logs durante uma execução de teste de carga:** você pode especificar a frequência com que deseja que o log do teste seja salvo quando o teste de carga é executado.|-   [Como especificar a frequência com que os logs de teste são salvos](../test/how-to-specify-how-frequently-test-logs-are-saved.md)|
|**Salvar logs se um teste de carga falhar:** você pode especificar se quer salvar o log de teste sempre que um teste de carga falhar.|-   [Como especificar se as falhas no teste são salvas em logs de teste](../test/how-to-specify-if-test-failures-are-saved-to-test-logs.md)|
|**Definir o tamanho máximo de arquivo para o arquivo de log:** você pode editar o arquivo de configuração XML associado ao serviço do controlador de teste para especificar o tamanho de arquivo máximo que deseja usar para o arquivo de log.|[Como especificar o tamanho máximo do arquivo de log](../test/how-to-specify-the-maximum-size-for-the-log-file.md)|

## <a name="related-tasks"></a>Tarefas relacionadas

Uma propriedade relacionada é **Armazenamento de Detalhes de Tempo**. Para saber mais, confira [Como configurar a coleta de detalhes completos para habilitar o gráfico de atividade do usuário virtual](../test/how-to-configure-load-tests-to-collect-full-details.md).

## <a name="see-also"></a>Consulte também

- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)