---
title: Comando contratos em Assemblies de interoperabilidade | Microsoft Docs
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
- command handling with interop assemblies, command contracts
- interop assemblies, command contracts
ms.assetid: 57245708-f539-42dc-8963-2754a48f0189
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8089314293c92a24396a90f4be4dd4120c03bbcd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725089"
---
# <a name="command-contracts-in-interop-assemblies"></a>Contratos de comando em assemblies de interoperabilidade
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O contrato básico para lidar com comandos por meio de <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface é que o ambiente chama o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método para determinar se há suporte para o comando e, se houver suporte, para determinar seu estado e texto. Em seguida, o ambiente chama o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método para executar o comando.  
  
 O <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método é tratado de forma idêntica para todos os comandos. A comunicação adicional, se necessário (por exemplo, com listas suspensas) é gerenciada por meio da chamada a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método com os parâmetros apropriados. A interpretação desses parâmetros depende do comando especificado.  
  
 Se o destino do comando retorna os valores no parâmetro de saída, o chamador sempre é responsável por liberar quaisquer recursos que foram alocados. Como esse parâmetro é uma variante, limpando a variante libera os recursos.  
  
 Em casos em que os comandos devem operar dentro de uma janela de hierarquia, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface deve ser usada. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface tem um contrato semelhante com métodos semelhantes: <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da Interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Roteamento de comando em VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)   
 [Implementação](../../extensibility/internals/command-implementation.md)

