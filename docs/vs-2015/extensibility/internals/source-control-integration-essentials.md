---
title: Fundamentos da integração do controle de origem | Microsoft Docs
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
- Source Control Integration, essentials
- Source Control Integration,overview
- essentials, Source Control Integration
ms.assetid: 442057cb-fd54-4283-96f8-2f6dc8bf2de7
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9893d5525bf66b167dea170c0c5fae8285aa40af
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780965"
---
# <a name="source-control-integration-essentials"></a>Conceitos básicos da integração do controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] dá suporte a dois tipos de integração de controle do código-fonte: um plug-in de controle de origem que fornece a funcionalidade básica e é criado usando a API de plug-in de controle do código-fonte (anteriormente conhecido como a API de MSSCCI) e uma solução de integração de controle do código-fonte com base em VSPackage que fornece a funcionalidade mais robusta.  
  
## <a name="source-control-plug-in"></a>Plug-in de controle do código-fonte  
 Um plug-in de controle do código-fonte é gravada como uma DLL que implementa a API de plug-in de controle do código-fonte. Funcionalidade de integração de controle de origem e de registro é fornecida por meio da API. Essa abordagem é mais fácil de implementar do que um VSPackage de controle do código-fonte e usa o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] interface do usuário (UI) para a maioria das operações de controle do código-fonte.  
  
 Para implementar um plug-in para usar a API de plug-in de controle do código-fonte do controle de fonte, siga estas etapas:  
  
1. Criar uma DLL que implementa as funções especificadas na [Plug-ins de controle de origem](../../extensibility/source-control-plug-ins.md).  
  
2. Registrar a DLL, tornando as entradas de registro apropriadas, conforme descrito em [como: instalar um plug-in de controle do código-fonte](../../extensibility/internals/how-to-install-a-source-control-plug-in.md).  
  
3. Criar um auxiliar de interface do usuário e exibi-la quando for solicitado pelo pacote de adaptador de controle de origem (o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] componente que manipula a funcionalidade de controle do código-fonte por meio do plug-ins de controle do código-fonte).  
  
   Para obter mais informações, consulte [criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md).  
  
## <a name="source-control-vspackage"></a>VSPackage de controle do código-fonte  
 Um implementação de VSPackage do controle de origem permite que você desenvolva uma substituição personalizada para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] da interface do usuário do controle de origem. Essa abordagem fornece controle total sobre a integração de controle do código-fonte, mas exige que você forneça os elementos de interface do usuário e implementam as interfaces de controle do código-fonte que outra forma seriam fornecidas sob a abordagem de plug-in.  
  
 Para implementar um VSPackage de controle do código-fonte, faça o seguinte:  
  
1. Criar e registrar seu próprio controle do código-fonte VSPackage, conforme descrito em [registro e seleção](../../extensibility/internals/registration-and-selection-source-control-vspackage.md).  
  
2. Substitua o controle de fonte padrão da interface do usuário com sua interface do usuário personalizada. Ver [Interface do usuário personalizada](../../extensibility/internals/custom-user-interface-source-control-vspackage.md).  
  
3. Especificar glifos a ser usada e manipular **Gerenciador de soluções** eventos de glifo. Ver [controle de glifo](../../extensibility/internals/glyph-control-source-control-vspackage.md).  
  
4. Manipular eventos de consulta de editar e salvar consulta, conforme mostrado na [consulta Editar consulta salvar](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md).  
  
   Para obter mais informações, consulte [criando um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral](../../extensibility/internals/source-control-integration-overview.md)   
 [Criando um controle de fonte plug-in](../../extensibility/internals/creating-a-source-control-plug-in.md)   
 [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)

