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
ms.openlocfilehash: c22ba73b464f91bf3036541304cdf94e8660970d
ms.sourcegitcommit: 1c675dae7c348defb32d9f7ccf7079a1062a1c4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48244098"
---
1. Se você pretende implantar seus aplicativos com implantação da Web no Visual Studio, instale a versão mais recente da implantação da Web no servidor.

    Para instalar a implantação da Web, use o [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx). (Para localizar o link do instalador de plataforma da Web do IIS, selecione **IIS** no painel esquerdo do Gerenciador do servidor. O servidor com o botão direito e selecione **serviços de informações da Internet (IIS) Manager**.)

    O Web Platform Installer, você encontrará implantação da Web na guia aplicativos. Você também pode obter um instalador diretamente na [Microsoft Download Center](https://www.microsoft.com/search/result.aspx?q=webdeploy&form=dlc). 

2. Verificar a implantação da Web está executando corretamente abrindo **painel de controle > sistema e segurança > Ferramentas administrativas > serviços** e certifique-se de que **serviço de agente de implantação da Web** está em execução (o nome do serviço é diferente em versões mais antigas).

    Se o serviço de agente não está em execução, inicie-o. Se não estiver presente em todos os, acesse **painel de controle > Programas > desinstalar um programa**, localize **Microsoft Web Deploy <version>** . Escolher **alteração** a instalação e certifique-se de que você escolhe **será instalado na unidade de disco rígido local** para os componentes de implantação da Web. Conclua as etapas de instalação de alteração.