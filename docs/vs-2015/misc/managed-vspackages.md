---
title: Gerenciado VSPackages | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSPackages, managed
- managed VSPackages
ms.assetid: a4f17068-c563-45a8-bbbf-4203ea99e9d2
caps.latest.revision: 34
manager: douge
ms.openlocfilehash: 44507112ceb3e7bed452ef4ced7633001224ad82
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49227065"
---
# <a name="managed-vspackages"></a>VSPackages gerenciados
Os tópicos a seguir explicam como criar um VSPackage. Um VSPackage é um módulo de software que estende o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE), fornecendo elementos de (UI) interface do usuário, serviços, projetos, editores e designers. Para obter mais informações, consulte [VSPackages](../extensibility/internals/vspackages.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usar assemblies de interoperabilidade do Visual Studio](../extensibility/internals/using-visual-studio-interop-assemblies.md)  
 Descreve a função e o local do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] assemblies de interoperabilidade e os namespaces que eles fornecem.  
  
 [Informações de HRESULT em código gerenciado](../misc/hresult-information-in-managed-code.md)  
 Discute como converte as informações de HRESULT para exceções geradas e `int` valores de retorno no código gerenciado.  
  
 [Marshaling do parâmetro de assembly de interoperabilidade do Visual Studio](../misc/visual-studio-interop-assembly-parameter-marshaling.md)  
 Discute problemas de interoperabilidade entre o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] assemblies de interoperabilidade e interfaces COM.  
  
 [Os VSPackages e a estrutura de pacote gerenciado](../misc/vspackages-and-the-managed-package-framework.md)  
 Descreve e lista os namespaces de classe do framework (MPF) de pacote gerenciado e arquivos DLL e mostra como usá-los para criar um VSPackage.  
  
 [Recursos em VSPackages](../extensibility/internals/resources-in-vspackages.md)  
 Descreve o uso de recursos gerenciados e não gerenciados em VSPackages gerenciados.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Utilitários VSSDK](../extensibility/internals/vssdk-utilities.md)  
 Apresenta um conjunto de recursos internos de VSPackage e tópicos avançados.