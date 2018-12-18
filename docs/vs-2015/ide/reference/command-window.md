---
title: Janela Comando | Microsoft Docs
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
- VS.CommandWindow
helpviewer_keywords:
- IDE, Command window
- Mark mode in Command window
- Command window
- Command mode in Command window
- IDE Command window
ms.assetid: 48711628-1909-4713-a73e-d7b714c77f8a
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b83a9e86aea02e27242a0c1f02ca3f8459152214
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49870179"
---
# <a name="command-window"></a>Janela Comando
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
A janela **Comando** é usada para executar comandos ou aliases diretamente no IDE (ambiente de desenvolvimento integrado) do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Você pode executar tanto comandos de menu quanto comandos que não aparecem em nenhum menu. Para exibir a janela **Comando**, escolha **Outras Janelas** no menu **Exibir** e selecione **Janela Comando**.  
  
## <a name="displaying-the-values-of-variables"></a>Exibindo os valores de variáveis  
 Para verificar o valor de uma variável `varA`, use o [Comando Imprimir](../../ide/reference/print-command.md):  
  
```  
>Debug.Print varA  
```  
  
 O ponto de interrogação (?) é um alias para `Debug.Print`, portanto, esse comando também pode ser escrito:  
  
```  
>? varA  
```  
  
 As duas versões desse comando retornarão o valor da variável `varA`.  
  
## <a name="entering-commands"></a>Inserindo comandos  
 O símbolo de maior que (`>`) é exibido na borda esquerda da janela Comando como um prompt para novas linhas. Use as teclas de SETA PARA CIMA e SETA PARA BAIXO para rolar os comandos emitidos anteriormente.  
  
|Tarefa|Solução|Exemplo|  
|----------|--------------|-------------|  
|Avaliar uma expressão.|Preceda a expressão com um ponto de interrogação (`?`).|`? myvar`|  
|Mude para uma janela Imediata.|Digite `immed` na janela, sem o sinal de maior que (>)|`immed`|  
|Mude de volta para a janela Comando em uma janela Imediata.|Digite `cmd` na janela.|`>cmd`|  
  
 Os seguintes atalhos ajudarão a navegar no modo Comando.  
  
|Ação|Local do cursor|Keybinding|  
|------------|---------------------|----------------|  
|Percorra a lista de comandos inseridos anteriormente.|Linha de entrada|SETA PARA CIMA E SETA PARA BAIXO|  
|Role para cima na janela.|Conteúdo da janela Comando|CTRL+SETA PARA CIMA|  
|Role para baixo na janela.|Conteúdo da janela Comando|SETA PARA BAIXO ou CTRL+SETA PARA BAIXO|  
  
> [!TIP]
>  Você pode copiar todo ou parte de um comando anterior para a linha de entrada rolando até ele, realçando todo ou parte dele e pressionando ENTER.  
  
## <a name="mark-mode"></a>Modo de Marca  
 Quando você clica em qualquer linha anterior na janela **Comando**, você muda automaticamente para o modo Marca. Isso permite selecionar, editar e copiar o texto de comandos anteriores como você faria em qualquer editor de texto e colá-lo na linha atual.  
  
## <a name="the-equals--sign"></a>O sinal de igual (=)  
 A janela usada para inserir o comando `EvaluateStatement` determina se um sinal de igual (=) é interpretado como um operador de comparação ou um operador de atribuição.  
  
 Na janela **Comando**, um sinal de igual (=) é interpretado como um operador de comparação. Você não pode usar operadores de atribuição na janela **Comando**. Dessa forma, por exemplo, se os valores das variáveis `varA` e `varB` forem diferentes, o comando  
  
```  
>Debug.EvaluateStatement(varA=varB)  
```  
  
 retornará um valor de `False`.  
  
 Na janela **Imediato**, por outro lado, um sinal de igual (=) é interpretado como um operador de atribuição. Assim, por exemplo, o comando  
  
```  
>Debug.EvaluateStatement(varA=varB)  
```  
  
 atribuirá à variável `varA` o valor da variável `varB`.  
  
## <a name="parameters-switches-and-values"></a>Parâmetros, Opções e Valores  
 Alguns comandos [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] têm argumentos, opções e valores obrigatórios e opcionais. Certas regras se aplicam ao lidar com esses comandos. A seguir está um exemplo de um comando avançado para esclarecer a terminologia.  
  
```  
Edit.ReplaceInFiles /case /pattern:regex var[1-3]+ oldpar   
```  
  
 Neste exemplo,  
  
- `Edit.ReplaceInFiles` é o comando  
  
- `/case` e `/pattern:regex` são opções (precedidas pelo caractere de barra invertida [/])  
  
- `regex` é o valor da opção `/pattern`; a opção `/case` não tem valor  
  
- `var[1-3]+` e `oldpar` são parâmetros  
  
  > [!NOTE]
  >  Qualquer comando, parâmetro, opção ou valor que contenha espaços deve ter aspas duplas em um dos lados.  
  
  A posição de opções e parâmetros pode ser trocada livremente na linha de comando, com exceção do comando [Shell](../../ide/reference/shell-command.md), que exige uma ordem específica para opções e parâmetros.  
  
  Quase todas as opções com suporte em um comando têm dois formatos: um formato abreviado (um caractere) e um formato longo. Várias opções de formato curto podem ser combinadas em um grupo. Por exemplo, `/p /g /m` pode ser expressos, alternativamente, como `/pgm`.  
  
  Se opções de formato curto forem combinadas em um grupo e receberem um determinado valor, esse valor se aplicará a todas as opções. Por exemplo, `/pgm:123` é igual a `/p:123 /g:123 /m:123`. Um erro ocorrerá se alguma das opções no grupo não aceitar um valor.  
  
## <a name="escape-characters"></a>Caracteres de escape  
 Um caractere de acento circunflexo (^) em uma linha de comando significa que o caractere imediatamente a seguir é interpretado literalmente, em vez de como um caractere de controle. Isso pode ser usado para inserir aspas retas ("), espaços, barras iniciais, acentos circunflexos ou quaisquer outros caracteres literais em um parâmetro ou valor de opção, com a exceção de nomes de opção. Por exemplo,  
  
```  
>Edit.Find ^^t /regex  
```  
  
 Um acento circunflexo funciona da mesma forma tanto dentro quanto fora das aspas. Se um acento circunflexo for o último caractere na linha, ele será ignorado. O exemplo mostrado aqui demonstra como pesquisar o padrão "^t".  
  
## <a name="use-quotes-for-path-names-with-spaces"></a>Usar aspas para nomes de caminho com espaços  
 Se, por exemplo, você quiser abrir um arquivo com um caminho que contenha espaços, deverá colocar aspas duplas ao redor do caminho ou segmento do caminho que contém espaços: **C:\\"Arquivos de Programas"** ou **"C:\Arquivos de Programas"**.  
  
## <a name="see-also"></a>Consulte também  
 [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)   
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)



