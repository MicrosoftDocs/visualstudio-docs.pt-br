---
title: Exibir arquivos usando o comando Abrir arquivo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- project types, supporting Open File command
- Open File command
- persistence, supporting Open File command
ms.assetid: 4fff0576-b2f3-4f17-9769-930f926f273c
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1f1a2ca2b87cadf118c83501bbd6b6bf78af761a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727274"
---
# <a name="displaying-files-by-using-the-open-file-command"></a>Exibindo arquivos usando o comando Abrir Arquivo
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

As etapas a seguir descrevem como o IDE manipula a **abrir arquivo** comando, que está disponível na **arquivo** menu no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. As etapas também descrevem como projetos devem responder a chamadas originadas desse comando.  
  
 Quando um usuário clica o **abrir arquivo** comando as **arquivo** menu e seleciona um arquivo do **abrir arquivo** caixa de diálogo, o seguinte processo ocorre.  
  
1.  Usando a tabela de documento em execução, o IDE determina se o arquivo já está aberto em um projeto.  
  
    -   Se o arquivo estiver aberto, o IDE resurfaces a janela.  
  
    -   Se o arquivo não estiver aberto, o IDE chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> para cada projeto para determinar qual projeto pode abrir o arquivo de consulta.  
  
        > [!NOTE]
        >  Na implementação do projeto <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>, forneça um valor de prioridade que indica o nível no qual seu projeto abre o arquivo. Os valores de prioridade são fornecidos no <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> enumeração.  
  
2.  Cada projeto responde com um nível de prioridade que indica a importância coloca em que está sendo o projeto para abrir o arquivo.  
  
3.  O IDE usa os seguintes critérios para determinar qual projeto abre o arquivo:  
  
    -   O projeto que responde com a prioridade mais alta (DP_Intrinsic) abre o arquivo. Se mais de um projeto responder com essa prioridade, o primeiro projeto responder abre o arquivo.  
  
    -   Se nenhum responde de projeto com a prioridade mais alta (DP_Intrinsic), mas responder de todos os projetos com a mesma, com baixa prioridade, o projeto ativo abre o arquivo. Se nenhum projeto estiver ativo, o primeiro projeto responder abre o arquivo.  
  
    -   Se nenhum projeto declarações de propriedade do arquivo (DP_Unsupported), o projeto arquivos diversos abre o arquivo.  
  
         Se uma instância do projeto arquivos diversos é criada, o projeto sempre responde com o valor DP_CanAddAsExternal. Esse valor indica que o projeto pode abrir o arquivo. Este projeto é usado para hospedar os arquivos abertos que não estão em qualquer outro projeto. A lista de itens neste projeto não é persistente; Este projeto está visível no **Gerenciador de soluções** somente quando ele é usado para abrir um arquivo.  
  
         Se o projeto arquivos diversos não indicar que ele pode abrir o arquivo, uma instância do projeto não foi criada. Nesse caso, o IDE cria uma instância do projeto arquivos diversos e informa o projeto para abrir o arquivo.  
  
4.  Assim que o IDE determina qual projeto abre o arquivo, ele chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método nesse projeto.  
  
5.  O projeto, em seguida, tem a opção de abrir o arquivo usando um editor específico do projeto ou um editor padrão. Para obter mais informações, consulte [como: os editores abertos específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md) e [como: abrir editores padrão](../../extensibility/how-to-open-standard-editors.md), respectivamente.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir arquivos usando o aberto com o comando](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)   
 [Abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)   
 [Como: abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md)   
 [Como abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)

