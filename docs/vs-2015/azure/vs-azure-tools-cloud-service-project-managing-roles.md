---
title: Gerenciando funções nos serviços de nuvem do Azure com o Visual Studio | Microsoft Docs
description: Saiba como adicionar e remover funções nos serviços de nuvem do Azure com o Visual Studio.
author: ghogen
manager: douge
assetId: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: 35221cbf98f26a71e2b4adf0a7178342616ff7c0
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001302"
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Gerenciando funções nos serviços de nuvem do Azure com o Visual Studio
Depois de criar seu serviço de nuvem do Azure, você pode adicionar novas funções a ele ou remover funções existentes. Você também pode importar um projeto existente e convertê-lo em uma função. Por exemplo, você pode importar um aplicativo web ASP.NET e designá-lo como uma função web.

## <a name="adding-a-role-to-an-azure-cloud-service"></a>Adicionar uma função a um serviço de nuvem do Azure
As etapas a seguir explicarão como adicionar uma função web ou de trabalho para um projeto de serviço de nuvem do Azure no Visual Studio.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, expanda o nó do projeto

1. Clique com botão direito do **funções** nó para exibir o menu de contexto. No menu de contexto, selecione **adicionar**, em seguida, selecione uma função web existente ou a função de trabalho da solução atual ou criar um projeto de função web ou de trabalho. Você também pode selecionar um projeto apropriado, como um projeto de aplicativo web ASP.NET e associá-lo a um projeto de função.

    ![Opções de menu para adicionar uma função a um projeto de serviço de nuvem do Azure](./media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Remoção de uma função de um serviço de nuvem do Azure
As etapas a seguir explicarão como remover uma função web ou de trabalho de um projeto de serviço de nuvem do Azure no Visual Studio.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, expanda o nó do projeto

1. Expanda o **funções** nó.

1. Clique com botão direito no nó que você deseja remover e, no menu de contexto, selecione **remover**. 

    ![Opções de menu para adicionar uma função a um serviço de nuvem do Azure](./media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a>Lendo uma função a um projeto de serviço de nuvem do Azure
Se você remove uma função de seu projeto de serviço de nuvem, mas decide posteriormente adicionar a função de volta para o projeto, somente a declaração de função e os atributos básicos, como informações de diagnóstico e pontos de extremidade são adicionados. Nenhuma referência ou recursos adicionais é adicionada para o `ServiceDefinition.csdef` arquivo ou para o `ServiceConfiguration.cscfg` arquivo. Se você quiser adicionar essas informações, você precisará adicioná-lo manualmente nesses arquivos.

Por exemplo, você pode remover uma função de serviço web e decidir posteriormente adicionar essa função de volta em sua solução. Se você fizer isso, ocorrerá um erro. Para evitar esse erro, você precisa adicionar o `<LocalResources>` elemento mostrado no seguinte XML de volta para o `ServiceDefinition.csdef` arquivo. Use o nome da função de serviço web que você adicionou novamente ao projeto como parte do nome do atributo para o **<LocalStorage>** elemento. Neste exemplo, é o nome da função de serviço web **WCFServiceWebRole1**.

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
- [Configure as funções para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
