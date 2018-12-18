---
title: Propriedades gerais do projeto (Android C++) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 65f4868b-b864-4989-a275-1e51869ef599
author: corob
ms.author: mblome
manager: douge
f1_keywords:
- VC.Project.VCConfiguration.OutputDirectory
- VC.Project.VCConfiguration.IntermediateDirectory
- VC.Project.VCConfiguration.TargetName
- VC.Project.VCConfiguration.TargetExt
- VC.Project.VCConfiguration.DeleteExtensionsOnClean
- VC.Project.VCConfiguration.BuildLogFile
- VC.Project.VCConfiguration.PlatformToolset
- VC.Project.VCConfiguration.ConfigurationType
- VC.Project.VCConfiguration.DeleteExtensionsOnClean
- VC.Project.VCConfiguration.UseOfSTL
- VC.Project.VCConfiguration.ThumbMode
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: b72cbb0d2660507a0578781c79a7cbdf60be7d8b
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39252232"
---
# <a name="general-project-properties-android-c"></a>Propriedades gerais do projeto (Android C++)

Propriedade | Descrição | Opções
--- | ---| ---
Diretório de saída | Especifica um caminho relativo para o diretório de arquivo de saída e pode incluir variáveis de ambiente.
Diretório intermediário | Especifica um caminho relativo para o diretório de arquivo intermediário e pode incluir variáveis de ambiente.
Nome de Destino | Especifica um nome de arquivo que será gerado por este projeto.
Extensão de Destino | Especifica uma extensão de arquivo que será gerada por este projeto. (Exemplo: *.exe* ou *.dll*)
Extensões a serem excluídas na limpeza | Especificação de curinga delimitado por ponto e vírgula para os arquivos no diretório intermediário que deverão ser excluídos na limpeza ou na recompilação.
Arquivo de log de build | Especifica o arquivo de log de build para gravação quando o registro em log de build está habilitado.
Conjunto de ferramentas da plataforma | Especifica o conjunto de ferramentas usado para compilar a configuração atual. Se não estiver definido, o conjunto de ferramentas padrão será usado
Tipo de configuração | Especifica o tipo de saída gerado por essa configuração. | **Biblioteca Dinâmica (.so)** – Biblioteca Dinâmica (*.so*)<br>**Biblioteca estática (.a)** – Biblioteca estática (*.a*)<br>**Utilitário** – utilitário<br>**Makefile** – makefile<br>
Nível da API de destino | Nível da API do Android NDK de destino dessa configuração.
Uso de STL | Especifica qual biblioteca padrão C++ deve ser usada para essa configuração. | **Biblioteca de tempo de execução C++ mínima (sistema)**<br>**Biblioteca estática de tempo de execução C++ (gabi++_static)**<br>**Biblioteca compartilhada de tempo de execução C++ (gabi++_shared)**<br>**Biblioteca estática de tempo de execução STLport (stlport_static)**<br>**Biblioteca compartilhada de tempo de execução STLport (stlport_shared)**<br>**Biblioteca estática GNU STL (gnustl_static)**<br>**Biblioteca compartilhada GNU STL (gnustl_shared)**<br>**Biblioteca estática LLVM libc++ (c++_static)**<br>**Biblioteca compartilhada LLVM libc++ (c++_shared)**<br>
Modo Thumb | Gerar um código que pode ser executado em microarquiteturas thumb. Somente se aplica a arquiteturas arm. | **Thumb**<br>**ARM**<br>**Desabilitado**<br>
