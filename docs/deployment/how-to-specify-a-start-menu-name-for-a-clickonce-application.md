---
title: Como especificar um nome do menu Iniciar para um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Start menu resource name
- Start menu name
- ClickOnce deployment, Start menu name
ms.assetid: 4b5183b2-2fd4-4433-9310-4a73bb12c4e3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 882d6f7471530a101404040368dbc6088e9b5d96
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381919"
---
# <a name="how-to-specify-a-start-menu-name-for-a-clickonce-application"></a>Como especificar um nome no menu Iniciar para um aplicativo ClickOnce
Quando um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo é instalado para uso online e offline, uma entrada é adicionada ao menu **Iniciar** e à lista **Adicionar ou remover programas** . Por padrão, o nome de exibição é o mesmo que o nome do assembly do aplicativo, mas você pode alterar o nome de exibição definindo o **nome do produto** na caixa de diálogo **Opções de publicação** .

 O **nome do produto** será exibido na página *publish.htm* ; para um aplicativo offline instalado, ele será o nome da entrada no menu **Iniciar** e também será o nome exibido em **Adicionar ou remover programas**.

 **O nome do editor** será exibido na página de *publish.htm* acima do **nome do produto**e, para um aplicativo offline instalado, ele também será o nome da pasta que contém o ícone do aplicativo no menu **Iniciar** .

 O atalho do menu iniciar ou a referência do aplicativo são criados em *%AppData%\Microsoft\Windows\Start iniciar\programas \\<nome \> do editor*. A referência de atalho ou de aplicativo tem o mesmo nome que o nome do produto.

 Você pode definir as **Propriedades nome do produto** e nome do **Editor** na caixa de diálogo **Opções de publicação** , disponível na página **publicar** do **Designer de projeto**.

### <a name="to-specify-a-start-menu-name"></a>Para especificar um nome do menu iniciar

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **Opções** para abrir a caixa de diálogo **Opções de publicação** .

4. Clique em **Descrição**.

5. Na caixa de diálogo **Opções de publicação** , digite o nome a ser exibido no **nome do produto**.

6. Opcionalmente, você pode inserir um nome de editor no **nome do editor**.

## <a name="see-also"></a>Veja também
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)