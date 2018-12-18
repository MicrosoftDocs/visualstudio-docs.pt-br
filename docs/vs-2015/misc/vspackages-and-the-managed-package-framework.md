---
title: Os VSPackages e a estrutura de pacote gerenciado | Microsoft Docs
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
- managed package framework
- VSPackages, managed package framework
- managed VSPackages, managed package framework
ms.assetid: e8d80e0f-6b5b-4baf-a7df-59fd808c60cd
caps.latest.revision: 16
manager: douge
ms.openlocfilehash: 2e265a342ec32abea40ab9b352b5735079462a46
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49227975"
---
# <a name="vspackages-and-the-managed-package-framework"></a>Os VSPackages e a estrutura de pacote gerenciado
Você pode reduzir o tempo de desenvolvimento com a criação de um VSPackage com o pacote gerenciado classes do framework (MPF) em vez de por meio de classes de interoperabilidade COM.  
  
 Há duas maneiras de criar um VSPackage gerenciado:  
  
-   Use o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelo de projeto de pacote  
  
     Para obter mais informações, consulte [instruções passo a passo: Criando um Menu de comando usando o modelo de pacote do Visual Studio](http://msdn.microsoft.com/library/1985fa7d-aad4-4866-b356-a125b6a246de).  
  
-   Compilar o VSPackage sem o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelo de projeto de pacote  
  
     Por exemplo, você pode copiar um exemplo de VSPackage e alterar os GUIDs e os nomes. Você pode encontrar exemplos na seção VSX [Galeria de códigos](http://code.msdn.microsoft.com/vsx/).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Classes da estrutura de pacote gerenciado](../misc/managed-package-framework-classes.md)  
 Descreve e lista os namespaces de classe MPF e arquivos DLL.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Passo a passo: Criando um comando de Menu usando o modelo de pacote do Visual Studio](http://msdn.microsoft.com/library/1985fa7d-aad4-4866-b356-a125b6a246de)  
 Explica como criar um VSPackage gerenciado.  
  
 [VSPackages gerenciados](../misc/managed-vspackages.md)  
 Apresenta os aspectos de VSPackages que se aplicam ao código gerenciado.