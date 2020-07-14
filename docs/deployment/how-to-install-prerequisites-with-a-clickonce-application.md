---
title: Como instalar pré-requisitos com um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], prerequisites
- prerequisites, ClickOnce
- components, bootstrapping
ms.assetid: e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce4ad97439d330a6fc51e741e9ea05ef53a5798a
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382374"
---
# <a name="how-to-install-prerequisites-with-a-clickonce-application"></a>Como instalar pré-requisitos com um aplicativo ClickOnce
Todos os [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos exigem que a versão correta do .NET Framework seja instalada em um computador antes que possam ser executadas; muitos aplicativos também têm outros pré-requisitos. Ao publicar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo, você pode escolher um conjunto de componentes de pré-requisito para ser empacotado junto com seu aplicativo. No momento da instalação, uma verificação será executada para cada pré-requisito para determinar se ele já existe; Se não for, ele será instalado antes da instalação do [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo.

 Em vez de empacotar e publicar os pré-requisitos, você também pode especificar um local de download para os componentes. Por exemplo, em vez de incluir pré-requisitos em cada aplicativo publicado, você pode usar um compartilhamento de arquivos centralizado ou um local da Web que contenha os instaladores para todos os seus pré-requisitos — no momento da instalação, os componentes serão baixados e instalados nesse local.

> [!IMPORTANT]
> Você deve adicionar pacotes de instalador de pré-requisito ao seu computador de desenvolvimento antes de publicar seu primeiro [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. Para obter mais informações, consulte [como: incluir pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-include-prerequisites-with-a-clickonce-application.md).

 Os pré-requisitos são gerenciados na caixa de diálogo **pré-requisitos** , acessíveis no painel de **publicação** do **Designer de projeto**.

> [!NOTE]
> Além da lista predeterminada de pré-requisitos, você pode adicionar seus próprios componentes à lista. Para obter mais informações, consulte [Creating bootstrapper Packages](../deployment/creating-bootstrapper-packages.md).

### <a name="to-specify-prerequisites-to-install-with-a-clickonce-application"></a>Para especificar os pré-requisitos para instalar com um aplicativo ClickOnce

1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2. Selecione o painel **publicar** .

3. Clique no botão **pré-requisitos** para abrir a caixa de diálogo **pré-requisitos** .

4. Na caixa de diálogo **Pré-requisitos**, verifique se a caixa de seleção **Criar programa de instalação para instalar os componentes dos pré-requisitos** está marcada.

5. Na lista **pré-requisitos** , verifique os componentes que você deseja instalar e clique em **OK**.

     Os componentes selecionados serão empacotados e publicados junto com seu aplicativo.

### <a name="to-specify-a-different-download-location-for-prerequisites"></a>Para especificar um local de download diferente para os pré-requisitos

1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2. Selecione o painel **publicar** .

3. Clique no botão **pré-requisitos** para abrir a caixa de diálogo **pré-requisitos** .

4. Na caixa de diálogo **Pré-requisitos**, verifique se a caixa de seleção **Criar programa de instalação para instalar os componentes dos pré-requisitos** está marcada.

5. Na seção **especificar o local de instalação para os pré-requisitos** , selecione **baixar pré-requisitos no seguinte local**.

6. Selecione um local na lista suspensa ou insira uma URL, um caminho de arquivo ou um local de FTP e clique em **OK.**

    > [!NOTE]
    > Você deve verificar se os instaladores para os componentes especificados existem no local especificado.

## <a name="see-also"></a>Veja também
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)