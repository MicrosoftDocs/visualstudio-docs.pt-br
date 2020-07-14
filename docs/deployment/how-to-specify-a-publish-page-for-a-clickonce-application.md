---
title: Como especificar uma página de publicação para um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying publish page
- Publish Page property
- publishing, ClickOnce
- ClickOnce deployment, specifying publish page
ms.assetid: 9d70eebb-bdee-4b42-8e7e-7a07e199bdf7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: acf7178a6b5456d048421533b8497682d69c2ee0
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381958"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>Como especificar uma página de publicação para um aplicativo ClickOnce
Ao publicar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo, uma página da Web padrão (publish.htm) é gerada e publicada junto com o aplicativo. Esta página contém o nome do aplicativo, um link para instalar o aplicativo e/ou quaisquer pré-requisitos e um link para um tópico da ajuda que descreve [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] . A propriedade **Publicar página** para seu projeto permite que você especifique um nome para a página da Web para seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo.

 Depois que a página de publicação for especificada, na próxima vez que você publicá-la, ela será copiada para o local de publicação; Ele não será substituído se você publicar novamente. Se você quiser personalizar a aparência da página, poderá fazer isso sem se preocupar com a perda de suas alterações. Para obter mais informações, consulte [como: personalizar a página da Web padrão do ClickOnce](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md).

 A propriedade **Publicar página** pode ser definida na caixa de diálogo **Opções de publicação** , acessível no painel **publicar** do designer de **projeto**.

### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>Para especificar uma página da Web personalizada para um aplicativo ClickOnce

1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2. Selecione o painel **publicar** .

3. Clique no botão **Opções** para abrir a caixa de diálogo **Opções de publicação** .

4. Clique em **Implantação**.

5. Na caixa de diálogo **Opções de publicação** , certifique-se de que a caixa de seleção **abrir página da Web de implantação após a publicação** esteja marcada (ela deve ser selecionada por padrão).

6. Na caixa **da página da Web de implantação** , digite o nome da página da Web e clique em **OK**.

### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>Para impedir que a página publicar seja iniciada cada vez que você publicar

1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2. Selecione o painel **publicar** .

3. Clique no botão **Opções** para abrir a caixa de diálogo **Opções de publicação** .

4. Clique em **Implantação**.

5. Na caixa de diálogo **Opções de publicação** , desmarque a caixa de seleção **abrir página da Web de implantação após a publicação** .

## <a name="see-also"></a>Veja também
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [Como personalizar a página da Web padrão do ClickOnce](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)