---
title: Uso de RDT_ReadLock | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7fda2fbb4a4b03dff9d677d9c7581a4138d9fcf7
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131675"
---
# <a name="rdtreadlock-usage"></a>Uso de RDT_ReadLock

<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> é um sinalizador que fornece a lógica para bloquear um documento no executando o documento de tabela (RDT), que é a lista de todos os documentos abertos no momento no IDE do Visual Studio. Esse sinalizador determina quando os documentos são abertos, e se um documento está visível na interface do usuário ou de forma invisível em memória.

Em geral, você usaria <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> quando uma das seguintes condições for verdadeira:

- Quando você deseja abrir um documento de forma invisível e somente leitura, mas ela não ainda tiver sido estabelecida que <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> devem possuir a ele.

- Quando você deseja que o usuário seja solicitado a salvar um documento que foi aberto de forma invisível antes que o usuário exibido-la na interface de usuário e, em seguida, tentou fechá-lo.

## <a name="how-to-manage-visible-and-invisible-documents"></a>Como gerenciar documentos visíveis e invisíveis

Quando um usuário abre um documento na interface de usuário, uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> proprietário do documento deve ser estabelecido e um <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> sinalizador deve ser definido. Se nenhum <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> proprietário pode ser estabelecido, em seguida, o documento não serão salvas quando o usuário clica **Salvar tudo** ou fecha o IDE. Isso significa que se um documento está aberto forma invisível em que ele foi modificado na memória, e o usuário é solicitado a salvar o documento no desligamento ou salvo se **Salvar tudo** for escolhido, então um `RDT_ReadLock` não pode ser usado. Em vez disso, você deve usar um `RDT_EditLock` e registre um <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> quando um <xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER> sinalizador.

## <a name="rdteditlock-and-document-modification"></a>RDT_EditLock e modificação de documento

O sinalizador anterior mencionado indica que produzirá a abertura invisível do documento de seu `RDT_EditLock` quando o documento for aberto pelo usuário em um visível **DocumentWindow**. Quando isso ocorre, o usuário receberá uma **salvar** Avisar quando o visível **DocumentWindow** está fechado. `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` implementações que usam o <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> serviço inicialmente funciona quando somente um `RDT_ReadLock` é obtido (ou seja, quando o documento for aberto de forma invisível para analisar as informações). Posteriormente, se o documento deve ser modificado, em seguida, o bloqueio é atualizado para um fraca **RDT_EditLock**. Se o usuário abre o documento em um visível **DocumentWindow**, o `CodeModel`do fraca `RDT_EditLock` é liberado.

Se o usuário fecha o **DocumentWindow** e escolhe **não** quando solicitado a salvar o documento aberto, em seguida, o `CodeModel` implementação descarta todas as informações do documento e reabrir o documento do disco de forma invisível na próxima vez em que mais informações são necessárias para o documento. O recurso desse comportamento é uma instância em que o usuário abre o **DocumentWindow** do documento aberto invisível, modifica-lo, fechá-lo e, em seguida, escolhe **não** quando for solicitado a salvar o documento. Nesse caso, se o documento possui um `RDT_ReadLock`, o documento não será fechado, na verdade, e o documento modificado permanecerá aberto de forma invisível na memória, mesmo que o usuário optou por não salvar o documento.

Se a abertura invisível do documento usa um fraca `RDT_EditLock`, em seguida, ele gera seu bloqueio quando o usuário abre o documento visivelmente e outros bloqueios não são mantidos. Quando o usuário fecha o **DocumentWindow** e escolhe **não** quando solicitado a salvar o documento, em seguida, o documento deve ser fechado da memória. Isso significa que o cliente invisível deve escutar eventos RDT controlar essa ocorrência. Na próxima vez em que o documento é necessário, o documento deve ser reaberto.