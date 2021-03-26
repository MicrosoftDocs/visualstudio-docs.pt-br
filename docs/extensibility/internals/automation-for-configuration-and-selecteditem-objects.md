---
title: Automação para objetos de configuração e SelectedItem | Microsoft Docs
description: Saiba como automatizar a compilação do Visual Studio e os processos de item selecionados usando os objetos Configuration e SelectedItem na interoperabilidade do Shell.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f6e7f153e7d5b32e54cc51e3b7af06f14545cea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086255"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>Automação para objetos de configuração e SelectedItem

Você pode automatizar os processos de compilação e item selecionado no Visual Studio.

## <a name="automation-for-builds"></a>Automação para compilações

A compilação ou configuração tem um modelo de automação que é fornecido quando você implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> . Para obter mais informações, consulte [Compreender configurações de build](../../ide/understanding-build-configurations.md).

Se você criar um VSPackage e quiser controlar as opções de configuração, deverá usar o modelo de automação.

## <a name="automation-for-selecteditem"></a>Automação para SelectedItem

Você não precisa fornecer uma implementação para o `SelectedItem` objeto porque o Visual Studio contém uma implementação padrão. No entanto, você pode implementar o `SelectedItem` objeto se preferir. Você deve implementar um objeto que contém a `SelectedItem` interface e retornar uma resposta a uma chamada para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método com `VSITEMID` definido como [__VSHPROPID. VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>).

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [Contribuir para o modelo de automação](../../extensibility/internals/contributing-to-the-automation-model.md)
- [Noções sobre configurações de build](../../ide/understanding-build-configurations.md)
