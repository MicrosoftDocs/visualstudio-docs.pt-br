---
title: 'Como: definir um local de arquivo de Log personalizado para erros de implantação do ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- ClickOnce deployment, error logging
ms.assetid: 77424414-7f0e-4b99-94bb-ea130de92d09
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: e4108287e120eabb4c8fc38d1dc29f2a81ea3d47
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49207695"
---
# <a name="how-to-set-a-custom-log-file-location-for-clickonce-deployment-errors"></a>Como definir o local de um arquivo de log personalizado para erros de implantação do ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] mantém os arquivos de log de ativação para todas as implantações. Esses logs documente todos os erros relacionados à instalação e inicializando uma [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação. Por padrão, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] cria um arquivo de log para cada ativação de implantação. Ele armazena esses arquivos de log na pasta Temporary Internet Files. O arquivo de log para uma implantação é exibido ao usuário quando ocorrer uma falha de ativação, e o usuário clica **detalhes** na caixa de diálogo de erro resultante.  
  
 Você pode alterar esse comportamento para um cliente específico usando o Editor do registro (**regedit.exe**) para definir um caminho de arquivo de log personalizado. Nesse caso, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] registra êxitos de ativação e falhas para todas as implantações em um único arquivo.  
  
> [!CAUTION]
>  Se você usar o Editor do Registro incorretamente, poderá causar sérios problemas que talvez exijam a reinstalação do sistema operacional. Use o Editor do registro por seu próprio risco.  
  
> [!NOTE]
>  Você precisará Trunque ou exclua o arquivo de log, ocasionalmente, para impedir que ele fique muito grande.  
  
 O procedimento a seguir descreve como definir um local de arquivo de log personalizado para um único cliente.  
  
### <a name="to-set-a-custom-log-file-location"></a>Para definir um local de arquivo de log personalizado  
  
1.  Abra **Regedit.exe**.  
  
2.  Navegue até o nó `HKCU\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment`.  
  
3.  Defina o valor de cadeia de caracteres `LogFilePath` para o caminho completo e nome de arquivo do seu local preferido de log personalizado.  
  
     Esse local deve estar em um diretório ao qual o usuário tem acesso de gravação. Por exemplo, no Windows Vista, crie a seguinte estrutura de pasta e defina `LogFilePath` até C:\Users\\< nome de usuário\>\Documents\Logs\ClickOnce\installation.log.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas de implantações ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)





