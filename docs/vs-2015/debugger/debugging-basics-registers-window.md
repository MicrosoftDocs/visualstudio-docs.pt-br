---
title: 'Noções básicas de depuração: Janela registros | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- Registers window, about Registers window
- debugging [Visual Studio], Registers window
ms.assetid: ab354047-053e-4f94-8ac1-26e761442b6f
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 27337c5bea0d0216b27411dc5e91d7ca4c778615
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722339"
---
# <a name="debugging-basics-registers-window"></a>Noções básicas sobre depuração: janela Registros
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **registra** janela está disponível somente se a depuração do nível de endereços estiver habilitada na **opções** caixa de diálogo **depuração** nó.  
  
 Os registros são locais especiais dentro de um processador (CPU) que são usados para armazenar partes pequenas de dados em que o processador está trabalhando ativamente. Compilar ou interpretar o código-fonte gera instruções que movem dados da memória para os registros e de volta, conforme o necessário. Acessar dados em registros é muito rápido comparado a acessar dados na memória. Sendo assim, o código que permite que o processador mantenha dados em um registro e os acesse repetidamente tende a ser executado mais rápido do que o código que requer que o processador carregue e descarregue registros constantemente. Para que o compilador possa manter os dados nos registros e executar outras otimizações, evite usar variáveis globais e confie em variáveis locais o máximo possível. O código escrito dessa maneira tem boa a localidade de referência. Em algumas linguagens, por exemplo, C/C++, o desenvolvedor pode declarar uma variável do registro, que diz ao compilador para tentar o melhor possível para manter a variável em um registro constantemente. Para obter mais informações, consulte [registrar palavra-chave](http://msdn.microsoft.com/en-us/5b66905a-2f7f-4918-bb55-5e66d4bc50f9).  
  
 Os registros podem ser divididos em dois tipos: uso geral e finalidade especial. Os registros de uso geral mantêm dados para operações gerais, por exemplo, adicionar dois números ou referenciar um elemento em uma matriz. Os registros de finalidade especial têm finalidades específicas e significado especializado. Um bom exemplo é o registro do ponteiro de pilha, que o processador usa para manter controle da pilha de chamadas do programa. Como programador, você provavelmente não manipulará o ponteiro de pilhas diretamente. No entanto, é essencial para o funcionamento correto do programa porque, sem o ponteiro de pilha, o processador não saberia para onde retornar ao término de uma chamada de função.  
  
 A maioria de registros de uso geral contém apenas um elemento de dados. Por exemplo, um único inteiro, número de ponto flutuante ou elemento de uma matriz. Alguns processadores mais novos têm registros maiores, chamados de registros de vetor, que podem manter uma matriz de dados pequena. Como eles contêm tantos dados, os registros de vetor permitem que as operações que envolvem as matrizes sejam executadas muito rapidamente. Os registros de vetor foram usados primeiro em supercomputadores caros de alto desempenho, mas agora estão se tornando disponíveis em microprocessadores onde estão acostumados a grande vantagem em operações gráficas intensivas.  
  
 Um processador normalmente tem dois conjuntos de registros de uso geral, um otimizado para operações de ponto flutuante e o outro para operações de inteiros. Não é surpresa eles serem chamados de registros de pontos flutuante e inteiros.  
  
 O código gerenciado é compilado em tempo de execução para o código nativo que acessa os registros físicos do microprocessador. O **registra** janela exibe esses registros físicos para common language runtime ou código nativo. O **registra** janela exibe informações de registro para o script ou aplicativo SQL, porque o script e SQL são linguagens que não dão suporte ao conceito de registros.  
  
 Para obter mais informações sobre como exibir o **registra** janela, consulte [usando a janela de registros](../debugger/how-to-use-the-registers-window.md).  
  
 Quando você observa a **registra** janela, você verá entradas como este exemplo:  
  
```  
EAX = 003110D8  
```  
  
 O símbolo à esquerda do sinal = é o nome do registro, EAX, nesse caso. O número à direita do sinal = representa o conteúdo do registro.  
  
 O **registra** janela permite que você faça mais do que simplesmente exibir o conteúdo de um registro. Quando você está no modo de interrupção em código nativo, pode clicar no conteúdo de um registro e editar o valor. Isso não é algo que você deve fazer aleatoriamente. A menos que você compreenda o registro que está editando, e os dados que ele contém, o resultado de uma edição descuidada provavelmente será uma falha de programa ou alguma outra consequência indesejada. Infelizmente, uma explicação detalhada dos conjuntos de registro dos vários processadores Intel e compatíveis com Intel vai além do escopo dessa breve introdução.  
  
## <a name="register-groups"></a>Registrar grupos  
 Para reduzir a desordem, o **registra** janela organiza registros em grupos. Se o botão direito do mouse sobre o **registra** janela, você verá um menu de atalho contendo uma lista de grupos, que você pode exibir ou ocultar como achar melhor.  
  
## <a name="see-also"></a>Consulte também  
 [Como: usar a janela registros](../debugger/how-to-use-the-registers-window.md)   
 [Noções básicas do depurador](../debugger/debugger-basics.md)





