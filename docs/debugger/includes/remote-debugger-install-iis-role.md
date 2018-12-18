---
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: 103000c2ded944236762ffd55603877ece7b7968
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38809426"
---
Estas etapas mostram apenas uma configuração básica do IIS. Para obter informações mais detalhadas ou para instalar em uma máquina de área de trabalho do Windows, consulte [publicar no IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration) ou [IIS 8.0 usando ASP.NET 3.5 e ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45).

Para sistemas operacionais Windows Server, use o **adicionar funções e recursos** por meio do assistente a **gerenciar** link ou o **painel** link no **Gerenciador do servidor**. Na etapa **Funções de Servidor**, marque a caixa de **Servidor Web (IIS)**.

![A função de Servidor Web IIS é selecionada na etapa Selecionar funções de servidor.](../media/remotedbg-server-roles-ws2012.png)

Na etapa **Serviços de função**, selecione os serviços de função do IIS desejados ou aceite os serviços de função padrão fornecidos. Se você quiser habilitar a implantação usando o Web Deploy e configurações de publicação, certifique-se de que **ferramentas e Scripts de gerenciamento do IIS** está selecionado.

Continue com as etapas de confirmação para instalar a função de servidor web e serviços. Uma reinicialização do servidor/IIS não é necessária após a instalação da função do Servidor Web (IIS).