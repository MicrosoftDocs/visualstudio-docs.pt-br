---
title: Como exportar uma textura que tenha Alfa pré-multiplicado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 05348afa-f079-4f53-a05b-ecd91d13adab
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: a68f6c58ad7e497dfc0e91e92f2cf40e4bd8d992
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49897521"
---
# <a name="how-to-export-a-texture-that-has-premultiplied-alpha"></a>Como exportar uma textura que tenha Alfa pré-multiplicado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Pipeline de conteúdo de imagem pode gerar texturas alfa pré-multiplicadas de uma imagem de origem. Eles podem ser mais simples de usar e mais robustos do que texturas que não contêm alfa pré-multiplicado.  
  
 Este documento demonstra essas atividades:  
  
-   Configurando a imagem de origem a ser processada pelo Pipeline de conteúdo da imagem.  
  
-   Configurando o Pipeline de conteúdo de imagem para gerar alfa pré-multiplicado.  
  
## <a name="premultiplied-alpha"></a>Alfa pré-multiplicado  
 Alfa pré-multiplicado oferece diversas vantagens em relação a alfa convencional, alfa não pré-multiplicado, porque ele representa mais bem a interação do mundo real da luz com materiais físicos, separando a contribuição de cor de texel (a cor que ele adiciona à cena) de sua transparência (a quantidade de cor de fundo que pode passar). Algumas das vantagens de usar alfa pré-multiplicado são:  
  
-   A combinação com alfa pré-multiplicado é uma operação de associação; o resultado da combinação de várias texturas translúcidas é o mesmo, independentemente da ordem na qual as texturas são mescladas.  
  
-   Devido à natureza associativa de combinação com alfa pré-multiplicado, a renderização multipassagem de objetos translúcidos é simplificada.  
  
-   Ao usar alfa pré-multiplicado, tanto a combinação aditiva pura (pela configuração de alfa para zero) quanto a combinação interpoladas linearmente podem ser obtidas simultaneamente. Por exemplo, em um sistema de partículas, uma partícula de fogo combinada de maneira aditiva pode se tornar uma partícula de fumaça translúcida que é combinada por meio da interpolação linear. Sem alfa pré-multiplicado, você precisa extrair as partículas de fogo separadamente das partículas de fumaça e modificar o estado de renderização entre chamadas de retirada.  
  
-   Texturas que usam alfa pré-multiplicada comprimem com qualidade mais alta que aquelas que não usam e elas não exibem as bordas descoloridas — ou "efeito de halo" — que podem ocorrer quando você combina texturas que não usam alfa pré-multiplicado.  
  
#### <a name="to-create-a-texture-that-uses-premultiplied-alpha"></a>Como criar uma textura que usa alfa pré-multiplicado  
  
1. Comece com uma textura básica. Carregue um arquivo de imagem existente ou crie um conforme descrito em [Como criar uma textura básica](../designers/how-to-create-a-basic-texture.md).  
  
2. Configure o arquivo de textura para que ele seja processado pelo Pipeline de conteúdo de imagem. No **Gerenciador de Soluções**, abra o menu de atalho do arquivo de textura e escolha **Propriedades**. Na página **Propriedades de Configuração**, **Geral**, defina a propriedade **Tipo de Item** como **Pipeline de Conteúdo de Imagem**. Verifique se a propriedade **Conteúdo** está definida como **Sim** e se **Excluir do Build** está definido como **Não** e, em seguida, escolha o botão **Aplicar**. A página de propriedades de configuração **Pipeline de Conteúdo de Imagem** é exibida.  
  
3. Configure o Pipeline de conteúdo de imagem para gerar alfa pré-multiplicado. Na página **Propriedades de Configuração**, **Pipeline de Conteúdo de Imagem**, **geral**, defina a propriedade **Converter para formato alfa pré-multiplicado** como **Sim (/ generatepremultipliedalpha)**.  
  
4. Escolha o botão **OK**.  
  
   Quando você compila o projeto, o Pipeline de conteúdo de imagem converte a imagem de origem do formato de trabalho para o formato de saída que você especificou, incluindo a conversão da imagem para o formato alfa pré-multiplicado e o resultado é copiado para o diretório de saída do projeto.



