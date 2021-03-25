---
title: Persistência e a tabela de documentos em execução | Microsoft Docs
description: Saiba como os projetos coordenam a abertura, a gravação e a renomeação de documentos na tabela de documentos em execução, que controla o estado do documento no IDE do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5244e14498da0f556a71b8d710ccbaa8b9b03e65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095115"
---
# <a name="persistence-and-the-running-document-table"></a>Persistência e a tabela de documentos em execução
No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE, os projetos são totalmente responsáveis por gerenciar a persistência de seus itens de projeto, que são realizados usando o serviço, <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> . Os documentos são a unidade básica de persistência no ambiente do Visual Studio. Os projetos coordenam a abertura, o salvamento e a renomeação de documentos com a tabela de documentos em execução (RDT), um recurso que controla o estado de todos os documentos abertos.

## <a name="managing-persistence"></a>Gerenciando a persistência
 Os projetos controlam o serviço de persistência do ambiente implementando a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> interface. Embora o ambiente nunca solicite diretamente que um documento persista, ele solicita que o projeto proprietário (ou hierarquia) salve o documento. Isso possibilita que o projeto Salve seus dados de item de projeto em arquivos locais, em arquivos remotos, em um banco de dado, em um repositório ou em outro meio.

 O ambiente global mantém o RDT. O ambiente mantém entradas para todas as janelas e documentos abertos no RDT, o que torna possível que eles recebam notificações especiais, como quando uma solução é fechada. Além disso, o RDT possibilita que o ambiente acompanhe seus nós correspondentes no **Gerenciador de soluções**. O RDT mantém um registro por objeto aberto e persistente, incluindo arquivos de projeto e documentos de item de projeto.

## <a name="see-also"></a>Confira também
- [Tabela de documento em execução](../../extensibility/internals/running-document-table.md)
- [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)
