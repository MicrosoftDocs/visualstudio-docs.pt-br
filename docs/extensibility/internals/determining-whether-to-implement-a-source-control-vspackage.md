---
title: Determinar se deve implementar um VSPackage de controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d3bef6030b6a21eeda708a5258c47c9dfdcfc0a3
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497307"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>Determinar se deve implementar um VSPackage de controle do código-fonte
Esta seção aborda as opções de plug-ins de controle do código-fonte e os VSPackages de controle de origem para estender o controle de fonte de soluções e fornece diretrizes amplas sobre como escolher um caminho de integração adequada.  
  
## <a name="small-source-control-solution-with-limited-resources"></a>Solução de controle de origem pequenas com recursos limitados  
 Se você tiver recursos limitados e não pode ser sobrecarregado com a sobrecarga de escrever um pacote de controle do código-fonte, você pode criar plug-ins baseados na API de plug-in de controle do código-fonte. Isso permite que você trabalhe lado a lado com pacotes de controle do código-fonte, e você pode alternar entre pacotes sob demanda e plug-ins de controle de origem. Para obter mais informações, consulte [registro e seleção](../../extensibility/internals/registration-and-selection-source-control-vspackage.md).  
  
## <a name="large-source-control-solution-with-a-rich-feature-set"></a>Solução de controle de origem grande com um rico conjunto de recursos  
 Se você quiser implementar uma solução de controle do código-fonte que fornece um modelo de controle de fonte avançada que não é capturado adequadamente, usando a API de plug-in de controle do código-fonte, você pode considerar um pacote de controle do código-fonte como o caminho de integração. Isso se aplica especialmente se você substituiria o pacote do adaptador de controle de origem (que se comunica com o plug-ins de controle do código-fonte e fornece um controle de origem básico da interface do usuário) em vez disso, com seu próprio para que você pode manipular os eventos de controle de origem de uma maneira personalizada. Se você já tiver uma fonte satisfatória de controle da interface do usuário e deseja preservar essa experiência em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], a opção de controle de origem do pacote lhe permite fazer exatamente isso. O pacote de controle de origem não é genérico e destina-se unicamente para uso com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.  
  
 Se você quiser implementar uma solução de controle do código-fonte que fornece flexibilidade e controle avançado sobre a lógica de controle do código-fonte e a interface do usuário, talvez você prefira a rota de integração de pacote de controle de origem. Você pode:  
  
1.  Registrar seu próprio VSPackage de controle do código-fonte (consulte [registro e seleção](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)).  
  
2.  Substitua o controle de fonte padrão da interface do usuário com sua interface do usuário personalizada (consulte [interface do usuário personalizada](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)).  
  
3.  Especifique os glifos a ser usada e manipular eventos de glifo do Gerenciador de soluções (veja [controle de glifo](../../extensibility/internals/glyph-control-source-control-vspackage.md)).  
  
4.  Manipular eventos de consulta de editar e salvar consulta (consulte [consulta Editar consulta salvar](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um controle de fonte plug-in](../../extensibility/internals/creating-a-source-control-plug-in.md)