---
title: '&lt;fileAssociation&gt; elemento (aplicativo ClickOnce) | Microsoft Docs'
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
- <fileAssociation> element [ClickOnce application manifest]
- manifests [ClickOnce], fileAssociation element
ms.assetid: 8f951b4f-54f9-412e-a9e5-af4e379fcf08
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: e827f0829cfe0436f491196b7f1dab99ac87c4fc
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49234449"
---
# <a name="ltfileassociationgt-element-clickonce-application"></a>&lt;fileAssociation&gt; elemento (aplicativo ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Identifica uma extensão de arquivo a ser associado com o aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<fileAssociation  
    xmlns="urn:schemas-microsoft-com:clickonce.v1"  
    extension  
    description  
    progid  
    defaultIcon  
/>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O elemento `fileAssociation` é opcional. O elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`extension`|Necessário. A extensão de arquivo a ser associado com o aplicativo.|  
|`description`|Necessário. Uma descrição do tipo de arquivo para uso pelo shell.|  
|`progid`|Necessário. Um nome que identifica exclusivamente o tipo de arquivo.|  
|`defaultIcon`|Necessário. Especifica o ícone a ser usado para arquivos com essa extensão. O arquivo de ícone deve ser especificado usando o [ \<arquivo > elemento](../deployment/file-element-clickonce-application.md) dentro de [ \<assembly > elemento](../deployment/assembly-element-clickonce-application.md) que contém esse elemento.|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento deve incluir uma referência ao namespace XML para "urn: schemas-microsoft-com:clickonce.v1". Se o `<fileAssociation>` elemento é usado, ele deve vir após o `<application>` elemento em seu pai [ \<assembly > elemento](../deployment/assembly-element-clickonce-application.md).  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] não substituirá as associações de arquivo existente. No entanto, um aplicativo ClickOnce pode substituir a extensão de arquivo para o usuário atual. Após a desinstalação do aplicativo ClickOnce, ClickOnce exclui a associação de arquivo para o usuário e a associação de por máquina está ativa novamente.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra `fileAssociation` elementos em um aplicativo de manifesto para um aplicativo de editor de texto implantado usando [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. Este exemplo de código também inclui o [ \<arquivo > elemento](../deployment/file-element-clickonce-application.md) exigido pelo `defaultIcon` atributo.  
  
```  
<file name="text.ico" size="4286">  
  <hash>  
    <dsig:Transforms>  
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
    </dsig:Transforms>  
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
    <dsig:DigestValue>0joAqhmfeBb93ZneZv/oTMP2brY=</dsig:DigestValue>  
  </hash>  
</file>  
<file name="writing.ico" size="9662">  
  <hash>  
    <dsig:Transforms>  
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
    </dsig:Transforms>  
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
    <dsig:DigestValue>2cL2U7cm13nG40v9MQdxYKazIwI=</dsig:DigestValue>  
  </hash>  
</file>  
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".text" description="Text  Document (ClickOnce)" progid="Text.Document" defaultIcon="text.ico" />  
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".writing" description="Writings (ClickOnce)" progid="Writing.Document" defaultIcon="writing.ico" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto de aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)



