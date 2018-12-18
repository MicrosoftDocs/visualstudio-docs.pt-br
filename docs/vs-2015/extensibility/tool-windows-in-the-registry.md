---
title: Ferramenta do Windows no registro | Microsoft Docs
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
- tool windows, registering
ms.assetid: c4bb8add-7148-49e4-a377-01d059fd5524
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f24c51b3cf1a4930fa0cc496e12ffd31170389b0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781901"
---
# <a name="tool-windows-in-the-registry"></a>Ferramenta Windows no registro
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os VSPackages que fornecem as janelas de ferramentas deve registrar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] como provedores de janela de ferramentas. Janelas de ferramentas criadas usando o modelo de pacote do Visual Studio fazer isso por padrão. Provedores de janela de ferramenta têm chaves de registro do sistema que especifica os atributos de visibilidade, como tamanho de janela de ferramenta padrão e o local, o GUID da janela que serve como o painel de janela de ferramentas e o estilo de encaixe.  
  
 Durante o desenvolvimento, provedores de janela de ferramenta gerenciado registrar janelas de ferramentas adicionando atributos no código-fonte, e em seguida, executando o utilitário RegPkg.exe o assembly resultante. Para obter mais informações, consulte [registrando uma janela de ferramentas](../extensibility/registering-a-tool-window.md).  
  
## <a name="registering-unmanaged-tool-window-providers"></a>Registrando provedores de janela de ferramenta não gerenciado  
 Provedores de janela de ferramenta não gerenciado devem registrar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] na seção Windows 2000ferramenta de registro do sistema. O fragmento de arquivo. reg a seguir mostra como uma janela de ferramenta dinâmica pode ser registrada:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\<version number>\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}]  
@="{01069cdd-95ce-4620-ac21-ddff6c57f012}"  
"Name"="Microsoft.Samples.VisualStudio.IDE.ToolWindow.DynamicWindowPane"  
"Float"="250, 250, 410, 430"  
"DontForceCreate"=dword:00000001  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}\Visibility]  
"{f1536ef8-92ec-443c-9ed7-fdadf150da82}"=dword:00000000  
```  
  
 Na primeira chave no exemplo acima, o número de versão é a versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], tais como 7.1 ou 8.0, a subchave {f0e1e9a1-9860-484d-ad5d-367d79aabf55} é o GUID do painel de janela de ferramentas (DynamicWindowPane) e o {de valor padrão 01069cdd-95ce-4620-Ac21-ddff6c57f012} é o GUID do VSPackage fornecendo a janela da ferramenta. Para obter uma explicação das subchaves Float e DontForceCreate, consulte [configuração de exibição da janela de ferramenta](../extensibility/tool-window-display-configuration.md).  
  
 A segunda chave opcional ToolWindows\Visibility, especifica os GUIDs dos comandos que exigem a janela da ferramenta para ficar visível. Nesse caso, não há nenhum comando especificado. Para obter mais informações, consulte [configuração de exibição da janela de ferramenta](../extensibility/tool-window-display-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do VSPackage](../misc/vspackage-essentials.md)

