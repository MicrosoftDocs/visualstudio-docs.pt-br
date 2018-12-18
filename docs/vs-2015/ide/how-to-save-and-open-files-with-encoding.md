---
title: Como salvar e abrir arquivos com codificação | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Unicode, bi-directional language support
- files, encoding
- bi-directional language support, encoded files
- file encoding, bi-directional languages
ms.assetid: cb52b732-b395-4ba1-a3ef-104b3942a12a
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b179637d9607db70aac415abd477da4a62852efe
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49213779"
---
# <a name="how-to-save-and-open-files-with-encoding"></a>Como salvar e abrir arquivos com codificação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível salvar arquivos com uma codificação de caracteres específica para dar suporte a idiomas bidirecionais. Também é possível especificar uma codificação ao abrir um arquivo, para que o Visual Studio exiba o arquivo corretamente.  
  
### <a name="to-save-a-file-with-encoding"></a>Para salvar um arquivo com codificação  
  
1.  No menu **Arquivo**, escolha **Salvar Arquivo Como** e clique no botão suspenso ao lado do botão **Salvar**.  
  
     A caixa de diálogo **Opções de Salvamento Avançadas** é exibida.  
  
2.  Em **Codificação**, selecione a codificação a ser usada para o arquivo.  
  
3.  Opcionalmente, em **Terminações de linha**, selecione o formato para caracteres de final de linha.  
  
     Essa opção é útil se você pretende trocar o arquivo com usuários de outro sistema operacional.  
  
     Se deseja trabalhar com um arquivo que você sabe que está codificado de uma maneira específica, é possível informar ao Visual Studio para usar essa codificação ao abrir o arquivo. O método usado dependerá se o arquivo faz parte do projeto.  
  
### <a name="to-open-an-encoded-file-that-is-part-of-a-project"></a>Para abrir um arquivo codificado que faz parte de um projeto  
  
1.  Em **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo e escolha **Abrir Com**.  
  
2.  Na caixa de diálogo **Abrir Com**, escolha o editor com o qual o arquivo será aberto.  
  
     Muitos editores do Visual Studio, como o editor de formulários, detectarão a codificação automaticamente e abrirão o arquivo de forma adequada. Se você escolher um editor que permite escolher uma codificação, a caixa de diálogo **Codificação** será exibida.  
  
3.  Na caixa de diálogo **Codificação**, selecione a codificação que o editor deverá usar.  
  
### <a name="to-open-an-encoded-file-that-is-not-part-of-a-project"></a>Para abrir um arquivo codificado que não faz parte de um projeto  
  
1.  No menu **Arquivo**, aponte para **Abrir**, escolha **Arquivo** ou **Arquivo da Web** e, em seguida, selecione o arquivo a ser aberto.  
  
2.  Clique no botão suspenso ao lado do botão **Abrir** e escolha **Abrir Com**.  
  
3.  Siga as Etapas 2 e 3 do procedimento anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Codificação e globalização do Windows Forms](http://msdn.microsoft.com/library/22e8965d-a712-42b3-8167-3ee346bd70f9)   
 [Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)

