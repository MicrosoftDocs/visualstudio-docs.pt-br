---
title: Referência de API não gerenciada (desenvolvimento do Office no Visual Studio)
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, reference
- Office development in Visual Studio, unmanaged API reference
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9b0f48ea5997c2c8c2dd7d90eebde8322fad8a7a
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669915"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>Referência de API não gerenciada (desenvolvimento do Office no Visual Studio)
  Começando com o 2007 Microsoft Office system, aplicativos do Office usam as [interface IManagedAddin](../vsto/imanagedaddin-interface.md) interface para chamar em um suplemento do VSTO carregador componente que está incluído com o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Esse componente é usado para ajudar a carga gerenciado VSTO Add-ins. Você pode criar seu próprio componente de carregador de suplemento do VSTO ao implementar essa interface.  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Interface IManagedAddin](../vsto/imanagedaddin-interface.md)  
 Uma interface COM que você pode implementar para carregar e descarregar gerenciado VSTO Add-ins em aplicativos do Office.  
  
  