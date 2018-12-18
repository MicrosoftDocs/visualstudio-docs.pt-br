---
title: 'Como: definir uma zona de segurança para um aplicativo ClickOnce | Microsoft Docs'
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
- ClickOnce deployment, security settings
- code access security, ClickOnce applications
- security zones, ClickOnce applications
ms.assetid: d3dac454-518a-44d7-a76e-ccb7b9c3a150
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 58924d86126d12e0d278c890f8721e665a7cb5ac
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49298409"
---
# <a name="how-to-set-a-security-zone-for-a-clickonce-application"></a>Como definir uma zona de segurança para um aplicativo ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao definir permissões de segurança para um aplicativo ClickOnce de acesso do código, você precisa para começar com um conjunto básico de permissões na **segurança** página do **Designer de projeto**.  
  
 Na maioria dos casos, você também pode escolher o **Internet** zona que contém um conjunto limitado de permissões, ou o **Intranet Local** zona que contém um conjunto maior de permissões. Se seu aplicativo exigir permissões personalizadas, você pode fazer isso escolhendo os **personalizado** zona de segurança. Para obter mais informações sobre como definir permissões personalizadas, consulte [como: definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md).  
  
### <a name="to-set-a-security-zone"></a>Para definir uma zona de segurança  
  
1.  Com um projeto selecionado no **Gerenciador de soluções**diante a **Project** menu, clique em **propriedades**.  
  
2.  Clique na guia **Segurança**.  
  
3.  Selecione o **Habilitar configurações de segurança do ClickOnce** caixa de seleção.  
  
4.  Selecione o **este é um aplicativo de confiança parcial** botão de opção.  
  
     Os controles na **permissões de segurança do ClickOnce** seção estão habilitados.  
  
5.  No **seu aplicativo será instalado a partir de zona** lista suspensa, selecione uma zona de segurança.  
  
## <a name="see-also"></a>Consulte também  
 [Como definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)   
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)



