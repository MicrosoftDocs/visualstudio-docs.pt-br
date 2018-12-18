---
title: Caixa de diálogo de páginas de propriedade do código-fonte arquivos, propriedades comuns, solução de depuração | Microsoft Docs
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
- vs.debug.options.FindSource
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- VB
- CSharp
- C++
helpviewer_keywords:
- Debug Source Files property page
- debugging [Visual Studio], specifying source and symbol files
- source files, specifying in debugger
- debugger, source files
ms.assetid: 0af11464-eeb1-4d0b-87a6-0cc96779afb1
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 84bf975065d73cd2d25994855a4c8a236f706e3b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744674"
---
# <a name="debug-source-files-common-properties-solution-property-pages-dialog-box"></a>Caixa de diálogo Depurar Arquivos de Origem, Propriedades Comuns, Páginas de Propriedades da Solução
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta página de propriedades especifica onde o depurador procurará arquivos de origem ao depurar a solução.  
  
 Para acessar o **depurar arquivos fonte** página de propriedades, o botão direito do mouse na solução em **Gerenciador de soluções** e selecione **propriedades** no menu de atalho. Expanda o **propriedades comuns** pasta e clique no **depurar arquivos fonte** página.  
  
 **Diretórios que contêm o código-fonte**  
 Contém uma lista de diretórios nos quais o depurador procura arquivos de origem ao depurar a solução. Os subdiretórios dos diretórios especificados também são pesquisados.  
  
 **Não procure esses arquivos de origem**  
 Insira os nomes de todos os arquivos que você não deseja que o depurador leia. Se o depurador encontrar um desses arquivos em um dos diretórios especificados acima, ele o ignorará. Se o **Localizar origem** caixa de diálogo aparece durante a depuração, e você clicar em **Cancelar**, o arquivo que você estava procurando é adicionado a essa lista para que o depurador não continuará a procurar o arquivo.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)



