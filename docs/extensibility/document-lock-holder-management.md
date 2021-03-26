---
title: Gerenciamento de suporte de bloqueio de documento | Microsoft Docs
description: Saiba como inserir um bloqueio de edição em um documento na tabela de documentos em execução sem que o usuário veja um documento aberto em uma janela de documento.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88e66ed3b0a5434f4d875bf941e3eeffb8adc092
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091182"
---
# <a name="document-lock-holder-management"></a>Gerenciamento de titular de bloqueio de documento

A tabela de documentos em execução (RDT) mantém uma contagem de documentos abertos e de quaisquer bloqueios de edição que eles têm. Você pode inserir um bloqueio de edição em um documento no RDT quando ele for editado de forma programática em segundo plano sem que o usuário veja um documento aberto em uma janela de documento. Essa funcionalidade é geralmente usada por designers que modificam vários arquivos por meio de uma interface gráfica do usuário.

## <a name="document-lock-holder-scenarios"></a>Cenários de detentor de bloqueio de documento

### <a name="file-a-has-a-dependence-on-file-b"></a>O arquivo "a" tem uma dependência no arquivo "b"

Considere uma situação em que você implementa um editor padrão "A" para o tipo de arquivo "a", e cada arquivo do tipo "a" tem uma referência a (ou dependência) de um arquivo do tipo "b". Um editor padrão "B" existe para arquivos do tipo "b". Quando o editor "A" abre o arquivo "a", ele recupera a referência ao arquivo "b" correspondente. O arquivo "b" não é exibido, mas o editor "A" pode modificá-lo. O editor "A" Obtém uma referência para os dados de documento do arquivo "b" do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método e também mantém um bloqueio de edição no arquivo "b". Depois que o editor "A" terminar de modificar o arquivo "b", você poderá decrementar a contagem de bloqueios de edição no arquivo "b" chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> método. Você pode omitir essa etapa se tiver chamado o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método com o parâmetro `dwRDTLockType` definido como [_VSRDTFLAGS. RDT_NoLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_NoLock>).

### <a name="file-b-is-opened-by-a-different-editor"></a>O arquivo "b" é aberto por um editor diferente

Caso o arquivo "b" já esteja aberto pelo editor "B" quando o editor "A" tentar abri-lo, há dois cenários separados a serem manipulados:

- Se o arquivo "b" estiver aberto em um editor compatível, você deverá ter o editor "A" registrar um bloqueio de edição do documento no arquivo "b" usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> método. Depois que o editor "A" terminar de modificar o arquivo "b", cancele o registro do bloqueio de edição do documento usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A> método.

- Se o arquivo "b" estiver aberto de forma incompatível, você poderá deixar a tentativa de abrir o arquivo "b" pelo editor "A" falhar ou permitir que a exibição associada ao editor "A" seja aberta parcialmente e exibir uma mensagem de erro apropriada. A mensagem de erro deve instruir o usuário a fechar o arquivo "b" no editor incompatível e, em seguida, abrir novamente o arquivo "a" usando o editor "A". Você também pode implementar o [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] método <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A> para solicitar que o usuário feche o arquivo "b" que está aberto no editor incompatível. Se o usuário fechar o arquivo "b", a abertura do arquivo "a" no editor "A" continuará normalmente.

## <a name="additional-document-edit-lock-considerations"></a>Outras considerações de bloqueio de edição de documento

Você obterá um comportamento diferente se o editor "A" for o único editor que tem um bloqueio de edição de documento no arquivo "b" do que você faria se o editor "B" também mantiver um bloqueio de edição de documento no arquivo "b". No [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] , **Designer de classe** é um exemplo de um designer visual que não mantém um bloqueio de edição no arquivo de código associado. Ou seja, se o usuário tiver um diagrama de classe aberto no modo Design e o arquivo de código associado for aberto simultaneamente, e se o usuário modificar o arquivo de código, mas não salvar as alterações, as alterações também serão perdidas no arquivo de diagrama de classe (. CD). Se o **Designer de classe** tiver o único bloqueio de edição de documento no arquivo de código, o usuário não será solicitado a salvar as alterações ao fechar o arquivo de código. O IDE solicita que o usuário salve as alterações somente depois que o usuário fechar a **Designer de classe**. As alterações salvas são refletidas em ambos os arquivos. Se o **Designer de classe** e o editor de arquivo de código mantinham os bloqueios de edição no arquivo de código, o usuário será solicitado a salvar ao fechar o arquivo de código ou o formulário. Nesse ponto, as alterações salvas são refletidas tanto no formulário quanto no arquivo de código. Para obter mais informações sobre diagramas de classe, consulte [trabalhar com diagramas de classe (Designer de classe)](../ide/class-designer/designing-and-viewing-classes-and-types.md).

Observe que, se você precisar inserir um bloqueio de edição em um documento para um não editor, deverá implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface.

Muitas vezes, um designer de interface do usuário que modifica arquivos de código programaticamente faz alterações em mais de um arquivo. Nesses casos, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A> método manipula a gravação de um ou mais documentos por meio da caixa de diálogo deseja **salvar as alterações nos seguintes itens?**

## <a name="see-also"></a>Confira também

- [Executando tabela de documentos](../extensibility/internals/running-document-table.md)
- [Persistência e a tabela de documentos em execução](../extensibility/internals/persistence-and-the-running-document-table.md)
