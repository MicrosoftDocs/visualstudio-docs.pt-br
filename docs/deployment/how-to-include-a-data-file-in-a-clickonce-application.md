---
title: Como incluir um arquivo de dados em um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 7630d1b363afa7caeae361f607f4b73929fbba1b
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382400"
---
# <a name="how-to-include-a-data-file-in-a-clickonce-application"></a>Como incluir um arquivo de dados em um aplicativo ClickOnce
Cada [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo que você instala recebe um diretório de dados no disco local do computador de destino onde o aplicativo pode gerenciar seus próprios dados. Os arquivos de dados podem incluir arquivos de qualquer tipo: Arquivos de texto, arquivos XML ou até mesmo arquivos de banco de dados do Microsoft Access (*. mdb*). Os procedimentos a seguir mostram como adicionar um arquivo de dados de qualquer tipo em seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo.

### <a name="to-include-a-data-file-by-using-mageexe"></a>Para incluir um arquivo de dados usando Mage.exe

1. Adicione o arquivo de dados ao diretório do aplicativo com o restante dos arquivos do aplicativo.

    Normalmente, o diretório do aplicativo será um diretório rotulado com a versão atual da implantação — por exemplo, v 1.0.0.0.

2. Atualize o manifesto do aplicativo para listar o arquivo de dados.

    `mage -u v1.0.0.0\Application.manifest -FromDirectory v1.0.0.0`

    Executar essa tarefa recria a lista de arquivos no manifesto do aplicativo e também gera automaticamente as assinaturas de hash.

3. Abra o manifesto do aplicativo no seu editor de XML ou texto preferido e localize o `file` elemento para o arquivo adicionado recentemente.

    Se você adicionou um arquivo XML chamado `Data.xml` , o arquivo será semelhante ao exemplo de código a seguir.

   `<file name="Data.xml" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

4. Adicione o atributo `type` a esse elemento e forneça-o com um valor de `data` .

   `<file name="Data.xml" writeableType="applicationData" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

5. Assine novamente o manifesto do aplicativo usando seu par de chaves ou certificado e, em seguida, assine novamente o manifesto de implantação.

    Você deve assinar novamente o manifesto de implantação porque seu hash do manifesto do aplicativo foi alterado.

    `mage -s app manifest -cf cert_file -pwd password`

    `mage -u deployment manifest -appm app manifest`

    `mage -s deployment manifest -cf certfile -pwd password`

### <a name="to-include-a-data-file-by-using-mageuiexe"></a>Para incluir um arquivo de dados usando MageUI.exe

1. Adicione o arquivo de dados ao diretório do aplicativo com o restante dos arquivos do aplicativo.

2. Normalmente, o diretório do aplicativo será um diretório rotulado com a versão atual da implantação — por exemplo, v 1.0.0.0.

3. No menu **arquivo** , clique em **abrir** para abrir o manifesto do aplicativo.

4. Selecione a guia **arquivos** .

5. Na caixa de texto na parte superior da guia, insira o diretório que contém os arquivos do aplicativo e clique em **popular**.

     O arquivo de dados aparecerá na grade.

6. Defina o valor do **tipo de arquivo** do arquivo de dados para **dados**.

7. Salve o manifesto do aplicativo e, em seguida, assine novamente o arquivo.

     *MageUI.exe* solicitará que você assine novamente o arquivo.

8. Assinar novamente seu manifesto de implantação

     Você deve assinar novamente o manifesto de implantação porque seu hash do manifesto do aplicativo foi alterado.

## <a name="see-also"></a>Veja também
- [Acesso a dados locais e remotos em aplicativos ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)