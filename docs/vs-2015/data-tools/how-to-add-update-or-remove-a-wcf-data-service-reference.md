---
title: 'Como: adicionar, atualizar ou remover uma referência de serviço do WCF Data | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- service references [Visual Studio]
- WCF Data Service reference
- WCF data service references
- ADO.NET service references
- ADO.NET Data Service reference
ms.assetid: 892ebf37-3af4-472e-8744-92837677d611
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b14a83b195809dff89fa89bb6fcf91050e2f8a0c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49192251"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>Como adicionar, atualizar ou remover uma referência de WCF Data Services
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Um *referência de serviço* permite que um projeto para acessar um ou mais [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]. Use o **adicionar referência de serviço** caixa de diálogo para pesquisar [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] na solução atual, localmente, em uma rede local ou na Internet.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="adding-a-service-reference"></a>Adicionando uma referência de serviço  
  
#### <a name="to-add-a-reference-to-an-external-service"></a>Para adicionar uma referência para um serviço externo  
  
1.  Na **Gerenciador de soluções**, clique no nome do projeto que você deseja adicionar o serviço e, em seguida, clique em **Add Service Reference**.  
  
     O **adicionar referência de serviço** caixa de diálogo é exibida.  
  
2.  No **endereço** caixa, digite a URL para o serviço e, em seguida, clique em **vá** para procurar o serviço. Se o serviço implementar segurança de nome e a senha do usuário, você será solicitado um nome de usuário e senha.  
  
    > [!NOTE]
    >  Você só deve fazer referência a serviços de uma fonte confiável. A adição de referências de uma fonte não confiável pode comprometer a segurança.  
  
     Você também pode selecionar a URL do **endereço** lista, que armazena as URLs de 15 anteriores na qual os metadados de serviço válido foi encontrado.  
  
     Uma barra de progresso é exibida quando a pesquisa está sendo executada. Você pode parar a pesquisa a qualquer momento clicando **parar**.  
  
3.  No **Services** lista, expanda o nó para o serviço que você deseja usar e selecione um conjunto de entidades.  
  
4.  No **Namespace** , digite o namespace que você deseja usar para a referência.  
  
5.  Clique em **Okey** para adicionar a referência ao projeto.  
  
     Um cliente de serviço (proxy) é gerado e metadados que descrevem o serviço é adicionado ao arquivo App. config.  
  
#### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>Para adicionar uma referência a um serviço na solução atual  
  
1.  Na **Gerenciador de soluções**, clique no nome do projeto que você deseja adicionar o serviço e, em seguida, clique em **Add Service Reference**.  
  
     O **adicionar referência de serviço** caixa de diálogo é exibida.  
  
2.  Clique em **descobrir**.  
  
     Todos os serviços (ambos [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] e os serviços WCF) na solução atual são adicionados para o **serviços** lista.  
  
3.  No **Services** lista, expanda o nó para o serviço que você deseja usar e selecione um conjunto de entidades.  
  
4.  No **Namespace** , digite o namespace que você deseja usar para a referência.  
  
5.  Clique em **Okey** para adicionar a referência ao projeto.  
  
     Um cliente de serviço (proxy) é gerado e metadados que descrevem o serviço é adicionado ao arquivo App. config.  
  
## <a name="updating-a-service-reference"></a>Atualizando uma referência de serviço  
 O modelo de dados de entidade para um [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] , às vezes, será alterado. Quando isso acontece, a referência de serviço deve ser atualizada.  
  
#### <a name="to-update-a-service-reference"></a>Para atualizar uma referência de serviço  
  
-   Na **Gerenciador de soluções**, a referência de serviço com o botão direito e, em seguida, clique em **Update Service Reference**.  
  
     Uma caixa de diálogo de progresso é exibida enquanto a referência é atualizada de seu local original e o cliente do serviço for gerado novamente para refletir quaisquer alterações nos metadados.  
  
## <a name="removing-a-service-reference"></a>Remover uma referência de serviço  
 Se uma referência de serviço não estiver sendo usada, remova-a da sua solução.  
  
#### <a name="to-remove-a-service-reference"></a>Para remover uma referência de serviço  
  
-   Na **Gerenciador de soluções**, a referência de serviço com o botão direito e, em seguida, clique em **excluir**.  
  
     O cliente do serviço será removido da solução e os metadados que descrevem o serviço serão removido do arquivo App. config.  
  
    > [!NOTE]
    >  Qualquer código que faz referência a referência de serviço precisará ser removido manualmente.  
  
## <a name="see-also"></a>Consulte também  
 [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

