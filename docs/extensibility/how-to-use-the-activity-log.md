---
title: 'Como: usar o Log de atividades | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fa564919abcfb4c8bd94fbaf139b69f2375deebd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825810"
---
# <a name="how-to-use-the-activity-log"></a>Como: usar o log de atividades
Os VSPackages pode gravar mensagens no log de atividade. Esse recurso é especialmente útil para depurar os VSPackages em ambientes de varejo.  
  
> [!TIP]
>  O log de atividades está sempre ativado. O Visual Studio manterá um buffer progressivo das últimas 100 entradas, bem como as 10 primeiras entradas, o que tem informações de configuração geral.  
  
## <a name="to-write-an-entry-to-the-activity-log"></a>Para gravar uma entrada ao log de atividades  
  
1.  Inserir este código no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método ou em qualquer outro método, exceto no construtor de VSPackage:  
  
    ```csharp  
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
    if (log == null) return;  
  
    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,  
        this.ToString(),  
        string.Format(CultureInfo.CurrentCulture,  
        "Called for: {0}", this.ToString()));  
    ```  
  
     Esse código obtém os <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> de serviço e a converte para um <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> interface. <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> grava uma entrada informativa no log de atividades usando o contexto cultural atual.  
  
2.  Quando o VSPackage é carregado (normalmente, quando um comando é invocado ou uma janela é aberta), o texto é escrito para o log de atividades.  
  
## <a name="to-examine-the-activity-log"></a>Para examinar o log de atividades  
  
1. Executar o Visual Studio com o [/Log](../ide/reference/log-devenv-exe.md) opção de linha de comando para gravar activitylog. XML no disco durante a sessão.

2. Depois de fechar o Visual Studio, localize o log de atividades na subpasta para dados do Visual Studio:  <em>*% AppData %</em>\Microsoft\VisualStudio\15.0\ActivityLog.xml*.  
  
3. Abra o log de atividades com qualquer editor de texto. Aqui está uma entrada típica:  
  
   ```  
   Called for: Company.MyApp.MyAppPackage ...  
   ```  
  
## <a name="robust-programming"></a>Programação robusta  
 Como o log de atividades é um serviço, o log de atividades não está disponível no construtor de VSPackage.  
  
 Você deve obter o log de atividades antes de gravar. Não armazenar em cache ou salvar o log de atividades para uso futuro.  
  
## <a name="see-also"></a>Consulte também
 [/ Log (devenv.exe)](../ide/reference/log-devenv-exe.md)   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>   
 [Solucionar problemas de VSPackages](../extensibility/troubleshooting-vspackages.md)   
 [VSPackages](../extensibility/internals/vspackages.md)
