---
title: Modificar o Shell isolado usando o. Arquivo Pkgundef | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .pkgundef file
ms.assetid: 9cee2a20-f8ac-4d9d-aef9-068fcd9f27a4
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2266eda9b3e50d85131148d708a934835340f074
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51802688"
---
# <a name="modifying-the-isolated-shell-by-using-the-pkgundef-file"></a>Modificar o Shell isolado usando o. Arquivo Pkgundef
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode modificar o arquivo. pkgundef para excluir as entradas do Registro especificada de um aplicativo de shell isolado. Normalmente, a primeira vez que um aplicativo é iniciado em um computador, o shell do Visual Studio copia as entradas de registro existentes do Visual Studio para a chave do registro raiz para o aplicativo. Isso inclui todas as referências a VSPackages atualmente instalados.  
  
 Para excluir uma entrada de registro específica de um aplicativo de shell isolado, adicione a chave do pacote seguida pela entrada do arquivo de. pkgundef do aplicativo. As chaves e as entradas são representadas assim como no arquivo. pkgdef; ou seja, como [$RootKey$] ou [$ $RootKey\\*subchave*] e "*entrada*" =*valor*, em que *subchave* é a subchave para afetar, *entrada* é a entrada a ser removida, e *valor* seja `""` ou `dword:00000000`.  
  
 Para excluir várias entradas de uma chave do registro, simplesmente liste a chave de uma vez, seguido por uma linha para cada entrada a ser excluído.  
  
 Para excluir uma chave de todo o registro de um aplicativo de shell isolado, adicione a chave para o arquivo. pkgundef de aplicativo, mas não especificar as entradas de registro para essa chave.  
  
 Você pode adicionar comentários ao arquivo. pkgundef. Um comentário de linha única deve ter duas barras "/" como os dois primeiros caracteres.  
  
 Por exemplo, para remover o **conectar-se ao banco de dados** e **conectar ao r Serve** os comandos no **ferramentas** menu, você pode remover o comentário da linha:  
  
```  
[$RootKey$\Packages\{8D8529D3-625D-4496-8354-3DAD630ECC1B}]  
```  
  
 e adicione a linha:  
  
```  
[$RootKey$\Packages\{198E76C1-34C0-424D-9957-B3EBD80265FB}]  
```  
  
 para o arquivo do aplicativo. pkgundef.  
  
## <a name="see-also"></a>Consulte também  
 [GUIDs de pacote de recursos do Visual Studio](../extensibility/package-guids-of-visual-studio-features.md)   
 [Personalizar o Shell isolado](../extensibility/customizing-the-isolated-shell.md)

