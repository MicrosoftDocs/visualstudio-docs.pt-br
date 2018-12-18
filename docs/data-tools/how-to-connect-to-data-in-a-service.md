---
title: Como conectar a dados em um serviço
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], connecting to web services
- data sources, creating from web services
- data [Visual Studio], reading from web services
- reading data, from web services
- web services, reading data
- web services, as data sources
- web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: f8f7371418df19ec8452334641c7c9414328e557
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305007"
---
# <a name="how-to-connect-to-data-in-a-service"></a>Como se conectar a dados em um serviço

Você conecta seu aplicativo para os dados retornados de um serviço executando o [Data Source Configuration Wizard](../data-tools/media/data-source-configuration-wizard.png) e selecionando **serviço** sobre o **escolher um tipo de fonte de dados**página.

Após a conclusão do assistente, uma referência de serviço é adicionada ao seu projeto e fica imediatamente disponível na [janela Data Sources](add-new-data-sources.md#data-sources-window).

> [!NOTE]
> Os itens que aparecem na janela **Fontes de Dados** são dependentes das informações que o serviço retorna. Alguns serviços podem não fornecer informações suficientes para o **Assistente de Configuração de Fonte de Dados** criar objetos associáveis. Por exemplo, se o serviço retorna um conjunto de dados não tipado, nenhum item aparecerá na **fontes de dados** janela após concluir o assistente. Isso ocorre porque os conjuntos de dados não tipados não fornecem esquema, portanto, o assistente não tem informações suficientes para criar a fonte de dados.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-connect-your-application-to-a-service"></a>Conectar seu aplicativo a um serviço

1.  No menu **Dados**, clique em **Adicionar Nova Fonte de Dados**.

2.  Selecione **serviço** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.

3.  Insira o endereço do serviço que você deseja usar ou clique em **Discover** para localizar serviços na solução atual e, em seguida, clique em **vá**.

4.  Opcionalmente, você pode digitar um novo **Namespace** no lugar do valor padrão.

    > [!NOTE]
    > Clique em **Advanced** para abrir o [caixa de diálogo Configurar referência de serviço](../data-tools/configure-service-reference-dialog-box.md).

5.  Clique em **Okey** para adicionar uma referência de serviço ao seu projeto.

6.  Clique em **Finalizar**.

     A fonte de dados é adicionada para o **fontes de dados** janela.

## <a name="next-steps"></a>Próximas etapas

Para adicionar funcionalidade ao seu aplicativo, selecione um item na **fontes de dados** janela e arraste-o para um formulário para criar controles associados. Para obter mais informações, confira [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).

## <a name="see-also"></a>Consulte também

- [Associar controles WPF a um WCF Data Service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)
- [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)