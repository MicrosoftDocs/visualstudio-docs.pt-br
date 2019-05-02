---
title: 'Como: Instalar pré-requisitos com um aplicativo ClickOnce | Microsoft Docs'
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434076"
---
# <a name="how-to-install-prerequisites-with-a-clickonce-application"></a>Como: Instalar pré-requisitos com um aplicativo ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Todos os [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos exigem que a versão correta do .NET Framework está instalada em um computador antes que eles possam ser executados; muitos aplicativos têm também outros pré-requisitos. Ao publicar um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo, você pode escolher um conjunto de componentes de pré-requisitos sejam empacotados juntamente com seu aplicativo. No momento da instalação, uma verificação será executada para cada pré-requisito determinar se ele já existe; Se não, ele será instalado antes de instalar o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo.  
  
 Em vez de empacotamento e publicação de pré-requisitos, você também pode especificar um local de download para os componentes. Por exemplo, em vez de incluir pré-requisitos com todos os aplicativos que você publicar, você pode usar um compartilhamento de arquivos centralizado ou o local da Web que contém os instaladores para todos os seus pré-requisitos — no momento da instalação, os componentes serão baixados e instalado a partir desse local.  
  
> [!IMPORTANT]
> Você deve adicionar pacotes de instalador de pré-requisitos para seu computador de desenvolvimento antes de publicar seu primeiro [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo. Para obter mais informações, confira [Como: Incluir pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-include-prerequisites-with-a-clickonce-application.md).  
  
 Pré-requisitos são gerenciados na **pré-requisitos** caixa de diálogo, acessível a partir o **publicar** painel do **Project Designer**.  
  
> [!NOTE]
> Além da lista predeterminada de pré-requisitos, você pode adicionar seus próprios componentes à lista. Para obter mais informações, consulte [criação de pacotes de Bootstrapper](../deployment/creating-bootstrapper-packages.md).  
  
### <a name="to-specify-prerequisites-to-install-with-a-clickonce-application"></a>Para especificar os pré-requisitos para instalar com um aplicativo ClickOnce  
  
1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2. Selecione o **publicar** painel.  
  
3. Clique o **pré-requisitos** para abrir o **pré-requisitos** caixa de diálogo.  
  
4. Na caixa de diálogo **Pré-requisitos**, verifique se a caixa de seleção **Criar programa de instalação para instalar os componentes dos pré-requisitos** está marcada.  
  
5. No **pré-requisitos** lista, verifique os componentes que você deseja instalar e, em seguida, clique em **Okey**.  
  
     Os componentes selecionados serão empacotados e publicados junto com seu aplicativo.  
  
### <a name="to-specify-a-different-download-location-for-prerequisites"></a>Para especificar um local de download diferentes para pré-requisitos  
  
1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2. Selecione o **publicar** painel.  
  
3. Clique o **pré-requisitos** para abrir o **pré-requisitos** caixa de diálogo.  
  
4. Na caixa de diálogo **Pré-requisitos**, verifique se a caixa de seleção **Criar programa de instalação para instalar os componentes dos pré-requisitos** está marcada.  
  
5. No **especifique o local de instalação de pré-requisitos** seção, selecione **baixar os pré-requisitos no seguinte local**.  
  
6. Selecione um local na lista suspensa, ou digite uma URL, o caminho do arquivo ou o local do FTP e, em seguida, clique em **Okey.**  
  
    > [!NOTE]
    > Certifique-se de que os instaladores para os componentes especificados existem no local especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como: Publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
