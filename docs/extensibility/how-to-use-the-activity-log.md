---
title: 'Como: usar o log de atividades | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 824feee64f928dc837a379aeb539daaa5ba0d1db
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905585"
---
# <a name="how-to-use-the-activity-log"></a>Como: usar o log de atividades
VSPackages pode gravar mensagens no log de atividades. Esse recurso é especialmente útil para depurar VSPackages em ambientes de varejo.

> [!TIP]
> O log de atividades está sempre ativado. O Visual Studio mantém um buffer de sobreversão das últimas 100 entradas, bem como as 10 primeiras entradas, que têm informações gerais de configuração.

## <a name="to-write-an-entry-to-the-activity-log"></a>Para gravar uma entrada no log de atividades

1. Insira esse código no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método ou em qualquer outro método, exceto o Construtor VSPackage:

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     Esse código obtém o <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> serviço e o converte em uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> interface. <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A>grava uma entrada informativa no log de atividades usando o contexto cultural atual.

2. Quando o VSPackage é carregado (geralmente quando um comando é invocado ou uma janela é aberta), o texto é gravado no log de atividades.

## <a name="to-examine-the-activity-log"></a>Para examinar o log de atividades

1. Execute o Visual Studio com a opção de linha de comando [/log](../ide/reference/log-devenv-exe.md) para gravar ActivityLog.xml em disco durante a sessão.

2. Depois de fechar o Visual Studio, localize o log de atividades na subpasta para dados do Visual Studio:

   <em> *% AppData%</em>\Microsoft\VisualStudio \\ \<version>\ActivityLog.xml*.

3. Abra o log de atividades com qualquer editor de texto. Aqui está uma entrada típica:

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>Programação robusta

Como o log de atividades é um serviço, o log de atividades fica indisponível no Construtor VSPackage.

Você deve obter o log de atividades logo antes de gravar nele. Não armazene em cache ou salve o log de atividades para uso futuro.

## <a name="see-also"></a>Confira também

- [/Log (devenv.exe)](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [Solucionando problemas de VSPackages](../extensibility/troubleshooting-vspackages.md)
- [VSPackages](../extensibility/internals/vspackages.md)
