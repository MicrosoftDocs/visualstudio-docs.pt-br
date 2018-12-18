---
title: 'Como: conectar-se aos dados em um serviço | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], connecting to Web services
- data sources, creating from Web services
- data [Visual Studio], reading from Web services
- reading data, from Web services
- Web services, reading data
- Web services, as data sources
- Web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ce851a864dd11759c36c7ae6cb275e9e71cd11a1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49301789"
---
# <a name="how-to-connect-to-data-in-a-service"></a>Como conectar a dados em um serviço
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você conecta seu aplicativo para os dados retornados de um serviço executando o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) e selecionando **serviço** sobre o **escolher um tipo de fonte de dados**página.  
  
 Após a conclusão do assistente, uma referência de serviço é adicionada ao seu projeto e fica imediatamente disponível na [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992).  
  
> [!NOTE]
>  Os itens que aparecem na **fontes de dados** janela são dependentes das informações que o serviço retorna. Alguns serviços não podem fornecer informações suficientes para que o **Data Source Configuration Wizard** criar objetos associáveis. Por exemplo, se o serviço retorna um conjunto de dados não tipado, então nenhum item aparecerá na **janela fontes de dados** após concluir o assistente. Isso ocorre porque os conjuntos de dados não tipados não fornecem esquema, portanto, o assistente não tem informações suficientes para criar a fonte de dados.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-connect-your-application-to-a-service"></a>Conectar seu aplicativo a um serviço  
  
1.  Sobre o **dados** menu, clique em **Add New Data Source**.  
  
2.  Selecione **serviço** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.  
  
3.  Insira o endereço do serviço que você deseja usar ou clique em **Discover** para localizar serviços na solução atual e, em seguida, clique em **vá**.  
  
4.  Opcionalmente, um novo **Namespace** podem ser digitados no lugar do valor padrão.  
  
    > [!NOTE]
    >  Clique em **Advanced** para abrir o [configurar a caixa de diálogo de referência de serviço](../data-tools/configure-service-reference-dialog-box.md).  
  
5.  Clique em **Okey** para adicionar uma referência de serviço ao seu projeto.  
  
6.  Clique em **Finalizar**.  
  
     A fonte de dados é adicionada para o **fontes de dados** janela.  
  
## <a name="next-steps"></a>Próximas etapas  
  
#### <a name="to-add-functionality-to-your-application"></a>Para adicionar funcionalidade ao seu aplicativo  
  
-   Selecione um item na **fontes de dados** janela e arraste-o para um formulário para criar controles associados. Para obter mais informações, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles WPF a um WCF data service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)   
 [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

