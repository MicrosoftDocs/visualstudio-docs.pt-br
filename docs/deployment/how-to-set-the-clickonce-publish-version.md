---
title: Como definir a versão de publicação do ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, setting publish version
- publishing, ClickOnce
- Publish Version property
ms.assetid: 06f15504-6385-40a6-b01d-cd90ca36dc73
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df5e1d91de14e3da4f188c276ef7dd74943d8978
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382114"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>Como definir a versão da publicação do ClickOnce
A [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `Publish Version` propriedade determina se o aplicativo que você está publicando será tratado como uma atualização. Cada versão de tempo é incrementada, o aplicativo será publicado como uma atualização.

 A `Publish Version` propriedade pode ser definida na página **publicar** do designer de **projeto**.

> [!NOTE]
> Há uma opção de projeto que incrementará automaticamente a `Publish Version` Propriedade cada vez que o aplicativo for publicado; essa opção é habilitada por padrão. Para obter mais informações, consulte [como incrementar automaticamente a versão de publicação do ClickOnce](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md).

### <a name="to-change-the-publish-version"></a>Para alterar a versão de publicação

1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. No **campo versão de publicação** , aumente os números de versão **principal**, **secundária**, de **compilação**ou de **revisão** .

    > [!NOTE]
    > Você nunca deve decrementar um número de versão; Isso pode causar um comportamento de atualização imprevisível.

## <a name="see-also"></a>Veja também
- [Escolher uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md)
- [Como: incrementar automaticamente a versão de publicação do ClickOnce](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)