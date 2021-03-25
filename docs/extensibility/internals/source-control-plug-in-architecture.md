---
title: Arquitetura de plug-in de controle do código-fonte | Microsoft Docs
description: Saiba como adicionar suporte ao controle do código-fonte ao IDE do Visual Studio implementando e anexando um plug-in de controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3fe51878603996044535b0abfb70302ef9027c03
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064248"
---
# <a name="source-control-plug-in-architecture"></a>Arquitetura do plug-in de controle do código-fonte
Você pode adicionar suporte de controle do código-fonte ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE) implementando e anexando um plug-in de controle do código-fonte. O IDE conecta-se ao plug-in de controle do código-fonte por meio do controle do código-fonte bem definido Plug-In API. O IDE expõe os recursos de controle de versão do sistema de controle do código-fonte fornecendo uma interface do usuário (IU) que consiste em barras de ferramentas e comandos de menu. O plug-in de controle do código-fonte implementa a funcionalidade de controle do código-fonte.

## <a name="source-control-plug-in-resources"></a>Recursos de plug-in de controle do código-fonte
 O plug-in de controle do código-fonte fornece recursos para ajudar a criar e conectar seu aplicativo de versionamento ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. O plug-in de controle do código-fonte contém a especificação da API que deve ser implementada por um plug-in de controle do código-fonte para que ele possa ser integrado ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. Ele também contém um exemplo de código (escrito em C++) que implementa um esqueleto de controle do código-fonte que demonstra a implementação de funções essenciais em conformidade com a API de plug-in de controle do código-fonte.

 A especificação da API de plug-in de controle do código-fonte permite aproveitar qualquer sistema de controle do código-fonte de sua escolha se você criar uma DLL de controle do código-fonte com o conjunto de funções necessário implementado de acordo com a API de plug-in de controle do código-fonte

## <a name="components"></a>Componentes
 O pacote do adaptador de controle do código-fonte no diagrama é o componente do IDE que traduz a solicitação do usuário para uma operação de controle do código-fonte em uma chamada de função com suporte pelo plug-in de controle do código-fonte. Para que isso aconteça, o IDE e o plug-in de controle do código-fonte devem ter uma caixa de diálogo efetiva que passa informações entre o IDE e o plug-in. Para que essa caixa de diálogo ocorra, ambas devem falar do mesmo idioma. A API de plug-in de controle do código-fonte descrita nesta documentação é o vocabulário comum para essa troca.

 ![Diagrama da arquitetura de controle do código-fonte](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch") Diagrama de arquitetura mostrando a interação entre o VS e o plug-in de controle do código-fonte

 Como mostrado no diagrama de arquitetura, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell, rotulado como shell do vs no diagrama, hospeda os projetos de trabalho e os componentes associados do usuário, como os editores e Gerenciador de soluções. O pacote do adaptador de controle do código-fonte manipula a interação entre o IDE e o plug-in de controle do código-fonte. O pacote do adaptador de controle de origem fornece sua própria interface do usuário de controle do código-fonte É a interface de usuário de nível superior com a qual o usuário interage para iniciar e definir o escopo de uma operação de controle do código-fonte.

 O plug-in de controle do código-fonte pode ter sua própria interface do usuário, que pode consistir em duas partes, conforme mostrado na figura. A caixa rotulada "IU do fornecedor" representa os elementos personalizados da interface do usuário que você, como um criador de plug-in de controle do código-fonte, fornecem. Eles são exibidos diretamente pelo plug-in de controle do código-fonte quando o usuário invoca uma operação de controle do código-fonte avançado. A caixa rotulada "auxiliar UI" é um conjunto de recursos de interface do usuário de plug-in de controle do código-fonte que são indiretamente invocados por meio do IDE. O plug-in de controle do código-fonte passa mensagens relacionadas à interface do usuário para o IDE por meio de funções especiais de retorno de chamada fornecidas pelo IDE. A interface do usuário auxiliar facilita uma integração mais direta com o IDE (geralmente por meio do uso de um botão **avançado** ) e, portanto, fornece uma experiência do usuário final mais unificada.

 Um plug-in de controle do código-fonte não pode fazer alterações no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell e, consequentemente, no pacote do adaptador de controle do código-fonte ou na interface do usuário do controle do código-fonte fornecido pelo IDE. Ele deve fazer uso máximo da flexibilidade oferecida por meio da implementação das várias funções de API de plug-in de controle do código-fonte que contribuem para uma experiência integrada para o usuário final. A seção de referência da documentação da API de plug-in de controle do código-fonte inclui informações para alguns recursos avançados de plug-in de controle do código-fonte. Para explorar esses recursos, o plug-in de controle do código-fonte deve declarar seus recursos avançados para o IDE durante a inicialização e deve implementar funções avançadas específicas para cada recurso.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md)
- [Glossário](../../extensibility/source-control-plug-in-glossary.md)
- [Criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)
