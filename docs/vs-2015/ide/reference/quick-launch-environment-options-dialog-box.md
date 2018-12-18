---
title: Caixa de diálogo Início Rápido, Ambiente, Opções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Environment.QuickLaunch
- vs.quicklaunch
helpviewer_keywords:
- searching IDE
- IDE, searching
ms.assetid: 4200f297-d065-4723-9a30-d91ff2e26c9d
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1e012e5ec4d9326cb1e6732ed78a8de8a60aeda8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49269055"
---
# <a name="quick-launch-environment-options-dialog-box"></a>Caixa de diálogo de início rápido, ambiente, opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Você pode usar o **Início Rápido** para pesquisar e executar rapidamente ações para ativos do IDE, como opções, modelos e menus. Não é possível usar o **Início Rápido** para pesquisar código e símbolos. A caixa de pesquisa **Início Rápido** fica localizada no canto superior direito da barra de menus e pode ser acessada usando as teclas Ctrl + Q. Basta digitar a cadeia de caracteres de pesquisa na caixa. Para pesquisar cadeias de caracteres que contêm @, use “@@”.  
  
 O **Início Rápido** é habilitado por padrão quando você instala o Visual Studio. Na barra de menus, você pode mostrar ou ocultar o **Início Rápido** escolhendo **Ferramentas**, **Opções**. Expanda o nó **Ambientes** e escolha **Início Rápido**. Marque ou desmarque a caixa de seleção **Habilitar Início Rápido**. Também é possível habilitar ou desabilitar categorias de pesquisa nesta página.  
  
## <a name="category-list"></a>Lista de Categorias  
 Os resultados da pesquisa do Início Rápido aparecem em quatro categorias: **Usados Recentemente**, **Menus**, **Opções** e **Documentos Abertos**, em conjunto com o número de itens na categoria. Para percorrer os resultados da pesquisa por categoria, pressione as teclas Ctrl + Q para mostrar todos os resultados da categoria seguinte. Após a última categoria apareces, Ctrl + Q mostra alguns resultados de cada categoria. Você pode usar Ctrl + Shift + Q para navegar pelas categorias em ordem inversa. Para exibir todos os resultados da pesquisa em uma categoria, escolha o nome da categoria.  
  
 É possível usar os seguintes atalhos para limitar a pesquisa a categorias específicas.  
  
|Categoria|Atalho|Descrição do atalho|  
|--------------|--------------|--------------------------|  
|Usados Recentemente|@mru<br /><br /> Por exemplo, `@mru font`|Exibe até cinco dos itens que foram **Usados Recentemente**.|  
|Menus|@menu<br /><br /> Por exemplo, `@menu font`|Limita a pesquisa a itens de menu.|  
|Opções|@opt<br /><br /> Por exemplo, `@opt font`|Limita a pesquisa a configurações na caixa de diálogo **Opções**.|  
|Documentos|@doc<br /><br /> Por exemplo, `@doc font`|Limita a pesquisa a nomes de arquivo e caminhos de documentos abertos para os critérios de pesquisa, mas não pesquisa o texto dentro dos próprios arquivos.|  
  
> [!NOTE]
>  Você pode alterar as teclas de atalho na página **Geral**, **Teclado** na caixa de diálogo **Opções**.  
  
## <a name="show-previous-results"></a>Mostrar resultados anteriores  
 Por padrão, o termo de pesquisa que você inserir não persiste entre sessões de pesquisa. A cadeia de caracteres de pesquisa é apagada se você pesquisar um termo, mover o cursor para fora da área de **Início Rápido** e, depois, voltar. Para manter os resultados da pesquisa, acesse a caixa de diálogo **Opções**, escolha **Início Rápido** e, em seguida, marque a caixa de seleção **Mostrar resultados da pesquisa anterior quando o Início Rápido estiver ativado.** . Na próxima vez em que fizer uma pesquisa, deixe a área de Início Rápido e volte, o Início Rápido manterá o termo de pesquisa usado pela última vez e mostrará os resultados da pesquisa.  
  
 Para ver as dicas e truques mais recentes sobre o uso do **Início Rápido**, consulte [O Blog do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=236054).  
  
## <a name="see-also"></a>Consulte também  
 [Elementos gerais da interface do usuário (Visual Studio)](../../ide/reference/general-user-interface-elements-visual-studio.md)   
 [Caixa de diálogo Opções do Ambiente](../../ide/reference/environment-options-dialog-box.md)



