---
title: Ferramenta do Windows no registro | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering
ms.assetid: c4bb8add-7148-49e4-a377-01d059fd5524
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 234a3f50865e77f2c6b5a4057e6766b26d7ff521
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31138441"
---
# <a name="tool-windows-in-the-registry"></a>Janelas de ferramenta no registro
VSPackages que fornecem as janelas de ferramentas deve registrar com [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] como provedores de janela de ferramenta. Janelas de ferramentas criadas usando o modelo de pacote do Visual Studio fazer isso por padrão. Provedores de janela de ferramenta tenham chaves de registro do sistema que especifica os atributos de visibilidade, como tamanho de janela de ferramenta padrão e o local, o GUID da janela que serve como o painel de janela de ferramenta e o estilo de encaixe.  
  
 Durante o desenvolvimento, provedores de janela de ferramenta gerenciado registrar janelas de ferramentas adicionando atributos para o código-fonte e, em seguida, executando o utilitário RegPkg.exe o assembly resultante. Para obter mais informações, consulte [registrando uma janela de ferramenta](../extensibility/registering-a-tool-window.md).  
  
## <a name="registering-unmanaged-tool-window-providers"></a>Registrar provedores de janela de ferramenta não gerenciado  
 Provedores de janela de ferramenta não gerenciado devem registrar [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] na seção de ToolWindows do registro do sistema. O fragmento de arquivo. reg a seguir mostra como uma janela de ferramenta dinâmico pode ser registrada:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\<version number>\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}]  
@="{01069cdd-95ce-4620-ac21-ddff6c57f012}"  
"Name"="Microsoft.Samples.VisualStudio.IDE.ToolWindow.DynamicWindowPane"  
"Float"="250, 250, 410, 430"  
"DontForceCreate"=dword:00000001  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}\Visibility]  
"{f1536ef8-92ec-443c-9ed7-fdadf150da82}"=dword:00000000  
```  
  
 Na primeira chave no exemplo acima, o número de versão é a versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], como 7.1 ou 8.0, a subchave {f0e1e9a1-9860-484d-ad5d-367d79aabf55} é o GUID do painel de janela de ferramenta (DynamicWindowPane) e o {de valor padrão 01069cdd-95ce-4620-Ac21-ddff6c57f012} é o GUID do VSPackage fornecendo a janela da ferramenta. Para obter uma explicação das subchaves Float e DontForceCreate, consulte [configuração de exibição da janela de ferramenta](../extensibility/tool-window-display-configuration.md).  
  
 A segunda chave opcional, ToolWindows\Visibility, especifica os GUIDs dos comandos que exigem a janela da ferramenta para ficar visível. Nesse caso, não há nenhum comando especificado. Para obter mais informações, consulte [configuração de exibição da janela de ferramenta](../extensibility/tool-window-display-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)