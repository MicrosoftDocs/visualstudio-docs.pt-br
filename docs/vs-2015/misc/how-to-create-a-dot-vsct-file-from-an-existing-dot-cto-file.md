---
title: 'Como: criar um. Arquivo VSCT de um existente. Arquivo CTO | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSCT files, creating based on a .cto file
ms.assetid: 847717c9-477d-4ac9-8b2c-2da878912478
caps.latest.revision: 11
manager: douge
ms.openlocfilehash: 82cf711d33b3b3ca5150378e7111a2a21c8c03cf
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49235736"
---
# <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>Como: criar um. Arquivo VSCT de um existente. Arquivo CTO
Você pode criar um arquivo. VSCT de baseado em XML de um arquivo binário CTO de já existente. Isso permite aproveitar o novo formato de compilador de tabela do comando. Esse processo funciona mesmo se o arquivo de CTO já foi compilado a partir de um arquivo. ctc. Você pode editar e compilar o arquivo. VSCT em outro arquivo CTO já.  
  
### <a name="to-create-a-vsct-file-from-a-cto-file"></a>Para criar um arquivo. VSCT de um arquivo CTO já  
  
1.  Obter cópias do arquivo CTO já e seu arquivo .ctsym correspondente.  
  
2.  Coloque os arquivos no mesmo diretório que o compilador vsct.exe.  
  
3.  No Visual Studio Prompt de comando, vá para o diretório que contém os arquivos CTO já e .ctsym.  
  
4.  Tipo de **vsct.exe** _ctofilename_**CTO já** _vsctfilename_**VSCT -S**  _symfilename_**.ctsym**.  
  
     `ctofilename` é o nome do arquivo CTO já `vsctfilename` é o nome do arquivo vsct para criar, e `symfilename` é o nome do arquivo .ctsym.  
  
     Esse processo cria um novo arquivo. VSCT XML comando tabela compilador. Você pode editar e compilar o arquivo com vsct.exe, o compilador vsct, como você faria com qualquer outro arquivo. VSCT.  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar um. Arquivo VSCT](../extensibility/internals/how-to-create-a-dot-vsct-file.md)   
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)