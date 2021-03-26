---
title: Uso de RDT_ReadLock | Microsoft Docs
description: Saiba mais sobre o _VSRDTFLAGS. RDT_ReadLock sinalizador, que fornece a lógica para bloquear um documento na tabela de documentos em execução.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6add02e763c9664c19fe21b1cfc37dd29b3010b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060829"
---
# <a name="rdt_readlock-usage"></a>Uso de RDT_ReadLock

[_VSRDTFLAGS. RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) é um sinalizador que fornece a lógica para bloquear um documento na tabela de documentos em execução (Rdt), que é a lista de todos os documentos que estão abertos no IDE do Visual Studio. Esse sinalizador determina quando os documentos são abertos e se um documento está visível na interface do usuário ou mantido de forma invisível na memória.

Em geral, você usa [_VSRDTFLAGS. RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) quando uma das seguintes opções for verdadeira:

- Você deseja abrir um documento de forma invisível e somente leitura, mas ele ainda não foi estabelecido <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> .

- Você deseja que o usuário seja solicitado a salvar um documento que estava aberto de forma invisível antes de o usuário exibi-lo na interface de usuário e, em seguida, tentou fechá-lo.

## <a name="how-to-manage-visible-and-invisible-documents"></a>Como gerenciar documentos visíveis e invisíveis

Quando um usuário abre um documento na interface do usuário, <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> deve ser estabelecido um proprietário para o documento e um [_VSRDTFLAGS. RDT_EditLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>) sinalizador deve ser definido. Se nenhum <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> proprietário puder ser estabelecido, o documento não será salvo quando o usuário clicar em **salvar tudo** ou fechar o IDE. Isso significa que, se um documento estiver aberto invisivelmente, onde ele é modificado na memória, e o usuário for solicitado a salvar o documento no desligamento ou salvo se **salvar tudo** for escolhido, um `RDT_ReadLock` não poderá ser usado. Em vez disso, você deve usar um `RDT_EditLock` e registrar um <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> quando um [__VSREGDOCLOCKHOLDER. ](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>) Sinalizador de RDLH_WeakLockHolder.

## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock e modificação de documento

O sinalizador anterior mencionado indica que a abertura invisível do documento produzirá seu `RDT_EditLock` quando o documento for aberto pelo usuário em um **DocumentWindow** visível. Quando isso ocorre, o usuário recebe um aviso de **salvamento** quando o **DocumentWindow** visível é fechado. `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` as implementações que usam o <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> serviço inicialmente funcionam quando apenas um `RDT_ReadLock` é tomado (ou seja, quando o documento é aberto invisivelmente para analisar informações). Posteriormente, se o documento precisar ser modificado, o bloqueio será atualizado para um **RDT_EditLock** fraco. Se o usuário abrir o documento em uma **DocumentWindow** visível, o `CodeModel` será ineficaz `RDT_EditLock` .

Se o usuário fechar a **DocumentWindow** e escolher **não** quando for solicitado a salvar o documento aberto, a `CodeModel` implementação descartará todas as informações no documento e reabrirá o documento do disco de forma invisível na próxima vez em que mais informações forem necessárias para o documento. A sutileza desse comportamento é uma instância em que o usuário abre o **DocumentWindow** do documento aberto invisível, modifica-o, fecha-o e, em seguida, escolhe **não** quando é solicitado a salvar o documento. Nesse caso, se o documento tiver um `RDT_ReadLock` , o documento não será fechado de fato e o documento modificado permanecerá aberto de forma invisível na memória, mesmo que o usuário decida não salvar o documento.

Se a abertura invisível do documento usar uma fraca `RDT_EditLock` , ela resultará em seu bloqueio quando o usuário abrir o documento visivelmente e nenhum outro bloqueio for mantido. Quando o usuário fechar a **DocumentWindow** e escolher **não** quando for solicitado a salvar o documento, o documento deverá ser fechado da memória. Isso significa que o cliente invisível deve escutar eventos RDT para controlar essa ocorrência. Na próxima vez em que o documento for necessário, o documento deverá ser reaberto.
