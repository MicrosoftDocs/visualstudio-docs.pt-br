---
title: 'Como: Incluir um arquivo de dados em um aplicativo ClickOnce | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- deploying applications [ClickOnce], data files
- data access, ClickOnce applications
ms.assetid: 89ee46ef-bc8c-4ab0-a2ac-1220f9da06fc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 673b22dfbde5497f6be7b24bf04773f6cddf4a01
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54999659"
---
# <a name="how-to-include-a-data-file-in-a-clickonce-application"></a>Como: Incluir um arquivo de dados em um aplicativo ClickOnce
Cada [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] instalação de aplicativo é atribuído a um diretório de dados no disco local do computador de destino, onde o aplicativo pode gerenciar seus próprios dados. Arquivos de dados podem incluir arquivos de qualquer tipo: arquivos de texto, arquivos XML ou até mesmo banco de dados do Microsoft Access (*. mdb*) arquivos. Os procedimentos a seguir mostram como adicionar um arquivo de dados de qualquer tipo em seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo.  
  
### <a name="to-include-a-data-file-by-using-mageexe"></a>Para incluir um arquivo de dados usando Mage.exe  
  
1. Adicione o arquivo de dados ao seu diretório de aplicativo com o restante dos arquivos do seu aplicativo.  
  
    Normalmente, o diretório de seu aplicativo será um diretório rotulado com a versão atual da implantação — por exemplo, v1.0.0.0.  
  
2. Atualize o manifesto do aplicativo para o arquivo de dados de lista.  
  
    `mage -u v1.0.0.0\Application.manifest -FromDirectory v1.0.0.0`  
  
    Executar esta tarefa cria novamente a lista de arquivos no manifesto do aplicativo e também gera automaticamente as assinaturas de hash.  
  
3. Abra o manifesto do aplicativo em seu texto preferido ou editor XML e localize o `file` elemento para o arquivo adicionado recentemente.  
  
    Se você tiver adicionado um arquivo XML denominado `Data.xml`, o arquivo será semelhante ao exemplo de código a seguir.  
  
   `<file name="Data.xml" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`  
  
4. Adicione o atributo `type` a esse elemento e fornecê-lo com um valor de `data`.  
  
   `<file name="Data.xml" writeableType="applicationData" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`  
  
5. Assinar novamente o manifesto do aplicativo usando o par de chaves ou certificado e assinar novamente o manifesto de implantação.  
  
    Você deve reassinar o manifesto de implantação porque seu hash do manifesto do aplicativo foi alterado.  
  
    `mage -s app manifest -cf cert_file -pwd password`
  
    `mage -u deployment manifest -appm app manifest`
  
    `mage -s deployment manifest -cf certfile -pwd password`
  
### <a name="to-include-a-data-file-by-using-mageuiexe"></a>Para incluir um arquivo de dados usando MageUI.exe  
  
1.  Adicione o arquivo de dados ao seu diretório de aplicativo com o restante dos arquivos do seu aplicativo.  
  
2.  Normalmente, o diretório de seu aplicativo será um diretório rotulado com a versão atual da implantação — por exemplo, v1.0.0.0.  
  
3.  Sobre o **arquivo** menu, clique em **abrir** para abrir o manifesto do aplicativo.  
  
4.  Selecione o **arquivos** guia.  
  
5.  Na caixa de texto na parte superior da guia, insira o diretório que contém os arquivos do aplicativo e, em seguida, clique em **popular**.  
  
     O arquivo de dados será exibida na grade.  
  
6.  Defina as **tipo de arquivo** o valor do arquivo de dados para **dados**.  
  
7.  Salve o manifesto do aplicativo e, em seguida, assinar novamente o arquivo.  
  
     *MageUI.exe* solicitará que você assine novamente o arquivo.  
  
8.  Assinar novamente o manifesto de implantação  
  
     Você deve reassinar o manifesto de implantação porque seu hash do manifesto do aplicativo foi alterado.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a dados locais e remotos em aplicativos ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)