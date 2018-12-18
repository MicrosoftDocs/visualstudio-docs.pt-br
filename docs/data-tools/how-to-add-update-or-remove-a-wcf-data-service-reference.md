---
title: Como adicionar, atualizar ou remover uma referência de WCF Data Services
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- service references [Visual Studio]
- WCF Data Service reference
- WCF data service references
- ADO.NET service references
- ADO.NET Data Service reference
ms.assetid: 892ebf37-3af4-472e-8744-92837677d611
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 9099c1ee0b1ed3af108c11792f7629453dfbf7c6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49819030"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>Como: adicionar, atualizar ou remover uma referência de serviço de dados do WCF
Um *referência de serviço* permite que um projeto para acessar um ou mais [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]. Use o **adicionar referência de serviço** caixa de diálogo para pesquisar [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] na solução atual, localmente, em uma rede local ou na Internet.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-service-reference"></a>Adicionar uma referência de serviço

### <a name="to-add-a-reference-to-an-external-service"></a>Para adicionar uma referência para um serviço externo

1.  Na **Gerenciador de soluções**, clique no nome do projeto ao qual você deseja adicionar o serviço e, em seguida, clique em **Add Service Reference**.

     O **adicionar referência de serviço** caixa de diálogo é exibida.

2.  No **endereço** caixa, digite a URL para o serviço e, em seguida, clique em **vá** para procurar o serviço. Se o serviço implementar segurança de nome e a senha do usuário, você será solicitado um nome de usuário e senha.

    > [!NOTE]
    >  Você só deve fazer referência a serviços de uma fonte confiável. A adição de referências de uma fonte não confiável pode comprometer a segurança.

     Você também pode selecionar a URL do **endereço** lista, que armazena as URLs de 15 anteriores na qual os metadados de serviço válido foi encontrado.

     Uma barra de progresso exibe quando a pesquisa está sendo executada. Você pode parar a pesquisa a qualquer momento clicando **parar**.

3.  No **Services** lista, expanda o nó para o serviço que você deseja usar e selecione um conjunto de entidades.

4.  No **Namespace** , digite o namespace que você deseja usar para a referência.

5.  Clique em **Okey** para adicionar a referência ao projeto.

     Um cliente de serviço (proxy) é gerado e metadados que descrevem o serviço é adicionado para o *App. config* arquivo.

### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>Para adicionar uma referência a um serviço na solução atual

1. Na **Gerenciador de soluções**, clique no nome do projeto ao qual você deseja adicionar o serviço e, em seguida, clique em **Add Service Reference**.

    O **adicionar referência de serviço** caixa de diálogo é exibida.

2. Clique em **descobrir**.

    Todos os serviços (ambos [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] e os serviços WCF) na solução atual são adicionados para o **serviços** lista.

3. No **Services** lista, expanda o nó para o serviço que você deseja usar e selecione um conjunto de entidades.

4. No **Namespace** , digite o namespace que você deseja usar para a referência.

5. Clique em **Okey** para adicionar a referência ao projeto.

    Gera um cliente de serviço (proxy), e metadados que descrevem o serviço é adicionado para o *App. config* arquivo.

## <a name="update-a-service-reference"></a>Atualizar uma referência de serviço
 O modelo de dados de entidade para um [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] , às vezes, é alterado. Quando isso acontece, você deve atualizar a referência de serviço.

### <a name="to-update-a-service-reference"></a>Para atualizar uma referência de serviço

-   Na **Gerenciador de soluções**, a referência de serviço com o botão direito e, em seguida, clique em **Update Service Reference**.

     Uma caixa de diálogo de progresso exibe enquanto a referência é atualizada de seu local original e o cliente do serviço for gerado novamente para refletir quaisquer alterações nos metadados.

## <a name="remove-a-service-reference"></a>Remover uma referência de serviço
 Se uma referência de serviço não estiver sendo usada, remova-a da sua solução.

### <a name="to-remove-a-service-reference"></a>Para remover uma referência de serviço

-   Na **Gerenciador de soluções**, a referência de serviço com o botão direito e, em seguida, clique em **excluir**.

     O cliente do serviço será removido da solução e os metadados que descrevem o serviço serão removido do *App. config* arquivo.

    > [!NOTE]
    >  Qualquer código que faz referência a referência de serviço deve ser removido manualmente.

## <a name="see-also"></a>Consulte também

- [Serviços do Windows Communication Foundation e WCF data services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)