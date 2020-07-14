---
title: Como especificar o modo de instalação do ClickOnce offline ou online | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, specifying install mode
- install mode
- online applications
- offline applications
- ClickOnce install mode
ms.assetid: 0aee5fc1-e966-4bda-9b8f-d9997aeaa779
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dcd9eeedfdd2a4661e3744da369a6fadc11039a3
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381750"
---
# <a name="how-to-specify-the-clickonce-offline-or-online-install-mode"></a>Como especificar o modo de instalação offline ou online do ClickOnce
O `Install Mode` para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo determina se o aplicativo estará disponível offline ou online. Quando você escolhe **o aplicativo está disponível somente online**, o usuário deve ter acesso ao [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] local de publicação (uma página da Web ou um compartilhamento de arquivos) para executar o aplicativo. Quando você escolhe **o aplicativo também está disponível offline**, o aplicativo adiciona entradas ao menu **Iniciar** e à caixa de diálogo **Adicionar ou remover programas** ; o usuário é capaz de executar o aplicativo quando não está conectado.

O `Install Mode` pode ser definido na página **publicar** do designer de **projeto**.

> [!NOTE]
> O `Install Mode` também pode ser definido usando o assistente de publicação. Para obter mais informações, consulte [como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).

### <a name="to-make-a-clickonce-application-available-online-only"></a>Para tornar um aplicativo ClickOnce disponível somente online

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Na área **modo de instalação e configurações** , clique no botão **de opção o aplicativo está disponível somente online** .

### <a name="to-make-a-clickonce-application-available-online-or-offline"></a>Para tornar um aplicativo ClickOnce disponível online ou offline

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Na área **modo de instalação e configurações** , clique no botão **de opção o aplicativo está disponível offline também** .

     Quando instalado, o aplicativo adiciona entradas ao menu **Iniciar** e **adiciona ou remove programas** no painel de controle.

## <a name="see-also"></a>Veja também
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [Escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)