---
title: Tabela de documento de persistência e a execução | Microsoft Docs
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
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b734d21950fd3765a7c331bbcdc47177f48e2b0a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726093"
---
# <a name="persistence-and-the-running-document-table"></a>Persistência e a tabela de documentos em execução
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE, os projetos são completamente responsáveis por gerenciar a persistência dos seus itens de projeto, eles realizar usando o serviço, <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>. Documentos são a unidade básica de persistência no ambiente do Visual Studio. Projetos de coordenam a abertura, salvando e renomeando de documentos com a tabela em execução documento (RDT), um recurso que controla o estado de todos os documentos abertos.  
  
## <a name="managing-persistence"></a>Gerenciamento da persistência  
 Projetos de controle de serviço de persistência do ambiente, Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> interface. Enquanto o ambiente nunca diretamente solicita um documento para persistir em si, ele solicita o projeto proprietário (ou hierarquia) para salvar o documento. Isso torna possível para o projeto salvar seus dados de item de projeto em arquivos locais, arquivos remotos, um banco de dados, um repositório ou outro meio.  
  
 O ambiente global mantém o RDT. O ambiente mantém as entradas para todas as janelas abertas e documentos em RDT, o que torna possível para que eles possam recebem notificações especiais, como quando uma solução é fechada. Além disso, o RDT torna possível para o ambiente controlar seus nós correspondentes na **Gerenciador de soluções**. O RDT mantém um registro por objeto aberto, persistente, incluindo arquivos de projeto e documentos de item de projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Tabela de documento em execução](../../extensibility/internals/running-document-table.md)   
 [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)

