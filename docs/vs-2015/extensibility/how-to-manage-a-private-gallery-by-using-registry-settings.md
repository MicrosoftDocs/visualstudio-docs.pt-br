---
title: 'Como: gerenciar uma galeria privada usando configurações de registro | Microsoft Docs'
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
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 371fea42e1e59907c08d0a7e51a56875c1b73537
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744452"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>Como: gerenciar uma galeria privada usando configurações do registro
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você for um administrador ou desenvolvedor de uma extensão de Shell isolado, você pode controlar o acesso para os controles, modelos e ferramentas na Galeria do Visual Studio, a Galeria de exemplos ou galerias privadas. Para tornar uma galeria disponíveis ou não disponíveis, crie um arquivo. pkgdef que descreve as chaves do registro modificado e seus valores.  
  
## <a name="managing-private-galleries"></a>Gerenciar galerias privadas  
 Você pode criar um arquivo. pkgdef para controlar o acesso a galerias em vários computadores. Esse arquivo deve ter o formato a seguir.  
  
```  
[$RootPath$\ExtensionManager\Repositories\{UniqueGUID}]  
@={URI}  (REG_SZ)  
Disabled=0 | 1 (DWORD)  
Priority=0 (highest priority) … MaxInt (lowest priority) (DWORD) (uint)  
Protocol=Atom Feed|Sharepoint (REG_SZ)  
DisplayName={DisplayName} (REG_SZ)  
DisplayNameResourceID={ID} (REG_SZ)  
DisplayNamePackageGuid={GUID} (REG_SZ)  
  
```  
  
 O `Repositories` chave refere-se para a Galeria para ser habilitado ou desabilitado. Galeria do Visual Studio e a Galeria de exemplos usam GUIDs do repositório a seguir:  
  
- Galeria do Visual Studio: 0F45E408-7995-4375-9485-86B8DB553DC9  
  
- Galeria de exemplos: AEB9CB40-D8E6-4615-B52C-27E307F8506C  
  
  O `Disabled` valor é opcional. Por padrão, uma galeria está habilitada.  
  
  O `Priority` valor determina a ordem na qual as galerias são listadas na caixa de diálogo Opções. Galeria do Visual Studio tem prioridade 10 e a Galeria de exemplos tem prioridade 20. Galerias privadas começam em prioridade 100. Se várias galerias têm o mesmo valor de prioridade, a ordem na qual eles aparecem é determinada pelos valores de suas localizada `DisplayName` atributos.  
  
  O `Protocol` valor é necessário para galerias baseada no SharePoint ou Atom.  
  
  Tanto `DisplayName`, ou ambos `DisplayNameResourceID` e `DisplayNamePackageGuid`, deve ser especificado. Se todos estiverem especificados, o `DisplayNameResourceID` e `DisplayNamePackageGuid` par é usado.  
  
## <a name="disabling-the-visual-studio-gallery-using-a-pkgdef-file"></a>Desabilitando a Galeria do Visual Studio usando um arquivo. pkgdef  
 Você pode desabilitar uma galeria em um arquivo. pkgdef. A entrada a seguir desabilita a Galeria do Visual Studio:  
  
```  
[$RootPath$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]  
"Disabled"=dword:00000001  
  
```  
  
 A entrada a seguir desabilita a Galeria de exemplos:  
  
```  
[$RootPath$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]  
"Disabled"=dword:00000001  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Galerias privadas](../extensibility/private-galleries.md)

