---
title: As atribuições de porta do depurador remoto | Microsoft Docs
ms.custom: H1Hack27Feb2017
ms.date: 05/18/2017
ms.technology: vs-ide-debug
ms.topic: reference
ms.assetid: 238bb4ec-bb00-4c2b-986e-18ac278f3959
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1570468a56a4eaba80965d8feea669a0d3f3cb1c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49905058"
---
# <a name="remote-debugger-port-assignments"></a>Atribuições de porta do depurador remoto
O depurador remoto do Visual Studio pode ser executado como um aplicativo ou como um serviço em segundo plano. Quando ele é executado como um aplicativo, ele usa uma porta atribuída por padrão, da seguinte maneira:  

- Visual Studio 2017:4022

- Visual Studio 2015:4020  
  
- Visual Studio 2013:4018  
  
- Visual Studio 2012:4016  
  
  Em outras palavras, o número da porta atribuída ao depurador remoto é incrementado por 2 para cada versão. Você pode definir um número de porta diferente da que você deseja. Explicaremos como definir os números de porta em uma seção posterior.  
  
## <a name="the-remote-debugger-port-on-32-bit-operating-systems"></a>A porta do depurador remoto em sistemas operacionais de 32 bits  
 TCP 4022 (no Visual Studio 2017) é a porta principal e é necessário para todos os cenários. Você pode configurar isso na linha de comando ou a janela do depurador remoto.  
  
 Na janela do depurador remoto, clique em **Ferramentas > Opções**e defina o número da porta TCP/IP.  
  
 Na linha de comando, iniciar o depurador remoto com o **/porta** alternar: **msvsmon /port \<número da porta >**.  
  
 Você pode encontrar o depurador remoto de linha de comando na Ajuda de depuração remota (pressione **F1** ou clique em **Ajuda > uso** na janela do depurador remoto).  
  
## <a name="the-remote-debugger-port-on-64-bit-operating-systems"></a>A porta do depurador remoto em sistemas operacionais de 64 bits  
 Quando a versão de 64 bits do depurador remoto é iniciada, ele usa a porta 4022 por padrão.  Se você depurar um processo de 32 bits, a versão de 64 bits do depurador remoto inicia uma versão de 32 bits do depurador remoto na porta 4023. Se você executar o depurador remoto de 32 bits, ele usa 4022 e 4023 não é usado.  
  
 Essa porta é configurável na linha de comando: **Msvsmon /wow64port \<número da porta >**.  
  
## <a name="the-discovery-port"></a>A porta de descoberta  
 UDP 3702 é usada para localizar instâncias em execução do depurador remoto na rede (por exemplo, o **encontrar** caixa de diálogo na **anexar ao processo** caixa de diálogo). Ele é usado apenas para a descoberta de uma máquina executando o depurador remoto, portanto, é opcional se você tiver alguma outra maneira de saber o nome do computador ou endereço IP do computador de destino. Esta é uma porta padrão para a descoberta, portanto, o número da porta não pode ser configurado.  
  
 Se você não quiser habilitar a descoberta, você pode iniciar o msvsmon da linha de comando com a descoberta desabilitada: **Msvsmon /nodiscovery**.  
  
## <a name="remote-debugger-ports-on-azure"></a>Portas do depurador remoto no Azure  
 As seguintes portas são usadas pelo depurador remoto no Azure. As portas no serviço de nuvem são mapeadas para as portas na VM individual. Todas as portas são TCP.  
  
|Conexão|Porta no serviço de nuvem|Porta na VM|
|-|-|-|  
|Remotedebugger|30400|30398|  
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Forwarder|31400|31398|  
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.FileUpload|32400|32398|  
  
## <a name="see-also"></a>Consulte também  
 [Depuração remota](../debugger/remote-debugging.md)