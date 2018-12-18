---
title: Arquitetura de plug-in de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 498f3aeb87855a0dac5afacc1baa7e2e816375f2
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31132385"
---
# <a name="source-control-plug-in-architecture"></a>Arquitetura de plug-in de controle de origem
Você pode adicionar suporte a controle de origem para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o ambiente de desenvolvimento integrado (IDE) implementando e anexando um plug-in de controle de origem. O IDE conecta-se para o plug-in por meio da API de plug-in de controle de origem bem definido de controle de origem. O IDE expõe os recursos de controle de versão do sistema de controle de origem, fornecendo uma interface do usuário (UI) que consiste em barras de ferramentas e comandos de menu. O plug-in de controle de origem implementa a funcionalidade de controle de origem.  
  
## <a name="source-control-plug-in-resources"></a>Recursos de plug-in de controle de origem  
 O plug-in de controle de origem fornece recursos para ajudar a criar e conectar seu aplicativo de controle de versão para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. O plug-in de controle de origem contém a especificação de API que deve ser implementada por um plug-in de controle de origem para que ele pode ser integrado a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. Ele também contém um exemplo de código (escrito em C++) que implementa uma origem esqueleto plug-in demonstram implementação de controle de funções essenciais compatíveis com a API de plug-in de controle de origem.  
  
 A especificação de API de plug-in de controle de origem permite que você utilize qualquer sistema de controle de origem de sua escolha, se você criar uma DLL de controle do código-fonte com o conjunto necessário de funções implementadas de acordo com a API de plug-in de controle de origem.  
  
## <a name="components"></a>Componentes  
 O pacote de adaptador de controle de origem no diagrama é o componente do IDE que converte a solicitação do usuário para uma operação de controle de origem em uma chamada de função que o plug-in de controle de origem com suporte. Para que isso aconteça, o IDE e o plug-in de controle de origem devem ter uma caixa de diálogo efetivada que passa informações e para trás entre o IDE e o plug-in. Para essa caixa de diálogo ocorra, ambas devem falar o mesmo idioma. A API de plug-in de controle de origem descritos nesta documentação é o vocabulário comum para essa troca.  
  
 ![Diagrama de arquitetura de controle do código de origem](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch")  
Diagrama de arquitetura mostrando a interação entre VS e controle de origem plug-in  
  
 Conforme mostrado no diagrama da arquitetura, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell, rotulado como shell do VS no diagrama, hospeda projetos de trabalho e os componentes associados, como o Gerenciador de soluções e editores do usuário. O pacote de adaptador de controle de origem trata a interação entre o IDE e o plug-in de controle de origem. O pacote de adaptador de controle de origem fornece seu próprio controle de origem da interface do usuário. É a interface de usuário de nível superior que o usuário interage para iniciar e definir o escopo de uma operação de controle de origem.  
  
 O plug-in de controle de origem pode ter sua própria interface do usuário, que pode consistir em duas partes como mostrado na figura. A caixa de "Interface de usuário de fornecedor" representa elementos da interface do usuário personalizada fornecida por você, como um criador de plug-in de controle de origem. Eles são exibidos diretamente, o plug-in de controle de origem quando o usuário chama uma operação de controle do código-fonte avançadas. A caixa "Auxiliar de interface do usuário" é um conjunto de plug-in da interface do usuário recursos de controle fonte que são invocados indiretamente por meio do IDE. O plug-in de controle de origem passa mensagens relacionadas a interface do usuário para o IDE por meio de funções de retorno de chamada especiais fornecidos pelo IDE. O auxiliar de interface do usuário facilita uma integração perfeita com o IDE (geralmente através do uso de um **avançado** botão) e, portanto, fornece uma experiência de usuário final mais unificada.  
  
 Um plug-in de controle de origem não pode fazer alterações para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] de shell e, consequentemente, o pacote de adaptador de controle de origem ou fonte de controle fornecido pelo IDE de interface do usuário. Ele deve aproveitar ao máximo a flexibilidade oferecida por meio da implementação de várias funções de API de plug-in de controle de origem que contribuem para uma experiência integrada para o usuário final. A seção de referência da documentação de API de plug-in de controle de origem inclui informações para alguns recursos de plug-in de controle de origem avançadas. Para explorar esses recursos, o plug-in de controle de origem deve declarar seus recursos avançados para o IDE durante a inicialização e ele deve implementar funções avançadas específicas para cada recurso.  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle de origem](../../extensibility/source-control-plug-ins.md)   
 [Glossário](../../extensibility/source-control-plug-in-glossary.md)   
 [Criar um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)