---
title: Como habilitar as configurações de segurança do ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- security [Visual Studio], ClickOnce applications
- ClickOnce deployment, security settings
- security settings, ClickOnce deployment
ms.assetid: 73cd3e9d-cd72-4ad2-8cae-94d6bb6b01e0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d673edac957e9625f7d948fbe766ee08b23b6b52
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382426"
---
# <a name="how-to-enable-clickonce-security-settings"></a>Como habilitar configurações de segurança do ClickOnce
A segurança de acesso do código para aplicativos ClickOnce deve ser habilitada para publicar o aplicativo. Isso é feito automaticamente quando você publica um aplicativo usando o assistente de publicação.

 Em alguns casos, a habilitação da segurança de acesso a código pode afetar o desempenho ao criar ou depurar seu aplicativo; nesses casos, talvez você queira desabilitar temporariamente as configurações de segurança.

 As configurações de segurança do ClickOnce podem ser habilitadas ou desabilitadas na página **segurança** do **Designer de projeto**.

### <a name="to-enable-clickonce-security-settings"></a>Para habilitar as configurações de segurança do ClickOnce

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Segurança**.

3. Marque a caixa de seleção **Habilitar configurações de segurança do ClickOnce** .

     Agora você pode personalizar as configurações de segurança para seu aplicativo na página segurança.

    > [!NOTE]
    > Essa caixa de seleção é selecionada automaticamente toda vez que o aplicativo é publicado com o assistente de **publicação** .

### <a name="to-disable-clickonce-security-settings"></a>Para desabilitar as configurações de segurança do ClickOnce

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Segurança**.

3. Desmarque a caixa de seleção **Habilitar configurações de segurança do ClickOnce** .

     Seu aplicativo será executado com as configurações de segurança de confiança total; as configurações na página **segurança** serão ignoradas.

    > [!NOTE]
    > Cada vez que o aplicativo é publicado com o assistente de publicação, essa caixa de seleção será selecionada; Você deve limpá-lo novamente após a publicação bem-sucedida.

## <a name="see-also"></a>Veja também
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)
- [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)
