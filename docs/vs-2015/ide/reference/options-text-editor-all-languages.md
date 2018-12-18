---
title: Opções, Editor de Texto, Todos os idiomas | Microsoft Docs
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
- VS.ToolsOptionsPages.Text_Editor.JavaScript.General
- VS.ToolsOptionsPages.Text_Editor.ResJSON.General
- vs.toolsoptionspages.text_editor.all_languages.scrollbars
helpviewer_keywords:
- Text Editor Options dialog box
- statement completion
- word wrap
- General dialog box
- line numbers
- virtual space
ms.assetid: 49ee7306-9d46-4170-850f-a1716171752d
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 987e0339f2d27405c81ce05b6a30181a1469be7b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884167"
---
# <a name="options-text-editor-all-languages"></a>Opções, Editor de Texto, Todos os Idiomas
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Esta caixa de diálogo permite alterar o comportamento padrão do Editor de Código. Essas configurações também se aplicam a outros editores baseados no Editor de código, como o modo de exibição de Fonte do Designer de HTML. Para abrir essa caixa de diálogo, selecione **Opções** no menu **Ferramentas**. Dentro da pasta **Editor de Texto**, expanda a subpasta **Todos os Idiomas** e, em seguida, escolha **Geral**.  
  
> [!CAUTION]
>  Esta página define opções padrão para todas as linguagens de desenvolvimento. Lembre-se de que redefinir uma opção nessa caixa de diálogo redefinirá as opções Geral em todas as linguagens, não importa quais opções sejam selecionadas aqui. Para alterar as opções do Editor de Texto para apenas uma linguagem, expanda a subpasta para aquela linguagem e selecione suas páginas de opções.  
  
 Uma marca de seleção esmaecida é exibida quando uma opção tiver sido selecionada nas páginas de opções Geral para algumas linguagens de programação, mas não para outras.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="statement-completion"></a>Preenchimento de declaração  
 Membros automático de lista  
 Quando selecionadas, listas pop-up de membros, propriedades, valores ou métodos disponíveis são exibidas pelo IntelliSense conforme você digita no editor. Escolha qualquer item da lista pop-up para inseri-lo no código. Selecionar essa opção habilita a opção **Ocultar membros avançados**.  
  
 Ocultar membros avançados  
 Quando selecionada, diminui listas de preenchimento de declaração pop-up exibindo somente os itens mais usados. Outros itens são filtrados da lista.  
  
 Informações de parâmetro  
 Quando selecionada, a sintaxe completa para a declaração ou procedimento atual é exibida sob o ponto de inserção no editor, com todos os seus parâmetros disponíveis. O parâmetro que a seguir você pode atribuir é exibido em negrito.  
  
## <a name="settings"></a>Configurações  
 Ativar o espaço virtual  
 Quando esta opção está selecionada e a caixa de seleção **Quebra automática de linha** está desmarcada, você pode clicar em qualquer lugar além do final de uma linha no Editor de Códigos e digitar. Esse recurso pode ser usado para posicionar comentários em um ponto consistente ao lado do seu código.  
  
 Quebra automática de linha  
 Quando selecionada, qualquer parte de uma linha que se estenda horizontalmente além da área visível do editor é exibida automaticamente na próxima linha. Selecionar essa opção habilita a opção **Mostrar glifos visuais para quebra automática de linha**.  
  
> [!NOTE]
>  O recurso **Espaço Virtual** é desativado enquanto **Quebra automática de linha** está ativada.  
  
 Glifos visuais de apresentação para a quebra automática de linha  
 Quando selecionada, um indicador de seta d retorno é exibido no ponto em que uma linha longa quebra-se para uma segunda linha.  
  
 ![Captura de tela de LineBreakSymbol](../../ide/reference/media/linebreak.gif "linebreak")  
  
 Desmarque esta opção se preferir não exibir esses indicadores.  
  
> [!NOTE]
>  Essas setas de lembrete não são adicionadas ao seu código, e não imprimem. São somente para referência.  
  
 Aplicar comandos recortar ou de impressão para linhas em branco quando não há nenhuma seleção  
 Esta opção define o comportamento do editor quando você coloque o ponto de inserção em uma linha em branco, não seleciona nada e então Copia ou Corta.  
  
- Quando essa opção está selecionada, a linha em branco é copiada ou cortada. Se você então Colar, uma nova linha em branco será inserida.  
  
- Quando essa opção está desmarcada, o comando Cortar remove linhas em branco. No entanto, os dados na Área de Transferência são preservados. Portanto, se você usar o comando Colar, o conteúdo copiado mais recentemente para a Área de Transferência será colado. Se nada foi copiado anteriormente, nada é colado.  
  
  Essa configuração não tem efeito sobre o Copiar ou Cortar quando uma linha não está em branco. Se nada é selecionado, a linha inteira é copiada ou recortar. Se você então Colar, o texto da linha inteira e seu caractere de fim de linha serão colados.  
  
> [!TIP]
>  Para exibir indicadores para espaços, tabulações e fins de linha, e assim distinguir linhas recuadas de linhas totalmente em branco, selecione **Avançado** no menu **Editar** e escolha **Exibir Espaço em Branco**.  
  
## <a name="display"></a>Monitor  
 Os números de linha  
 Quando selecionada, um número de linha aparece ao lado de cada linha de código.  
  
> [!NOTE]
>  Esses números de linha não são adicionados ao seu código e não são impressos. São somente para referência.  
  
 Permitir a navegação URL de clique único  
 Quando selecionada, o cursor do mouse muda para uma mão apontando conforme passa sobre uma URL no editor. Você pode clicar no URL para exibir a página indicada no seu navegador da Web.  
  
 Barra de navegação  
 Quando selecionada, exibe a **Barra de navegação** na parte superior do editor de código. Suas listas suspensas **Objetos** e **Membros** permitem escolher um objeto específico no código, selecionar entre seus membros e navegar para a declaração do membro selecionado no Editor de Códigos.  
  
## <a name="see-also"></a>Consulte também  
 [Opções, Editor de Texto, Todas as Linguagens, Guias](../../ide/reference/options-text-editor-all-languages-tabs.md)   
 [Caixa de diálogo Geral, Ambiente, Opções](../../ide/reference/general-environment-options-dialog-box.md)   
 [Usando o IntelliSense](../../ide/using-intellisense.md)



