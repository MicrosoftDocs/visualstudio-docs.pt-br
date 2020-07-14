---
title: Como gerenciar atualizações para um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.Update
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, managing applications
- ClickOnce deployment, updates
- updating data, ClickOnce
- application updates
ms.assetid: a3f23f05-e7f1-4620-b23c-2d68f9643684
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 534171d9145d0a21fee7f8831e9a6355e6079cbd
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382348"
---
# <a name="how-to-manage-updates-for-a-clickonce-application"></a>Como gerenciar atualizações em um aplicativo ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]os aplicativos podem verificar se há atualizações automaticamente ou programaticamente. Como desenvolvedor, você tem muita flexibilidade para especificar quando e como as verificações de atualização são executadas, se as atualizações são obrigatórias e onde o aplicativo deve verificar se há atualizações.

 Você pode configurar o aplicativo para verificar se há atualizações automaticamente antes do início do aplicativo ou em intervalos definidos após o início do aplicativo. Além disso, você pode especificar uma versão mínima necessária; ou seja, uma atualização será instalada se a versão do usuário for menor do que a versão necessária.

 Você pode configurar o aplicativo para verificar se há atualizações programaticamente com base em um evento, como uma solicitação de usuário. O procedimento "para verificar se há atualizações programaticamente" neste tópico mostra como você escreveria um código que usa a <xref:System.Deployment.Application.ApplicationDeployment> classe para verificar se há atualizações com base em um evento.

 Você também pode implantar seu aplicativo de um local e atualizá-lo de outro. Consulte o procedimento "para especificar um local de atualização diferente".

 Para obter mais informações, confira [Escolhendo uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md).

 O comportamento da atualização é gerenciado na caixa de diálogo **atualizações do aplicativo** , disponível na página **publicar** do **Designer de projeto.**

### <a name="to-check-for-updates-before-the-application-starts"></a>Para verificar se há atualizações antes de iniciar o aplicativo

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **atualizações** para abrir a caixa de diálogo **atualizações do aplicativo** .

4. Na caixa de diálogo **atualizações do aplicativo** , verifique se a caixa de seleção **o aplicativo deve verificar** se há atualizações está marcada.

5. Na seção **escolher quando o aplicativo deve verificar se há atualizações** , selecione **antes de o aplicativo ser iniciado**. Isso garante que os usuários conectados à rede sempre executem o aplicativo com as atualizações mais recentes.

### <a name="to-check-for-updates-in-the-background-after-the-application-starts"></a>Para verificar atualizações em segundo plano, depois que o aplicativo é iniciado

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **atualizações** para abrir a caixa de diálogo **atualizações do aplicativo** .

4. Na caixa de diálogo **atualizações do aplicativo** , verifique se a caixa de seleção **o aplicativo deve verificar** se há atualizações está selecionada.

5. Na **seção escolher quando o aplicativo deve verificar se há atualizações**, selecione **depois que o aplicativo for iniciado**. O aplicativo será iniciado mais rapidamente dessa maneira e, em seguida, verificará se há atualizações em segundo plano e somente notificará o usuário quando uma atualização estiver disponível. Uma vez instaladas, as atualizações não terão efeito até que o aplicativo seja reiniciado.

6. Na seção **especificar com que frequência o aplicativo deve verificar se há atualizações** , selecione **verificar sempre que o aplicativo for executado** (o padrão) ou **verificar a cada** e insira um número e um intervalo de tempo.

### <a name="to-specify-a-minimum-required-version-for-the-application"></a>Para especificar uma versão mínima necessária para o aplicativo

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **atualizações** para abrir a caixa de diálogo **atualizações do aplicativo** .

4. Na caixa de diálogo **atualizações do aplicativo** , verifique se a caixa de seleção **o aplicativo deve verificar** se há atualizações está marcada.

5. Marque a caixa de seleção **especificar uma versão mínima necessária para este aplicativo** e insira os números **principal**, **secundário**, de **compilação**e de **revisão** para o aplicativo.

### <a name="to-specify-a-different-update-location"></a>Para especificar um local de atualização diferente

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **atualizações** para abrir a caixa de diálogo **atualizações do aplicativo** .

4. Na caixa de diálogo **atualizações do aplicativo** , verifique se a caixa de seleção **o aplicativo deve verificar** se há atualizações está marcada.

5. No campo **local de atualização** , insira o local de atualização com uma URL totalmente qualificada, usando o formato *http://Hostname/ApplicationName* ou um caminho UNC usando o formato * \\ \Server\ApplicationName*, ou clique no botão **procurar** para procurar o local de atualização.

### <a name="to-check-for-updates-programmatically"></a>Para verificar se há atualizações programaticamente

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **atualizações** para abrir a caixa de diálogo **atualizações do aplicativo** .

4. Na caixa de diálogo **atualizações do aplicativo** , verifique se a caixa de seleção **o aplicativo deve verificar** se há atualizações está desmarcada. (Opcionalmente, você pode marcar essa caixa de seleção para verificar se há atualizações programaticamente e também permitir que o tempo de execução do ClickOnce faça atualizações automaticamente.)

5. No campo **local de atualização** , insira o local de atualização com uma URL totalmente qualificada, usando o formato *http://Hostname/ApplicationName* ou um caminho UNC usando o formato * \\ \Server\ApplicationName*, ou clique no botão **procurar** para procurar o local de atualização. O local de atualização é onde o aplicativo procurará uma versão atualizada de si mesmo.

6. Crie um botão, um item de menu ou outro item de interface do usuário em um formulário do Windows que os usuários selecionarão para verificar se há atualizações. Do manipulador de eventos desse item, chame um método para verificar e instalar atualizações. Você pode encontrar um exemplo de código do Visual Basic e do Visual C# para tal método em [como: verificar se há atualizações de aplicativos programaticamente usando a API de implantação do ClickOnce](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md).

7. Compile seu aplicativo.

## <a name="see-also"></a>Veja também
- <xref:System.Deployment.Application.ApplicationDeployment>
- [Caixa de diálogo Atualizações do aplicativo](/previous-versions/visualstudio/visual-studio-2010/axw1fa38(v=vs.100))
- [Escolher uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md)
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [Como verificar se há atualizações do aplicativo programaticamente usando a API de implantação do ClickOnce](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)
