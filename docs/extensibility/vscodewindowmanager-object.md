---
title: Objeto VSCodeWindowManager | Microsoft Docs
description: Saiba mais sobre o objeto VSCodeWindowManager, que é responsável pelo gerenciamento de adornos, por exemplo, a barra suspensa.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VSCodeWindowManager
helpviewer_keywords:
- VsCodeWindowManager object
- views [Visual Studio SDK], VSCodeWindowManager object
ms.assetid: e313add5-afdb-4d8d-abd1-764e1fc10c44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 76ab3d2a72c957b20a79850dc312f5c16de98afc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905287"
---
# <a name="vscodewindowmanager-object"></a>Objeto VSCodeWindowManager

O serviço de linguagem implementa o Gerenciador de janelas de código e é responsável por gerenciar adornos (por exemplo, a barra suspensa). Para obter mais informações, consulte [Personalizando janelas de código usando a API herdada](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015).

A tabela a seguir mostra as interfaces no `VSCodeWindowManager` objeto.

|Interface|Descrição|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|Permite que adorners (como barras suspensas) sejam adicionados ou removidos de uma janela de código.|