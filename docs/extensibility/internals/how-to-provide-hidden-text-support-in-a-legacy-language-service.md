---
title: Fornecer suporte a texto oculto no serviço de linguagem herddo
description: Saiba como fornecer suporte a texto oculto em um serviço de linguagem herdado adicionando regiões de texto oculta controladas pelo editor ou controladas pelo cliente.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- hidden text, supporting
- editors [Visual Studio SDK], hidden text
- language services, implementing hidden text regions
ms.assetid: 1c1dce9f-bbe2-4fc3-a736-5f78a237f4cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 31c62f50cfff8662c543d24dceabdb429a9b9b05
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901780"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>Como fornecer suporte a texto oculto em um serviço de linguagem herdados
Você pode criar regiões de texto ocultas além de regiões de contorno. As regiões de texto ocultas podem ser controladas pelo cliente ou controladas pelo editor e são usadas para ocultar completamente uma região de texto. O editor exibe uma região oculta como linhas horizontais. Um exemplo disso é a **exibição Somente Script** no editor HTML.

## <a name="to-implement-a-hidden-text-region"></a>Para implementar uma região de texto oculto

1. Chame `QueryService` para <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> .

     Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> .

2. Chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> , passando um ponteiro para um buffer de texto determinado. Isso determina se uma sessão de texto oculta já existe para o buffer.

3. Se já existir um, você não precisará criar um e um ponteiro para o objeto <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> existente será retornado. Use este ponteiro para enumerar e criar regiões de texto ocultas. Caso contrário, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> chame para criar uma sessão de texto oculto para o buffer.

     Um ponteiro para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto é retornado.

    > [!NOTE]
    > Ao chamar `CreateHiddenTextSession` , você pode especificar um cliente de texto oculto (ou seja, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> ). O cliente de texto oculto notifica você quando o texto oculto ou a estrutura de estrutura de texto é expandido ou recolhido pelo usuário.

4. Chame para adicionar uma ou mais novas regiões de contorno por vez, especificando as <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> seguintes informações no parâmetro ( ) `reHidReg` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> :

    1. Especifique um valor de no membro da estrutura para indicar que você está criando uma `hrtConcealed` `iType` região <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> oculta, em vez de uma região de estrutura de contorno.

        > [!NOTE]
        > Quando as regiões ocultas são ocultadas, o editor exibe automaticamente linhas em torno das regiões ocultas para indicar sua presença.

    2. Especifique se a região é controlada pelo cliente ou controlada pelo editor nos `dwBehavior` membros da <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura. Sua implementação delineamento inteligente pode conter uma combinação de contornos controlados pelo editor e pelo cliente e regiões de texto ocultas.
