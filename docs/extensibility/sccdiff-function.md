---
title: Função SccDiff | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 898c5b1b9de186a7ac704b4987fb090de5381f07
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884765"
---
# <a name="sccdiff-function"></a>Função SccDiff
Esta função exibe (ou, opcionalmente, apenas verifica) as diferenças entre o arquivo atual (no disco local) e a última versão de check-in na fonte de sistema de controle.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccDiff(  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LPCSTR    lpFileName,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpFileName  
 [in] Nome do arquivo para o qual a diferença é solicitada.  
  
 fOptions  
 [in] Sinalizadores de comando. Consulte os comentários para obter detalhes.  
  
 pvOptions  
 [in] Opções de plug-in específico de controle de origem.  
  
## <a name="return-value"></a>Valor retornado  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|A versão de trabalho de cópia e o servidor são idênticos.|  
|SCC_I_FILESDIFFERS|A cópia de trabalho é diferente da versão sob controle do código-fonte.|  
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|  
|SCC_E_FILENOTCONTROLLED|O arquivo não está sob controle de origem.|  
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NONSPECIFICERROR|Falha não específica; diferença de arquivo não foi obtida.|  
|SCC_E_FILENOTEXIST|O arquivo local não foi encontrado.|  
  
## <a name="remarks"></a>Comentários  
 Essa função tem duas finalidades diferentes. Por padrão, ele exibe uma lista de alterações para um arquivo. O plug-in de controle do código-fonte abre sua própria janela, em qualquer formato que escolher, para exibir as diferenças entre o arquivo do usuário no disco e a versão mais recente do arquivo sob controle do código-fonte.  
  
 Como alternativa, o IDE pode simplesmente precisar determinar se um arquivo foi alterado. Por exemplo, o IDE talvez precise determinar se é seguro fazer check-out de um arquivo sem informar o usuário. Nesse caso, o IDE passa a `SCC_DIFF_CONTENTS` sinalizador. O plug-in de controle do código-fonte deve verificar o arquivo no disco, byte por byte, com o arquivo de controle do código-fonte e retornar um valor que indica se os dois arquivos são diferentes, sem exibir nada ao usuário.  
  
 Como uma otimização de desempenho, o plug-in de controle de origem pode usar uma alternativa com base em uma soma de verificação ou um carimbo de hora, em vez da comparação byte por byte chamado para `SCC_DIFF_CONTENTS`: essas formas de comparação são, obviamente, mais rápido, mas menos confiável. Nem todos os sistemas de controle do código-fonte podem dar suporte a esses métodos alternativos de comparação, e o plug-in pode ter a cair para uma comparação de conteúdo. Controle de origem todos os plug-ins deve, no mínimo, dar suporte a uma comparação de conteúdo.  
  
> [!NOTE]
>  Os sinalizadores de diferença rápido são mutuamente exclusivos. Ele é válido não passar nenhum sinalizador, mas não é válido para transmitir simultaneamente mais de um. `SCC_DIFF_QUICK_DIFF`, que é uma máscara que combina todos os sinalizadores, pode ser usado para testar, mas nunca deve ser passado como um parâmetro.  
  
|`fOption`|Significado|  
|---------------|-------------|  
|SCC_DIFF_IGNORECASE|Comparação diferencia maiusculas de minúsculas (pode ser usado para rápido ou visual diferença).|  
|SCC_DIFF_IGNORESPACE|Ignora o espaço em branco (pode ser usado para rápido ou visual diferença).|  
|SCC_DIFF_QD_CONTENTS|Compara silenciosamente o arquivo, byte por byte.|  
|SCC_DIFF_QD_CHECKSUM|Compara silenciosamente o arquivo por meio de uma soma de verificação quando houver suporte. Se não tiver suporte, voltará a uma comparação de conteúdo.|  
|SCC_DIFF_QD_TIME|Compara silenciosamente o arquivo por meio de seu carimbo de hora quando houver suporte. Se não tiver suporte, voltará a uma comparação de conteúdo.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in da controle de origem](../extensibility/source-control-plug-in-api-functions.md)