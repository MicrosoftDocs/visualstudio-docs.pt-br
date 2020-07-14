---
title: Visão geral de aplicativos de dados de N camadas
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- presentation tier
- middle tier
- data tier
- n-tier applications, about n-tier applications
ms.assetid: 1020581d-eaaa-41a2-aca4-bf4c212895f6
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 14527e84d5bbd2d06b2d091ba7a9d4daa9763462
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281949"
---
# <a name="n-tier-data-applications-overview"></a>Visão geral de aplicativos de dados de N camadas
Os aplicativos *de dados de N camadas* são aplicativos de dados separados em várias *camadas*. Também chamados de "aplicativos distribuídos" e "aplicativos multicamadas", os aplicativos de n camadas separam o processamento em camadas discretas que são distribuídas entre o cliente e o servidor. Ao desenvolver aplicativos que acessam dados, você deve ter uma separação clara entre as várias camadas que compõem o aplicativo.

Um aplicativo de n camadas típico inclui uma camada de apresentação, uma camada intermediária e uma camada de dados. A maneira mais fácil de separar as várias camadas em um aplicativo de n camadas é criar projetos discretos para cada camada que você deseja incluir em seu aplicativo. Por exemplo, a camada de apresentação pode ser um aplicativo Windows Forms, enquanto a lógica de acesso a dados pode ser uma biblioteca de classes localizada na camada intermediária. Além disso, a camada de apresentação pode se comunicar com a lógica de acesso de dados na camada intermediária por meio de um serviço, como um serviço Web. Dividir componentes do aplicativo em camadas separadas aumenta a facilidade de manutenção e a escalabilidade do aplicativo. Ele faz isso habilitando a adoção mais fácil de novas tecnologias que podem ser aplicadas a uma única camada sem a necessidade de reprojetar a solução inteira. Além disso, os aplicativos de n camadas normalmente armazenam informações confidenciais na camada intermediária, o que mantém o isolamento da camada de apresentação.

O Visual Studio contém vários recursos para ajudar os desenvolvedores a criar aplicativos de n camadas:

- O conjunto de dados fornece uma propriedade de **projeto de conjunto** de dados que permite que você separe o conjunto de dados (camada de entidade de dado) e os TableAdapters (camada de acesso a dados) em projetos discretos.

- As [ferramentas de LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) fornecem configurações para gerar o DataContext e as classes de dados em namespaces separados. Isso permite a separação lógica das camadas de acesso a dados e de entidade de dados.

- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) fornece o <xref:System.Data.Linq.Table%601.Attach%2A> método que permite reunir o DataContext de diferentes camadas em um aplicativo. Para obter mais informações, consulte [N camadas e aplicativos remotos com LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql).

## <a name="presentation-tier"></a>Camada de apresentação
A *camada de apresentação* é a camada na qual os usuários interagem com um aplicativo. Ele geralmente também contém lógica adicional do aplicativo. Os componentes típicos da camada de apresentação incluem o seguinte:

- Componentes de vinculação de dados, como o <xref:System.Windows.Forms.BindingSource> e o <xref:System.Windows.Forms.BindingNavigator> .

- Representações de objeto de dados, como [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) classes de entidade para uso na camada de apresentação.

A camada de apresentação normalmente acessa a camada intermediária usando uma referência de serviço (por exemplo, um [Windows Communication Foundation serviços e WCF Data Services no aplicativo do Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) ). A camada de apresentação não acessa diretamente a camada de dados. A camada de apresentação se comunica com a camada de dados por meio do componente de acesso a dados na camada intermediária.

## <a name="middle-tier"></a>Camada intermediária
A camada *intermediária* é a camada que a camada de apresentação e a camada de dados usam para se comunicar entre si. Os componentes típicos da camada intermediária incluem o seguinte:

- Lógica de negócios, como regras de negócio e validação de dados.

- Componentes de acesso a dados e lógica, como o seguinte:

  - [TableAdapters](create-and-configure-tableadapters.md) e [dataadaptadores e datalêrs](/dotnet/framework/data/adonet/dataadapters-and-datareaders).

  - Representações de objeto de dados, como [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) classes de entidade.

  - Serviços de aplicativos comuns, como autenticação, autorização e personalização.

A ilustração a seguir mostra os recursos e as tecnologias disponíveis no Visual Studio e onde eles podem se ajustar à camada intermediária de um aplicativo de n camadas.

![Camada intermediária dos componentes da camada intermediária ](../data-tools/media/ntiermid.png)

A camada intermediária normalmente se conecta à camada de dados usando uma conexão de dados. Essa conexão de dados normalmente é armazenada no componente de acesso a dados.

## <a name="data-tier"></a>Camada de dados
A *camada de dados* é basicamente o servidor que armazena os dados de um aplicativo (por exemplo, um servidor que executa o SQL Server).

A ilustração a seguir mostra os recursos e as tecnologias disponíveis no Visual Studio e onde eles podem se ajustar à camada de dados de um aplicativo de n camadas.

![Camada de dados dos componentes da camada de dados ](../data-tools/media/ntierdatatier.png)

A camada de dados não pode ser acessada diretamente do cliente na camada de apresentação. Em vez disso, o componente de acesso a dados na camada intermediária é usado para comunicação entre as camadas de apresentação e de dados.

## <a name="help-for-n-tier-development"></a>Ajuda para o desenvolvimento de n camadas
Os tópicos a seguir fornecem informações sobre como trabalhar com aplicativos de n camadas:

[Separar conjuntos de dados e TableAdapters em diferentes projetos](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)

[Walkthrough: Criando um aplicativo de dados de n camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)

[Aplicativos de N camadas e remotos com LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)

## <a name="see-also"></a>Veja também

- [Walkthrough: Criando um aplicativo de dados de n camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [Atualização hierárquica](../data-tools/hierarchical-update.md)
- [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
