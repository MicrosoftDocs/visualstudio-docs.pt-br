---
title: 'Introdução ao PTVS: depuração | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-python
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82803559-1d60-4c57-98fb-2dc1e0182b42
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: ghogen
ms.openlocfilehash: 8a92eb3779abf5be00f39bd4aa3e66238a729ded
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49204913"
---
# <a name="getting-started-with-ptvs-debugging"></a>Introdução ao PTVS: depurando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O depurador interativo do Visual Studio facilita o diagnóstico e a solução de problemas em seu código Python.  
  
 É possível assistir a essas instruções em um breve [vídeo no YouTube](https://www.youtube.com/watch?v=bO7wpzgy74A&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=4).  
  
 No tópico de introdução anterior, você criou um projeto de Aplicativo Python vazio e inseriu o código a seguir em PythonApplication1.py:  
  
```python  
from math import sin, cos, radians  
import sys  
  
def make_dot_string(x):  
    return ' ' * int(10 * cos(radians(x)) + 10) + 'o'  
  
assert make_dot_string(90) == "          o"  
assert make_dot_string(180) == "o"  
  
def main():  
    for i in range(10000000):  
        s = make_dot_string(i)  
        print(s)  
  
if __name__ == "__main__":  
    sys.exit(int(main() or 0))  
```  
  
 Normalmente, quando estiver trabalhando com código no Visual Studio, você começará a executar o código pressionando F5.  Este comando compila as partes do seu projeto que precisam ser compiladas e começa a executar o código no depurador.  Você pode pressionar Ctrl+F5 para compilar e inicializar seu código sem o depurador.  Com o depurador, seu código é executado um pouco mais lentamente, mas você obtêm excelentes recursos de depuração.  
  
 Outra maneira de inicializar seu código é com o comando Executar em Etapas (normalmente associado ao F11).  Ele é como o F5, mas pausa a execução a cada instrução.  Se quiser interromper o programa em um determinado ponto, você pode pressionar o botão do ponteiro esquerdo na margem esquerda do editor de código para definir um ponto de interrupção.  Quando você pressionar F5, a execução do programa será interrompida ou encerrada na linha com o ponto de interrupção.  O menu Depurar tem mais opções para a execução em etapas, como passar direto por chamadas de função (F10), intervir em chamadas de função (F11) ou ignorar no final de uma função (shift-F11).  
  
 Há mais coisas que você pode fazer quando a execução é interrompida no depurador.  A janela Locais mostra os valores atuais das variáveis locais.  Conforme você executa seu código em etapas, a exibição de locais é atualizada automaticamente.  A janela Autos, que mostra as variáveis próximas à linha atual quando a execução foi interrompida.  Na janela Inspeção, você pode digitar qualquer expressão Python que o depurador atualizará automaticamente sempre que a execução for interrompida.  Também é possível passar o ponteiro sobre variáveis nas janelas do editor para ver uma exibição pop-up dos valores da variável e essa exibição de dica de dados permite que você inspecione objetos.  Alguns tipos de dados têm visualizadores especiais que são acessíveis da exibição de dica de dados (por exemplo, cadeias de caracteres com formatação especial, como HTML, XML ou JSON).  
  
 A janela Pilha de Chamadas mostra as chamadas de função pendentes que levaram à instrução atual em que o depurador foi interrompido.  Você pode escolher diferentes registros de ativação (linhas na pilha de chamadas) nos quais o código continuará sendo executado em cada função, procurar valores de variáveis e assim por diante.  
  
 É possível assistir a essas instruções em um breve [vídeo no YouTube](https://www.youtube.com/watch?v=bO7wpzgy74A&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=4).  
  
## <a name="see-also"></a>Consulte também  
 [Documentação do wiki](https://github.com/Microsoft/PTVS/wiki/Debugging)   
 [Introdução ao PTVS e vídeos de aprofundamento](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)

