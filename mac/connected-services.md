---
title: Serviços Conectados
description: Adicione o armazenamento de dados, a autenticação e as notificações por push do Azure a aplicativos móveis usando o Visual Studio para Mac
ms.assetid: 41CB62FF-0F39-4CE8-8917-6A77F058719F
author: conceptdev
ms.author: crdun
ms.date: 11/06/2018
ms.openlocfilehash: ada47aa3d0cb0d9917404efc2775b843223c6e86
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948940"
---
# <a name="connected-services-walkthrough"></a>Passo a passo do Connected Services

O fluxo de trabalho do Connected Services leva o fluxo de trabalho do portal do Azure ao Visual Studio para Mac, para que não seja necessário sair do projeto para adicionar serviços.

Este passo a passo mostra como adicionar um serviço de back-end do Azure, que oferece armazenamento de dados em nuvem, autenticação e notificações por push, em um aplicativo PCL (Biblioteca de Classes Portátil) multiplataforma do Xamarin.Forms.

1. Para começar, clique duas vezes no nó **Serviços Conectados** na solução, o que abre a **Galeria de Serviços**.
  Esta é uma lista de todos os serviços disponíveis para o tipo de aplicativo. Selecione um serviço (como **Back-end móvel com o Serviço de Aplicativo do Azure**) clicando nele.

    [![Nó do Connected Services no Visual Studio para Mac](media/connected-services-image001-sml.png "Nó do Connected Services no Visual Studio para Mac")](media/connected-services-image001.png#lightbox)

2. A página de Detalhes do Serviço oferece uma descrição do serviço e das dependências que serão instaladas.
  Clique no botão **Adicionar** para adicionar as dependências ao aplicativo:

    [![Back-end móvel com o Azure](media/connected-services-image002-sml.png "Back-end móvel com o Azure")](media/connected-services-image002.png#lightbox)

3. As dependências precisam ser adicionadas aos projetos PCL e específicos da plataforma para que funcionem.
  Marque as caixas de seleção para adicionar o serviço em cada projeto que o referenciará (direta ou indiretamente):

    [![Marque todos os projetos que devem referenciar o serviço](media/connected-services-image003-sml.png "Marque todos os projetos que devem referenciar o serviço")](media/connected-services-image003.png#lightbox)

4. Escolha **Aceitar** nas caixas de diálogo **Aceitação da licença** dos pacotes NuGet.
  Pode haver duas caixas de diálogo a serem aceitas, uma do MobileClient e das dependências e outra do SQLiteStore, que é necessário para a sincronização de dados offline:

    [![Aceite os contratos de licença](media/connected-services-image004-sml.png "Aceite os contratos de licença")](media/connected-services-image004.png#lightbox)

    ![Janela de aceitação da licença](media/connected-services-image005.png "Janela de aceitação da licença")

5. Quando as dependências forem adicionadas, será solicitado que você faça logon com a conta que deseja usar para se comunicar com o Azure.
  Se você já tiver feito logon com uma ID da Microsoft, o Visual Studio para Mac tentará buscar suas assinaturas do Azure e todos os serviços de aplicativo associados a elas. Se você não tiver nenhuma assinatura, adicione uma inscrevendo-se para uma avaliação gratuita ou comprando um plano de assinatura no Portal do Azure.

6. Selecione um serviço de aplicativo na lista. Isso preencherá o código de modelo para o objeto `MobileServiceClient` com a URL correspondente do serviço de aplicativo no Azure:

    [![Selecione o serviço de aplicativo na lista](media/connected-services-image006-sml.png "Selecione o serviço de aplicativo na lista")](media/connected-services-image006.png#lightbox)

    Se não houver nenhum serviço listado, clique no botão **Novo** (confira a Etapa 9).

7. Copie o código de modelo do `MobileServiceClient` no PCL. O local do arquivo não é importante, desde que haja apenas uma instância dele.
  A abordagem recomendada é criar uma classe `AzureService` que manipule todas as interações do Azure e use o `MobileServiceClient`:

    ![Copie o código de configuração no aplicativo](media/connected-services-image007.png "Copie o código de configuração no aplicativo")

8. Siga a documentação em **Próximas Etapas** para adicionar dados, sincronizar offline, autenticar e enviar notificações por push para o aplicativo:

    [![Examine as instruções das próximas etapas](media/connected-services-image008-sml.png "Examine as instruções das próximas etapas")](media/connected-services-image008.png#lightbox)

9. Se você não tiver nenhum serviço de aplicativo existente, crie serviços usando o Visual Studio para Mac.
  Clique no botão **Novo** no canto inferior esquerdo da lista de serviços para abrir a caixa de diálogo **Novo Serviço de Aplicativo**:

    [![Crie um serviço de aplicativo no Visual Studio para Mac](media/connected-services-image009-sml.png "Crie um serviço de aplicativo no Visual Studio para Mac")](media/connected-services-image009.png#lightbox)

Um novo serviço requer os seguintes parâmetros:

-   **Nome do serviço de aplicativo** – nome/ID exclusiva do plano
-   **Assinatura** – a assinatura que você deseja usar para pagar pelo serviço
-   **Grupo de Recursos** – um modo de organizar todos os recursos do Azure para um projeto. Opção de usar um existente ou criar um. Se esse for seu primeiro serviço do Azure, crie um.
-   **Plano de Serviço** – determina o local e o custo dos recursos que o usam. Opção de usar um existente ou criar um. Se esse for o primeiro serviço do Azure, use o padrão ou crie um novo na camada gratuita (F1).

Visite a [Documentação dos aplicativos móveis](/azure/app-service-mobile/) para obter mais informações.

## <a name="see-also"></a>Consulte também

- [Serviços Conectados (Visual Studio no Windows)](/visualstudio/azure/vs-azure-tools-connected-services-storage)