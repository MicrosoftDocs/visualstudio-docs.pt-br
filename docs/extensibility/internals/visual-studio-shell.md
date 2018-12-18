---
title: Shell do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0ef0bf2811e9858925398637e835be8684c7f9ef
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928939"
---
# <a name="visual-studio-shell"></a>Shell do Visual Studio
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell é o principal agente de integração no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. O shell fornece a funcionalidade necessária para habilitar os VSPackages compartilhar serviços comuns. Porque o objetivo de arquitetura de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é casaco principal funcionalidade em VSPackages, o shell é uma estrutura para fornecer a funcionalidade básica e dar suporte a comunicação cruzada entre seu componente VSPackages.  
  
## <a name="shell-responsibilities"></a>Responsabilidades do shell  
 O shell tem as seguintes responsabilidades principais:  
  
- Elementos básicos que dão suporte a (por meio de interfaces COM) da interface do usuário (IU). Eles incluem barras de ferramentas e menus padrão, janelas filho de interface de vários documentos (MDI), ou quadros de janela de documento e quadros de janela de ferramenta e suporte de encaixe.  
  
- Manter uma lista de todos os documentos abertos no momento em uma tabela de documento (RDT) em execução para coordenar a persistência de documentos e a garantia de que um documento não pode ser aberto em mais de uma forma ou em formas incompatíveis.  
  
- Suporte a interface do roteamento de comando e manipulação de comandos, `IOleCommandTarget`.  
  
- Carregar VSPackages em momentos apropriados. Carregamento de atraso de um VSPackage é necessário para melhorar o desempenho do shell.  
  
- Gerenciando determinados serviços compartilhados, tais como <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>, que fornece a funcionalidade básica de shell e <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>, que fornece a funcionalidade básica de janelas.  
  
- Gerenciando os arquivos de solução (. sln). As soluções contêm grupos de projetos relacionados, semelhantes aos arquivos de espaço de trabalho (dsw) no Visual C++ 6.0.  
  
- Seleção de todo o shell de acompanhamento, o contexto e moeda. O shell rastreia os seguintes tipos de itens:  
  
  -   O projeto atual  
  
  -   O item de projeto atual ou ItemID atual <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>  
  
  -   A seleção atual para o **propriedades** janela ou `SelectionContainer`  
  
  -   O contexto de interface do usuário IDs ou CmdUIGuids que controlam a visibilidade de comandos, menus e barras de ferramentas  
  
  -   Os elementos ativos no momento, como a janela ativa, o documento e o Gerenciador de desfazer  
  
  -   Os atributos de contexto de usuário que orientam a Ajuda dinâmica  
  
  O shell também atua como mediador de comunicação entre os VSPackages instalados e os serviços atuais. Ele dá suporte aos principais recursos do shell e torna-os disponíveis para todos os VSPackages integrados no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Esses principais recursos incluem os seguintes itens:  
  
- **Sobre** tela inicial e de caixa de diálogo  
  
- **Adicionar novo e Adicionar Item existente** caixas de diálogo  
  
- **Exibição de classe** janela e **Pesquisador de objetos**  
  
- **Referências** caixa de diálogo  
  
- **Estrutura de tópicos de documento** janela  
  
- **Ajuda dinâmica** janela  
  
- **Encontre** e **substituir**  
  
- **Abrir projeto** e **abrir arquivo** caixas de diálogo sobre o **New** menu  
  
- **As opções** caixa de diálogo de **ferramentas** menu  
  
- Janela **Propriedades**  
  
- **Gerenciador de Soluções**  
  
- **Lista de tarefas** janela  
  
- **Caixa de Ferramentas**  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>   
 [VSPackages](../../extensibility/internals/vspackages.md)