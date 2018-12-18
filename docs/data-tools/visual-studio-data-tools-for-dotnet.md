---
title: Ferramentas de dados para o .NET
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
- dotnet
ms.openlocfilehash: bf28747e8bd111767fbe314cbb658a38ef059ae2
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066334"
---
# <a name="visual-studio-data-tools-for-net"></a>Ferramentas de dados do Visual Studio para .NET

Visual Studio e o .NET Framework juntos fornecem API abrangente e suporte a ferramentas para conectar-se aos bancos de dados, modelagem de dados na memória e exibir os dados na interface do usuário. As classes do .NET Framework que fornecem funcionalidade de acesso a dados são conhecidas como [ADO.NET](/dotnet/framework/data/adonet/index). ADO.NET, juntamente com os dados de ferramentas no Visual Studio, foi projetado principalmente para dar suporte a bancos de dados relacionais e XML. Hoje em dia, muitos fornecedores de banco de dados NoSQL, ou por terceiros, oferecem provedores ADO.NET.

[.NET core](/dotnet/core/) dá suporte ao ADO.NET, exceto para conjuntos de dados e tipos relacionados. Se você estiver direcionando o .NET Core e exige uma camada de mapeamento relacional de objeto (ORM), use [Entity Framework Core](/ef/core/).

O diagrama a seguir mostra uma exibição simplificada da arquitetura básica:

![Arquitetura do ADO.NET](../data-tools/media/raddata-ado-net-architecture-diagram.png)

## <a name="typical-workflow"></a>Fluxo de trabalho típico

O fluxo de trabalho típico é o seguinte:

1. Instale um desenvolvimento ou teste de banco de dados em seu computador local. Ver [instalando sistemas de banco de dados, ferramentas e exemplos](../data-tools/installing-database-systems-tools-and-samples.md). Se você estiver usando um serviço de dados do Azure, essa etapa não é necessária.

2. Teste a conexão ao banco de dados (ou serviço ou arquivo local) no Visual Studio. Ver [adicionar novas conexões](../data-tools/add-new-connections.md).

3. (Opcional) Use as ferramentas para gerar e configurar um novo modelo. Modelos com base no Entity Framework são a recomendação padrão para novos aplicativos. O modelo, seja qual for o que você utiliza, é a fonte de dados com o qual o aplicativo interage. O modelo logicamente fica entre o banco de dados ou serviço e o aplicativo. Ver [adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).

4. Arraste a fonte de dados do **fontes de dados** janela na superfície de design do Windows Forms, ASP.NET ou Windows Presentation Foundation para gerar o código de associação de dados que exibirá os dados para o usuário da maneira que você especificar. Ver [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).

5. Adicione código personalizado para coisas como as regras de negócio, pesquisa e validação de dados, ou para tirar proveito da funcionalidade personalizada que expõe o banco de dados subjacente.

Você pode ignorar a etapa 3 e programar um aplicativo .NET para emitir comandos diretamente para um banco de dados, em vez de usar um modelo. Nesse caso, você encontrará a documentação relevante aqui: [ADO.NET](/dotnet/framework/data/adonet/index). Observe que você ainda pode usar o **Data Source Configuration Wizard** e designers para gerar o código de associação de dados ao popular seus próprios objetos na memória e, em seguida, vincular dados em controles de interface do usuário a esses objetos.

## <a name="see-also"></a>Consulte também

- [Acessar dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)