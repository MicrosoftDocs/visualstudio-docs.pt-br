---
title: Ferramentas de dados para .NET
ms.date: 11/04/2016
ms.topic: overview
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
- dotnet
ms.openlocfilehash: 67cf4969a5db8900910b375d4cf560b1e30da4eb
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281065"
---
# <a name="visual-studio-data-tools-for-net"></a>Ferramentas de dados do Visual Studio para .NET

O Visual Studio e o .NET juntos fornecem amplo suporte de API e ferramentas para conectar-se a bancos de dados, modelar os dados na memória e exibir os dados na interface do usuário. As classes .NET que fornecem a funcionalidade de acesso a dados são conhecidas como [ADO.net](/dotnet/framework/data/adonet/index). O ADO.NET, juntamente com as ferramentas de dados no Visual Studio, foi projetado principalmente para dar suporte a bancos de dados relacionais e XML. Atualmente, muitos fornecedores de banco de dados NoSQL ou terceiros oferecem provedores de ADO.NET.

O [.NET Core](/dotnet/core/) dá suporte a ADO.net, exceto para conjuntos de valores e seus tipos relacionados. Se você estiver direcionando o .NET Core e exigir uma camada de ORM (mapeamento relacional de objeto), use [Entity Framework Core](/ef/core/).

O diagrama a seguir mostra uma visão simplificada da arquitetura básica:

![Arquitetura do ADO.NET](../data-tools/media/raddata-ado-net-architecture-diagram.png)

## <a name="typical-workflow"></a>Fluxo de trabalho típico

O fluxo de trabalho típico é o seguinte:

1. Instale um banco de dados de desenvolvimento ou de teste no computador local. Consulte [instalando sistemas de banco de dados, ferramentas e exemplos](../data-tools/installing-database-systems-tools-and-samples.md). Se você estiver usando um serviço de dados do Azure, essa etapa não será necessária.

2. Teste a conexão com o banco de dados (ou o serviço ou arquivo local) no Visual Studio. Consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

3. Adicional Use as ferramentas para gerar e configurar um novo modelo. Modelos baseados em Entity Framework são a recomendação padrão para novos aplicativos. O modelo, seja qual for o que você usa, é a fonte de dados com a qual o aplicativo interage. O modelo fica logicamente entre o banco de dados ou o serviço e o aplicativo. Consulte [adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).

4. Arraste a fonte de dados da janela **fontes de dados** para um Windows Forms, ASP.NET ou Windows Presentation Foundation superfície de design para gerar o código de vinculação de dados que exibirá os dados para o usuário da maneira que você especificar. Consulte [ligar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).

5. Adicione código personalizado para coisas como regras de negócio, pesquisa e validação de dados, ou para aproveitar a funcionalidade personalizada que o Database subjacente expõe.

Você pode ignorar a etapa 3 e programar um aplicativo .NET para emitir comandos diretamente para um banco de dados, em vez de usar um modelo. Nesse caso, você encontrará a documentação relevante aqui: [ADO.NET](/dotnet/framework/data/adonet/index). Observe que você ainda pode usar o **Assistente de configuração da fonte de dados** e designers para gerar código de vinculação de dados quando você preenche seus próprios objetos na memória e os controles de interface do usuário de ligação de dados com esses objetos.

## <a name="see-also"></a>Veja também

- [Acessar dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
