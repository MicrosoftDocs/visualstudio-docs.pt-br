---
title: Arquitetura de VSPackage do controle de origem | Microsoft Docs
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
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
caps.latest.revision: 26
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5fc639214757649dcc1bee191b7b268d7b6fdbcc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51802142"
---
# <a name="source-control-vspackage-architecture"></a>Arquitetura do VSPackage de controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um pacote de controle de origem é um VSPackage que usa os serviços que o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE fornece. Em troca, um pacote de controle do código-fonte fornece sua funcionalidade como um serviço de controle do código-fonte. Além disso, um pacote de controle de origem é uma alternativa mais versáteis que o plug-in para a integração de controle de origem em um controle de fonte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 Um controle de fonte plug-in para que implementa a API de plug-in de controle do código-fonte segue um contrato rígida. Por exemplo, um plug-in não pode substituir o padrão [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] interface do usuário (IU). Além disso, a API de plug-in de controle do código-fonte não permite um plug-in implementar seu próprio modelo de controle do código-fonte. No entanto, um pacote de controle de origem, supera essas limitações. Um pacote de controle de origem tem controle completo sobre a experiência de controle de origem de um [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] usuário. Além disso, um pacote de controle de origem pode usar seu próprio modelo de controle de origem e a lógica, e ele pode definir todas as interfaces de usuário relacionados ao controle de origem.  
  
## <a name="source-control-package-components"></a>Componentes de controle de origem do pacote  
 Conforme mostrado no diagrama da arquitetura, uma [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] componente denominado o Stub de controle do código-fonte é um VSPackage que integra um pacote de controle de origem com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 Stub de controle do código-fonte controla as tarefas a seguir.  
  
- Fornece a interface do usuário comum que é necessário para o registro do pacote de controle de origem.  
  
- Carrega um pacote de controle de origem.  
  
- Define um pacote de controle de origem como ativo/inativo.  
  
  Stub de controle do código-fonte entrada todas as chamadas de serviço do IDE para que o pacote de rotas e procura o serviço do Active Directory para o pacote de controle de origem.  
  
  O pacote de adaptador de controle do código-fonte é um controle de fonte especial de pacote que [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] fornece. Este pacote é o componente central para dar suporte a controle plug-ins de origem com base em que a API de plug-in de controle do código-fonte. Quando um plug-in de controle de origem é o plug-in Active Directory, o Stub de controle de origem envia seus eventos para o pacote de adaptador de controle do código-fonte. Por sua vez, o pacote de adaptador de controle do código-fonte se comunica com o plug-in de controle do código-fonte usando a API de plug-in de controle do código-fonte e também fornece uma interface do usuário que é comum para controle de origem todos os plug-ins padrão.  
  
  Quando um pacote de controle de origem é o pacote do Active Directory, por outro lado, o Stub de controle do código-fonte se comunica diretamente com o pacote usando o [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] interfaces de controle de origem de pacote. O pacote de controle de origem é responsável por hospedar seu próprio controle do código-fonte da interface do usuário.  
  
  ![Gráfico de arquitetura de controle do código-fonte](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")  
  
  Para um pacote de controle de origem, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] não fornece o código de controle do código-fonte ou uma API para integração. Compare isso com a abordagem descrita na [criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md) onde o plug-in de controle do código-fonte tem que implementar um conjunto rígido de funções e os retornos de chamada.  
  
  Como qualquer VSPackage, um pacote de controle de origem é um objeto COM que pode ser criado usando `CoCreateInstance`. O VSPackage se torna disponível para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE com a implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>. Quando uma instância tiver sido criada, um VSPackage recebe um ponteiro de site e um <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> interface que fornece o VSPackage acessem os serviços disponíveis e interfaces no IDE.  
  
  Escrever um pacote de controle de origem com base em VSPackage requer conhecimento de programação mais avançado que escrever uma API de plug-in de controle de origem com base no plug-in.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>   
 [Introdução](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

