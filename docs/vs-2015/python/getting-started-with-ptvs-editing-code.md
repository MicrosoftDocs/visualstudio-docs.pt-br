---
title: 'Introdução ao PTVS: editando código | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-python
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b412c87c-2f09-4e25-9cc8-ab54f4c44412
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: ghogen
ms.openlocfilehash: ef0a84523a2d828e696fb50f641f392ab7bbd39f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49265779"
---
# <a name="getting-started-with-ptvs-editing-code"></a>Introdução ao PTVS: editando código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O PTVS fornece a experiência produtiva de editor Visual Studio para o Python.  
  
 É possível assistir a essas instruções em um breve [vídeo no YouTube](https://www.youtube.com/watch?v=uZGZNEyyeKs&index=3&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff).  
  
 Comece com o modelo básico de projeto vazio de Aplicativo Python.  
  
 Comece a digitar uma linha de `from … import` no editor.  Você verá que a lista de preenchimento pop-up tem uma lista completa dos módulos que estão disponíveis para importação.  Essa lista varia de acordo com sua versão do Python e quais bibliotecas que você instalou.  Use a biblioteca de matemática como um exemplo.  Você notará que, conforme você digita, a lista de preenchimento filtra esses itens, incluindo os caracteres digitados.  Conclua a instrução importando o identificador `sin`.  
  
```python  
from math import sin  
  
```  
  
 Durante a codificação, se você usar um identificador que seja desvinculado, mas que pode ser encontrado em suas bibliotecas, o PTVS oferece uma correção rápida pop-up para adicionar a instrução de importação adequada de que precisa.  Por exemplo, se você digitou `cos`, então, você verá **importar da matemática**.  
  
 Você pode usar um snippet para gerar o código.  No menu Editar, selecione IntelliSense e depois insira Snippet.  Agora, selecione Python e, em seguida, def.  Chame a função `make_dot_string` e adicione um parâmetro `x`.  Agora, já é possível adicionar asserções ao arquivo para desenvolvimento orientado por testes e você verá que o PTVS já oferece a nova função em listas de preenchimento.  
  
```python  
assert make_dot_string(90) == '          o'  
assert make_dot_string(180) == 'o'  
  
```  
  
 Agora, volte para a nova função e comece a escrever o seguinte corpo:  
  
```python  
return " " * int(10 * cos(radians(x)) + 10) + "o"  
  
```  
  
 Você verá que o PTVS supõe que o parâmetro é um inteiro porque analisou os sites de chamada para essa função.   Você também precisará usar a correção rápida para importar `radians`.  
  
 Use outro snippet para criar um bloco principal digitando `main` no nível superior, invocando a interface do usuário de smart tag e usando a guia para selecionar "def main..."  Escreva um loop básico para chamar `make_dot_string`.  Você verá o que o PTVS sabe que a função retorna uma cadeia de caracteres se pressionar ponto e verá os preenchimentos disponibilizados.  Essas informações de tipo fluirão em todo seu programa, portanto, sempre que seus valores acabarem, podemos fornecer dicas de ferramenta e preenchimentos que o ajudarão a compreender e escrever mais bem seu código.  
  
 Adicione uma chamada para impressão e receberá um principal semelhante ao seguinte:  
  
```python  
def main ():  
    for i in range(10000000):  
        s = make_dot_string(i)  
        print(s)  
```  
  
 Se pressionar F5, o código será executado em uma janela cmd.exe e você verá um ponto oscilando para frente e para trás.  
  
 É possível assistir a essas instruções em um breve [vídeo no YouTube](https://www.youtube.com/watch?v=uZGZNEyyeKs&index=3&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff).  
  
## <a name="see-also"></a>Consulte também  
 [Documentação do wiki](https://github.com/Microsoft/PTVS/wiki/Editor-Features)   
 [Introdução ao PTVS e vídeos de aprofundamento](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)

