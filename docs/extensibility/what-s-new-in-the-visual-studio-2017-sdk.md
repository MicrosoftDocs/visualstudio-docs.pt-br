---
title: O que&#39;novo no SDK do Visual Studio 2017 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6f2a003bc19764aa07262552d3f0cc41316835b6
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566902"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>O que&#39;novo no SDK do Visual Studio 2017

O SDK do Visual Studio tem os seguintes recursos novos e atualizados do Visual Studio 2017.

## <a name="vsix-v3-format"></a>Formato do VSIX v3

Para dar suporte à nova instalação leve do Visual Studio 2017, o formato de manifesto de extensão do VSIX foi atualizado para a versão 3 (v3 VSIX).

O novo formato tem suporte para:

* Declarar explicitamente os pré-requisitos para ser detectada e instalada pelo VSIXInstaller.
* Assemblies do NGen na instalação da extensão.
* Instalando os ativos de fora da raiz da extensão usual.

Para saber mais sobre essas alterações, consulte os tópicos a seguir:

* [Alterações à extensibilidade para 2017](breaking-changes-2017.md)
* [Suporte a Ngen no VSIX v3](ngen-support.md)
* [Instalar fora da pasta de extensões](set-install-root.md)
* [Perguntas frequentes para extensibilidade do Visual Studio 2017](faq-2017.md)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>Migrar o projeto de extensibilidade para o Visual Studio 2017

Para saber como atualizar seus projetos de extensibilidade e seus manifestos VSIX para Visual Studio 2017, consulte [como: migrar projetos de extensibilidade para o Visual Studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

## <a name="custom-project-and-item-templates"></a>Modelos de item e projeto personalizados

A partir do Visual Studio 2017, verificação de modelos de item e projeto personalizados será não é mais executada. Em vez disso, a extensão deve fornecer os arquivos de manifesto de modelo que descrevem o local de instalação desses modelos. Você pode usar o Visual Studio 2017 para atualizar as extensões VSIX. Se você implantar sua extensão usando um MSI, você deve gerar os arquivos de manifesto do modelo manualmente. Para obter mais informações, consulte [atualizar modelos de item e projeto personalizados para o Visual Studio 2017](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md). O esquema de modelo de manifesto está documentado em [referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).

## <a name="updated-extension-performance-guidelines"></a>Diretrizes de desempenho de extensão atualizado

Há uma nova [como: diagnosticar o desempenho da extensão](how-to-diagnose-extension-performance.md) artigo sob [gerenciar VSPackages](managing-vspackages.md) para mostrar como detectar e analisar o impacto de extensão no Visual Studio inicialização e solução de tempos de carregamento.
