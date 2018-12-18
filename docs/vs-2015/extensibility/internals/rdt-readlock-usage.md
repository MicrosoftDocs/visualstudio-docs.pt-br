---
title: Uso de RDT_ReadLock | Microsoft Docs
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
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 337fa34bce713f743b8962f41a6889335b54b722
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817445"
---
# <a name="rdtreadlock-usage"></a>Uso de RDT_ReadLock
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> é um sinalizador que fornece a lógica para bloquear um documento no executando o documento de tabela (RDT), que é a lista de todos os documentos estão abertos no IDE do Visual Studio. Este sinalizador determina quando os documentos estão abertos, e se um documento está visível na interface do usuário ou mantido de forma invisível na memória.  
  
 Em geral, você usaria <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> quando uma das seguintes opções for verdadeira:  
  
-   Quando você deseja abrir um documento de forma invisível e somente leitura, mas ele ainda não tiver sido estabelecida que <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> deve possuí-lo.  
  
-   Quando você deseja que o usuário para ser solicitado a salvar um documento que foi aberto de forma invisível antes do usuário exibido-lo na interface do usuário e, em seguida, tentou fechá-lo.  
  
## <a name="how-to-manage-visible-and-invisible-documents"></a>Como gerenciar documentos visíveis e invisíveis  
 Quando um usuário abre um documento na interface do usuário, uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> proprietário para o documento deve ser estabelecido e um <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> sinalizador deve ser definido. Se nenhum <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> proprietário pode ser estabelecido e, em seguida, o documento não será salvo quando o usuário clica **Salvar tudo** ou fecha o IDE. Isso significa que se um documento é aberto modo invisível onde ele foi modificado na memória, e o usuário é solicitado a salvar o documento no desligamento ou salvo se **Salvar tudo** for escolhido, então um `RDT_ReadLock` não pode ser usado. Em vez disso, você deve usar um `RDT_EditLock` e registrar um <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> quando um <xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER> sinalizador.  
  
## <a name="rdteditlock-and-document-modification"></a>RDT_EditLock e modificação do documento  
<<<<<<< HEAD o sinalizador anterior mencionado indica que produzirá a abertura invisível do documento de seu `RDT_EditLock` quando o documento é aberto pelo usuário em um visíveis **DocumentWindow**. Quando isso ocorre, o usuário é apresentado com uma **salvar** solicitar quando o visíveis **DocumentWindow** está fechado. `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` as implementações que usam o <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> serviço inicialmente funciona quando somente um `RDT_ReadLock` é executada (ou seja, quando o documento for aberto de forma invisível para analisar as informações). Posteriormente, se o documento deve ser modificado, em seguida, o bloqueio é atualizado para uma fraca **RDT_EditLock**. Se o usuário abre o documento em um visíveis **DocumentWindow**, o `CodeModel`do fraco `RDT_EditLock` é liberado.  
= = = O sinalizador anterior mencionado indica que produzirá a abertura invisível do documento seus `RDT_EditLock` quando o documento é aberto pelo usuário em um visíveis **DocumentWindow**. Quando isso ocorre, o usuário é apresentado com uma **salvar** solicitar quando o visíveis **DocumentWindow** está fechado. As implementações de Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel que usam o <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> serviço inicialmente funciona quando somente um `RDT_ReadLock` é executada (ou seja, quando o documento for aberto de forma invisível para analisar as informações). Posteriormente, se o documento deve ser modificado, em seguida, o bloqueio é atualizado para uma fraca **RDT_EditLock**. Se o usuário abre o documento em um visíveis **DocumentWindow**, o `CodeModel`do fraco `RDT_EditLock` é liberado.  
>>>>>>> 9c8493a8dd... Tente um novo intervalo de moniker para dar suporte a versões de combinação
  
 Se o usuário, em seguida, fecha o **DocumentWindow** e escolhe **não** quando solicitado a salvar o documento aberto, em seguida, a `CodeModel` implementação descarta todas as informações do documento e reabra o documento do disco de forma invisível na próxima vez em que mais informações são necessárias para o documento. A sutileza desse comportamento é uma instância em que o usuário abre o **DocumentWindow** do documento aberto invisível, modifica, fecha e, em seguida, escolhe **não** quando for solicitado a salvar o documento. Nesse caso, se o documento possui um `RDT_ReadLock`, em seguida, o documento não será fechado, na verdade, e o documento modificado permanecerá aberto de forma invisível na memória, mesmo que o usuário optou por não salvar o documento.  
  
 Se a abertura invisível do documento usa uma fraca `RDT_EditLock`, em seguida, ele produz seu bloqueio quando o usuário abre o documento visivelmente e outros bloqueios não são mantidos. Quando o usuário fechar o **DocumentWindow** e escolhe **não** quando solicitado a salvar o documento, em seguida, o documento deve ser fechado da memória. Isso significa que o cliente invisível deve escutar eventos RDT acompanhar esta ocorrência. Na próxima vez em que o documento é necessário, o documento deverá ser reaberto.

