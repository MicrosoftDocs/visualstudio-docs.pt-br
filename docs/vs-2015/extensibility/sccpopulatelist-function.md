---
title: Função SccPopulateList | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: fccf5ba354a99eaef6968c5d5027e8540762af75
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798892"
---
# <a name="sccpopulatelist-function"></a>Função SccPopulateList
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função atualiza uma lista de arquivos para um comando de controle de origem em particular e fornece o status de controle do código-fonte em todos os arquivos de determinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccPopulateList (  
   LPVOID          pvContext,  
   enum SCCCOMMAND nCommand,  
   LONG            nFiles,  
   LPCSTR*         lpFileNames,  
   POPLISTFUNC     pfnPopulate,  
   LPVOID          pvCallerData,  
   LPLONG          lpStatus,  
   LONG            fOptions  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 Ncomando  
 [in] O comando de controle de origem que será aplicado a todos os arquivos a `lpFileNames` matriz (consulte [código do comando](../extensibility/command-code-enumerator.md) para obter uma lista de comandos possíveis).  
  
 nFiles  
 [in] Número de arquivos a `lpFileNames` matriz.  
  
 lpFileNames  
 [in] Uma matriz de nomes de arquivo conhecidas para o IDE.  
  
 pfnPopulate  
 [in] A função de retorno de chamada IDE para chamar para adicionar e remover arquivos (consulte [POPLISTFUNC](../extensibility/poplistfunc.md) para obter detalhes).  
  
 pvCallerData  
 [in] Valor a ser passados inalterados para a função de retorno de chamada.  
  
 lpStatus  
 [no, out] Uma matriz para o plug-in para retornar os sinalizadores de status para cada arquivo de controle de origem.  
  
 fOptions  
 [in] Sinalizadores de comando (consulte a seção "PopulateList sinalizador" [sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md) para obter detalhes).  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Êxito.|  
|SCC_E_NONSPECIFICERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 Essa função examina a lista de arquivos para seu status atual. Ele usa o `pfnPopulate` função de retorno de chamada para notificar o chamador quando um arquivo não coincide com os critérios para o `nCommand`. Por exemplo, se o comando é `SCC_COMMAND_CHECKIN` e um arquivo na lista não é check-out e, em seguida, o retorno de chamada é usado para informar o chamador. Ocasionalmente, o plug-in de controle do código-fonte pode encontrar outros arquivos que poderiam ser parte do comando e adicioná-los. Isso permite, por exemplo, um usuário do Visual Basic fazer check-out de um arquivo. bmp que é usado pelo seu projeto, mas não aparece no arquivo de projeto do Visual Basic. Um usuário escolhe o **obter** comando no IDE. O IDE exibirá uma lista de todos os arquivos que ele considera que o usuário pode obter, mas antes que a lista é mostrada, o `SccPopulateList` função é chamada para certificar-se de que a lista a ser exibido está atualizada.  
  
## <a name="example"></a>Exemplo  
 O IDE compila uma lista de arquivos que ele considera que o usuário pode obter. Antes de exibir essa lista, ele chama o `SccPopulateList` de função, fornecendo o plug-in de controle do código-fonte a oportunidade de adicionar e excluir arquivos na lista. O plug-in modifica a lista, chamando a função de retorno de chamada específico (consulte [POPLISTFUNC](../extensibility/poplistfunc.md) para obter mais detalhes).  
  
 O plug-in continua a chamar o `pfnPopulate` função, que adiciona e exclui os arquivos, até que ele for concluído e então retornará o `SccPopulateList` função. O IDE, em seguida, pode exibir sua lista. O `lpStatus` matriz representa todos os arquivos na lista original passada pelo IDE. O plug-in, preenche o status de todos esses arquivos, além de tomada de usa a função de retorno de chamada.  
  
> [!NOTE]
>  Um plug-in de controle do código-fonte sempre tem a opção de simplesmente retornam imediatamente dessa função, deixando a lista como está. Se um plug-in implementa essa função, isso pode indicar isso definindo a `SCC_CAP_POPULATELIST` bitflag de recurso na primeira chamada para o [SccInitialize](../extensibility/sccinitialize-function.md). Por padrão, o plug-in deve sempre presumir que todos os itens sendo passados são arquivos. No entanto, se o IDE define a `SCC_PL_DIR` sinalizador no `fOptions` parâmetro, todos os itens que está sendo transmitidos devem ser considerados como diretórios. O plug-in deve adicionar todos os arquivos que pertencem nos diretórios. O IDE nunca passará uma mistura de arquivos e diretórios.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)   
 [POPLISTFUNC](../extensibility/poplistfunc.md)   
 [Sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)   
 [Código de comando](../extensibility/command-code-enumerator.md)

