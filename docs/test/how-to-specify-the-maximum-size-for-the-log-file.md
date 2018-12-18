---
title: Tamanho do arquivo de log para testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, logging
ms.assetid: 417059bf-37ae-4e7a-b9b0-29bd71f1414f
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 22cc77426abca46a95fd12c8954fd0965a194f5e
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894424"
---
# <a name="how-to-specify-the-maximum-size-for-the-log-file-for-load-tests"></a>Como especificar o tamanho máximo do arquivo de log para testes de carga

Por padrão, o tamanho máximo do arquivo de log que é usado para testes de carga é definido como 20 megabytes. É possível alterar esse valor editando o arquivo de configuração associado ao serviço do controlador.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="specify-the-maximum-log-file-size-for-load-test"></a>Especificar o tamanho máximo do arquivo de log para teste de carga

1.  Abra o arquivo de configuração XML *QTCcontroller.exe.config* localizado em *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\QTCcontroller.exe.config*.

2.  Localize a entrada `<add key="LogSizeLimitInMegs" value="20"/>` na marca `<appSettings>`.

    ```xml
    <appSettings>
        <add key="LogSizeLimitInMegs" value="20"/>
        <add key="AgentConnectionTimeoutInSeconds" value="120"/>
        <add key="AgentSyncTimeoutInSeconds" value="300"/>
        <add key="ControllerServicePort" value="6901"/>
        <add key="ControllerUsersGroup" value="TeamTestControllerUsers"/>
        <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins"/>
        <add key="CreateTraceListener" value="no"/>
      </appSettings>
    ```

3.  Modifique `value ="20"` para o tamanho máximo permitido que você deseja especificar para o arquivo de log.

    > [!NOTE]
    > A inserção de um valor "0" especifica que o arquivo de log está limitado em tamanho somente pelo espaço em disco disponível.

## <a name="see-also"></a>Consulte também

- [Modificar configurações de registro em log de testes de carga](../test/modify-load-test-logging-settings.md)
- [Configurar portas para controladores e agentes de teste](../test/configure-ports-for-test-controllers-and-test-agents.md)