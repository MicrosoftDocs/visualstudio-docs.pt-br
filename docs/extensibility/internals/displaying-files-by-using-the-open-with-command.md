---
title: Exibir arquivos usando o aberto com o comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open With command
- Open With command
- persistence, supporting Open With command
ms.assetid: 53794bc3-1b73-4d40-954e-cfade1abddcf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5ba2aa9ad9a80a820a1ab8311280c3bf2dedc476
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53820245"
---
# <a name="display-files-by-using-the-open-with-command"></a>Exibir arquivos usando o comando Abrir com
Um projeto pode fazer o IDE para exibir o **abrir com** caixa de diálogo. Essa solicitação solicita que o usuário abrir um arquivo que tem uma seleção de editores padrão. As etapas a seguir descrevem esse processo:  
  
1.  As chamadas de projeto <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>, especificando um valor de `OSE_UseOpenWithDialog` para o `OSEOpenDocEditor` parâmetro.  
  
2.  Com base na extensão de nome de arquivo do documento, o IDE determina quais editores listados no registro podem abram o documento especificado e exibe essas informações na **abrir com** caixa de diálogo.  
  
    > [!NOTE]
    >  Projetos que têm um editor intrínseco que deve ser incluído na **abrir com** caixa de diálogo deve ser registrado uma fábrica de editor para cada editor tal. Editores intrínseco só funcionam junto com um tipo específico de projeto, que é imposto na implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método. O IDE tem uma fábrica de editor interno para o editor de texto principal e o editor binário. O IDE também cria uma instância de uma fábrica de editor em nome de cada associação de arquivo do Windows registrada. Um exemplo desse arquivo é o Microsoft Word.  
  
3.  Assim que o usuário seleciona um item do **abrir com** caixa de diálogo, o IDE, em seguida, abre o documento chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método. Para obter mais informações, confira [Como: Abrir editores padrão](../../extensibility/how-to-open-standard-editors.md).  
  
## <a name="see-also"></a>Consulte também  
 [Abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)   
 [Exibir arquivos usando o comando Abrir arquivo](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)   
 [Como: Abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)
