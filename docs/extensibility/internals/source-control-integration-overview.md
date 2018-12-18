---
title: Visão geral da integração de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], about source control
ms.assetid: 3a46e4eb-e677-49c3-8647-d927d035a19a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: edd2e04f4e1102d66cc04cd1365dc7abd1488c9c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49931827"
---
# <a name="source-control-integration-overview"></a>Visão geral da integração do controle do código-fonte
Esta seção compara as duas formas de integrar o controle do código-fonte do Visual Studio; um controle de fonte plug-in e um VSPackage que fornece uma solução de controle do código-fonte e destaca os novos recursos de controle do código-fonte. Visual Studio permite manual alternando VSPackages de controle de origem e plug-ins de controle de origem, bem como a comutação automática baseados em soluções.  
  
## <a name="source-control-integration"></a>Integração de controle do código-fonte  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] dá suporte a dois tipos de opções de integração de controle de origem. Todas as versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], você ainda pode integrar um plug-in com base em que a API de plug-in de controle do código-fonte (anteriormente também conhecida como a API de MSSCCI), e que fornece funcionalidade de controle de origem básicos ao usar o Visual Studio fonte (de interface de usuário de controle INTERFACE DO USUÁRIO). Um controle de fonte VSPackage, por outro lado, fornece uma integração profunda nova, [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] caminho adequado para a integração de controle do código-fonte que exige um alto nível de sofisticação e autonomia em seu modelo de controle do código-fonte.  
  
 ![Visão geral do controle de origem](../../extensibility/internals/media/sourcectnrloverview.gif "SourceCtnrlOverview")  
  
## <a name="source-control-plug-in"></a>Plug-in de controle do código-fonte  
 Todas as versões do Visual Studio dão suporte a API de plug-in de controle de fonte de especificação de versão 1.2 como um caminho de integração. Um implementador de plug-in de controle do código-fonte grava uma DLL que implementa as funções de API de plug-in de controle do código-fonte para integração de controle do código-fonte e o registro conforme descrito em [criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md). Nessa abordagem, o ambiente de desenvolvimento integrado (IDE) usa o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário para as caixas de diálogo, como check-in, check-out e glifos de controle do código-fonte, barras de ferramentas e páginas de propriedades de ferramentas/opções. Estrita aderência a API de plug-in de controle de origem assegura uma fácil integração com o Visual Studio e uma experiência sem problemas para o usuário. Isso significa que o plug-in de controle de origem deve implementar a maioria das funções e dos retornos de chamada detalhados na API.  
  
 Para implementar um plug-in para usar a API de plug-in de controle do código-fonte do controle de fonte, siga estas etapas:  
  
1. Criar uma DLL que implementa as funções especificadas na [Plug-ins de controle de origem](../../extensibility/source-control-plug-ins.md).  
  
2. Registrar a DLL, tornando as entradas do registro apropriado (descrito na [como: instalar um plug-in de controle do código-fonte](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)).  
  
3. Criar um auxiliar de interface do usuário e a exibição quando solicitado pelo pacote de adaptador de controle de origem (o componente do Visual Studio que manipula a funcionalidade de controle do código-fonte por meio do plug-ins de controle de origem)  
  
   Em resposta a um comando de controle do código-fonte, o IDE do Visual Studio apresenta uma interface do usuário padrão para as operações básicas e, em seguida, passa as informações para o controle de fonte plug-in por meio de funções definidas na API de plug-in de controle do código-fonte. Para opções avançadas, o plug-in de controle do código-fonte pode ser chamado em para apresentar sua própria interface do usuário, por exemplo, navegando para um projeto de controle do código-fonte. Isso significa que o usuário pode ser apresentado com dois possivelmente diferentes estilos de interface do usuário ao lidar com controle de origem: a interface do usuário que apresenta o Visual Studio e a interface do usuário que apresenta o plug-in de controle do código-fonte. Isso é mais perceptível com operações de controle de código-fonte avançadas.  
  
### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>Desvantagens para implementar um plug-in de controle do código-fonte  
  
-   Recursos avançados, o usuário poderá ver dois estilos diferentes de interfaces, levando a possível confusão.  
  
-   O plug-in de controle do código-fonte está confinada ao modelo de controle de origem indicado pela API de plug-in de controle do código-fonte.  
  
-   A API de plug-in de controle do código-fonte pode ser muito restritiva para alguns cenários de controle do código-fonte.  
  
### <a name="advantages-to-implementing-a-source-control-plug-in"></a>Vantagens para a implementação de um plug-in de controle do código-fonte  
  
-   O Visual Studio fornece toda a interface do usuário para todas as operações de controle de origem básicos para que o plug-in de controle do código-fonte não tem que implementar a interface do usuário potencialmente complexo.  
  
-   Por causa da API estrita, o plug-in de controle do código-fonte prontamente pode interagir com programas de controle de fonte externa para fornecer a funcionalidade mais ampla; Visual Studio, não importa muito bem como a funcionalidade de controle do código-fonte é realizada, apenas que ele é realizado de acordo com a API de plug-in de controle do código-fonte.  
  
-   É mais fácil de implementar um plug-in que um VSPackage de controle do código-fonte do controle de fonte.  
  
## <a name="source-control-vspackage"></a>VSPackage de controle do código-fonte  
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] permite uma integração profunda com controle total sobre a funcionalidade de controle do código-fonte e uma substituição completa da interface do usuário de controle de origem fornecida pelo Visual Studio para o Visual Studio. Um controle de fonte VSPackage é registrado com o Visual Studio e fornece a funcionalidade de controle do código-fonte. Embora vários VSPackages de controle de origem pode ser registrado com o Visual Studio, apenas um deles pode ser ativo a qualquer momento. Um VSPackage de controle do código-fonte tem controle total sobre a aparência e funcionalidade de controle do código-fonte no Visual Studio enquanto estiver ativo. Todos os outro controle de origem VSPackages que pode ser registrados no sistema estão inativo e não exibirá nenhuma interface do usuário em todos os.  
  
 Implementar um VSPackage de controle do código-fonte exige uma estratégia "tudo ou nada". O criador de um VSPackage de controle do código-fonte deve investir uma quantidade significativa de esforço na implementação de um número de interfaces de controle do código-fonte e os novos elementos de interface do usuário (caixas de diálogo, menus e barras de ferramentas) para cobrir a funcionalidade de controle de origem inteira. Ver [criando um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md) para obter mais detalhes.  
  
### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>Desvantagens para implementar um VSPackage de controle do código-fonte  
  
-   O VSPackage deve implementar um número de interfaces complexas para integrar com êxito com o Visual Studio.  
  
-   O VSPackage deverá fornecer toda a interface do usuário necessário para o controle do código-fonte; Visual Studio não fornecerá nenhuma assistência nessa área.  
  
-   Um controle de fonte VSPackage está intimamente relacionado ao Visual Studio e não pode operar com programas autônomos, portanto, a funcionalidade não pode ser facilmente compartilhada com uma versão externa do programa de controle de origem.  
  
### <a name="advantages-to-implementing-a-source-control-vspackage"></a>Vantagens para a implementação de um VSPackage de controle do código-fonte  
  
-   Como o VSPackage possui funcionalidade e controle total sobre o controle do código-fonte da interface do usuário, o usuário é apresentado com uma interface direta para controle de origem.  
  
-   O VSPackage não está limitado a um modelo de controle de origem em particular.  
  
## <a name="see-also"></a>Consulte também  
 [Controle de origem](../../extensibility/internals/source-control.md)   
 [Criando um controle de fonte plug-in](../../extensibility/internals/creating-a-source-control-plug-in.md)   
 [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)   
 [Novidades no controle do código-fonte](../../extensibility/internals/what-s-new-in-source-control.md)