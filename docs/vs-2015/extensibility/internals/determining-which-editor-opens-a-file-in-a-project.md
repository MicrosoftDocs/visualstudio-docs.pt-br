---
title: Determinando qual Editor abre um arquivo em um projeto | Microsoft Docs
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
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 832fd838246c075087700494b09757184be687a7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741613"
---
# <a name="determining-which-editor-opens-a-file-in-a-project"></a>Determinando qual editor abre um arquivo em um projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando um usuário abre um arquivo em um projeto, o ambiente passa por um processo de sondagem, eventualmente, abrindo o editor apropriado ou o designer para esse arquivo. O procedimento inicial empregado pelo ambiente é o mesmo para os editores padrão e personalizadas. O ambiente usa uma variedade de critérios ao sondar qual editor a ser usado para abrir um arquivo e o VSPackage deve coordenar com o ambiente durante esse processo.  
  
 Por exemplo, quando um usuário seleciona o **aberto** comando da **arquivo** menu e, em seguida, escolhe `filename`. rtf (ou qualquer outro arquivo com uma extensão. rtf), as chamadas de ambiente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> implementação para cada projeto, eventualmente circulando através de todas as instâncias do projeto na solução. Projetos de retornam um conjunto de sinalizadores que identificam as declarações em um documento por prioridade. Usando a prioridade mais alta, o ambiente chama apropriado <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método. Para obter mais informações sobre o processo de sondagem [adicionando projeto e modelos de Item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).  
  
 Todos os arquivos que não são solicitados por outros projetos de declarações do projeto arquivos diversos. Dessa forma, editores personalizados podem abrir documentos antes de editores padrão abri-los. Se um projeto arquivos diversos declarações em um arquivo, o ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para abrir o arquivo com um editor padrão. O ambiente verifica sua lista interna de editores registrados para aquele que trata de arquivos. rtf. Esta lista está localizada no registro na seguinte chave:  
  
 [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\<`version`> \Editors\\{<`editor factory guid`>} \Extensions]  
  
 O ambiente também verifica se os identificadores de classe na chave HKEY_CLASSES_ROOT\CLSID para todos os objetos que têm DocObject sub-chave. Se a extensão de arquivo for encontrada lá, uma versão incorporada do aplicativo, como o Microsoft Word, será criada no local no Visual Studio. Esses objetos de documento devem ser arquivos compostos que implementam o <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage> interface ou o objeto deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> interface.  
  
 Se não há nenhuma fábrica de editor para arquivos. rtf no registro, o ambiente examina o HKEY_CLASSES_ROOT \\chave. rtf e abre o editor especificado existe. Se a extensão de arquivo não for encontrada em HKEY_CLASSES_ROOT, o ambiente usa o editor de texto de principal do Visual Studio para abrir o arquivo se ele for um arquivo de texto.  
  
 Se o editor de texto principal falhar, o que ocorre que se o arquivo não for um arquivo de texto, em seguida, o ambiente usa seu editor binário para o arquivo.  
  
 Se o ambiente de encontrar um editor para a extensão. RTF em seu registro, ele carregará o VSPackage que implementa a fábrica de editor. O ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> método no novo VSPackage. As chamadas de VSPackage `QueryService` para `SID_SVsRegistorEditor`, usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> método para registrar a fábrica do editor com o ambiente.  
  
 O ambiente agora verifica novamente sua lista interna de editores registrados para localizar a fábrica de editor registrado recentemente de arquivos. rtf. O ambiente chama sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método, passando o tipo de nome e o modo de exibição de arquivo para criar.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>   
 <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>

