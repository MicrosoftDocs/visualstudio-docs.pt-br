---
title: Visão geral da integração de controle do código-fonte | Microsoft Docs
description: 'Saiba mais sobre as diferenças entre as duas maneiras de integrar o controle do código-fonte no Visual Studio: um plug-in de controle do código-fonte e um VSPackage.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], about source control
ms.assetid: 3a46e4eb-e677-49c3-8647-d927d035a19a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9feacd8e051b47b1fec6c3d3ad08e34e591fc57c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064300"
---
# <a name="source-control-integration-overview"></a>Visão geral da integração do controle do código-fonte
Esta seção compara as duas maneiras de integrar-se ao controle do código-fonte do Visual Studio; um plug-in de controle de origem e um VSPackage que fornece uma solução de controle do código-fonte e realça os novos recursos de controle do código-fonte. O Visual Studio permite a alternância manual entre o controle do código-fonte VSPackages e os plug-ins de controle do código-fonte, bem como a alternância automática baseada em soluções.

## <a name="source-control-integration"></a>Integração de controle do código-fonte
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] dá suporte a dois tipos de opções de integração de controle do código-fonte. Em todas as versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , você ainda pode integrar um plug-in com base na API de plug-in de controle do código-fonte (anteriormente também conhecida como API MSSCCI), que fornece a funcionalidade básica de controle do código-fonte ao usar a interface do usuário do controle do código-fonte do Visual Studio. Um VSPackage de controle do código-fonte, por outro lado, fornece um novo [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] caminho de integração profunda adequado para a integração de controle do código-fonte que exige um alto nível de sofisticação e autonomia em seu modelo de controle do código-fonte.

 ![Visão geral do controle do código-fonte](../../extensibility/internals/media/sourcectnrloverview.gif "SourceCtnrlOverview")

## <a name="source-control-plug-in"></a>Plug-in de controle do código-fonte
 Todas as versões do Visual Studio dão suporte à especificação da API de plug-in de controle do código-fonte versão 1,2 como um caminho de integração. Um implementador de plug-in de controle do código-fonte grava uma DLL que implementa as funções da API de plug-in de controle do código-fonte para integração e registro de controle do código-fonte, conforme descrito em [criando um plug-in de controle](../../extensibility/internals/creating-a-source-control-plug-in.md) Nessa abordagem, o ambiente de desenvolvimento integrado (IDE) usa a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário para caixas de diálogo, como check-in, check-in, ferramentas/opções páginas de propriedades, barras de ferramentas e glifos de controle do código-fonte. A adesão estrita à API de plug-in de controle do código-fonte garante uma fácil integração no Visual Studio e uma experiência sem problemas para o usuário. Isso significa que o plug-in de controle do código-fonte deve implementar a maioria das funções e retornos de chamada detalhados na API.

 Para implementar um plug-in de controle do código-fonte usando a API de plug-in de controle do código-fonte, siga estas etapas:

1. Crie uma DLL que implemente as funções especificadas em [plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md).

2. Registre a DLL fazendo as entradas de registro apropriadas (descritas em [como instalar um plug-in de controle do código-fonte](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)).

3. Criar uma interface do usuário auxiliar e exibir quando solicitado pelo pacote do adaptador de controle do código-fonte (o componente do Visual Studio que manipula a funcionalidade de controle de origem por meio de plug-ins de controle do código-fonte

   Em resposta a um comando de controle do código-fonte, o IDE do Visual Studio apresenta uma interface do usuário padrão para as operações básicas e passa as informações para o plug-in de controle do código-fonte por meio das funções definidas na API de plug-in de controle do código-fonte. Para opções avançadas, o plug-in de controle do código-fonte pode ser chamado em para apresentar sua própria interface do usuário, por exemplo, procurando um projeto de origem controlada. Isso significa que o usuário pode receber dois estilos possivelmente diferentes de interface de usuário ao lidar com o controle do código-fonte: a interface de usuário que o Visual Studio apresenta e a interface do usuário que o plug-in de controle do código-fonte apresenta. Isso é mais perceptível com as operações avançadas de controle do código-fonte.

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>Desvantagens da implementação de um plug-in de controle do código-fonte

- Para recursos avançados, o usuário pode ver dois estilos diferentes de interfaces, levando a uma possível confusão.

- O plug-in de controle do código-fonte é restrito ao modelo de controle do código-fonte implícito pela API de plug-in de controle do código-fonte.

- A API de plug-in de controle do código-fonte pode ser muito restritiva para alguns cenários de controle do código-fonte.

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>Vantagens de implementar um plug-in de controle do código-fonte

- O Visual Studio fornece toda a interface do usuário para todas as operações básicas de controle do código-fonte para que o plug-in de controle do código-fonte não precise implementar uma interface do usuário potencialmente complexa.

- Devido à API estrita, o plug-in de controle do código-fonte pode interagir prontamente com programas de controle do código-fonte externo para fornecer funcionalidade mais abrangente; O Visual Studio não se preocupa muito com a forma como a funcionalidade de controle do código-fonte é realizada, apenas que é realizada de acordo com a API de plug-in de controle do código-fonte.

- É mais fácil implementar um plug-in de controle do código-fonte do que um VSPackage de controle do código-fonte.

## <a name="source-control-vspackage"></a>VSPackage de controle do código-fonte
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] permite a integração profunda com o Visual Studio com controle total da funcionalidade de controle do código-fonte e a substituição da interface do usuário do controle do código-fonte fornecido pelo Visual Studio. Um VSPackage de controle do código-fonte é registrado com o Visual Studio e fornece funcionalidade de controle do código-fonte. Embora vários VSPackages de controle do código-fonte possam ser registrados com o Visual Studio, apenas um deles pode estar ativo a qualquer momento. Um VSPackage de controle do código-fonte tem controle total sobre a funcionalidade de controle do código-fonte e a aparência no Visual Studio enquanto ele está ativo. Todas as outras VSPackages de controle do código-fonte que podem ser registradas no sistema estão inativas e não exibirão nenhuma interface do usuário.

 A implementação de um VSPackage de controle do código-fonte requer uma estratégia "tudo ou nada". O criador de um VSPackage de controle do código-fonte deve investir uma quantidade significativa de esforço na implementação de uma série de interfaces de controle do código-fonte e novos elementos da interface do usuário (caixas de diálogo, menus e barras de ferramentas) para cobrir toda a funcionalidade de controle do código-fonte. Consulte [criando um controle do código-fonte VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md) para obter mais detalhes.

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>Desvantagens da implementação de um controle do código-fonte VSPackage

- O VSPackage deve implementar várias interfaces complexas para integrar com êxito com o Visual Studio.

- O VSPackage deve fornecer toda a interface do usuário necessária para o controle do código-fonte; O Visual Studio não oferecerá nenhuma assistência nessa área.

- Um VSPackage de controle do código-fonte está intimamente ligado ao Visual Studio e não pode operar com programas autônomos, portanto, a funcionalidade não pode ser facilmente compartilhada com uma versão externa do programa de controle do código-fonte.

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>Vantagens de implementar um controle do código-fonte VSPackage

- Como o VSPackage tem controle total sobre a interface do usuário do controle do código-fonte e a funcionalidade, o usuário recebe uma interface direta para o controle do código-fonte.

- O VSPackage não é confinado para um modelo de controle do código-fonte específico.

## <a name="see-also"></a>Confira também
- [Controle do código-fonte](../../extensibility/internals/source-control.md)
- [Criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [Novidades no controle do código-fonte](../../extensibility/internals/what-s-new-in-source-control.md)
