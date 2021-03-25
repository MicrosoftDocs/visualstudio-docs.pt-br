---
title: Estendendo projetos | Microsoft Docs
description: Saiba como criar seus próprios tipos de projeto personalizados no SDK do Visual Studio e como gerenciar diferentes tipos de soluções do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
ms.assetid: 096d273d-4fe9-4f24-9b00-470bfbdf4bdf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c3d4b962475e2f0705d8a46624a8f47d802ff2f4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075153"
---
# <a name="extend-projects"></a>Estender projetos
Projetos e soluções são as maneiras como o Visual Studio organiza arquivos de código e de recursos em unidades de compilação e implantação. Você pode encontrar mais informações sobre projetos em [projetos (Visual Studio SDK)](../extensibility/extending-projects.md).

 Você pode criar seus próprios tipos de projeto com o SDK do Visual Studio e a estrutura de pacote gerenciada para projetos, que você pode baixar em [estrutura de pacote gerenciado para projetos](https://github.com/tunnelvisionlabs/MPFProj10). Para entender como os projetos personalizados são implementados, consulte [nova geração de projeto: nos bastidores, parte 1](../extensibility/internals/new-project-generation-under-the-hood-part-one.md) e [nova geração de projeto: nos bastidores, parte dois](../extensibility/internals/new-project-generation-under-the-hood-part-two.md).

 Os tópicos nesta seção descrevem como criar projetos personalizados e como gerenciar diferentes tipos de solução do Visual Studio.

## <a name="in-this-section"></a>Nesta seção
- [Criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md) Descreve como criar um sistema de projeto personalizado.

- [Criar um sistema de projeto básico, parte 2](../extensibility/creating-a-basic-project-system-part-2.md) Descreve como criar um sistema de projeto personalizado.

- [Salvar dados em arquivos de projeto](../extensibility/saving-data-in-project-files.md) Explica como adicionar ao projeto (<em>.</em> proj *) arquivos.

- [Verificar subtipos de um projeto em tempo de execução](../extensibility/verifying-subtypes-of-a-project-at-run-time.md) Explica como verificar o subtipo de um projeto em tempo de execução.

- [Adicionar e remover páginas de propriedades](../extensibility/adding-and-removing-property-pages.md) Explica como personalizar as páginas de propriedades para seu projeto personalizado.

- [Adicionar um atributo a um item de projeto](../extensibility/adding-an-attribute-to-a-project-item.md) Explica como adicionar um atributo a um item de projeto personalizado.

- [Persistir a propriedade de um item de projeto](../extensibility/persisting-the-property-of-a-project-item.md) Explica como manter as propriedades de um item de projeto personalizado.

- [Gerenciar projetos universais do Windows](../extensibility/managing-universal-windows-projects.md) Explica como gerenciar projetos universais.
