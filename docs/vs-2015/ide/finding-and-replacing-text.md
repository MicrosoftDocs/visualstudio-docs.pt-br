---
title: Localizando e substituindo texto | Microsoft Docs
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
- vs.find
- vs.findreplacecontrol
- vs.findreplace.findsymbol
- vs.findreplace.symbol
- findresultswindow
- vs.findreplace.quickreplace
- vs.findsymbol
- vs.findinfiles
- vs.findresults1
- vs,findsymbolwindow
- vs.findreplace.quickfind
- vs.lookin
- vs.replace
helpviewer_keywords:
- text searches
- Replace in Files dialog box
- find, text
- Find in Files dialog box
- find
- text searches, finding and replacing text
- Replace dialog box
- text, finding and replacing
- find, symbol
- find and replace
- replace
- find text
- replacing text
ms.assetid: a62545c3-1570-4d12-99fb-a82607eb35a1
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e4bbe1456632b2707ca548582bb278f7646ec540
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49273436"
---
# <a name="finding-and-replacing-text"></a>Localizando e substituindo texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível localizar e substituir texto no editor de código do Visual Studio, bem como em determinadas janelas de saída baseadas em texto, como as janelas **Localizar Resultados**, usando o controle **Localizar e Substituir** controle ou **Localizar/Substituir em Arquivos**. Você também pode pesquisar e substituir em algumas janelas de designer, como o designer XAML e o Designer de Formulários do Windows, e em janelas de ferramentas  
  
 É possível definir o escopo das pesquisas para o documento atual, a solução atual ou um conjunto personalizado de pastas. Também é possível especificar um conjunto de extensões de nome de arquivo para pesquisas em vários arquivos. Você pode personalizar a sintaxe de pesquisa usando expressões regulares do .NET.  
  
 Para localizar e substituir expressões regulares, consulte [Usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).  
  
> [!TIP]
>  A caixa **Localizar/Comando** ainda está disponível como um controle de barra de ferramentas, mas não fica mais visível por padrão. Você pode exibir a caixa **Localizar/Comando** escolhendo **Adicionar ou Remover Botões** na barra de ferramentas **Padrão** e escolhendo **Localizar**. Para obter mais informações, consulte [Caixa Localizar/Comando](../ide/find-command-box.md).  
  
## <a name="find-and-replace-control"></a>Controle Localizar e Substituir  
 O controle **Localizar e Substituir** aparece no canto superior direito da janela do editor de código. O controle **Localizar e Substituir** realça imediatamente todas as ocorrências da cadeia de caracteres de pesquisa fornecida no documento atual. Você pode navegar de uma ocorrência para outra escolhendo o botão **Localizar próximo** ou o botão **Localizar anterior** no controle de pesquisa.  
  
 Você pode acessar opções de substituição escolhendo o botão ao lado da caixa de texto **Localizar**. Para fazer uma substituição por vez, escolha o botão **Substituir próximo** ao lado da caixa de texto **Substituir**. Para substituir todas as correspondências, escolha o botão **Substituir tudo**.  
  
 Para alterar a cor de realce das correspondências, escolha o menu **Ferramentas**, selecione **Opções** e, em seguida, escolha **Ambiente** e selecione **Fontes e Cores**. Na lista **Mostrar configurações de**, selecione **Editor de Texto** e, na lista **Exibir Itens**, selecione **Localizar Realce (Extensão)**.  
  
### <a name="searching-tool-windows"></a>Pesquisando em janelas de ferramentas  
 É possível usar o controle **Localizar** em janelas de texto ou de código, como janelas de **Saída** e janelas **Localizar Resultados**, escolhendo **Localizar e Substituir** no menu **Editar** ou (CTRL + F).  
  
 Uma versão do controle Localizar também está disponível em algumas janelas de ferramentas. Por exemplo, agora você pode filtrar a lista de controles na janela **Caixa de Ferramentas** digitando texto na caixa de pesquisa. Outras janelas de ferramentas que agora permitem pesquisar seu conteúdo incluem o **Gerenciador de Soluções**, a janela **Propriedades** e o **Team Explorer**, entre outros.  
  
## <a name="findreplace-in-files"></a>Localizar/Substituir em Arquivos  
 **Localizar/substituir em Arquivos** funciona como o controle **Localizar e Substituir**, mas você pode definir um escopo para a pesquisa. Você pode pesquisar não apenas o atual arquivo aberto no editor, mas também pode pesquisar todos os documentos abertos, toda a solução, o projeto atual e conjuntos de pastas selecionadas. Você também pode pesquisar por extensão de nome de arquivo. Para acessar a caixa de diálogo **Localizar/Substituir em Arquivos**, escolha **Localizar e Substituir** no menu **Editar** (ou CTRL + SHIFT + F).  
  
 Quando você escolhe **Localizar tudo**, uma janela **Localizar Resultados** é aberta e lista as correspondências da pesquisa. Selecionar um resultado na lista exibe o arquivo associado e realça a correspondência. Se o arquivo ainda não estiver aberto para edição, ele será aberto em uma guia de visualização no lado direito da guia. É possível usar o controle **Localizar** para pesquisar na lista **Localizar Resultados**.  
  
### <a name="creating-custom-search-folder-sets"></a>Criando conjuntos de pastas de pesquisa personalizados  
 Você pode definir o escopo da pesquisa escolhendo o botão **Escolher Pastas de Pesquisa** (ele se parece com **...** ) ao lado da caixa **Examinar** caixa. Na caixa de diálogo **Escolher Pastas de Pesquisa**, você pode especificar um conjunto de pastas nas quais deseja pesquisar e pode salvar a especificação para utilizá-la novamente mais tarde. Você pode especificar pastas em um computador remoto somente se tiver mapeado sua unidade para o computador local.  
  
### <a name="creating-custom-component-sets"></a>Criando conjuntos de componentes personalizados  
 Você pode definir conjuntos de componentes como o escopo da pesquisa escolhendo o botão **Editar conjunto de componentes personalizados** ao lado da caixa **Examinar**. Você pode especificar componentes COM ou .NET instalados, projetos do Visual Studio incluídos em sua solução ou qualquer assembly ou biblioteca de tipos (.dll,.tlb, .olb, .exe ou .ocx). Para pesquisar referências, selecione a caixa **Examinar referências**.  
  
## <a name="see-also"></a>Consulte também  
 [Usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md)



