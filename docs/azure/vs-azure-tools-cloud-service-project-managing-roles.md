---
title: Gerenciando funções nos serviços de nuvem do Azure
description: Saiba como adicionar e remover funções nos serviços de nuvem do Azure com o Visual Studio.
author: ghogen
manager: jillfra
assetId: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.custom: seodec18
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: 02ebd2be3fc7cbb1f0003b2f44023b99cbc0c603
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55948037"
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Gerenciando funções nos serviços de nuvem do Azure com o Visual Studio
Depois de criar o serviço de nuvem do Azure, é possível adicionar novas funções a ele ou remover funções existentes. Você também pode importar um projeto existente e convertê-lo em uma função. Por exemplo, você pode importar um aplicativo Web ASP.NET e designá-lo como uma função web.

## <a name="adding-a-role-to-an-azure-cloud-service"></a>Adicionando uma função a um serviço de nuvem do Azure
As etapas a seguir explicarão como adicionar uma função web ou de trabalho a um projeto de serviço de nuvem do Azure no Visual Studio.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Gerenciador de Soluções**, expanda o nó do projeto

1. Clique com o botão direito do mouse no nó **Funções** para exibir o menu de contexto. No menu de contexto, selecione **Adicionar** e, em seguida, selecione uma função web ou função de trabalho existente da solução atual ou crie um projeto de função web ou função de trabalho. Também é possível selecionar um projeto apropriado, como um projeto de aplicativo Web ASP.NET e associá-lo a um projeto de função.

    ![Opções do menu para adicionar uma função a um projeto de serviço de nuvem do Azure](./media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Removendo uma função de um serviço de nuvem do Azure
As etapas a seguir explicarão como remover uma função web ou de trabalho de um projeto de serviço de nuvem do Azure no Visual Studio.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Gerenciador de Soluções**, expanda o nó do projeto

1. Expanda o nó **Funções**.

1. Clique com o botão direito do mouse no nó que você deseja remover e, no menu de contexto, selecione **Remover**.

    ![Opções do menu para adicionar uma função a um serviço de nuvem do Azure](./media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a>Lendo uma função de um projeto de serviço de nuvem do Azure
Se você remove uma função de seu projeto de serviço de nuvem, mas decide posteriormente adicionar a função de volta ao projeto, somente a declaração de função e os atributos básicos, como informações de diagnóstico e pontos de extremidade são adicionados. Nenhum recurso ou referência adicional é adicionado ao `ServiceDefinition.csdef` arquivo ou ao arquivo `ServiceConfiguration.cscfg`. Se desejar adicionar essas informações, adicione-as manualmente nesses arquivos.

Por exemplo, você pode remover uma função de serviço Web e decidir posteriormente adicionar essa função de volta em sua solução. Se você fizer isso, ocorrerá um erro. Para evitar esse erro, é necessário adicionar o elemento `<LocalResources>` mostrado no XML a seguir ao arquivo `ServiceDefinition.csdef`. Use o nome da função de serviço Web que você adicionou novamente ao projeto como parte do atributo de nome para o elemento **<LocalStorage>** . Neste exemplo, o nome da função de serviço Web é **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Próximas etapas
- [Configurar as funções para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
