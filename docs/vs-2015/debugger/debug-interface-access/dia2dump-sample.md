---
title: Exemplo de Dia2dump | Microsoft Docs
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
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 727d7a4a97bc0aa55d370a45549941ab286930f9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805392"
---
# <a name="dia2dump-sample"></a>Exemplo de Dia2dump
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O exemplo de Dia2dump é instalado com o Visual Studio e contém a função de origem dia2dump.cpp. O executável compilado é executado da linha de comando e exibe o conteúdo de um arquivo de banco de dados (. PDB) do programa inteiro.  
  
### <a name="to-install-the-sample"></a>Para instalar o exemplo  
  
1.  Verifique se o seu sistema atende a todos os requisitos de instalação descritos a página inicial de instalação do Visual Studio.  
  
2.  Instalar o Visual Studio e siga todas as instruções de instalação e configuração para os exemplos incluídos.  
  
#### <a name="to-build-the-sample"></a>Para criar o exemplo  
  
1.  Abra o arquivo Dia2dump.sln no Visual Studio. (Se necessário, o Visual Studio pela primeira vez ajudará você atualizar o projeto Dia2dump.)  
  
2.  Nas páginas de propriedade do projeto, nos **C/C++** &#124; **geral** &#124; **diretórios de inclusão adicionais** propriedade, especifique o `..\DIA SDK\include` directory. Isso garante que o compilador pode localizar o arquivo de dia2.h.  
  
3.  Sobre o **construir** menu, clique em **recompilar solução**.  
  
4.  Feche o Visual Studio.  
  
#### <a name="to-run-the-sample"></a>Para executar a amostra  
  
1.  Abra um prompt de comando e digite o seguinte:  
  
    ```  
    dia2dump filename  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Origem Dia2dump.cpp](../../debugger/debug-interface-access/dia2dump-cpp-source-file.md)   
 [Como solucionar problemas de atualizações de projeto do Visual Studio malsucedidas](../../porting/how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades.md)



