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
ms.openlocfilehash: d24bb1b3af468f35ae333407fc96c42f4f9e669b
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894879"
---
# <a name="modify-load-test-logging-settings"></a>Modificar configurações de registro em log de testes de carga

O resultado de teste de carga para o teste de carga concluído contém exemplos de contador de desempenho e informações de erros que foram coletados em um log periodicamente dos computadores em teste. Um grande número de exemplos de contador de desempenho podem ser coletados durante a execução de um teste de carga. A quantidade de dados de desempenho coletados depende da extensão da execução, do intervalo de amostragem, do número de computadores em teste, e do número de contadores para coletar. Para um teste de carga grande, a quantidade de dados de desempenho coletados pode ser facilmente vários gigabytes; portanto, você deverá considerar a possibilidade de modificar o modo como os dados são salvos com frequência no log. Consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

O *controlador de teste* armazena em spool todos os dados de exemplo do teste de carga em um log de banco de dados durante a execução do teste. Os dados adicionais, como detalhes dos erros e de medição de tempo, são carregados no banco de dados quando o teste é concluído.

|Tarefa|Tópicos associados|
|-|-----------------------|
|**Salvar logs se um teste de carga falhar:** você pode especificar se quer salvar o log de teste sempre que um teste de carga falhar.|-   [Como especificar se as falhas no teste são salvas em logs de teste](../test/how-to-specify-if-test-failures-are-saved-to-test-logs.md)|
|**Definir o tamanho máximo de arquivo para o arquivo de log:** você pode editar o arquivo de configuração XML associado ao serviço do controlador de teste para especificar o tamanho de arquivo máximo que deseja usar para o arquivo de log.|[Como especificar o tamanho máximo do arquivo de log](../test/how-to-specify-the-maximum-size-for-the-log-file.md)|

## <a name="see-also"></a>Consulte também

- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)