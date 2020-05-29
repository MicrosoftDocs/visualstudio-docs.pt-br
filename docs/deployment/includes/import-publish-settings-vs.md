---
ms.openlocfilehash: f286002112667ba763419f0e3d6265dbe1942212
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173857"
---

1. No computador em que você tem o projeto ASP.NET aberto no Visual Studio, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e escolha **Publicar**.

1. Se você já tiver configurado anteriormente quaisquer perfis de publicação, o painel **Publicar** será exibido. Clique **Criar novo perfil**.

1. Na caixa de diálogo **Escolher um destino de publicação**, clique em **Importar perfil**.

    ![Escolha Publicar](../../deployment/media/tutorial-publish-tool-import-profile.png)

1. Navegue até a localização do arquivo de configurações de publicação que você criou na seção anterior.

1. Na caixa de diálogo **Importar arquivo de configurações de publicação** , navegue até e selecione o perfil que você criou na seção anterior e clique em **abrir**.

    O Visual Studio inicia o processo de implantação e a janela de Saída mostra o andamento e os resultados.

    Se você receber quaisquer erros de implantação, clique em **Configurações** para editá-las. Modifique as configurações e clique em **Validar** para testar as novas. Se o nome do host não for encontrado, experimente o endereço IP em vez do nome de host nos campos **Servidor** e **URL de destino**.

    ![Editar configurações na ferramenta Publicar](../../deployment/media/tutorial-configure-publish-settings-in-tool.png)
