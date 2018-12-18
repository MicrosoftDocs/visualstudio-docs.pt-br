---
title: 'Como: criar um. Arquivo VSCT de um existente. Arquivos CTC | Microsoft Docs'
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
- VSCT files, creating based on a .ctc file
ms.assetid: 700e80a4-c1e1-4178-af53-45e86dd2c08b
caps.latest.revision: 9
manager: douge
ms.openlocfilehash: e159fea34dc395ce2d7bded813f2d8feaa453006
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49303479"
---
# <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>Como: criar um. Arquivo VSCT de um existente. Arquivos CTC
Você pode criar um arquivo. VSCT de baseado em XML de um arquivo de código-fonte do comando tabela. ctc existente. Ao fazer isso, você pode tirar proveito do novo com base em XML [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] formato de compilador de tabela (VSCT) do comando.  
  
### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>Para criar um arquivo. VSCT de um arquivo. ctc  
  
1.  Obtenha uma cópia da linguagem Perl.  
  
2.  Obter uma cópia do script Perl ConvertCTCToVSCT.pl, geralmente localizada na  *\<caminho de instalação do SDK do Visual Studio >* \VisualStudioIntegration\Tools\bin pasta.  
  
3.  Obtenha uma cópia do arquivo de origem. ctc que você deseja converter.  
  
4.  Coloque os arquivos no mesmo diretório.  
  
5.  No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela de Prompt de comando, navegue até o diretório.  
  
6.  Tipo  
  
    ```  
    perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct  
    ```  
  
     onde PkgCmd.ctc é o nome do arquivo. ctc e PkgCmd.vsct é o nome do arquivo. VSCT que você deseja criar.  
  
     Isso cria um novo arquivo. VSCT XML comando tabela fonte. Você pode compilar o arquivo usando Vsct.exe, o compilador VSCT, como você faria com qualquer outro arquivo. VSCT.  
  
    > [!NOTE]
    >  Você pode melhorar a legibilidade do arquivo. VSCT, reformatar os comentários XML.  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar um. Arquivo VSCT](../extensibility/internals/how-to-create-a-dot-vsct-file.md)   
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)