---
title: Quais &apos; s novidades no SDK do Visual Studio 2017 | Microsoft Docs
description: O SDK do Visual Studio tem recursos novos e atualizados para o Visual Studio 2017, incluindo o formato atualizado do VSIX versão 3.
ms.custom: SEO-VS-2020
ms.date: 10/31/2017
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a1e34ac23a0e6c298dae14c1613e7af0fc7b25d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061921"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>O que&#39;s New no SDK do Visual Studio 2017

O SDK do Visual Studio tem os seguintes recursos novos e atualizados para o Visual Studio 2017.

## <a name="vsix-v3-format"></a>Formato VSIX v3

Para dar suporte à nova instalação leve do Visual Studio 2017, o formato de manifesto da extensão VSIX foi atualizado para a versão 3 (VSIX v3).

O novo formato tem suporte para:

* Declarando explicitamente os pré-requisitos a serem detectados e instalados pelo VSIXInstaller.
* Assemblies NGen na instalação da extensão.
* Instalando ativos fora da raiz de extensão usual.

Para saber mais sobre essas alterações, consulte os seguintes tópicos:

* [Alterações na extensibilidade para o Visual Studio 2017](breaking-changes-2017.md)
* [Suporte a NGen no VSIX v3](ngen-support.md)
* [Instalar fora da pasta de extensões](set-install-root.md)
* [Perguntas frequentes sobre a extensibilidade do Visual Studio 2017](faq-2017.md)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>Migrar projeto de extensibilidade para o Visual Studio 2017

Para saber como atualizar seus projetos de extensibilidade e seus manifestos VSIX para o Visual Studio 2017, consulte [como migrar projetos de extensibilidade para o visual studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

## <a name="custom-project-and-item-templates"></a>Modelos de item e projeto personalizados

A partir do Visual Studio 2017, a verificação de modelos de projeto e item personalizados não será mais executada. Em vez disso, a extensão deve fornecer arquivos de manifesto de modelo que descrevem o local de instalação desses modelos. Você pode usar o Visual Studio 2017 para atualizar suas extensões VSIX. Se você implantar sua extensão usando um MSI, deverá gerar os arquivos de manifesto de modelo manualmente. Para obter mais informações, consulte [Atualizar projetos personalizados e modelos de item para o Visual Studio 2017](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md). O esquema de manifesto de modelo está documentado na [referência de esquema de manifesto de modelo do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).

## <a name="updated-extension-performance-guidelines"></a>Diretrizes de desempenho de extensão atualizadas

Há um novo artigo [como: diagnosticar o desempenho da extensão](how-to-diagnose-extension-performance.md) em [gerenciar VSPackages](managing-vspackages.md) para mostrar como detectar e analisar o impacto da extensão nos tempos de carregamento da solução e inicialização do Visual Studio.
