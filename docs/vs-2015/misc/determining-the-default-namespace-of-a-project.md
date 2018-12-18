---
title: Determinando o Namespace padrão de um projeto | Microsoft Docs
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
- custom tools, computing default namespace
ms.assetid: 6d890676-7016-458c-8a6a-95cc0a068612
caps.latest.revision: 13
manager: douge
ms.openlocfilehash: c37c6f69c52677c1bd029f5e6c60d15313425abc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49950944"
---
# <a name="determining-the-default-namespace-of-a-project"></a>Determinando o Namespace padrão de um projeto
Para [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], se o `CustomToolNamespace` propriedade é definida no arquivo de entrada, em seguida, o valor de `CustomToolNamespace` torna-se o valor do parâmetro de namespace padrão passado para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> método. Caso contrário, o `wszDefaultNamespace` parâmetro passado para `Generate` é sempre igual ao namespace raiz. Para obter mais informações sobre namespaces, consulte [palavras-chave do Namespace](http://msdn.microsoft.com/library/091a66eb-b10d-4f54-9102-5ac0d4bdb84b).  
  
 [!INCLUDE[csprcs](../includes/csprcs-md.md)] usa namespaces baseados em pastas. Ou seja, o espaço para nome consiste o namespace raiz, além de nomes de qualquer pasta que contém a ferramenta personalizada. Cada nome de pasta é convertido em um identificador válido e períodos separam todos os nomes. Por exemplo, se o arquivo de entrada é FolderA\FolderB\FolderC\MyInput.txt e o namespace raiz é CL9, o namespace padrão computada seria **CL9. FolderA.FolderB.FolderC**.  
  
 Uma exceção a essa regra ocorre quando a cadeia de hierarquia contém uma pasta de referência da Web. Por exemplo, se:  
  
- FolderC eram uma pasta de referência da Web, o namespace seria **CL9. FolderC**.  
  
- PastaB eram uma pasta de referência da Web, o namespace seria **CL9. FolderB.FolderC**.  
  
  Ou seja, o namespace usa o seguinte formato:  
  
```  
rootNamespace.webReferenceFolder.containedFolder.containedFolder ...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Implementando geradores de arquivo único](../extensibility/internals/implementing-single-file-generators.md)   
 [Registrar geradores de arquivo único](../extensibility/internals/registering-single-file-generators.md)   
 [Expor tipos aos designers visuais](../extensibility/internals/exposing-types-to-visual-designers.md)