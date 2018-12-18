---
title: Guia de Introdução (depuração de acesso à Interface SDK) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- .dbg files
- DBG files
ms.assetid: cb3d040a-2846-40d7-bdbc-8a5beb5dd2f6
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e5cfcad351f19f48678d575e11b074375c6aaadc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887287"
---
# <a name="getting-started-debug-interface-access-sdk"></a>Guia de Introdução (SDK de Acesso à Interface de Depuração)
A depuração Interface de acesso (DIA) SDK fornece documentação das instruções e um exemplo que ilustra como usar a API do DIA. Use as interfaces e métodos em DIA SDK para desenvolver aplicativos personalizados que abrem os arquivos. PDB e. dbg e pesquisem seu conteúdo para símbolos, valores, atributos, endereços e outras informações de depuração. Esse SDK também fornece as tabelas de referência para as propriedades associadas com símbolos encontrados em aplicativos C++.  
  
 Para usar melhor o DIA SDK, você deve estar familiarizado com o seguinte:  
  
- Linguagem de programação do C++  
  
- Programação COM  
  
- Ambiente de desenvolvimento integrado Visual Studio (IDE) para compilar os exemplos  
  
  O DIA SDK é normalmente instalado com o Visual Studio e o local padrão é *[unidade]* \Program Files\Microsoft 9.0\DIA do Visual Studio SDK. Como parte da instalação, MSDIA90, que implementa o DIA SDK, é registrado automaticamente para que tudo o que você precisa fazer para usá-lo é incluir `dia2.h` em seu programa e um link para `diaguids.lib`.  
  
  Cabeçalho: include\dia2.h  
  
  Biblioteca: lib\diaguids.lib  
  
  DLL: bin\msdia80.dll  
  
  IDL: idl\dia2.idl  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)  
 Revisa a arquitetura básica do DIA.  
  
 [Consultando o arquivo .Pdb](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)  
 Fornece instruções passo a passo sobre como usar a API do DIA para consultar um arquivo. PDB.  
  
## <a name="see-also"></a>Consulte também  
 [SDK de Acesso à Interface de Depuração](../../debugger/debug-interface-access/debug-interface-access-sdk.md)