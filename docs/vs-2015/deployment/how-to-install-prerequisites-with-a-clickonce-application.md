---
title: 'Como: instalar pré-requisitos com um aplicativo ClickOnce | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], prerequisites
- prerequisites, ClickOnce
- components, bootstrapping
ms.assetid: e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 18c8dd4d0bc79ac2f3af44b8b5f8dd6faacb9f45
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "90838395"
---
# <a name="how-to-install-prerequisites-with-a-clickonce-application"></a>Como instalar pré-requisitos com um aplicativo ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Todos os [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos exigem que a versão correta do .NET Framework seja instalada em um computador antes que possam ser executadas; muitos aplicativos também têm outros pré-requisitos. Ao publicar um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo, você pode escolher um conjunto de componentes de pré-requisito para ser empacotado junto com seu aplicativo. No momento da instalação, uma verificação será executada para cada pré-requisito para determinar se ele já existe; Se não for, ele será instalado antes da instalação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo.  
  
 Em vez de empacotar e publicar os pré-requisitos, você também pode especificar um local de download para os componentes. Por exemplo, em vez de incluir pré-requisitos em cada aplicativo publicado, você pode usar um compartilhamento de arquivos centralizado ou um local da Web que contenha os instaladores para todos os seus pré-requisitos — no momento da instalação, os componentes serão baixados e instalados nesse local.  
  
> [!IMPORTANT]
> Você deve adicionar pacotes de instalador de pré-requisito ao seu computador de desenvolvimento antes de publicar seu primeiro [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo. Para obter mais informações, consulte [como: incluir pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-include-prerequisites-with-a-clickonce-application.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como publicar um Aplicativo ClickOnce usando o Assistente de Publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
