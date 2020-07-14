---
ms.openlocfilehash: a292b37a50bbf667fa5b23f18879cd79c3f76805
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85292081"
---
A Implantação da Web 3.6 para Servidores de Hospedagem fornece recursos adicionais de configuração que permitem a criação do arquivo de configurações da publicação por meio da interface do usuário.

1. Se você já tiver o implantação da Web instalado no Windows Server, desinstale-o usando programas do **painel**  >  **Programs**  >  **de controle desinstalar um programa**.

2. Em seguida, instale Implantação da Web 3.6 para Servidores de Hospedagem no Windows Server.

    Para instalar a Implantação da Web para Servidores de Hospedagem, use o WebPI (Web Platform Installer). (Para localizar o link do Web Platform Installer do IIS, selecione **IIS** no painel esquerdo do Gerenciador do Servidor. No painel servidor, clique com o botão direito do mouse no servidor e selecione **Gerenciador de serviços de informações da Internet (IIS)**. Em seguida, use o link **obter novos componentes da Web Platform** na janela **ações** .) Você também pode obter o Web Platform Installer (WebPI) de [downloads](https://www.microsoft.com/web/downloads/platform.aspx).

    Na Web Platform Installer, você encontrará **Implantação da Web 3,6 para servidores de hospedagem** na guia aplicativos.

3. Se você ainda não instalou as **Ferramentas e Scripts de Gerenciamento do IIS**, instale-as agora.

    Vá para **selecionar funções de servidor**  >  ferramentas de gerenciamento**servidor Web (IIS)**  >  **Management Tools**e, em seguida, selecione a função **scripts e ferramentas de gerenciamento do IIS** , clique em **Avançar**e, em seguida, instale a função.

    ![Instalar Scripts de gerenciamento e ferramentas do IIS](../../deployment/media/tutorial-iis-management-scripts-and-tools.png)

    Os scripts e as ferramentas são necessários para permitir a geração do arquivo de configurações da publicação.

4. Adicional Verifique se Implantação da Web está sendo executado corretamente abrindo o **painel de controle > sistema e segurança > ferramentas administrativas > serviços**e, em seguida, verifique se:

    * O **serviço Web Deployment Agent** está em execução (o nome do serviço é diferente em versões mais antigas).

    * O **serviço de gerenciamento da Web** está em execução.

    Se um dos serviços do Agent não estiver em execução, reinicie o **serviço Web Deployment Agent**.

    Se o serviço Web Deployment Agent não estiver presente, vá para painel de **controle > programas > desinstalar um programa**, localize **o Microsoft implantação da Web \<version> **. Escolha **Alterar** a instalação e certifique-se de escolher **Será instalado na unidade de disco rígido local** para os componentes de Implantação da Web. Conclua as etapas de instalação de alteração.