---
title: Arquitetura de plug-in de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
caps.latest.revision: 25
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c7ded33f6296d9ddb0b87a3d2916a95249169f82
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805192"
---
# <a name="source-control-plug-in-architecture"></a>Arquitetura do plug-in de controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Você pode adicionar suporte de controle do código-fonte para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE), implementando e anexar um plug-in de controle do código-fonte. O IDE se conecta ao controle de fonte de plug-in por meio da API de plug-in de controle de origem bem definido. O IDE expõe os recursos de controle de versão do sistema de controle de origem, fornecendo uma interface do usuário (IU) que consiste em barras de ferramentas e comandos de menu. O plug-in de controle de origem implementa a funcionalidade de controle do código-fonte.  
  
## <a name="source-control-plug-in-resources"></a>Recursos de plug-in de controle do código-fonte  
 O plug-in de controle de origem fornece recursos para ajudar a criar e conectar seu aplicativo de controle de versão para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE. O plug-in de controle de origem contém a especificação de API que deve ser implementada por um plug-in de controle do código-fonte para que ele pode ser integrado a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE. Ele também contém um exemplo de código (escrito em C++) que implementa uma origem de esqueleto plug-in que demonstram implementação de controle de funções essenciais em conformidade com a API de plug-in de controle do código-fonte.  
  
 A especificação de API de plug-in de controle do código-fonte permite que você aproveite qualquer sistema de controle de origem de sua escolha, se você criar uma DLL de controle do código-fonte com o conjunto necessário de funções implementadas de acordo com a API de plug-in de controle do código-fonte.  
  
## <a name="components"></a>Componentes  
 O pacote de adaptador de controle de origem no diagrama é o componente do IDE que converte a solicitação do usuário para uma operação de controle do código-fonte em uma chamada de função compatível com o plug-in de controle de origem. Para que isso aconteça, o IDE e o plug-in de controle de origem devem ter uma caixa de diálogo efetivada que passa informações e para trás entre o IDE e o plug-in. Para esta caixa de diálogo entrar em vigor, ambos devem falarem o mesmo idioma. A API de plug-in de controle do código-fonte descritos nesta documentação é o vocabulário comum para essa troca.  
  
 ![Diagrama de arquitetura de controle do código de origem](../../extensibility/internals/media/vs-sccsdk-plug-in-arch.gif "vs_sccsdk_plug_in_arch")  
Diagrama de arquitetura mostrando a interação entre o VS e o controle de fonte de plug-in  
  
 Conforme mostrado no diagrama da arquitetura, o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] shell, rotulada como VS shell no diagrama, hospeda projetos de trabalho e componentes associados, como editores e do Gerenciador de soluções do usuário. O pacote de adaptador de controle do código-fonte manipula a interação entre o IDE e o plug-in de controle do código-fonte. O pacote de adaptador de controle do código-fonte fornece seu próprio controle do código-fonte da interface do usuário. Ele é a interface de usuário de nível superior que o usuário interage com a fim de iniciar e definir o escopo de uma operação de controle do código-fonte.  
  
 O plug-in de controle do código-fonte pode ter sua própria interface do usuário, que pode consistir em duas partes como mostrado na figura. A caixa rotulada "Interface do usuário do fornecedor" representa os elementos de interface do usuário personalizada fornecida por você, como um criador de plug-in de controle de origem. Eles são exibidos diretamente, o plug-in de controle do código-fonte quando o usuário invoca uma operação de controle de código-fonte avançadas. A caixa rotulada "Auxiliar de interface do usuário" é um conjunto de recursos código-fonte controle plug-in da interface do usuário que são invocados indiretamente por meio do IDE. O plug-in de controle do código-fonte passa mensagens relacionadas a interface do usuário para o IDE através das funções de retorno de chamada especial fornecida pelo IDE. O auxiliar de interface do usuário facilita uma integração perfeita com o IDE (geralmente por meio do uso de um **avançado** botão) e, portanto, fornece uma experiência mais unificada do usuário final.  
  
 Um plug-in de controle do código-fonte não pode fazer alterações para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] de shell e, consequentemente, o pacote de adaptador de controle do código-fonte ou a fonte de controle da interface do usuário fornecida pelo IDE. Ele deve aproveitar ao máximo a flexibilidade oferecida por meio da implementação das várias funções de API de plug-in de controle de origem que contribuem para uma experiência integrada para o usuário final. A seção de referência da documentação de API de plug-in de controle do código-fonte inclui informações para alguns recursos de plug-in de controle de origem avançada. Para explorar esses recursos, o plug-in de controle do código-fonte deve declarar seus recursos avançados para o IDE durante a inicialização, e ele deve implementar funções avançadas específicas para cada recurso.  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle de origem](../../extensibility/source-control-plug-ins.md)   
 [Glossário](../../extensibility/source-control-plug-in-glossary.md)   
 [Criar um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)

