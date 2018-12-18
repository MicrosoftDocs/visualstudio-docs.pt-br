---
title: 'Introdução ao PTVS: iniciar a codificação (projetos) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-python
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 14b85e70-b9a8-415c-a307-8c8c316a0495
caps.latest.revision: 7
author: kraigb
ms.author: kraigb
manager: ghogen
ms.openlocfilehash: a8e0bd339d8e7b6d145cc9a916dafc2be9fc975e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49845778"
---
# <a name="getting-started-with-ptvs-start-coding-projects"></a>Introdução ao PTVS: iniciar a codificação (projetos)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As PTVS (Ferramentas Python para Visual Studio) ajudam você a gerenciar seu código. 
 
 É possível assistir a essas instruções em um breve [vídeo no YouTube](https://www.youtube.com/watch?v=KHPoVpL7zHg&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=2). 
 
 Se já tiver usado o Python antes, você sabe que seu projeto é definido pela forma como você dispões seus arquivos em disco. Isso funciona muito bem para projetos de Python simples, mas quando você tiver mais arquivos (páginas da Web com JavaScript, testes de unidade e scripts de build), os sistemas de arquivos podem começar a ficar um pouco limitantes. O Visual Studio usa projetos para fazer três coisas. 
 
- Identificar arquivos críticos. Arquivos importantes são aqueles que você incorpora a um sistema de controle de versão (arquivos de origem, recursos etc.), mas não arquivos que são gerados como saída do build. Arquivos importantes também são aqueles que você pode copiar para outro computador para que outra pessoa possa trabalhar em seu aplicativo. 
 
- Especificar como os arquivos devem ser usados. Você pode ter arquivos que uma ferramenta precisa processar sempre que os arquivos forem alterados. Projetos do Visual Studio podem capturar essas informações 
 
- Definir os limites de seus componentes. Se tiver vários componentes em seu aplicativo, você pode colocar cada um em um projeto separado. Eles podem, eventualmente, ser implantados em servidores diferentes, compilados com diferentes configurações de depuração ou build ou podem até mesmo ser escritos usando outra linguagem com suporte do Visual Studio, como C++ ou Node. js 
 
  Existem vários modelos de projeto para ajudá-lo a começar. Se você já tiver um código Python no qual gostaria de trabalhar, o assistente de código "De um Existente" o ajudará a criar um projeto que inclui todos os arquivos. Existem vários projetos Web para algumas estruturas populares. Mais modelos que estão disponíveis no pacote de amostras das PTVS. Há opções para fazer com que os modelos Web fornecidos funcionem com outras estruturas. O modelo Python Application é um projeto limpo e vazio. Há um módulo para você começar. 
 
  O Visual Studio mostra seus projetos abertos na janela do Gerenciador de Soluções, incluindo todos os arquivos, caminhos de pesquisa e ambientes Python. Para adicionar novos itens, selecione a pasta do projeto e, no menu de contexto (pressione o botão do ponteiro à direita), escolha Adicionar e, em seguida, Novo Item. É possível selecionar qualquer item na caixa de diálogo, personalizar o nome do item e adicionar o item ao projeto. 
 
  É possível arrastar e soltar no Gerenciador de Soluções. Se já tiver copiado arquivos para sua estrutura de diretórios do projeto, você pode selecionar Mostrar Todos os Arquivos na parte superior do Gerenciador de Soluções. Em seguida, você pode selecionar os itens que deseja adicionar e, no menu de contexto, escolher Incluir no Projeto. 
 
  É possível assistir a essas instruções em um breve [vídeo no YouTube](https://www.youtube.com/watch?v=KHPoVpL7zHg&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=2). 
 
## <a name="see-also"></a>Consulte também 
 [Documentação do wiki](https://github.com/Microsoft/PTVS/wiki/Projects) [Introdução ao PTVS e vídeos de aprofundamento](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)

