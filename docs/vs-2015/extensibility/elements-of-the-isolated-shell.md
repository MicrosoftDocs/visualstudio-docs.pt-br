---
title: Elementos do Shell isolado | Microsoft Docs
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
- Visual Studio shell, isolated mode
ms.assetid: f8d68c3d-9134-4a8f-b566-485956cd321e
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e567fc212b9981d925fc11e8e0ae48132b3b05bf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51816808"
---
# <a name="elements-of-the-isolated-shell"></a>Elementos do Shell isolado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode modificar as configurações do registro, configurações de tempo de execução e ponto de entrada do aplicativo de seu aplicativo de shell isolado e seu. VSCT,. pkgdef, and.pkgundef arquivos.  
  
## <a name="registry-settings"></a>Configurações do registro  
 A. pkgdef e os arquivos. pkgundef modificam as configurações do registro para o aplicativo de shell isolado. Quando o aplicativo é executado, as configurações do registro são definidas na sequência a seguir:  
  
 Quando o aplicativo é executado, as configurações do registro são definidas na sequência a seguir:  
  
1.  A chave do registro para o aplicativo é criada.  
  
2.  O registro é atualizado a partir do arquivo. pkgdef do aplicativo definindo entradas e chaves especificadas.  
  
3.  Para cada pacote que faz parte do seu aplicativo, o registro é atualizado do arquivo. pkgdef do que o pacote. Cada pacote é definido no arquivo. pkgdef do aplicativo pelo $RootKey$ \packages.\\{*vsPackageGuid*} chave para o pacote.  
  
4.  O registro é atualizado na AppEnvConfig.pkgdef e BaseConfig.pkgdef na *caminho de instalação do SDK do Visual Studio*\Common7\IDE\ShellExtensions\Platform directory. Esses arquivos são parte do Visual Studio e também parte do pacote redistribuível do Shell do Visual Studio (modo isolado).  
  
5.  O registro é atualizado do arquivo. pkgundef do aplicativo, removendo as entradas e chaves especificadas.  
  
## <a name="run-time-settings"></a>Configurações de tempo de execução  
 Quando um usuário inicia o aplicativo de shell isolado, ele chama o ponto de entrada do início do shell do Visual Studio. Configurações do aplicativo são definidas quando o aplicativo é iniciado, da seguinte maneira:  
  
1. Shell do Visual Studio verifica o registro de aplicativo para chaves específicas. Se a configuração para uma chave for especificada na chamada para o ponto de entrada inicial, em seguida, esse valor substitui o valor no registro.  
  
2. Se o ponto de registro nem a entrada de parâmetro especifica o valor de uma configuração, o valor padrão para a configuração é usado.  
  
   Quando um usuário inicia o aplicativo da linha de comando, todos os comutadores de linha de comando são passados para o shell do Visual Studio, que trata da mesma maneira que faz do Devenv. Para obter mais informações sobre opções do Devenv, consulte [opções de linha de comando Devenv](../ide/reference/devenv-command-line-switches.md) e [opções de linha de comando Devenv para desenvolvimento de VSPackage](../extensibility/devenv-command-line-switches-for-vspackage-development.md). Para obter mais informações sobre como um pacote registra para opções de linha de comando, consulte [Adicionando opções de linha de comando](../extensibility/adding-command-line-switches.md).  
  
## <a name="the-start-entry-point"></a>O ponto de entrada inicial  
 O arquivo Appenvstub.dll contém pontos de entrada para acessar o shell isolado. Quando o aplicativo é iniciado, ele chama o ponto de entrada de início de Appenvstub.dll.  
  
 Você pode alterar o comportamento do aplicativo alterando o valor do último parâmetro que é passado para o ponto de entrada inicial. Para obter mais informações, consulte [Shell de entrada de ponto de parâmetros (C++) isolado](../extensibility/isolated-shell-entry-point-parameters-cpp.md).  
  
## <a name="the-vsct-file"></a>A. Arquivo VSCT  
 O arquivo. VSCT permite especificar quais elementos de interface de usuário do Visual Studio standard estão disponíveis no aplicativo. Para obter mais informações, consulte [. Arquivos de VSCT](../extensibility/modifying-the-isolated-shell-by-using-the-dot-vsct-file.md).  
  
## <a name="the-pkgundef-file"></a>A. Arquivo Pkgundef  
 Quando o aplicativo é instalado em um computador em que o Visual Studio já está instalado, é feita uma cópia das entradas do registro do Visual Studio para o aplicativo. Por padrão, o aplicativo usa os VSPackages que já estão instalados no computador. O arquivo. pkgundef permite a exclusão de entradas do registro para remover elementos específicos do shell do Visual Studio ou extensões do aplicativo. Para obter mais informações, consulte [. Arquivos de Pkgundef](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md).  
  
 O arquivo. pkgundef permite a exclusão de entradas do registro para remover elementos específicos do shell do Visual Studio ou extensões do aplicativo. Para obter mais informações, consulte [. Arquivos de Pkgundef](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md).  
  
 O conjunto de GUIDs que você pode excluir do pacote são listados na [pacote GUIDs de recursos do Visual Studio](../extensibility/package-guids-of-visual-studio-features.md).  
  
## <a name="the-pkgdef-file"></a>A. Arquivo Pkgdef  
 O arquivo. pkgdef permite definir entradas do registro para o aplicativo que são definidas quando o aplicativo está instalado. Para obter uma descrição do arquivo. pkgdef e uma lista de entradas do registro que usa o shell do Visual Studio, consulte [. Arquivos de Pkgdef](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md).  
  
## <a name="substitution-strings"></a>Cadeias de caracteres de substituição  
 As cadeias de caracteres de substituição usadas nos arquivos. pkgdef e. pkgundef estão listadas na [cadeias de caracteres de substituição usadas no. Pkgdef e. Arquivos de Pkgundef](../extensibility/substitution-strings-used-in-dot-pkgdef-and-dot-pkgundef-files.md).  
  
## <a name="other-settings"></a>Outras configurações  
 Se seu aplicativo de shell isolado depende Microsoft.VisualStudio.GraphModel.dll, você precisará adicionar o redirecionamento de associação a seguir ao arquivo. config do seu aplicativo de Shell isolado:  
  
```  
<dependentAssembly>  
    <assemblyIdentity name="Microsoft.VisualStudio.GraphModel" publicKeyToken="b03f5f7f11d50a3a" culture="neutral" />  
    <bindingRedirect oldVersion="11.0.0.0" newVersion="12.0.0.0"/>  
</dependentAssembly>  
  
```

