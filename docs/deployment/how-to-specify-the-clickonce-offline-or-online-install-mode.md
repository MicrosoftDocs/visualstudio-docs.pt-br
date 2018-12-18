---
title: 'Como: especificar o ClickOnce Offline ou Online de modo de instalação | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a1515d9b9b12d92f7189c1dda59659d6ea1c03d5
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39080167"
---
# <a name="how-to-specify-the-clickonce-offline-or-online-install-mode"></a>Como: especificar o ClickOnce off-line ou modo de instalação online
O `Install Mode` para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo determina se o aplicativo estará disponível offline ou online. Quando você escolhe **o aplicativo está disponível somente online**, o usuário deve ter acesso para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] local (uma página da Web ou um compartilhamento de arquivos) para executar o aplicativo de publicação. Quando você escolhe **o aplicativo está disponível também offline**, o aplicativo adiciona entradas para o **inicie** menu e o **adicionar ou remover programas** caixa de diálogo; o usuário é é possível executar o aplicativo quando eles não estão conectados.  
  
 O `Install Mode` podem ser definidos na **Publish** página da **Designer de projeto**.  
  
 **Observação** o `Install Mode` também podem ser definidas usando o Assistente de publicação. Para obter mais informações, consulte [como: publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).  
  
### <a name="to-make-a-clickonce-application-available-online-only"></a>Para disponibilizar um aplicativo ClickOnce online apenas  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  No **modo de instalação e as configurações** área, clique no **o aplicativo está disponível apenas online** botão de opção.  
  
### <a name="to-make-a-clickonce-application-available-online-or-offline"></a>Para disponibilizar um aplicativo ClickOnce online ou offline  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  No **modo de instalação e as configurações** área, clique no **o aplicativo está disponível também offline** botão de opção.  
  
     Quando instalado, o aplicativo adiciona entradas para o **inicie** menu e, ao **adicionar ou remover programas** no painel de controle.  
  
## <a name="see-also"></a>Consulte também  
 [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como: publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [Escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)