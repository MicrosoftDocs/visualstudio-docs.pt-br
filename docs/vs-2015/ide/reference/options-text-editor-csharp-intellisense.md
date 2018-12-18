---
title: Opções, Editor de Texto, C#, IntelliSense | Microsoft Docs
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
- VS.ToolsOptionsPages.Text_Editor.CSharp.Intellisense
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Intellisense
helpviewer_keywords:
- IntelliSense [J#], options
- underlines, wavy
- IntelliSense [C#], options
- IntelliSense [C#], wavy underlines
- wavy underlines
- Text Editor Options dialog box, IntelliSense
ms.assetid: 3466dedb-e5f4-424c-8dd8-e4941b2f4fc2
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 31c9909e5ea9364e806fdd2d7a39903bf1468abb
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49262165"
---
# <a name="options-text-editor-c-intellisense"></a>Opções, Editor de Texto, C#, IntelliSense
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use a página de propriedades **IntelliSense** para modificar as configurações que afetam o comportamento do IntelliSense no Visual C#. É possível acessar a página de propriedades **IntelliSense** clicando em **Opções** no menu **Ferramentas**, clicando em **C#** na pasta **Editor de Texto** e, em seguida, em **IntelliSense.**  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 A página de propriedades **IntelliSense** contém as seguintes propriedades:  
  
## <a name="completion-lists"></a>Listas de Conclusão  
 **Mostrar lista de preenchimento depois que um caractere é digitado**  
 Quando essa opção estiver selecionada, o IntelliSense exibirá automaticamente a lista de preenchimento quando você começar a digitar. Quando essa opção não estiver selecionada, o IntelliSense ainda estará disponível no menu **IntelliSense** ou pressionando CTRL+ESPAÇO.  
  
 **Colocar palavras-chave em listas de preenchimento**  
 Quando essa opção estiver selecionada, o IntelliSense adicionará palavras-chave do C#, por exemplo, [classe](http://msdn.microsoft.com/library/b95d8815-de18-4c3f-a8cc-a0a53bdf8690), à lista de preenchimento.  
  
 **Colocar snippets de código em listas de preenchimento**  
 Quando essa opção estiver selecionada, o IntelliSense adicionará aliases de snippets de código C# à lista de preenchimento. Caso o alias do snippet de código seja igual a uma palavra-chave, por exemplo, [classe](http://msdn.microsoft.com/library/b95d8815-de18-4c3f-a8cc-a0a53bdf8690), a palavra-chave será substituída pelo atalho. Para obter mais informações, consulte [Snippets de código do Visual C#](../../ide/visual-csharp-code-snippets.md).  
  
## <a name="selection-in-completion-lists"></a>Seleção em listas de preenchimento  
 **Confirmado pela digitação dos seguintes caracteres:**  
 Especifica todos os caracteres que executam o preenchimento automático do IntelliSense para o item selecionado na lista de preenchimento, depois de ele ser digitado.  
  
 **Confirmado pressionando a barra de espaço**  
 Especifica para incluir a ação de pressionar a barra de espaço para executar o preenchimento automático do IntelliSense para o item selecionado na lista de preenchimento.  
  
 **Adicionar uma nova linha ao pressionar Enter após o fim da palavra totalmente digitada**  
 Especifica que, se você digitar todos os caracteres de uma entrada na lista de preenchimento e, em seguida, pressionar ENTER, uma nova linha será criada automaticamente e o cursor será movido para a nova linha.  
  
 Por exemplo, se você digitar `else` e pressionar ENTER, isto será exibido no editor:  
  
 `else`  
  
 `|` (local do cursor)  
  
 No entanto, se você digitar apenas `el` e pressionar ENTER, isto será exibido no editor:  
  
 `else|` (local do cursor)  
  
## <a name="intellisense-member-selection"></a>Seleção de Membro IntelliSense  
 **Pré-seleciona o membro usado mais recentemente**  
 Quando essa opção estiver selecionada, o IntelliSense pré-selecionará os membros selecionados recentemente na caixa pop-up Listar Membros do preenchimento automático de nome de objeto durante a sessão atual no IDE (ambiente de desenvolvimento integrado). O histórico dos membros mais usados recentemente é limpo entre cada sessão no IDE. Para obter mais informações, consulte [IntelliSense para membros usados mais recentemente](../../misc/intellisense-for-most-recently-used-members.md).  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Geral, Ambiente, Opções](../../ide/reference/general-environment-options-dialog-box.md)   
 [Comentários da documentação XML](http://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)   
 [Usando o IntelliSense](../../ide/using-intellisense.md)



