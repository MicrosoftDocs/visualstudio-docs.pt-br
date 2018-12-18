---
title: 'Como: gerenciar uma galeria privada usando configurações de registro | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2351c048576d6cf0e93515df8bdce34eef09bfc8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49854657"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>Como: gerenciar uma galeria privada usando configurações de registro
Se você for um administrador ou desenvolvedor de uma extensão de Shell isolado, você pode controlar o acesso para os controles, modelos e ferramentas na Galeria do Visual Studio, a Galeria de exemplos ou galerias privadas. Para criar uma galeria disponíveis ou não disponíveis, crie uma *pkgdef* arquivo que descreve as chaves do registro modificado e seus valores.  
  
## <a name="manage-private-galleries"></a>Gerenciar galerias privadas  
 Você pode criar uma *pkgdef* arquivo para controlar o acesso a galerias em vários computadores. Esse arquivo deve ter o formato a seguir.  
  
```  
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]  
@={URI}  (REG_SZ)  
Disabled=0 | 1 (DWORD)  
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)  
Protocol=Atom Feed|Sharepoint (REG_SZ)  
DisplayName={DisplayName} (REG_SZ)  
DisplayNameResourceID={ID} (REG_SZ)  
DisplayNamePackageGuid={GUID} (REG_SZ)  
  
```  
  
 O `Repositories` chave refere-se para a Galeria para ser habilitado ou desabilitado. Galeria do Visual Studio e a Galeria de exemplos usam GUIDs do repositório a seguir:  
  
- Galeria do Visual Studio: 0F45E408-7995-4375-9485-86B8DB553DC9  
  
- Galeria de exemplos: AEB9CB40-D8E6-4615-B52C-27E307F8506C  
  
  O `Disabled` valor é opcional. Por padrão, uma galeria está habilitada.  
  
  O `Priority` valor determina a ordem na qual as galerias são listadas em de **opções** caixa de diálogo. Galeria do Visual Studio tem prioridade 10 e a Galeria de exemplos tem prioridade 20. Galerias privadas começam em prioridade 100. Se várias galerias têm o mesmo valor de prioridade, a ordem na qual eles aparecem é determinada pelos valores de suas localizada `DisplayName` atributos.  
  
  O `Protocol` valor é necessário para galerias baseada no SharePoint ou Atom.  
  
  Tanto `DisplayName`, ou ambos `DisplayNameResourceID` e `DisplayNamePackageGuid`, deve ser especificado. Se todos estiverem especificados, o `DisplayNameResourceID` e `DisplayNamePackageGuid` par é usado.  
  
## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>Desabilitar a Galeria do Visual Studio usando um arquivo. pkgdef  
 Você pode desabilitar uma galeria em uma *pkgdef* arquivo. A entrada a seguir desabilita a Galeria do Visual Studio:  
  
```  
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]  
"Disabled"=dword:00000001  
  
```  
  
 A entrada a seguir desabilita a Galeria de exemplos:  
  
```  
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]  
"Disabled"=dword:00000001  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Galerias privadas](../extensibility/private-galleries.md)