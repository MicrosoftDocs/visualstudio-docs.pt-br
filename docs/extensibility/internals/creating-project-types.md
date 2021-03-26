---
title: Criando tipos de projeto | Microsoft Docs
description: Saiba como estender o Visual Studio criando, criando e registrando um novo tipo de projeto que dá suporte a tarefas de programação.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5984afd2879f94a73ef02f77a85501c50f55bc93
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056812"
---
# <a name="create-project-types"></a>Criar tipos de projeto
Você pode estender [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] criando um novo tipo de projeto. Para criar um novo tipo de projeto, você deve compreender vários conceitos e concluir várias etapas. Os tópicos a seguir fornecem uma visão geral de como criar tipos de projeto.

## <a name="in-this-section"></a>Nesta seção
- [Decisões de design de tipo de projeto](../../extensibility/internals/project-type-design-decisions.md)

 Discute o item, a persistência de arquivo do projeto e as decisões de design mecânico de compromisso que você precisa fazer antes de criar um novo tipo de projeto.

- [Lista de verificação: criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)

 Fornece uma visão geral das etapas que você deve seguir para criar um novo tipo de projeto que dá suporte a tarefas de programação como edição de código e compilação, criação, depuração e implantação de aplicativos em seu projeto.

- [Criar instâncias de projeto usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)

 Fornece informações sobre como fornecer e usar uma fábrica de projetos para criar instâncias de um novo projeto.

- [Registrar um tipo de projeto](../../extensibility/internals/registering-a-project-type.md)

 Fornece exemplos de código de instruções do registro que fornecem caminhos e dados padrão e uma tabela que contém entradas do script de registro para cada instrução.

- [Persistência do projeto](../../extensibility/internals/project-persistence.md)

 Discute o uso de `IPersistFileFormat` para manter objetos de projeto de arquivo e não baseados em arquivo.

- [Usar o MSBuild](../../extensibility/internals/using-msbuild.md)

 Descreve como o tipo de projeto pode usar o [!INCLUDE[vstecmsbuild](../../extensibility/internals/includes/vstecmsbuild_md.md)] mecanismo de compilação para permitir que os usuários criem de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e na linha de comando.

## <a name="related-sections"></a>Seções relacionadas
- [Símbolo de suporte – ferramentas de navegação](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 Explica a arquitetura das ferramentas de exibição de código, como o **pesquisador de objetos** e a janela **modo de exibição de classe** . Descreve as interfaces e os métodos que são usados para implementar a navegação de objeto em um VSPackage.

- [Adicionar projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)

 Discute o significado que os projetos desempenham para determinar qual editor é usado quando um item de projeto é aberto e como os recursos do projeto podem ser manipulados.

- [Instalar o VSPackages com Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)

 Mostra como dar ao seu VSPackage sua própria identidade exclusiva e como encapsular suas DLLs do VSPackage e outras informações em um pacote de Windows Installer (*. Arquivo MSI* ) para implantação em seus clientes.

- [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)

 Descreve como [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Exibir e solucionar as hierarquias.

- [VSPackages](../../extensibility/internals/vspackages.md)

 Fornece uma visão geral de um VSPackage, um objeto COM instalável que estende o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente e discute como implementar seu próprio VSPackage.

- [Tipos de projeto](../../extensibility/internals/project-types.md)

 Discute como usar projetos para modificar código, compilar e compilar código, e executar e depurar código e fornece links para tópicos detalhados sobre como criar tipos de projeto.
