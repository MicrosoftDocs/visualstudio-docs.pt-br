---
title: As diretrizes de controle de origem adicionais para projetos e editores | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 454984334cbd91833447829227787b0679b4ed54
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497713"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>Diretrizes de controle de origem adicionais para projetos e editores
Há uma série de diretrizes que projetos e editores devem aderir a fim de dar suporte ao controle do código-fonte.  
  
## <a name="guidelines"></a>Diretrizes  
 O projeto ou o editor também deve fazer o seguinte para dar suporte a controle de origem:  
  
|Área|Projeto|Editor|Detalhes|  
|----------|-------------|------------|-------------|  
|Cópias privadas de arquivos|X||O ambiente dá suporte a cópias privadas de arquivos. Ou seja, cada pessoa inscrita no projeto tem sua própria cópia privada dos arquivos no projeto.|  
|Persistência de Unicode/ANSI|X|X|Se você escrever o código de persistência, manter os arquivos no formato ANSI porque a maioria dos programas de controle do código-fonte não damos suporte a Unicode.|  
|Enumerar arquivos|X||O projeto deve conter uma lista específica de todos os arquivos dentro dele e deve ser capaz de enumerar a lista de arquivos usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (VSH_PROPID_First_Child/Next_Sibling). O projeto também deve expor os nomes de item por meio de seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A> implementação e suporte à pesquisa de nome (incluindo arquivos especiais) por meio de seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> implementação.|  
|Formato de texto|X|X|Quando possível, os arquivos devem estar no formato de texto para dar suporte a mesclagem de versões diferentes. Arquivos que não estão no formato de texto não podem ser mesclados com outras versões do arquivo mais tarde. O formato de texto preferido é XML.|  
|Base de referência|X||Projetos baseados em referência prontamente têm suporte no controle de origem. No entanto, projetos baseados em diretório também são suportados pelo controle do código-fonte, desde que o projeto pode produzir uma lista de seus arquivos sob demanda, independentemente de existirem esses arquivos no disco. Ao abrir um projeto do controle de origem, o arquivo de projeto é interrompido primeiro antes de qualquer um dos seus arquivos.|  
|Persistir objetos e propriedades em ordem previsível|X|X|Persista seus arquivos em uma ordem previsível, como ordem alfabética, para facilitar a mesclagem.|  
|Recarregar|X|X|Quando um arquivo é alterado no disco, seu editor deve ser capaz de recarregá-lo. Quando você participa no controle de origem, o ambiente será recarregar dados para você, chamando seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> implementação. O caso de recarregar mais difíceis é quando um check-out ocorre quando você tiver chamado IVsQueryEditQuerySave::<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e são processamento das informações. No entanto, seu código de recarregar deve ser capaz de executar nessa situação.<br /><br /> O ambiente recarrega automaticamente arquivos de projeto. No entanto, um projeto deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> se ele tiver aninhado hierarquias para dar suporte a recarregamento aninhados arquivos de projeto.|  
  
## <a name="see-also"></a>Consulte também  
 [Dar suporte ao controle do código-fonte](../../extensibility/internals/supporting-source-control.md)