---
title: Referência de API não gerenciada (desenvolvimento do Office no Visual Studio)
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, reference
- Office development in Visual Studio, unmanaged API reference
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 79f48e7771b3e62c0c58fbc59bd9f9b534069d71
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584419"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>Referência de API não gerenciada (desenvolvimento do Office no Visual Studio)

A partir do sistema de Microsoft Office de 2007, os aplicativos do Office usam a interface de [interface IManagedAddin](../vsto/imanagedaddin-interface.md) para chamar um componente de carregador de suplemento do VSTO que está incluído no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] . Esse componente é usado para ajudar os suplementos do VSTO gerenciados por carga. Você pode criar seu próprio componente de carregador de suplemento do VSTO implementando essa interface.

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>Nesta seção

[Interface IManagedAddin](../vsto/imanagedaddin-interface.md)

Uma interface COM que você pode implementar para carregar e descarregar suplementos do VSTO gerenciados em aplicativos do Office.
