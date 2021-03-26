---
title: Diretrizes de controle do código-fonte para projetos e editores
description: Saiba mais sobre as diretrizes que os projetos e editores devem aderir para dar suporte ao controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2509f2f6f9da91c3df60d6b041d5ebb6bdd367b6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079001"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>Diretrizes adicionais de controle do código-fonte para projetos e editores
Há várias diretrizes que os projetos e editores devem seguir para dar suporte ao controle do código-fonte.

## <a name="guidelines"></a>Diretrizes
 Seu projeto ou editor também deve fazer o seguinte para dar suporte ao controle do código-fonte:

|Área|Project|Editor|Detalhes|
|----------|-------------|------------|-------------|
|Cópias particulares de arquivos|X||O ambiente oferece suporte a cópias particulares de arquivos. Ou seja, cada pessoa listada no projeto tem sua própria cópia privada dos arquivos nesse projeto.|
|Persistência de ANSI/Unicode|X|X|Se você escrever o código de persistência, persiste arquivos no formato ANSI porque a maioria dos programas de controle do código-fonte atualmente não oferece suporte a Unicode.|
|Enumerar arquivos|X||O projeto deve conter uma lista específica de todos os arquivos dentro dele e deve ser capaz de enumerar a lista de arquivos usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (VSH_PROPID_First_Child/Next_Sibling). O projeto também deve expor nomes de itens por meio de sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A> implementação e pesquisa de nome de suporte (incluindo arquivos especiais) por meio de sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> implementação.|
|Formato de texto|X|X|Quando possível, os arquivos devem estar no formato de texto para dar suporte à mesclagem de versões diferentes. Os arquivos que não estão no formato de texto não podem ser mesclados com outras versões do arquivo posteriormente. O formato de texto preferencial é XML.|
|Baseado em referência|X||Os projetos baseados em referência têm suporte imediato no controle do código-fonte. No entanto, os projetos baseados em diretório também têm suporte pelo controle do código-fonte, desde que o projeto possa produzir uma lista de seus arquivos sob demanda, independentemente de esses arquivos existirem no disco. Ao abrir um projeto do controle do código-fonte, o arquivo de projeto é desativado primeiro antes de qualquer um de seus arquivos.|
|Manter objetos e propriedades em ordem previsível|X|X|Mantenha seus arquivos em uma ordem previsível, como ordem alfabética, para facilitar a mesclagem.|
|Recarregar|X|X|Quando um arquivo é alterado no disco, seu editor deve ser capaz de recarregá-lo. Quando você participa do controle do código-fonte, o ambiente recarregará os dados para você chamando sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> implementação. O caso de recarga mais difícil é quando ocorre um check-out quando você chamou IVsQueryEditQuerySave:: <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e está processando informações. No entanto, seu código de recarga deve ser capaz de executar nessa situação.<br /><br /> O ambiente recarrega automaticamente os arquivos de projeto. No entanto, um projeto deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> se tiver hierarquias aninhadas a fim de dar suporte ao recarregamento de arquivos de projeto aninhados.|

## <a name="see-also"></a>Confira também
- [Suporte ao controle do código-fonte](../../extensibility/internals/supporting-source-control.md)
