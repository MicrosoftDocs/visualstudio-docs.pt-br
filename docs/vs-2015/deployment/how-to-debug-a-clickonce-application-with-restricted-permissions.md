---
title: 'Como: depurar um aplicativo ClickOnce com permissões restritas | Microsoft Docs'
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
- debugging [Visual Studio], ClickOnce applications
- ClickOnce deployment, debugging
- ClickOnce applications, debugging
ms.assetid: 6991ea91-5253-451b-923d-22273a3d38b1
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: d01cf2be1bef794f5aeb74b86d041408fa40ce4a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49209528"
---
# <a name="how-to-debug-a-clickonce-application-with-restricted-permissions"></a>Como depurar um aplicativo ClickOnce com permissões restritas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Como desenvolvedor, você provavelmente está executando seu computador de desenvolvimento com permissões de confiança total, portanto, você não verá as exceções de segurança mesmo quando estiver depurando um aplicativo ClickOnce que o usuário final poderá ver ao executá-lo com permissões restritas.  
  
 Para capturar essas exceções, você precisa depurar o aplicativo com as mesmas permissões que o usuário final. Depuração com permissões restritas pode ser habilitada no **segurança** página do **Designer de projeto**.  
  
 Além disso, quando você desenvolve aplicativos que chamam serviços da Web, esses serviços da Web geralmente residem em seu computador de desenvolvimento. Uma vez implantado, o usuário final acessará esses serviços Web de uma URL diferente. Para emular a experiência do usuário final durante a depuração, você pode especificar que uma URL e o depurador tratará os serviços Web como se eles estavam sendo chamados de URL.  
  
### <a name="to-enable-debugging-with-restricted-permissions"></a>Para habilitar a depuração com permissões restritas  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  No **Designer de projeto**, clique no **segurança** guia.  
  
3.  Selecione o **habilitar a configuração de segurança do ClickOnce** caixa de seleção e, em seguida, clique no **esse é um aplicativo de confiança parcial** botão de opção.  
  
4.  Clique no botão **Avançado**.  
  
5.  Selecione o **depurar este aplicativo com o conjunto de permissões selecionado** caixa de seleção e, em seguida, clique em **Okey**.  
  
     Quando você depura o aplicativo, qualquer tentativa de acessar uma permissão que não faz parte do conjunto de permissões irá gerar uma exceção de segurança.  
  
### <a name="to-specify-a-url-for-debugging"></a>Para especificar uma URL de depuração  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  No **Designer de projeto**, clique no **segurança** guia.  
  
3.  Selecione o **habilitar a configuração de segurança do ClickOnce** caixa de seleção e, em seguida, clique no **esse é um aplicativo de confiança parcial** botão de opção.  
  
4.  Clique no botão **Avançado**.  
  
5.  Selecione o **depurar este aplicativo com o conjunto de permissões selecionado** caixa de seleção e, em seguida, clique em **Okey**.  
  
6.  No **depurar este aplicativo como se ele tivesse sido baixado da URL a seguir** caixa de texto, insira uma URL ou caminho de rede.  
  
## <a name="see-also"></a>Consulte também  
 [Como definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)   
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)



