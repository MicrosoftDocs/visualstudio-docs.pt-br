---
title: Atribuições de porta do depurador remoto | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 238bb4ec-bb00-4c2b-986e-18ac278f3959
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2628d8929a0d2b6fd3561f88c81cfaa3b62564f0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542097"
---
# <a name="remote-debugger-port-assignments"></a>Atribuições de porta do depurador remoto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Depurador Remoto do Visual Studio pode ser executado como um aplicativo ou como um serviço em segundo plano. Quando ele é executado como um aplicativo, ele usa uma porta que é atribuída por padrão da seguinte maneira:  
  
- Visual Studio 2015: 4020  
  
- Visual Studio 2013: 4018  
  
- Visual Studio 2012: 4016  
  
  Em outras palavras, o número da porta atribuída ao depurador remoto é incrementado por 2 para cada versão. Você pode definir um número de porta diferente que desejar. Explicaremos como definir números de porta em uma seção posterior.  
  
## <a name="the-remote-debugger-port-on-32-bit-operating-systems"></a>A porta do depurador remoto em sistemas operacionais de 32 bits  
 O TCP 4020 (no Visual Studio 2015) é a porta principal e é necessário para todos os cenários. Você pode configurá-lo na linha de comando ou na janela do depurador remoto.  
  
 Na janela depurador remoto, clique em **ferramentas/opções**e defina o número da porta TCP/IP.  
  
 Na linha de comando, inicie o depurador remoto com a opção **/Port** : **msvsmon/Port \<port number> **.  
  
 Você pode encontrar todas as opções de linha de comando do depurador remoto na ajuda de depuração remota (pressione **F1** ou clique em **Ajuda/uso** na janela do depurador remoto).  
  
## <a name="the-remote-debugger-port-on-64-bit-operating-systems"></a>A porta do depurador remoto em sistemas operacionais de 64 bits  
 Quando a versão de 64 bits do depurador remoto é iniciada, ela usa a porta 4020 por padrão.  Se você depurar um processo de 32 bits, a versão de 64 bits do depurador remoto iniciará uma versão de 32 bits do depurador remoto na porta 4021. Se você executar o depurador remoto de 32 bits, ele usará 4020 e 4021 não será usado.  
  
 Essa porta é configurável na linha de comando: **msvsmon/wow64port \<port number> **.  
  
## <a name="the-discovery-port"></a>A porta de descoberta  
 O UDP 3702 é usado para localizar instâncias em execução do depurador remoto na rede (por exemplo, a caixa de diálogo **Localizar** na caixa de diálogo **anexar ao processo** ). Ele é usado apenas para descobrir um computador que executa o depurador remoto, portanto, é opcional se você tiver alguma outra forma de saber o nome do computador ou o endereço IP de um dos computadores de destino. Essa é uma porta padrão para descoberta, portanto, o número da porta não pode ser configurado.  
  
 Se não quiser habilitar a descoberta, você poderá iniciar o msvsmon na linha de comando com a descoberta desabilitada: **msvsmon/noDiscovery**.  
  
## <a name="remote-debugger-ports-on-azure"></a>Portas do depurador remoto no Azure  
 As portas a seguir são usadas pelo depurador remoto no Azure. As portas no serviço de nuvem são mapeadas para as portas na VM individual. Todas as portas são TCP.  

|**Conexão**|**Porta no serviço de nuvem**|**Porta na VM**|  
|-|-|-|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector|30400|30398|  
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Forwarder|31400|31398|  
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.FileUpload|32400|32398|  
  
## <a name="see-also"></a>Consulte Também  
 [Depuração remota](../debugger/remote-debugging.md)
