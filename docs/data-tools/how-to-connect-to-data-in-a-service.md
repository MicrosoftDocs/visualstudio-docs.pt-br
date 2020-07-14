---
title: Como conectar a dados em um serviço
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting to web services
- data sources, creating from web services
- data [Visual Studio], reading from web services
- reading data, from web services
- web services, reading data
- web services, as data sources
- web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 0b49840a2190abfd223edf5643b8d70da1a59d6b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282222"
---
# <a name="how-to-connect-to-data-in-a-service"></a>Como se conectar a dados em um serviço

Conecte seu aplicativo aos dados retornados de um serviço executando o [Assistente de configuração da fonte de dados](../data-tools/media/data-source-configuration-wizard.png) e selecionando **serviço** na página **escolher um tipo de fonte de dados** .

Após a conclusão do assistente, uma referência de serviço é adicionada ao seu projeto e fica imediatamente disponível na [janela fontes de dados](add-new-data-sources.md#data-sources-window).

> [!NOTE]
> Os itens que aparecem na janela **Fontes de Dados** são dependentes das informações que o serviço retorna. Alguns serviços podem não fornecer informações suficientes para o **Assistente de Configuração de Fonte de Dados** criar objetos associáveis. Por exemplo, se o serviço retornar um conjunto de dados não tipado, nenhum item aparecerá na janela **Data Sources** após a conclusão do assistente. Isso ocorre porque os conjuntos de dados não tipados não fornecem o esquema, portanto, o assistente não tem informações suficientes para criar a fonte de dados.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-connect-your-application-to-a-service"></a>Para conectar seu aplicativo a um serviço

1. No menu **Dados**, clique em **Adicionar Nova Fonte de Dados**.

2. Selecione **serviço** na página **escolher um tipo de fonte de dados** e clique em **Avançar**.

3. Insira o endereço do serviço que você deseja usar ou clique em **descobrir** para localizar os serviços na solução atual e, em seguida, clique em **ir**.

4. Opcionalmente, você pode digitar um novo **namespace** no lugar do valor padrão.

    > [!NOTE]
    > Clique em **avançado** para abrir a [caixa de diálogo Configurar referência de serviço](../data-tools/configure-service-reference-dialog-box.md).

5. Clique em **OK** para adicionar uma referência de serviço ao seu projeto.

6. Clique em **Concluir**.

     A fonte de dados é adicionada à janela **fontes de dados** .

## <a name="next-steps"></a>Próximas etapas

Para adicionar funcionalidade ao seu aplicativo, selecione um item na janela **fontes de dados** e arraste-o para um formulário para criar controles associados. Para obter mais informações, confira [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).

## <a name="see-also"></a>Veja também

- [Associar controles WPF a um WCF Data Service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)
- [Serviços de Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
