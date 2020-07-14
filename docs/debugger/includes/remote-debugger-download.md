---
title: Download do depurador remoto
description: Links de download para o depurador remoto
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 1e90a1d9e03892cf81bd2257d3dcc6e25ab36246
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149189"
---
No dispositivo ou servidor remoto no qual você deseja depurar, em vez de no computador do Visual Studio, baixe e instale a versão correta das ferramentas remotas nos links na tabela a seguir.

- Baixe as ferramentas remotas mais recentes para sua versão do Visual Studio. A versão mais recente das ferramentas remotas é compatível com versões anteriores do Visual Studio, mas versões anteriores das ferramentas remotas não são compatíveis com as versões posteriores do Visual Studio. (Por exemplo, se você estiver usando o Visual Studio 2017, baixe a atualização mais recente das ferramentas remotas para o Visual Studio 2017. Nesse cenário, não baixe as ferramentas remotas para o Visual Studio 2019.)
- Baixe as ferramentas remotas com a mesma arquitetura do computador em que você as está instalando. Por exemplo, se você quiser depurar um aplicativo de 32 bits em um computador remoto que executa um sistema operacional de 64 bits, instale as ferramentas remotas de 64 bits.

::: moniker range=">=vs-2019"

|Versão|Link|Observações|
|-|-|-|
|Visual Studio 2019|[Ferramentas remotas](https://visualstudio.microsoft.com/downloads#remote-tools-for-visual-studio-2019)|Compatível com todas as versões do Visual Studio 2019. Baixe a versão correspondente ao sistema operacional do dispositivo (x86, x64 ou ARM64). No Windows Server, consulte [desbloquear o download do arquivo](../../debugger/remote-debugging-unblock-file-download.md) para obter ajuda para baixar as ferramentas remotas.|
|Visual Studio 2017|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|Compatível com todas as versões do Visual Studio 2017. Baixe a versão correspondente ao sistema operacional do dispositivo (x86, x64 ou ARM64). No Windows Server, consulte [desbloquear o download do arquivo](../../debugger/remote-debugging-unblock-file-download.md) para obter ajuda para baixar as ferramentas remotas.|
|Visual Studio 2015|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|As ferramentas remotas para Visual Studio 2015 estão disponíveis em My.VisualStudio.com. Se solicitado, ingresse no programa de [Visual Studio dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) gratuito ou entre com sua ID de assinatura do Visual Studio. No Windows Server, consulte [desbloquear o download do arquivo](../../debugger/remote-debugging-unblock-file-download.md) para obter ajuda para baixar as ferramentas remotas.|
|Visual Studio 2013|[Ferramentas remotas](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Página de download na documentação do Visual Studio 2013|
|Visual Studio 2012|[Ferramentas remotas](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Página de download na documentação do Visual Studio 2012|

::: moniker-end

::: moniker range="vs-2017"

|Versão|Link|Observações|
|-|-|-|
|Visual Studio 2017|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|Compatível com todas as versões do Visual Studio 2017. Baixe a versão correspondente ao sistema operacional do dispositivo (x86, x64 ou ARM64). No Windows Server, consulte [desbloquear o download do arquivo](../../debugger/remote-debugging-unblock-file-download.md) para obter ajuda para baixar as ferramentas remotas. Para obter a versão mais recente das ferramentas remotas, abra o [documento do Visual Studio 2019](../../debugger/remote-debugging.md?view=vs-2019).|
|Visual Studio 2015|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|As ferramentas remotas para Visual Studio 2015 estão disponíveis em My.VisualStudio.com. Se solicitado, ingresse no programa de [Visual Studio dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) gratuito ou entre com sua ID de assinatura do Visual Studio. No Windows Server, consulte [desbloquear o download do arquivo](../../debugger/remote-debugging-unblock-file-download.md) para obter ajuda para baixar as ferramentas remotas.|
|Visual Studio 2013|[Ferramentas remotas](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Página de download na documentação do Visual Studio 2013|
|Visual Studio 2012|[Ferramentas remotas](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Página de download na documentação do Visual Studio 2012|

::: moniker-end

Você pode executar o depurador remoto copiando *msvsmon.exe* para o computador remoto, em vez de instalar as ferramentas remotas. No entanto, o assistente de configuração do depurador remoto (*rdbgwiz.exe*) está disponível somente quando você instala as ferramentas remotas. Talvez seja necessário usar o assistente para configuração se você quiser executar o depurador remoto como um serviço. Para obter mais informações, consulte [(opcional) configurar o depurador remoto como um serviço](../../debugger/remote-debugging.md#bkmk_configureService).

>[!NOTE]
>- Para depurar aplicativos do Windows 10 em dispositivos ARM, use o ARM64, que está disponível com a versão mais recente das ferramentas remotas.
>- Para depurar aplicativos do Windows 10 em dispositivos Windows RT, use o ARM, que está disponível somente no download de ferramentas remotas do Visual Studio 2015.
