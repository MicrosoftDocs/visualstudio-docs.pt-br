---
title: Comandos e Menus que usam Assemblies de interoperabilidade | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ad6b324953914df7103d0dec7371199e3cbbd937
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195041"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>Comandos e menus que usam assemblies de interoperabilidade
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um VSPackage que implementa os comandos de menu e barra de ferramentas usando assemblies de interoperabilidade deve:  
  
- Informar o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) sobre os comandos que ele suporta e se elas estão habilitadas.  
  
- Aderir às regras (contrato) para lidar com comandos.  
  
- Implementar explicitamente a manipulação de comando, usando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface.  
  
  O exemplo a seguir descreve como realizar essas tarefas.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Determinar o status do comando usando assemblies de interoperabilidade](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)  
 Descreve como um VSPackage notifica o IDE sobre os comandos que ele dá suporte e se elas estão habilitadas.  
  
 [Contratos de comando em assemblies de interoperabilidade](../../extensibility/internals/command-contracts-in-interop-assemblies.md)  
 Fornece uma definição de contrato comando básico usado por todos os VSPackages implementando comandos usando assemblies de interoperabilidade  
  
 [Implementação](../../extensibility/internals/command-implementation.md)  
 Fornece uma visão geral de como um VSPackage implementa um comando.  
  
 [Registrar manipuladores de comandos do assembly de interoperabilidade](../../extensibility/internals/registering-interop-assembly-command-handlers.md)  
 Descreve as entradas do registro necessárias para notificar o IDE que um VSPackage fornece um manipulador de comandos.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Disponibilidade](../../extensibility/internals/command-availability.md)  
 Descreve os critérios que são usados pelo IDE para determinar quais comandos VSPackage estão disponíveis e trata nos quais o objeto.  
  
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)  
 Fornece detalhes sobre como criar uma interface do usuário que usa [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] suporte de comando.  
  
 [Roteamento de comando em VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)  
 Uma visão geral do processo usado para relacionar um objeto com a solicitação de comando correto.
