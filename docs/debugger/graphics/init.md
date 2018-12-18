---
title: Init | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: c55ddec8-9101-4673-979b-4109caca9146
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0436384e0af816475590ab84dc645848113f5ab7
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31476192"
---
# <a name="init"></a>Init
Prepara o componente no aplicativo de diagnóstico de gráficos para capturar e registrar informações de elementos gráficos em um arquivo de log do gráfico ativamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
void Init(  
  std::function<void (int len, wchar_t * pszBuffer)> vsgLogGetter  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `vsgLogGetter`  
 Uma entidade que pode ser chamada — como uma função, o ponteiro de função, o lambda ou o objeto de função, que usa como parâmetros o comprimento de um buffer composto `wchar_t` e um ponteiro para esse buffer e retorna `void`. Quando chamado, a entidade que pode ser chamada determina o nome do arquivo que será usado para registrar informações de gráficos e grava-o buffer especificado antes de retornar.  
  
## <a name="remarks"></a>Comentários  
 O `Init` função é chamada automaticamente quando uma instância do `VsgDbg` classe é criada especificando a `bDefaultInit` parâmetro de seu construtor como `true`; caso contrário, `Init` deve ser chamado explicitamente antes de você pode capturar ativamente e gravar informações de gráficos.  
  
 Finalizar e fechar o ativo de gráficos o arquivo de log chamando `UnInit`e, em seguida, capturar e registrar mais informações de elementos gráficos em um novo arquivo de log de elementos gráficos chamando `Init` novamente. Você pode repetir esta quantas vezes você deseja criar o gráfico independente de vários arquivos de log usando o mesmo `VsgDbg` instância.  
  
## <a name="see-also"></a>Consulte também  
 [UnInit](init.md)