---
title: Usando o IntelliSense | Microsoft Docs
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
- vc.tools.intellisense
helpviewer_keywords:
- IntelliSense, Complete Word
- IntelliSense, completion mode
- parameter information
- IntelliSense, List Members
- Quick Info
- Parameter Info
- IntelliSense [Visual Studio]
- IntelliSense, suggestion mode
- IntelliSense, Parameter Info
- IntelliSense, customizing
- Complete Word
- IntelliSense
- List Members
ms.assetid: 9fdb489b-8b46-4b92-9ccc-c8f8cc184081
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 586a0b31166f3b7696865e54f7d2df9c415315f9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49197179"
---
# <a name="using-intellisense"></a>Usando IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O IntelliSense é o termo geral para vários recursos: Listar Membros, Informações do Parâmetro, Informação Rápida e Completar Palavra. Esses recursos ajudam você a aprender mais sobre o código que está usando, a manter o acompanhamento dos parâmetros que está digitando e a adicionar chamadas a métodos e propriedades pressionando apenas algumas teclas.  
  
 Vários aspectos do IntelliSense são específicos do idioma. Para obter mais informações sobre o IntelliSense para diferentes idiomas, consulte os tópicos listados em Consulte também.  
  
## <a name="list-members"></a>Listar Membros  
 Uma lista de membros válidos de um tipo (ou namespace) aparece depois que você digita um caractere disparador (por exemplo, um ponto (`.`) no código gerenciado ou `::` em C++). Se você continuar digitando caracteres, a lista será filtrada para incluir somente os membros que comecem com esses caracteres.  
  
 Após selecionar um item, você poderá inseri-lo em seu código pressionando TAB ou inserindo um espaço. Se você selecionar um item e digitar um ponto, o item aparecerá seguido pelo ponto, que abrirá outra lista de membros. Ao selecionar um item, mas antes de inseri-lo, você obtém a Informação Rápida do item.  
  
 Na lista de membros, o ícone à esquerda representa o tipo do membro, como namespace, classe, função ou variável. Para obter uma lista de ícones, consulte [Class View and Object Browser Icons (Modo de Exibição de Classe e ícones do Pesquisador de Objetos)](../ide/class-view-and-object-browser-icons.md). A lista pode ser muito longa, de modo que você pode pressionar PAGE UP e PAGE DOWN para mover para cima ou para baixo na lista.  
  
 ![Lista de membros do Visual Studio](../ide/media/vs2015-intellisense.png "vs2015_Intellisense")  
  
 É possível invocar o recurso **Listar membros** manualmente digitando CTRL+J, clicando em **Editar/IntelliSense/Listar Membros** ou clicando no botão **Listar membros** na barra de ferramentas do editor. Quando é invocada em uma linha em branco ou fora de um escopo reconhecível, a lista exibe símbolos no namespace global.  
  
 Para desativar Listar Membros por padrão (para que ele não seja exibido, exceto se especificamente invocado), vá para **Ferramentas/Opções/Todas as linguagens** e desmarque **Listar membros automaticamente**. Se você deseja desligar Listar Membros somente para uma linguagem específica, vá para as configurações **Gerais** dessa linguagem.  
  
 Você também pode alterar para o modo de sugestão, no qual apenas o texto que você digita é inserido no código. Por exemplo, se você inserir um identificador que não está na lista e pressionar TAB, no modo de preenchimento, a entrada poderá substituir o identificador digitado. Para alternar entre o modo de preenchimento e o modo de sugestão, pressione CTRL+ALT+ESPAÇO ou clique em **Editar/IntelliSense/Ativar/Desativar Modo de Preenchimento**.  
  
## <a name="parameter-info"></a>Informações de Parâmetro  
 Informações de Parâmetro fornecem informações sobre o número, os nomes e os tipos de parâmetros exigidos por um método, um parâmetro de tipo genérico de atributo (em C#) ou um modelo (em C++).  
  
 O parâmetro em negrito indica o próximo parâmetro que é necessário à medida que você digita a função. Para funções sobrecarregadas, você pode usar as teclas de seta PARA CIMA e PARA BAIXO para exibir informações de parâmetro alternativas para as sobrecargas de função.  
  
 ![Informações do parâmetro](../ide/media/vs2015-param-info.png "VS2015_param_Info")  
  
 Quando você anota funções e parâmetros com comentários da Documentação XML, os comentários são exibidos como Informações do Parâmetro. Para obter mais informações, consulte [Fornecendo comentários de código XML](../ide/supplying-xml-code-comments.md).  
  
 É possível invocar manualmente Informações do Parâmetro clicando em **Editar IntelliSense/Informações do Parâmetro**, digitando CTRL+SHIFT+ESPAÇO ou clicando no botão **Informações do Parâmetro** na barra de ferramentas do editor.  
  
## <a name="quick-info"></a>Informação Rápida  
 Informação Rápida exibe a declaração completa de qualquer identificador no seu código.  
  
 ![Informações rápidas do Visual Studio](../ide/media/vs2015-quick-info.png "VS2015_Quick_info")  
  
 Quando você seleciona um membro na caixa **Listar Membros**, as Informações Rápidas também são exibidas.  
  
 ![Informações do parâmetro em um arquivo de código C&#35;](../ide/media/vs2015-paraminfo.png "VS2015_ParamInfo")  
  
 É possível invocar Informações Rápidas clicando em **Editar/IntelliSense/Informações Rápidas**, digitando CTRL+I ou clicando no botão **Informações Rápidas** na barra de ferramentas do editor.  
  
 Se uma função estiver sobrecarregada, o IntelliSense não poderá exibir informações de todos os formulários da sobrecarga.  
  
 É possível desativar as Informações Rápidas no C++ definindo **Ferramentas/Opções/Editor de Texto/C/C++/Avançado/Informações Rápidas Automático** como `false`.  
  
## <a name="complete-word"></a>Completar Palavra  
 Completar Palavra completa o restante de uma variável, um comando ou um nome de função uma vez que você tenha inserido caracteres suficientes para remover ambiguidades do termo. É possível invocar Completar palavra clicando em **Editar/IntelliSense/Completar palavra**, digitando CTRL+ESPAÇO ou clicando no botão **Completar Palavra** na barra de ferramentas do editor.  
  
## <a name="intellisense-options"></a>Opções do IntelliSense  
 As opções do IntelliSense são ativadas por padrão. Para desativá-las, clique em **Ferramentas/Opções/Editor de Texto** e desmarque a seleção **Informações do parâmetro** ou **Listar membros automaticamente** se você não deseja o recurso Listar Membros.  
  
## <a name="troubleshooting-intellisense"></a>Solução de problemas do IntelliSense  
 As opções do IntelliSense podem não funcionar como você espera em alguns casos.  
  
 **O cursor está abaixo de um erro de código.** Talvez não seja possível usar o IntelliSense se uma função incompleta ou outro erro existirem no código acima do cursor, pois o IntelliSense talvez não possa analisar os elementos do código. Você pode resolver esse problema comentando o código aplicável.  
  
 **O cursor está em um comentário de código.** Não será possível usar o IntelliSense se o cursor estiver em um comentário no arquivo de origem.  
  
 **O cursor está em um literal de cadeia de caracteres.** Não será possível usar o IntelliSense se o cursor estiver entre aspas em um literal de cadeia de caracteres, como no exemplo a seguir:  
  
```  
MessageBox( hWnd, "String literal|") )  
```  
  
 **As opções automáticas estão desativadas.** Por padrão, o IntelliSense funciona automaticamente, mas é possível desabilitar isso. Mesmo se o preenchimento automático de declaração for desabilitado, é possível invocar um recurso IntelliSense.  
  
## <a name="see-also"></a>Consulte também  
 [IntelliSense específico do Visual Basic](../ide/visual-basic-specific-intellisense.md)   
 [Visual C# IntelliSense](../ide/visual-csharp-intellisense.md)   
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)   
 [Fornecendo comentários de código XML](../ide/supplying-xml-code-comments.md)



