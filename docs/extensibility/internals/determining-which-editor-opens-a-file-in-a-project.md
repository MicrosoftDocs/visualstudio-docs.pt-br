---
title: Determinando qual Editor abre um arquivo em um projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 655a5a28e3e16a1b07c52c37ef00d89d145a17a1
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39498536"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>Determinar qual editor abre um arquivo em um projeto
Quando um usuário abre um arquivo em um projeto, o ambiente passa por um processo de sondagem, eventualmente, abrindo o editor apropriado ou o designer para esse arquivo. O procedimento inicial empregado pelo ambiente é o mesmo para os editores padrão e personalizadas. O ambiente usa uma variedade de critérios ao sondar qual editor a ser usado para abrir um arquivo e o VSPackage deve coordenar com o ambiente durante esse processo.  
  
 Por exemplo, quando um usuário seleciona o **aberto** comando da **arquivo** menu e, em seguida, escolhe *filename.rtf* (ou qualquer outro arquivo com um *. rtf*extensão), o ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> implementação para cada projeto, eventualmente circulando através de todas as instâncias do projeto na solução. Projetos de retornam um conjunto de sinalizadores que identificam as declarações em um documento por prioridade. Usando a prioridade mais alta, o ambiente chama apropriado <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método. Para obter mais informações sobre o processo de sondagem, consulte [adicionar o projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).  
  
 Todos os arquivos que não são solicitados por outros projetos de declarações do projeto arquivos diversos. Dessa forma, editores personalizados podem abrir documentos antes de editores padrão abri-los. Se um projeto arquivos diversos declarações em um arquivo, o ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para abrir o arquivo com um editor padrão. O ambiente verifica sua lista interna de editores registrados para um que manipula *. rtf* arquivos. Esta lista está localizada no registro na seguinte chave:  
  
 **HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\\<versão > \Editors\\\<guid de fábrica do editor > \Extensions**
  
 O ambiente também verifica os identificadores de classe **HKEY_CLASSES_ROOT\CLSID** chaves para todos os objetos que têm uma subchave **DocObject**. Se a extensão de arquivo for encontrada lá, uma versão incorporada do aplicativo, como o Microsoft Word, será criada no local no Visual Studio. Esses objetos de documento devem ser arquivos compostos que implementam o <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage> interface ou o objeto deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> interface.  
  
 Se não houver nenhuma fábrica de editor para *. rtf* arquivos no registro, em seguida, examina o ambiente a **HKEY_CLASSES_ROOT\\. rtf** da chave e abre o editor especificado existe. Se a extensão de arquivo não for encontrada na **HKEY_CLASSES_ROOT**, em seguida, o ambiente usa o editor de texto de principal do Visual Studio para abrir o arquivo, se ele for um arquivo de texto.  
  
 Se o editor de texto principal falhar, o que ocorre que se o arquivo não for um arquivo de texto, em seguida, o ambiente usa seu editor binário para o arquivo.  
  
 Se o ambiente de encontrar um editor para o *. rtf* extensão no seu registro, ele carrega o VSPackage que implementa a fábrica de editor. O ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> método no novo VSPackage. As chamadas de VSPackage `QueryService` para `SID_SVsRegistorEditor`, usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> método para registrar a fábrica do editor com o ambiente.  
  
 O ambiente agora verifica novamente a sua lista interna de editores registrados para localizar a fábrica de editor registrado recentemente para *. rtf* arquivos. O ambiente chama sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método, passando o tipo de nome e o modo de exibição de arquivo para criar.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>   
 <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>