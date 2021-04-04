---
title: Atualizações automáticas de aplicativo usando a API de implantação do ClickOnce
description: Saiba como escrever código no ClickOnce que usa a classe ApplicationDeployment para verificar se há atualizações com base em um evento, como uma solicitação de usuário.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- application updates
ms.assetid: 1a886310-67c8-44e5-a382-c2f0454f887d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: db82151b7fd4dbe894cecf8fbf5f5b64cb2f5919
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213934"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>Como verificar se há atualizações do aplicativo programaticamente usando a API de implantação do ClickOnce
O ClickOnce fornece duas maneiras de atualizar um aplicativo quando ele é implantado. No primeiro método, você pode configurar a implantação do ClickOnce para verificar automaticamente se há atualizações em determinados intervalos. No segundo método, você pode escrever código que usa a <xref:System.Deployment.Application.ApplicationDeployment> classe para verificar se há atualizações com base em um evento, como uma solicitação de usuário.

 Os procedimentos a seguir mostram um código para executar uma atualização programática e também descrevem como configurar sua implantação do ClickOnce para habilitar verificações de atualização programática.

 Para atualizar um aplicativo ClickOnce programaticamente, você deve especificar um local para atualizações. Isso às vezes é chamado de provedor de implantação. Para obter mais informações sobre como definir essa propriedade, consulte [escolher uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md).

> [!NOTE]
> Você também pode usar a técnica descrita abaixo para implantar seu aplicativo de um local, mas atualizá-lo de outro. Para obter mais informações, consulte [como especificar um local alternativo para atualizações de implantação](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md).

### <a name="to-check-for-updates-programmatically"></a>Para verificar se há atualizações programaticamente

1. Crie um novo aplicativo Windows Forms usando sua linha de comando ou ferramentas visuais preferenciais.

2. Crie qualquer botão, item de menu ou outro item de interface do usuário que você deseja que os usuários selecionem para verificar se há atualizações. No manipulador de eventos desse item, chame o método a seguir para verificar e instalar atualizações.

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceAPI/CS/Form1.cs" id="Snippet6":::
    :::code language="cpp" source="../snippets/cpp/VS_Snippets_Winforms/ClickOnceAPI/cpp/form1.cpp" id="Snippet6":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceAPI/VB/Form1.vb" id="Snippet6":::

3. Compile seu aplicativo.

### <a name="use-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>Use Mage.exe para implantar um aplicativo que verifica atualizações programaticamente

- Siga as instruções para implantar seu aplicativo usando o Mage.exe, conforme explicado em [Walkthrough: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Ao chamar Mage.exe para gerar o manifesto de implantação, certifique-se de usar a opção de linha de comando `providerUrl` e para especificar a URL em que o ClickOnce deve verificar se há atualizações. Se o seu aplicativo for atualizado do `http://www.adatum.com/MyApp` , por exemplo, sua chamada para gerar o manifesto de implantação poderá ser assim:

    ```cmd
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application
    ```

### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>Usando MageUI.exe para implantar um aplicativo que verifica atualizações programaticamente

- Siga as instruções para implantar seu aplicativo usando o Mage.exe, conforme explicado em [Walkthrough: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Na guia **Opções de implantação** , defina o campo **local inicial** como o ClickOnce do manifesto do aplicativo deve verificar se há atualizações. Na guia **Opções de atualização** , desmarque a caixa de seleção **este aplicativo deve verificar** se há atualizações.

## <a name="net-framework-security"></a>Segurança do .NET Framework
 Seu aplicativo deve ter permissões de confiança total para usar a atualização programática.

## <a name="see-also"></a>Confira também
- [Como especificar um local alternativo para atualizações de implantação](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)
- [Escolher uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md)
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)