---
title: Função SccGetCommandOptions | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 846d1667e1f990a5580520353be46ede76644145
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49923739"
---
# <a name="sccgetcommandoptions-function"></a>Função SccGetCommandOptions
Essa função solicita ao usuário para opções avançadas para um determinado comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccGetCommandOptions(  
   LPVOID pvContext,  
   HWND hWnd,  
   enum SCCCOMMAND iCommand,  
   LPCMDOPTS* ppvOptions  
);  
```  
  
### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 iCommand  
 [in] O comando para o qual as opções avançadas são solicitadas (consulte [código de comando](../extensibility/command-code-enumerator.md) para possíveis valores).  
  
 ppvOptions  
 [in] A estrutura de opção (também pode ser `NULL`).  
  
## <a name="return-value"></a>Valor retornado  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Êxito.|  
|SCC_I_ADV_SUPPORT|O plug-in de controle de origem dá suporte a opções avançadas para o comando.|  
|SCC_I_OPERATIONCANCELED|O usuário cancelou o origem controle do plug-in **opções** caixa de diálogo.|  
|SCC_E_OPTNOTSUPPORTED|O plug-in de controle de origem não oferece suporte a essa operação.|  
|SCC_E_ISCHECKEDOUT|Não é possível executar esta operação em um arquivo que está sendo verificado.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NONSPECIFICERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 O IDE chama essa função pela primeira vez com `ppvOptions` = `NULL` para determinar se o plug-in de controle do código-fonte ofereça suporte ao recurso de opções avançadas para o comando especificado. Se o plug-in oferece suporte ao recurso para o comando, o IDE chama essa função novamente quando o usuário solicita opções avançadas (geralmente implementado como um **avançado** botão em uma caixa de diálogo) e fornece um ponteiro não nulo para `ppvOptions` que aponta para um `NULL` ponteiro. O plug-in armazena as opções avançadas, especificadas pelo usuário em uma estrutura em particular e retorna um ponteiro para essa estrutura no `ppvOptions`. Essa estrutura é passada para todas as outras funções de API de plug-in de controle do código-fonte que precisa saber sobre ele, incluindo as chamadas subsequentes para o `SccGetCommandOptions` função.  
  
 Um exemplo pode ajudar a esclarecer essa situação.  
  
 Um usuário escolhe o **Obtenha** comando e o IDE exibirá uma **obter** caixa de diálogo. O IDE chama o `SccGetCommandOptions` funcionar com `iCommand` definido como `SCC_COMMAND_GET` e `ppvOptions` definido como `NULL`. Isso é interpretado pelo controle de fonte de plug-in como a pergunta, "Você tem as opções avançadas para este comando?" Se o plug-in retorna `SCC_I_ADV_SUPPORT`, o IDE exibirá uma **Advanced** botão no seu **obter** caixa de diálogo.  
  
 Na primeira vez em que o usuário clica o **Advanced** botão, o IDE chama novamente o `SccGetCommandOptions` funcionar, desta vez com um não -`NULL``ppvOptions` que aponta para um `NULL` ponteiro. O plug-in exibe sua própria **obter opções** caixa de diálogo, solicita ao usuário informações, coloca essa informação em sua própria estrutura e retorna um ponteiro para essa estrutura no `ppvOptions`.  
  
 Se o usuário clica **Advanced** novamente na caixa de diálogo, o IDE chama o `SccGetCommandOptions` função novamente sem alterar `ppvOptions`, de modo que a estrutura é passada de volta para o plug-in. Isso permite que o plug-in reinicializar sua caixa de diálogo para os valores que o usuário tiver sido definida anteriormente. O plug-in modifica a estrutura em vigor antes de retornar.  
  
 Por fim, quando o usuário clica **Okey** no IDE do **obter** caixa de diálogo, as chamadas IDE a [SccGet](../extensibility/sccget-function.md), passando a estrutura retornada em `ppvOptions` que contém o Opções avançadas.  
  
> [!NOTE]
>  O comando `SCC_COMMAND_OPTIONS` é usado quando o IDE exibirá uma **opções** caixa de diálogo que permite que o usuário defina preferências que controlam como a integração funciona. Se desejar obter o plug-in de controle do código-fonte fornecer sua própria caixa de diálogo Preferências, ele pode exibi-lo de um **avançado** botão na caixa de diálogo de preferências do IDE. O plug-in é exclusivamente responsável por obter e manter essas informações; o IDE não usá-lo ou modificá-lo.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in da controle de origem](../extensibility/source-control-plug-in-api-functions.md)   
 [Código de comando](../extensibility/command-code-enumerator.md)