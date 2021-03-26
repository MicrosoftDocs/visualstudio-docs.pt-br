---
title: Shell do Visual Studio | Microsoft Docs
description: O Shell do Visual Studio é o principal agente de integração no Visual Studio e fornece funcionalidade básica e dá suporte à comunicação cruzada entre VSPackages.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5dafd90294fd0968c78846d4162c1ff02c584f3f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074334"
---
# <a name="visual-studio-shell"></a>Shell do Visual Studio
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell é o principal agente de integração no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . O Shell fornece a funcionalidade necessária para permitir que o VSPackages Compartilhe serviços comuns. Como o objetivo da arquitetura do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é a principal funcionalidade de benefício no VSPackages, o Shell é uma estrutura para fornecer funcionalidade básica e oferecer suporte à comunicação cruzada entre seu componente VSPackages.

## <a name="shell-responsibilities"></a>Responsabilidades do Shell
 O Shell tem as seguintes responsabilidades principais:

- Suporte a elementos básicos (por meio de interfaces COM) da interface do usuário. Isso inclui menus e barras de ferramentas padrão, quadros de janelas de documentos ou janelas filhas MDI (interface de vários documentos) e quadros de janelas de ferramentas e suporte a encaixe.

- Manter uma lista em execução de todos os documentos abertos no momento em uma tabela de documentos em execução (RDT) para coordenar a persistência de documentos e garantir que um documento não possa ser aberto em mais de uma maneira, ou em maneiras incompatíveis.

- Suporte à interface de roteamento de comandos e manipulação de comandos, `IOleCommandTarget` .

- Carregando VSPackages em momentos apropriados. O carregamento de atraso de um VSPackage é necessário para melhorar o desempenho do Shell.

- Gerenciar determinados serviços compartilhados, como <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> o, que fornece funcionalidade básica do Shell e <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> , que fornece funcionalidade básica de janela.

- Gerenciando os arquivos da solução (. sln). As soluções contêm grupos de projetos relacionados, semelhantes aos arquivos de espaço de trabalho (. DSW) no Visual C++ 6,0.

- Acompanhamento da seleção, do contexto e da moeda em todo o Shell. O Shell acompanha os seguintes tipos de itens:

  - O projeto atual

  - O item de projeto atual ou ItemID o atual <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

  - A seleção atual para a janela **Propriedades** ou `SelectionContainer`

  - As IDs de contexto da interface do usuário ou CmdUIGuids que controlam a visibilidade de comandos, menus e barras de ferramentas

  - Os elementos atualmente ativos, como a janela ativa, o documento e o Gerenciador de desfazer

  - Os atributos de contexto de usuário que orientam a ajuda dinâmica

  O Shell também Media a comunicação entre o VSPackages instalado e os serviços atuais. Ele dá suporte aos principais recursos do Shell e os torna disponíveis para todos os VSPackages integrados no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Esses recursos principais incluem os seguintes itens:

- Caixa de diálogo **sobre** e tela inicial

- **Adicionar novas caixas de diálogo e Adicionar item existente**

- Janela **modo de exibição de classe** e **pesquisador de objetos**

- Caixa de diálogo **referências**

- Janela **estrutura de tópicos do documento**

- Janela de **Ajuda dinâmica**

- **Localizar** e **substituir**

- **Abrir o projeto** e **abrir o arquivo** caixas de diálogo no **novo** menu

- Caixa de diálogo **Opções** no menu **ferramentas**

- Janela **Propriedades**

- **Gerenciador de Soluções**

- Janela de **lista de tarefas**

- **Caixa de Ferramentas**

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackages](../../extensibility/internals/vspackages.md)
