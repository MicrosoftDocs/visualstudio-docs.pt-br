---
title: Visão geral das opções de configuração | Microsoft Docs
description: Saiba mais sobre as opções de configurações de projeto no Visual Studio. Uma configuração é um tipo de compilação descrito com um conjunto nomeado de propriedades e locais de arquivo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations
- configuration options, about configuration options
ms.assetid: f4ad4dd3-b39e-42df-ad89-d403cdf24a2b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ad30e3f7b91e8a76715f66d9f6701597f3830bd6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057124"
---
# <a name="configuration-options-overview"></a>Visão geral das opções de configuração
Os projetos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] podem dar suporte a várias configurações que podem ser criadas, depuradas, executadas e/ou implantadas. Uma configuração é um tipo de compilação descrito com um conjunto nomeado de propriedades, normalmente comutadores de compilador e locais de arquivo. Por padrão, novas soluções contêm duas configurações, *depuração* e *versão*. Essas configurações podem ser aplicadas usando suas configurações padrão ou modificadas para atender aos requisitos de solução e/ou projeto específicos. Alguns pacotes podem ser criados de duas maneiras: como um editor do ActiveX ou um componente in-loco. No entanto, os projetos não precisam dar suporte a várias configurações. Se houver apenas uma configuração disponível, essa configuração será mapeada em todas as configurações da solução.

 As configurações normalmente consistem em duas partes: o nome da configuração (como *debug* ou *Release*) e as configurações da plataforma. O nome da plataforma de uma configuração identifica o ambiente de destino da configuração, como um conjunto de API ou plataforma do sistema operacional. Os usuários do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] não podem criar uma plataforma; eles devem escolher entre as seleções que um projeto VSPackage permite. Quando um usuário instala um VSPackage, a plataforma de entrega criada durante o desenvolvimento do pacote pode trazer qualquer nome de plataforma desejado com base em qualquer critério definido pelo criador do pacote. O usuário pode selecionar na lista de plataformas disponibilizadas por meio do VSPackage quando as páginas de propriedades são instanciadas.

 Os nomes de plataforma são opcionais, pois nem todos os projetos oferecem suporte ao conceito de plataformas. Quando uma configuração não tem um nome de plataforma, a cadeia de caracteres **N/a** é exibida na interface do usuário.

 Cada solução tem seu próprio conjunto de configurações, apenas uma das quais pode estar ativa por vez. Uma configuração de solução é um conjunto de no máximo uma configuração de cada projeto. A cláusula "no máximo" é devido à opção de excluir um projeto de uma configuração de solução. Os usuários podem criar suas próprias configurações de solução personalizadas.

 A tabela a seguir ilustra a configuração típica de configurações para um projeto do. As linhas são rotuladas com nomes de configuração e as colunas com nomes de plataforma.

|Nome da configuração|Plataforma: Win32|Plataforma: Win64|
|------------------------|----------------------|----------------------|
|*Depurar*|\<Debug Win32 settings>|\<Debug Win64 settings>|
|*Versão*|\<Release Win32 settings>|\<Release Win64 settings>|
|*Myconfig*|N/D|\<MyConfig Win64 settings>|

> [!NOTE]
> Não é possível criar uma configuração de solução *myconfig* que exclua uma plataforma Win32, a menos que o projeto que você está direcionando não ofereça suporte ao Win32.

 Alterar a configuração ativa de uma solução seleciona o conjunto de configurações de projeto que é criado, executado, depurado ou implantado nessa solução. Por exemplo, se você alterar a configuração de solução ativa de *versão* para *depuração*, todos os projetos dentro dessa solução serão criados automaticamente com a configuração de projetos indicada na configuração de depuração da solução. As configurações dos projetos também são nomeadas como *debug* , a menos que o usuário tenha feito alterações manuais na Configuration Manager do ambiente.

 As propriedades de configuração de solução armazenadas para cada projeto incluem o nome do projeto, o nome da configuração do projeto, os sinalizadores para indicar se deseja ou não compilar ou implantar, e o nome da plataforma. Para obter mais informações, consulte [configuração da solução](../../extensibility/internals/solution-configuration.md).

 O usuário pode exibir e definir parâmetros de configuração de solução selecionando a solução na hierarquia (Gerenciador de Soluções) e abrindo as páginas de propriedades. Da mesma forma, você pode exibir e definir parâmetros de configuração de projeto selecionando um projeto no Gerenciador de Soluções e abrindo as páginas de propriedades para esse projeto.

 O usuário também pode criar um projeto usando as definições de configuração de versão e todas as definições de configuração REST com depuração, se necessário. Para obter mais informações, consulte [configuração de projeto para compilação](../../extensibility/internals/project-configuration-for-building.md).

 O diagrama a seguir mostra como as interfaces que oferecem suporte a soluções e configurações de projeto são implementadas:

 ![Gráfico de interfaces de configuração](../../extensibility/internals/media/vsconfiginterfaces.gif "vsConfigInterfaces") Interfaces de configuração

 Algumas anotações relacionadas ao diagrama anterior:

- `IDispatch` é marcado como opcional no objeto de configuração. Especificamente, é opcional ter as interfaces de configuração no objeto de procura.

- `IVsDebuggableProjectCfg` é marcado como opcional no objeto de configuração, mas é necessário para a depuração de suporte.

- `IVsProjectCfg2` é marcado como opcional no objeto de configuração, mas é necessário para o suporte de agrupamento de saída.

- O objeto do provedor de configuração é marcado como um objeto opcional, mas a opção é onde implementá-lo. Você pode implementar o objeto no objeto Project ou em um objeto separado.

- `IVsCfgProvider2` é necessário para o suporte de plataforma e edição de configuração. `IVsCfgProvider` será suficiente se você não implementar essa funcionalidade.

- Alguns desses objetos mostrados no diagrama como objetos separados podem ser combinados na mesma classe onde for prático com base em seus requisitos de design específicos. Em outros tópicos desta seção, no entanto, os objetos e as interfaces associados a esses objetos serão discutidos de acordo com o cenário apresentado no diagrama.

- Determinados objetos são implementados separadamente. Por exemplo, a compilação de projeto e solução ocorre em threads separados e o objeto para gerenciar a compilação reside separadamente do objeto que descreve a configuração da compilação.

  Para obter mais informações sobre interfaces de objeto de configuração e interfaces de objeto de provedor de configuração no diagrama anterior, consulte [Project Configuration Object](../../extensibility/internals/project-configuration-object.md). Além disso, a [configuração de projeto para construção](../../extensibility/internals/project-configuration-for-building.md) fornece mais informações sobre o construtor de configuração e interfaces de objeto de dependência de compilação, e a [configuração de projeto para gerenciar a implantação](../../extensibility/internals/project-configuration-for-managing-deployment.md) descreve ainda mais as interfaces anexadas ao implantador de configuração e aos objetos de dependência de implantação. Por fim, a [configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md) descreve o grupo de saída e as interfaces de objeto de saída e o uso de páginas de propriedades para exibir e definir propriedades dependentes de configuração.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>
- [Configuração do projeto para compilação](../../extensibility/internals/project-configuration-for-building.md)
- [Configuração da solução](../../extensibility/internals/solution-configuration.md)
