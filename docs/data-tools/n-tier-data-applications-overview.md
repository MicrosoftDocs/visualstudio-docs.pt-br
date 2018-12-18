---
title: Visão geral de aplicativos de dados de N camadas
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- presentation tier
- middle tier
- data tier
- n-tier applications, about n-tier applications
ms.assetid: 1020581d-eaaa-41a2-aca4-bf4c212895f6
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 3f9cf8c6a75e5f2a517931bf0fd858ea8f8f860c
ms.sourcegitcommit: c9a01c599ce19a5845605b3b28c0229fd0abb93f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281739"
---
# <a name="n-tier-data-applications-overview"></a>Visão geral dos aplicativos de dados de N camadas
*N camadas* aplicativos de dados são aplicativos de dados que são separados em várias *camadas*. Aplicativos de n camadas também chamados de "aplicativos distribuídos" e "aplicativos multicamados", separam o processamento em camadas discretas que são distribuídas entre o cliente e o servidor. Quando você desenvolve aplicativos que acessam dados, você deve ter uma separação clara entre as várias camadas que compõem o aplicativo.

Um aplicativo de n camadas típico inclui uma camada de apresentação, uma camada intermediária e uma camada de dados. A maneira mais fácil para separar as várias camadas em um aplicativo de n camadas é criar projetos discretos para cada camada que você deseja incluir em seu aplicativo. Por exemplo, a camada de apresentação pode ser um aplicativo Windows Forms, enquanto a lógica de acesso de dados pode ser uma biblioteca de classes localizada na camada intermediária. Além disso, a camada de apresentação pode se comunicar com a lógica de acesso de dados na camada intermediária por meio de um serviço como um serviço. Dividir componentes do aplicativo em camadas separadas aumenta a facilidade de manutenção e a escalabilidade do aplicativo. Ele faz isso permitindo adoção mais fácil de novas tecnologias que podem ser aplicadas a uma única camada sem a necessidade de recriar a solução inteira. Além disso, os aplicativos de n camadas normalmente armazenam informações confidenciais na camada intermediária, que mantém o isolamento da camada de apresentação.

O Visual Studio contém vários recursos para ajudar os desenvolvedores a criar aplicativos de n camadas:

-   O conjunto de dados fornece um **projeto DataSet** propriedade que permite que você separe o conjunto de dados (camada de entidade de dados) e os TableAdapters (camada de acesso a dados) em projetos discretos.

-   O [LINQ to SQL das ferramentas no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) fornece configurações para gerar as classes DataContext e dados em namespaces separados. Isso permite uma separação lógica do acesso a dados e camadas de entidade de dados.

-   [O LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) fornece o <xref:System.Data.Linq.Table%601.Attach%2A> método que permite que você reúna o DataContext de diferentes camadas em um aplicativo. Para obter mais informações, consulte [de N camadas e aplicativos remotos com o LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql).

## <a name="presentation-tier"></a>Camada de apresentação
O *camada de apresentação* é a camada na qual os usuários interagem com um aplicativo. Ele normalmente contém lógica de aplicativo adicionais também. Componentes da camada de apresentação típicas incluem o seguinte:

-   Componentes de dados, como o <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator>.

-   Objeto de representações de dados, como [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) classes de entidade para uso na camada de apresentação.

A camada de apresentação normalmente acessa a camada intermediária usando uma referência de serviço (por exemplo, uma [serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) aplicativo). A camada de apresentação não pode acessar diretamente a camada de dados. A camada de apresentação se comunica com a camada de dados por meio do componente de acesso a dados na camada intermediária.

## <a name="middle-tier"></a>Camada intermediária
O *camada intermediária* é a camada que a camada de apresentação e os camada de dados usar para se comunicar entre si. Componentes de camada intermediária típicas incluem o seguinte:

-   Lógica de negócios, como a validação de regras e dados de negócios.

-   Componentes de acesso a dados e lógica, como o seguinte:

    -   [TableAdapters](create-and-configure-tableadapters.md) e [DataAdapters e DataReaders](/dotnet/framework/data/adonet/dataadapters-and-datareaders).

    -   Objeto de representações de dados, como [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) classes de entidade.

    -   Serviços de aplicativo comuns, como autenticação, autorização e personalização.

A ilustração a seguir mostra os recursos e tecnologias que estão disponíveis no Visual Studio e onde eles podem caber na camada intermediária de um aplicativo de n camadas.

![Componentes da camada de intermediária](../data-tools/media/ntiermid.png) camada intermediária

A camada intermediária geralmente se conecta à camada de dados usando uma conexão de dados. Esta conexão de dados normalmente é armazenada no componente de acesso de dados.

## <a name="data-tier"></a>Camada de dados
O *camada de dados* é basicamente o servidor que armazena dados de um aplicativo (por exemplo, um servidor executando o SQL Server).

A ilustração a seguir mostra os recursos e tecnologias que estão disponíveis no Visual Studio e onde eles podem caber na camada de dados de um aplicativo de n camadas.

![Componentes da camada de dados](../data-tools/media/ntierdatatier.png) camada de dados

A camada de dados não pode ser acessada diretamente do cliente na camada de apresentação. Em vez disso, o componente de acesso de dados na camada intermediária é usado para comunicação entre as camadas de dados e apresentação.

## <a name="help-for-n-tier-development"></a>Ajuda para o desenvolvimento de n camadas
Os tópicos a seguir fornecem informações sobre como trabalhar com aplicativos de n camadas:

[Separar conjuntos de dados e TableAdapters em diferentes projetos](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)

[Passo a passo: Criando um aplicativo de dados de n camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)

[De N camadas e aplicativos remotos com o LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)

## <a name="see-also"></a>Consulte também

- [Passo a passo: Criando um aplicativo de dados de n camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [Atualização hierárquica](../data-tools/hierarchical-update.md)
- [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)