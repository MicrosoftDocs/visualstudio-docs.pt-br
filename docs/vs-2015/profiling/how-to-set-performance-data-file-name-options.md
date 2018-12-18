---
title: Como definir opções de nome de arquivo de dados de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d7a8d6b9-ab23-46fb-98ed-774781157860
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 06751d510c38f055036865a8f368c4e0c3298a30
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801965"
---
# <a name="how-to-set-performance-data-file-name-options"></a>Como definir opções de nome de arquivo de dados de desempenho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Por padrão, um arquivo de dados de criação de perfil (.vsp) é salvo usando a sintaxe a seguir:  
  
 *Path\VSP-File\YYMMDD(N)* **.vsp**  
  
 Você pode alterar qualquer parâmetro de nomeação na página Geral da caixa de diálogo de propriedades da sessão de desempenho.  
  
 **Requisitos**  
  
-   [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
|||  
|-|-|  
|*Path*|O diretório que contém o relatório. O local padrão é a pasta da solução ou o local padrão para projetos e soluções do usuário.|  
|*VSP-File*|O nome do arquivo de dados de criação de perfil. O nome padrão é o nome da solução ou do executável que está sendo analisado.|  
|*AAMMDD*|Um carimbo de data que mostra o ano, mês e dia em que os dados de criação de perfil foram coletados.|  
|*(N)*|Se houver mais de um arquivo de dados de criação de perfil, um número incrementado será adicionado ao nome de arquivo entre parênteses.|  
  
### <a name="to-change-the-naming-syntax-of-the-profiling-data-files-of-a-performance-session"></a>Para alterar a sintaxe de nomenclatura dos arquivos de dados de criação de perfil de uma sessão de desempenho  
  
1.  No **Gerenciador de Desempenho**, clique com o botão direito do mouse no nome da sessão de desempenho e, em seguida, clique em **Propriedades**.  
  
2.  Clique em **Geral**.  
  
3.  Em **Relatório**, altere qualquer uma das seguintes configurações:  
  
    |||  
    |-|-|  
    |**Local do relatório**|Especifica um diretório para armazenar os arquivos de dados de criação de perfil.|  
    |**Nome do relatório**|Especifica um nome de base para os arquivos.|  
    |**Adicionar novos relatórios à sessão automaticamente**|Marque a caixa de seleção para adicionar automaticamente o arquivo de dados à sessão de desempenho.|  
    |**Anexar um número de incremento para relatórios gerados**|Marque a caixa de seleção para adicionar um número de incremento para o nome de arquivo quando existe mais de um arquivo com mesmo nome. Desmarque a caixa de seleção para substituir um arquivo existente.|  
    |**Usar um carimbo de data/hora para o número**|Marque a caixa de seleção para adicionar um carimbo de data ao nome do arquivo.|



