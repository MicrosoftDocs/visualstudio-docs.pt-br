---
title: Obtendo logs de build com o MSBuild | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, logging
- logging [MSBuild]
ms.assetid: 6ba9a754-9cc0-4fed-9fc8-4dcd3926a031
caps.latest.revision: 30
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c88288a7bed453ca14e9c14fd43706b97be04044
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "90838349"
---
# <a name="obtaining-build-logs-with-msbuild"></a>Obtendo logs de build com o MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando opções com o MSBuild, você pode especificar quantos dados de build você deseja examinar e se deseja salvar os dados de build em um ou mais arquivos. Você também pode especificar um agente personalizado para coletar dados de build. Para obter informações sobre as opções de linha de comando do MSBuild que este tópico não abrange, consulte [referência de linha de comando](../msbuild/msbuild-command-line-reference.md).  
  
> [!NOTE]
> Se você compilar projetos usando o IDE do Visual Studio, poderá solucionar os builds examinando os logs de build. Para obter mais informações, consulte [como exibir, salvar e configurar arquivos de log de compilação](../ide/how-to-view-save-and-configure-build-log-files.md).  
  
## <a name="setting-the-level-of-detail"></a>Definindo o nível de detalhes  
 Quando você compila um projeto usando MSBuild sem especificar um nível de detalhamento, as seguintes informações aparecem no log de saída:  
  
- Erros, avisos e mensagens que são classificados como altamente importante.  
  
- Alguns eventos de status.  
  
- Um resumo do build.  
  
  Usando a opção **detalhamento** (**/v**), você pode controlar a quantidade de dados exibida no log de saída. Para solucionar o problema, use um nível de detalhes de `detailed` (`d`) ou `diagnostic` (`diag`), que fornece o máximo de informações.  
  
  O processo de build pode ficar mais lento ao definir o **/verbosity** para `detailed` e ainda mais lento se definir o **/verbosity** para `diagnostic`.  
  
```  
msbuild MyProject.proj /t:go /v:diag  
```  
  
## <a name="saving-the-build-log-to-a-file"></a>Salvando o log de compilação em um arquivo  
 Você pode usar a opção **/FileLogger** (**fl**) para salvar dados de compilação em um arquivo. O exemplo a seguir salva dados de build em um arquivo chamado `msbuild.log`.  
  
```  
msbuild MyProject.proj /t:go /fileLogger  
```  
  
 No exemplo a seguir, o arquivo de log é denominado `MyProjectOutput.log` e o detalhamento da saída do log é definida como `diagnostic`. Você especifica essas duas configurações usando a opção **/filelogparameters** ( `flp` ).  
  
```  
msbuild MyProject.proj /t:go /fl /flp:logfile=MyProjectOutput.log;verbosity=diagnostic  
```  
  
 Para obter mais informações, consulte [referência de linha de comando](../msbuild/msbuild-command-line-reference.md).  
  
## <a name="saving-the-log-output-to-multiple-files"></a>Salvando a saída de log em vários arquivos  
 O exemplo a seguir salva o log inteiro em `msbuild1.log`, apenas os erros em `JustErrors.log` e apenas os avisos em `JustWarnings.log`. O exemplo usa números de arquivo para cada um dos três arquivos. Os números de arquivo são especificados logo após as opções **/fl** e **/FLP** (por exemplo, `/fl1` e `/flp1` ).  
  
 As opções de **/filelogparameters** ( `flp` ) para os arquivos 2 e 3 especificam o que nomear cada arquivo e o que incluir em cada arquivo. Nenhum nome foi especificado para o arquivo 1, então o nome padrão de `msbuild1.log` é usado.  
  
```  
msbuild MyProject.proj /t:go /fl1 /fl2 /fl3 /flp2:logfile=JustErrors.log;errorsonly /flp3:logfile=JustWarnings.log;warningsonly  
  
```  
  
 Para obter mais informações, consulte [referência de linha de comando](../msbuild/msbuild-command-line-reference.md).  
  
## <a name="using-a-custom-logger"></a>Usando um agente personalizado  
 Você pode escrever seu próprio agente por meio da criação de um tipo gerenciado que implementa a interface <xref:Microsoft.Build.Framework.ILogger>. Você pode usar um agente personalizado, por exemplo, para enviar erros de build por email, registrá-los em um banco de dados ou em um arquivo XML. Para obter mais informações, consulte [Compilar agentes](../msbuild/build-loggers.md).  
  
 Na linha de comando do MSBuild, você deve especificar o agente personalizado usando a opção **/logger**. Você também pode usar a opção **/noconsolelogger** para desabilitar o agente do console padrão.  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.Build.Framework.LoggerVerbosity>   
 [Compilar agentes](../msbuild/build-loggers.md)   
 [Fazendo logon em um ambiente com vários processadores](../msbuild/logging-in-a-multi-processor-environment.md)   
 [Criando agentes de encaminhamento](../msbuild/creating-forwarding-loggers.md)   
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)
