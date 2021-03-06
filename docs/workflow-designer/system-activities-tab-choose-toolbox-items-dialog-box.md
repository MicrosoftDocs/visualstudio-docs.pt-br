---
title: System. Activities, escolher itens da caixa de ferramentas
description: No Designer de Fluxo de Trabalho, saiba como a guia System. Activities exibe uma lista de atividades, modelos e itens do Windows Workflow Foundation (WF) disponíveis para você.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.CHOOSEITEMS.SYSTEM.ACTIVITIES_COMPONENTS
- VS.CHOOSEITEMS.SYSTEM.ACTIVITIES COMPONENTS
ms.assetid: cef390cd-eeda-42e6-9d2e-18c8325a4f06
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 73027013916d909fd5d9f4c9f00949ce9a863708
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867939"
---
# <a name="systemactivities-tab-choose-toolbox-items-dialog-box"></a>Guia System. Activities, escolher itens da caixa de ferramentas

Essa guia da caixa de diálogo **escolher itens de caixa de ferramentas** exibe uma lista de atividades, modelos e itens do Windows Workflow Foundation (WF) disponíveis para você. Para exibir essa lista, selecione **escolher itens da caixa de ferramentas** no menu **ferramentas** ou clicando com o botão direito do mouse na caixa de **ferramentas** e selecionando **escolher itens** para exibir os **itens escolher** lista de caixas de ferramentas e, em seguida, selecione a guia **sistema. atividades** . Na caixa, a lista contém as atividades de fluxo de trabalho dos assemblies System. Activities, System. ServiceModel. Activities e System. Activities. Core. Presentation; no entanto, somente as atividades fornecidas pelo sistema mostradas e as atividades adicionadas por meio de outros assemblies exibidos na **caixa de ferramentas** são verificadas por padrão. As atividades adicionadas recentemente são verificadas automaticamente e aparecem na caixa de **ferramentas** quando você clica em **OK** na caixa de diálogo. Além disso, esses itens aparecem na **caixa de ferramentas** em uma nova categoria que corresponde ao namespace no qual reside a atividade/item/modelo.

> [!WARNING]
> Se você tentar adicionar um conjunto que não contém quaisquer atividades de fluxo de trabalho, uma caixa de diálogo de erro é exibida para explicar que o assembly não contém quaisquer atividades.

Essa caixa de diálogo é independente do projeto e, portanto, a guia **System. Activities** continua a aparecer em XAML autônomo ou em um tipo de projeto que não seja de fluxo de trabalho.

A filtragem é feita em cada guia e não é possível adicionar atividades de fluxo de trabalho por meio da guia **componente .net** . Adicione-os pela própria guia **System. Activities** .

Você pode desmarcar os itens que não deseja ver na caixa de **ferramentas** dessa guia de caixa de diálogo ou, como alternativa, pode fazer isso usando a opção de menu **excluir** clique com o botão direito do mouse na **caixa de ferramentas** e desreferenciar um assembly não remove o item da **caixa de ferramentas**.

Criando uma instância da atividade, arrastando e soltando-os ao designer adiciona o assembly que contém o item à lista de módulos (assemblies) referenciados automaticamente. Também se a atividade referencia um assembly C 2.0, C 2.0 não adiciona à lista de assembly referenciado. O assembly C deve estar no GAC ou no mesmo diretório que a atividade B. No caso autônomo, o assembly deve estar no GAC ou nos caminhos de investigação do VS. Somente então você pode arrastar e soltar a atividade na superfície de fluxo de trabalho.

As configurações da **caixa de ferramentas** são salvas por padrão como opções do usuário, assim, na próxima vez que você abrir a **caixa de ferramentas**, ela exibirá sua lista personalizada de atividades de fluxo de trabalho. Um efeito colateral disso é que, se você tiver adicionado seus itens de domínio específicos à caixa de **ferramentas** por meio de **escolher itens de Toolbox** , você ainda continuará vendo esses itens quando estiver trabalhando em um aplicativo de console de fluxo de trabalho também. Se você não quiser vê-los, exclua-os usando o menu de atalho ou desmarque-os na caixa de diálogo **escolher itens de caixa de ferramentas** , conforme observado anteriormente.

As colunas nesta caixa de diálogo contém as informações a seguir:

Nome\
Lista os nomes das atividades de fluxo de trabalho registradas atualmente em seu computador local.

Namespace
Exibe a hierarquia do namespace .NET que define a estrutura da atividade.

Nome do assembly \
Exibe o nome e a versão do assembly .NET que contém a atividade.

Active
Exibe o local do assembly .NET que contém as atividades de fluxo de trabalho. O local padrão para todos os assemblies é o cachê global de assemblies.

Para classificar os componentes listados, selecione todo o título de coluna.
