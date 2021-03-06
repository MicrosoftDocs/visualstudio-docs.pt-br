---
ms.openlocfilehash: 94c2c733b631ef5e727c79a6e093bb224aec38c4
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249815"
---

1. No computador em que você tem o projeto ASP.NET aberto no Visual Studio, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e escolha **Publicar**.

   Se você já tiver configurado anteriormente quaisquer perfis de publicação, o painel **Publicar** será exibido. Clique em **novo** ou **criar novo perfil**.

1. Selecione a opção para importar um perfil.

   ::: moniker range=">=vs-2019"
   Na caixa de diálogo **publicar** , clique em **importar perfil**.
   ::: moniker-end
   ::: moniker range="vs-2017"
   Na caixa de diálogo **Escolher um destino de publicação**, clique em **Importar perfil**.
   ::: moniker-end

   ![Escolha Publicar](../../deployment/media/tutorial-publish-tool-import-profile.png)

1. Navegue até a localização do arquivo de configurações de publicação que você criou na seção anterior.

1. Na caixa de diálogo **Importar arquivo de configurações de publicação** , navegue até e selecione o perfil que você criou na seção anterior e clique em **abrir**.

   ::: moniker range=">=vs-2019"
   Clique em **concluir** para salvar o perfil de publicação e clique em **publicar**.

   O Visual Studio inicia o processo de implantação e a janela de Saída mostra o andamento e os resultados.

   Se você receber algum erro de implantação, clique em **Editar** para editar as configurações. Modifique as configurações e clique em **Validar** para testar as novas. Se o nome do host não for encontrado, experimente o endereço IP em vez do nome de host nos campos **Servidor** e **URL de destino**.
   ::: moniker-end
   ::: moniker range="vs-2017"
   O Visual Studio inicia o processo de implantação e a janela de Saída mostra o andamento e os resultados.

   Se você receber quaisquer erros de implantação, clique em **Configurações** para editá-las. Modifique as configurações e clique em **Validar** para testar as novas. Se o nome do host não for encontrado, experimente o endereço IP em vez do nome de host nos campos **Servidor** e **URL de destino**.
   ::: moniker-end

   ![Editar configurações na ferramenta Publicar](../../deployment/media/tutorial-configure-publish-settings-in-tool.png)
