---
title: Criar tipos de projeto | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bbe65d1615603e4dc7546dbfe3530093c62528e5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155035"
---
# <a name="creating-project-types"></a>Criando tipos de projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Você pode estender [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , criando um novo tipo de projeto. Para criar um novo tipo de projeto, você deve compreender os vários conceitos e concluir várias etapas. Os tópicos a seguir fornecem uma visão geral de como criar tipos de projeto.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Decisões de design do tipo de projeto](../../extensibility/internals/project-type-design-decisions.md)  
 Discute o item, persistência de arquivo de projeto e as decisões de design mechanic de compromisso que você precisa fazer antes de criar um novo tipo de projeto.  
  
 [Lista de verificação: criação de novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)  
 Fornece uma visão geral das etapas que devem ser seguidas para criar um novo tipo de projeto que dá suporte a tarefas de programação como editando o código e compilando, criação, depuração e implantação de aplicativos em seu projeto.  
  
 [Criar instâncias de projetos usando fábricas de projetos](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)  
 Fornece informações sobre como fornecer e usar uma fábrica de projeto para criar instâncias de um novo projeto.  
  
 [Registrar um tipo de projeto](../../extensibility/internals/registering-a-project-type.md)  
 Fornece exemplos de código de instruções do registro que fornecem os caminhos padrão e dados e uma tabela que contêm entradas do script do registro para cada instrução.  
  
 [Persistência do projeto](../../extensibility/internals/project-persistence.md)  
 Discute o uso de `IPersistFileFormat` para manter o arquivo e os objetos não são baseados em arquivo de projeto.  
  
 [Usar o MSBuild](../../extensibility/internals/using-msbuild.md)  
 Descreve como o tipo de projeto pode usar o [!INCLUDE[vstecmsbuild](../../includes/vstecmsbuild-md.md)] o mecanismo para permitir aos usuários criar a partir de build [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e na linha de comando.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Suporte a ferramentas de navegação por símbolo](../../extensibility/internals/supporting-symbol-browsing-tools.md)  
 Explica a arquitetura de código, ferramentas de visualização, como o **Pesquisador de objetos** e **Class View** janela. Descreve as interfaces e métodos que são usados para implementar a navegação do objeto em um VSPackage.  
  
 [Adicionar modelos projeto e de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)  
 Discute a importância que projetos reproduzir determinar qual editor é usado quando um item de projeto é aberto e como os recursos do projeto podem ser manipulados.  
  
 [Instalar VSPackages com o Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)  
 Mostra como conceder o VSPackage sua própria identidade exclusiva e como encapsular suas DLLs de VSPackage e outras informações em um pacote do Windows Installer (. Arquivo MSI) para a implantação para seus clientes.  
  
 [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)  
 Descreve como [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] hierarquias de modos de exibição e endereços.  
  
 [VSPackages](../../extensibility/internals/vspackages.md)  
 Fornece uma visão geral de um VSPackage, um objeto COM instalável que estende o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente e discute como implementar seu próprio VSPackage.  
  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Discute como usar os projetos para modificar o código, compile e compilar o código e executar e depurar o código e fornece links para tópicos detalhados sobre como criar tipos de projeto.
