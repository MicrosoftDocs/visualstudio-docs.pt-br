---
title: Determinando qual editor abre um arquivo em um projeto | Microsoft Docs
description: Saiba mais sobre as chaves do registro e os métodos do SDK do Visual Studio usados pelo Visual Studio para determinar qual editor abre um arquivo em um projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fb6f142ea25748f6798fb60d7c03862c51819349
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090857"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>Determinar qual editor abre um arquivo em um projeto
Quando um usuário abre um arquivo em um projeto, o ambiente passa por um processo de sondagem, eventualmente abrindo o editor ou designer apropriado para esse arquivo. O procedimento inicial empregado pelo ambiente é o mesmo para editores padrão e personalizados. O ambiente usa uma variedade de critérios ao sondar qual editor usar para abrir um arquivo e o VSPackage deve coordenar com o ambiente durante esse processo.

 Por exemplo, quando um usuário seleciona o comando **abrir** no menu **arquivo** e escolhe *filename. rtf* (ou qualquer outro arquivo com uma extensão *. rtf* ), o ambiente chama a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> implementação de cada projeto, eventualmente percorrendo todas as instâncias de projeto na solução. Os projetos retornam um conjunto de sinalizadores que identificam declarações em um documento por prioridade. Usando a prioridade mais alta, o ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método apropriado. Para obter mais informações sobre o processo de sondagem, consulte [Adicionar projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).

 O projeto de arquivos diversos declara todos os arquivos que não são reivindicados por outros projetos. Dessa forma, os editores personalizados podem abrir documentos antes que os editores padrão os abram. Se um projeto de arquivos diversos alegar um arquivo, o ambiente chamará o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para abrir o arquivo com um editor padrão. O ambiente verifica sua lista interna de editores registrados para um que manipula arquivos *. rtf* . Essa lista está localizada no registro na seguinte chave:

 **HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ \<version> \Editors \\ \<editor factory guid> \Extensions**

 O ambiente também verifica os identificadores de classe na chave **HKEY_CLASSES_ROOT\CLSID** para quaisquer objetos que tenham uma subchave **DocObject**. Se a extensão de arquivo for encontrada lá, uma versão incorporada do aplicativo, como o Microsoft Word, será criada in-loco no Visual Studio. Esses objetos de documento devem ser arquivos compostos que implementam a <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage> interface ou o objeto deve implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> interface.

 Se não houver nenhuma fábrica de editor para arquivos *. rtf* no registro, o ambiente procurará na chave **HKEY_CLASSES_ROOT \\ . rtf** e abrirá o editor especificado lá. Se a extensão de arquivo não for encontrada em **HKEY_CLASSES_ROOT**, o ambiente usará o editor de texto principal do Visual Studio para abrir o arquivo, se for um arquivo de texto.

 Se o editor de texto principal falhar, o que ocorrerá se o arquivo não for um arquivo de texto, o ambiente usará seu editor binário para o arquivo.

 Se o ambiente encontrar um editor para a extensão *. rtf* em seu registro, ele carregará o VSPackage que implementa essa fábrica de editor. O ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> método no novo VSPackage. O VSPackage chama o `QueryService` para `SID_SVsRegistorEditor` , usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> método para registrar a fábrica do editor com o ambiente.

 O ambiente agora verifica novamente sua lista interna de editores registrados para encontrar a fábrica de editor recém registrada para arquivos *. rtf* . O ambiente chama a implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método, passando o nome do arquivo e o tipo de exibição para criar.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>
- <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>
