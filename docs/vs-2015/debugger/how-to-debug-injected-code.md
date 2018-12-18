---
title: 'Como: depurar código injetado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.injected
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- assembly language, viewing
- debugging [C++], viewing assembly code
- debugging [C++], injected code
- debugging [C++], enabling source annotation
- injected code
- Show Source Code command [debugger]
- debugging [C++], using attributes
- disassembly code, debugging
ms.assetid: a1b4104d-d49e-451f-a91e-e39ceaf35875
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ff81b082c877098acec78e56ef9ef211cae8854
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51778144"
---
# <a name="how-to-debug-injected-code"></a>Como depurar código injetado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

OBSERVAÇÃO]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 Usar atributos pode simplificar muito a programação C++. Para obter mais informações, consulte [conceitos](http://msdn.microsoft.com/library/563e7e7c-65e1-44f4-b0b2-da04a6c1bc9e). Alguns atributos são interpretados diretamente pelo compilador. Outros atributos injetam o código na origem do programa, que o compilador em seguida compila. Este código injetado facilita a programação reduzindo a quantidade de códigos que você precisa escrever. Entretanto, às vezes, um bug pode causar falha no aplicativo ao executar o código injetado. Quando isso acontece, você provavelmente desejará examinar o código injetado. O Visual Studio fornece duas maneiras de ver o código injetado:  
  
- Você pode exibir o código injetado na **desmontagem** janela.  
  
- Usando o [/Fx](http://msdn.microsoft.com/library/14f0e301-3bab-45a3-bbdf-e7ce66f20560), você pode criar um arquivo de origem mesclada que contém o código original e injetado.  
  
  O **desmontagem** janela mostra instruções de linguagem de assembly que correspondem ao código-fonte e o código injetado por atributos. Além disso, o **desmontagem** janela pode mostrar a anotação do código-fonte.  
  
### <a name="to-turn-on-source-annotation"></a>Para ativar a anotação de origem  
  
-   Clique com botão direito do **desmontagem** janela e escolha **Mostrar código-fonte** no menu de atalho.  
  
     Se você souber o local de um atributo em uma janela de origem, você pode usar o menu de atalho para localizar o código injetado na **desmontagem** janela.  
  
### <a name="to-view-injected-code"></a>Para exibir o código injetado  
  
1.  O depurador deve estar no modo de interrupção.  
  
2.  Em uma janela do código-fonte, coloque o cursor na frente do atributo cujo código injetado você deseja exibir.  
  
3.  Clique com botão direito e selecione **ir para desmontagem** no menu de atalho.  
  
     Se o local do atributo estiver perto do ponto de execução atual, você pode selecionar o **desmontagem** janela a partir de **depurar** menu.  
  
### <a name="to-view-the-disassembly-code-at-the-current-execution-point"></a>Para exibir o código de desmontagem no ponto de execução atual  
  
1.  O depurador deve estar no modo de interrupção.  
  
2.  Dos **Debug** menu, escolha **Windows**e clique em **desmontagem**.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Depurando código nativo](../debugger/debugging-native-code.md)



