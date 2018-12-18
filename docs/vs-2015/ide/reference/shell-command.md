---
title: Comando Shell | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- tools.shell
helpviewer_keywords:
- exe files
- Shell command
- Tools.Shell command
- executables, running from Visual Studio
- .exe files
- Shell, launching exe files
- Visual Studio, executables from
ms.assetid: 737fda23-b852-45c4-a9fe-41cbce6ba70f
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 5f760e449921a45f7ad22a3d81376bca432fe24a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49242210"
---
# <a name="shell-command"></a>Comando Shell
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Inicia programas executáveis de dentro do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Tools.Shell [/command] [/output] [/dir:folder] path [args]  
```  
  
## <a name="arguments"></a>Arguments  
 `path`  
 Necessário. O caminho e o nome do arquivo a ser executado ou o documento a ser aberto. Será necessário um caminho completo se o arquivo especificado não estiver em um dos diretórios na variável de ambiente PATH.  
  
 `args`  
 Opcional. Quaisquer argumentos a serem passados para o programa invocado.  
  
## <a name="switches"></a>Opções  
 /commandwindow [ou] /command [ou] /c [ou] /cmd  
 Opcional. Especifica que a saída para o executável é exibida na janela **Comando**.  
  
 /dir:`folder` [ou] /d: `folder`  
 Opcional. Especifica o diretório de trabalho a ser definido quando o programa é executado.  
  
 /outputwindow [ou] /output [ou] /out [ou] /o  
 Opcional. Especifica que a saída para o executável é exibida na Janela de **Saída**.  
  
## <a name="remarks"></a>Comentários  
 As opções /dir /o /c devem ser especificadas imediatamente após `Tools.Shell`. Qualquer coisa especificada após o nome do executável é passada para ele como argumentos de linha de comando.  
  
 O alias predefinido `Shell` pode ser usado no lugar de `Tools.Shell`.  
  
> [!CAUTION]
>  Se o argumento `path` fornecer o caminho de diretório, bem como o nome de arquivo, é necessário colocar o nome do caminho inteiro em aspas literais ("""), conforme o seguinte:  
  
```  
Tools.Shell """C:\Program Files\SomeFile.exe"""  
```  
  
 Cada conjunto de três aspas duplas (""") é interpretado pelo processador `Shell` como um único caractere de aspas duplas. Portanto, o exemplo anterior, na verdade, passa a seguinte cadeia de caracteres de caminho para o comando `Shell`:  
  
```  
"C:\Program Files\SomeFile.exe"  
```  
  
> [!CAUTION]
>  Se você não colocar a cadeia de caracteres de caminho em aspas literais ("""), o Windows usará somente a parte da cadeia de caracteres que vai até o primeiro espaço. Por exemplo, se a cadeia de caracteres de caminho acima não tivesse sido colocada adequadamente entre aspas, Windows pareceria um arquivo denominado “Programa” localizado no diretório raiz C:\. Se um arquivo executável C:\Program.exe estivesse mesmo disponível, e inclusive tivesse sido instalado por adulteração ilícita, o Windows tentaria executar esse programa no lugar do programa “c:\Arquivos de Programas\SomeFile.exe”.  
  
## <a name="example"></a>Exemplo  
 O comando a seguir usa xcopy.exe para copiar o arquivo `MyText.txt` para a pasta `Text`. A saída de xcopy.exe é exibida na **Janela Comando** e na Janela de **Saída**.  
  
```  
>Tools.Shell /o /c xcopy.exe c:\MyText.txt c:\Text\MyText.txt  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Janela Comando](../../ide/reference/command-window.md)   
 [Janela de Saída](../../ide/reference/output-window.md)   
 [Caixa Localizar/Comando](../../ide/find-command-box.md)   
 [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)



