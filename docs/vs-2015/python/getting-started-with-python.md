---
title: Introdução ao Python | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-python
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33f4f6fb-0ae4-4234-9df2-531f2d3af17f
caps.latest.revision: 13
author: kraigb
ms.author: kraigb
manager: ghogen
ms.openlocfilehash: 5cb04bb01aaa6eb06c5e3c50aa13ab51c136678c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49275282"
---
# <a name="getting-started-with-python"></a>Introdução ao Python
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As ferramentas Python para Visual Studio (PTVS), é grátis, [livre](https://github.com/Microsoft/ptvs) plug-in para o Visual Studio que enfrentam um desenvolvimento avançado do Python.  
  
## <a name="python-the-language"></a>O idioma do Python
  
Python é uma linguagem de programação popular que é usada por muitas universidades, cientistas, os criadores de scripts do aplicativo, desenvolvedores casuais e desenvolvedores profissionais, trabalhando em aplicativos, sites e serviços de nuvem.

Como uma linguagem de programação Python é:
  
- Confiável.
- Geralmente é útil para programas rápidos de scripts, scripts de aplicativo, aplicativos da área de trabalho, servidores web, serviços web e computação científica.
- Fácil de aprender e tem um bom design para incentivar a boa codificação (muitas universidades usam-os para cursos introdutórios de programação).
- Flexível, suporte a estilos de programação imperativos, funcionais e orientada a objeto.
- Código-fonte aberto e gratuito.
- É executado bem em todos os principais sistemas operacionais.  
- Suporte para várias bibliotecas gratuitas, úteis e bem projetadas.  
- Compatível com muita documentação, exemplos e uma sólida comunidade de desenvolvedores.  

Para saber mais sobre a linguagem, comece com [Python para iniciantes](https://www.python.org/about/gettingstarted/) em python.org.

Para instalar o Python em si, visite [ https://www.python.org/download/ ](https://www.python.org/download/).
 
  
## <a name="python-tools-for-visual-studio"></a>Ferramentas Python para o Visual Studio
  
As ferramentas Python para Visual Studio, que pode ser instalado a partir [visualstudio.com](https://www.visualstudio.com/en-us/explore/python-vs), fornecem os seguintes recursos:  
  
- Suporte para vários intérpretes: várias versões de CPython, IronPython e IPython  
- Um sistema de projeto que seleciona implicitamente uma estrutura de pastas de código do Python e também permite controle explícito para que você possa identificar o código do aplicativo, código de teste, páginas da web, JavaScript, scripts de build e assim por diante.  
- Modelos de projeto para console, Web, Azure, ciência de dados e outros tipos de projetos.    
- O SDK do Azure para Python (veja abaixo)    
- Recursos de compreensão de código e edição avançada, incluindo coloração de sintaxe, preenchimento automático em todo o seu código e bibliotecas, ajuda com assinatura, modo de exibição de classe, Ir para Definição, Localizar Todas as Referências, refatoração e muito mais.    
- Uma Janela Interativa (REPL)
- IPython com visualizações de dados.
- Suporte para IronPython e .NET/WPF.    
- Depuração avançada sem um projeto do Visual Studio, a capacidade de depurar um executável existente, depuração de modo misto, depuração remota para Linux/Windows/Mac e depuração dentro da Janela Interativa.   
- Ferramentas de criação de perfil.  
- Ferramentas de teste.  
  
Os recursos a seguir o ajudarão a começar:

- [Guia de instalação](https://github.com/Microsoft/PTVS/wiki/PTVS-Installation)    
- [Introdução e vídeos de aprofundamento](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)  
- Instalação e demonstração de recursos (27 min)] (https://www.youtube.com/watch?v=JNNAOypc6Ek)  
- [Documentação](https://github.com/Microsoft/PTVS/wiki)  


Observe que o Visual Studio no momento fornece os meios para criar um executável autônomo usando o Python, que basicamente significa que um programa com um interpretador de Python incorporado. No entanto, há vários meios dentro da comunidade do Python para fazer isso, conforme descrito em [StackOverflow](http://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency). O CPython também dá suporte a ser inserido em um aplicativo nativo, conforme descrito na postagem do blog [Using CPython's Embeddable Zip File](https://blogs.msdn.microsoft.com/pythonengineering/2016/04/26/cpython-embeddable-zip-file/) (Usando o arquivo .zip que permite inserção do CPython).
  
## <a name="building-ui-with-python"></a>Construção da interface do usuário com o Python  

A oferta principal para criar uma interface do usuário com o Python é o [projeto Qt](https://www.qt.io/qt-for-application-development/), com associações de Python conhecidas como [PySide (a associação oficial)](http://wiki.qt.io/PySide) (Consulte também [downloads do PySide](https://download.qt.io/official_releases/pyside/.)) e [PyQt](https://wiki.python.org/moin/PyQt). No momento, o suporte do Python no Visual Studio não inclui quaisquer ferramentas específicas para desenvolvimento da interface do usuário.

## <a name="azure-sdk-for-python"></a>SDK do Azure para Python
  
O SDK do Azure para Python, que dá suporte a Windows, Mac e Linux, facilita o consumo e o gerenciamento de Serviços do Microsoft Azure. Consulte os recursos a seguir para obter detalhes: 

- Para instalar o SDK, use o [Índice de pacote Python](https://pypi.python.org/pypi/azure) ou siga [Instalar o Python e o SDK](https://azure.microsoft.com/documentation/articles/python-how-to-install/) na documentação do Azure. 
- A [Central de desenvolvedores do SDK do Azure para Python](https://azure.microsoft.com/develop/python/) tem muita ajuda, da instalação à documentação, com tutoriais.  Veja alguns destaques:  
- Guias de instruções:
  - [Armazenamento de blob](https://azure.microsoft.com/develop/python/how-to-guides/blob-service/)  
  - [Fila de armazenamento](https://azure.microsoft.com/develop/python/how-to-guides/queue-service/)  
  - [Tabela de página](https://azure.microsoft.com/develop/python/how-to-guides/table-service/)  
  - [Filas do Barramento de Serviço](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-queues/)
  - [Tópicos/assinaturas do Barramento de Serviço](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-topics/) 
  - [Gerenciamento de serviços](https://azure.microsoft.com/develop/python/how-to-guides/service-management/)  

## <a name="scientific-computing"></a>Computação científica

Além de todas as bibliotecas de cientistas de dados do Python, as Ferramentas Python para Visual Studio dão suporte a IPython e IPython Notebooks, que podem ser hospedados no Azure.

É recomendável obter bibliotecas do IPython e de computação científica (matplotlib, scipy, numpy etc.) da [Universidade da Califórnia, Irvine](http://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy-stack).  
  
## <a name="see-also"></a>Consulte também  

[Introdução ao PTVS: instalando o Visual Studio](../python/getting-started-with-ptvs-setting-up-visual-studio.md)
[Introdução ao PTVS: iniciar a codificação (projetos)](../python/getting-started-with-ptvs-start-coding-projects.md)
[Introdução ao PTVS: editando código](../python/getting-started-with-ptvs-editing-code.md)
[Introdução ao PTVS: depurando](../python/getting-started-with-ptvs-debugging.md)
[Introdução ao PTVS: Python interativo](../python/getting-started-with-ptvs-interactive-python.md)
[Introdução ao PTVS: compilando um site no Azure](../python/getting-started-with-ptvs-building-a-website-in-azure.md)

