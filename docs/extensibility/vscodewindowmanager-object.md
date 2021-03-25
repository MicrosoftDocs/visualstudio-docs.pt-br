---
title: Objeto VSCodeWindowManager | Microsoft Docs
description: Saiba mais sobre o objeto VSCodeWindowManager, que é responsável pelo gerenciamento de adornos, por exemplo, a barra suspensa.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 60093d237ed2aa7a14e5695efc66fe8edd515f4a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062389"
---
# <a name="vscodewindowmanager-object"></a>Objeto VSCodeWindowManager

O serviço de linguagem implementa o Gerenciador de janelas de código e é responsável por gerenciar adornos (por exemplo, a barra suspensa). Para obter mais informações, consulte [Personalizando janelas de código usando a API herdada](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015).

A tabela a seguir mostra as interfaces no `VSCodeWindowManager` objeto.

|Interface|Descrição|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|Permite que adorners (como barras suspensas) sejam adicionados ou removidos de uma janela de código.|