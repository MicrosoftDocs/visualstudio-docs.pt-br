---
title: 'Como: automaticamente incrementar a publicação do ClickOnce versão | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], incrementing publish version automatically
- Publish Version property, incrementing
- ClickOnce deployment, incrementing publish version automatically
- publishing, ClickOnce
ms.assetid: 686ab88a-6305-4914-a05b-fe269cc0ae1e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: ac5b4e67c0bbebba7586715e4ba491bf11bacc4a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49300216"
---
# <a name="how-to-automatically-increment-the-clickonce-publish-version"></a>Como incrementar a versão da publicação do ClickOnce automaticamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao publicar uma [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo, alterando o `Publish Version` propriedade faz com que o aplicativo a ser publicado como uma atualização. Por padrão, o Visual Studio incrementa automaticamente o `Revision` número das `Publish Version` cada vez que você publica o aplicativo.  
  
 Você pode desativar esse comportamento na **Publish** página do **Designer de projeto**.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-disable-automatically-incrementing-the-publish-version"></a>Para desabilitar automaticamente incrementando a versão de publicação  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  No **Publish Version** seção, desmarque as **incrementar automaticamente a revisão com cada versão** caixa de seleção.  
  
## <a name="see-also"></a>Consulte também  
 [Como definir a versão da publicação do ClickOnce](../deployment/how-to-set-the-clickonce-publish-version.md)   
 [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como publicar um aplicativo ClickOnce usando o Assistente de Publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)



