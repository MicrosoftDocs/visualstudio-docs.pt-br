---
title: Opções, Editor de Texto, C#, Avançado | Microsoft Docs
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
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Advanced
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
helpviewer_keywords:
- XML comments
- XML documentation, generating
- outlining options [C#]
- outlining options [J#]
- XML documentation, creating
ms.assetid: 947f9d9a-b0f3-408d-9866-d82895bcee31
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 51707a1df9c9f7144dc9a3af021262ca818f03b1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49850510"
---
# <a name="options-text-editor-c-advanced"></a>Opções, Editor de Texto, C#, Avançado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use essa caixa de diálogo para modificar as configurações de formatação do editor, refatoração de código e comentários da documentação XML do Visual C#. Para acessar essa caixa de diálogo, clique em **Opções** no menu **Ferramentas**, expanda a pasta **Editor de Texto**, expanda **C#** e, em seguida, clique em **Avançado**.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="outlining"></a>Estrutura de tópicos  
 Entre no modo estrutura de tópicos quando os arquivos abrem  
 Quando selecionado, descreve o arquivo de código automaticamente, o que cria blocos de código recolhíveis. Na primeira vez que um arquivo é aberto, blocos #regions e blocos de códigos inativos são recolhidos.  
  
## <a name="editor-help"></a>Ajuda do Editor  
 Sublinhar erros no editor  
 Identifica erros de build no código. Quando essa opção é selecionada, os sublinhados ondulados são exibidos em cores que têm significados específicos:  
  
- Erros de análise são vermelhos.  
  
- Erros de build são azuis.  
  
- Avisos de build são verdes.  
  
- Edições de [Editar e Continuar](../../debugger/edit-and-continue.md) inválidas são roxas.  
  
  Mova o ponteiro sobre o segmento de código sublinhado para ver uma ToolTip com informações sobre o erro.  
  
  Mostrar erros semânticos em tempo real  
  Identifica alguns erros de compilação sem compilação explícita, por exemplo, declarando e usando um tipo desconhecido ou referenciando uma propriedade desconhecida.  
  
  Realçar referências a símbolo sob o cursor  
  Quando o cursor é posicionado em um símbolo, ou ao clicar em um símbolo, todas as instâncias desse símbolo no arquivo de código são realçadas.  
  
## <a name="refactoring"></a>Refatoração  
 Verificar os resultados da refatoração  
 Exibe a caixa de diálogo **Resultados da Verificação** ao tentar refatorar o código que contém erros de build ou quando a refatoração causará uma referência de código para associar a algo diferente de sua associação original.  
  
 Avisar sobre membros com referências geradas por compilador  
 Exibe uma caixa de diálogo de aviso ao tentar refatorar um membro que tem o mesmo nome que uma referência gerada pelo compilador.  
  
## <a name="xml-documentation-comments"></a>Comentários da documentação XML  
 Gerar comentários da documentação XML para ///  
 Quando selecionado, insere as marcas de início e término \<summary> automaticamente em comentários da documentação XML depois de digitar a introdução de comentário ///. Para obter mais informações sobre a documentação XML, consulte [Comentários da documentação XML](http://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199).  
  
## <a name="implement-interface"></a>Implementar interface  
 Envolver o código gerado com #region  
 Insere um Membro \<*interface name*> de #region em torno de métodos quando a opção Implementar Interface ou Implementar Interface Explicitamente é usada.  
  
## <a name="organize-usings"></a>Organizar Usos  
 Colocar as diretivas “System” primeiro ao classificar os usos  
 Quando selecionado, `System` usando diretivas é exibido antes de outras diretivas de uso. Para obter mais informações, consulte [Classificar usos](../../misc/sort-usings.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comentários da documentação XML](http://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)   
 [Configurando opções do editor específicas a um idioma](../../ide/reference/setting-language-specific-editor-options.md)   
 [Visual C# IntelliSense](../../ide/visual-csharp-intellisense.md)



