---
title: Avisos de VSInstr | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- instrumentation, VSInstr tool
- warnings
- VSInstr tool
- warnings, VSInstr tool
- performance tools, VSInstr tool
ms.assetid: 47512bc9-a8e9-4628-883a-d9888edab786
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a306276e015d06fe3becf297d0bb5834f640a1a7
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34571640"
---
# <a name="vsinstr-warnings"></a>Avisos de VSInstr
A tabela a seguir lista os avisos emitidos pela ferramenta *VSInstr.exe*. Você pode usar a opção NOWARN junto com os números de aviso para suprimir o aviso seja exibido.  
  
|Número do aviso|Descrição|  
|--------------------|-----------------|  
|**VSP2000**|Erro interno. Não é possível obter o nome de arquivo do módulo para este executável.|  
|**VSP2001**|\<assembly name> é um assembly de nome forte. Ele deve ser assinado novamente antes de ser executado.<br /><br /> Este aviso ocorre quando um assembly assinado é instrumentado. Use a ferramenta *sn.exe* para desistir do binário ou desligar temporariamente o requisito de nome forte. Para obter mais informações, confira [Sn.exe (ferramenta de nome forte)](/dotnet/framework/tools/sn-exe-strong-name-tool).|  
|**VSP2002**|Não foi possível localizar a função \<funcname > no arquivo \<filename ><br /><br /> Este aviso ocorrerá se uma função não puder ser localizada no arquivo especificado.|  
|**VSP2003**|Não foi possível encontrar um salto cruzado para a função \<funcname> no arquivo \<filename>.<br /><br /> Este aviso ocorre se VSInstr não puder anular saltos cruzados. Saltos cruzados são usados para otimização do código.|  
|**VSP2004**|A função \<funcname> foi excluída por meio da opção de linha de comando EXCLUDE, mas ela era necessária porque continha um salto cruzado.<br /><br /> Este aviso ocorre se a função foi excluída usando a opção EXCLUDE, mas é necessária durante o processo de instrumentação. O criador de perfil inclui automaticamente a função necessária.|  
|**VSP2005**|Erro de Instrumentação Interno \<error text><br /><br /> Esse aviso será emitido se a instrumentação não puder ser executada. Examine o texto de erro para determinar se ele pode ser corrigido.|  
|**VSP2006**|Não foi possível localizar PDB para \<name><br /><br /> Este aviso ocorre se o arquivo PDB não corresponde ao binário ou não existe no caminho de pesquisa.|  
|**VSP2007**|\<filename> não contém código instrumentável.<br /><br /> Esse aviso é emitido se as funções no arquivo binário foram excluídas ou se o arquivo especificado contém somente os recursos.|  
|**VSP2008**|Não é possível obter atributos de segurança de \<name>. Código de erro \<code><br /><br /> Este aviso ocorrerá se o usuário não tiver a permissão READ_DAC. Durante o processo de instrumentação, o criador de perfil tenta preservar a DACL original para o binário. Porque o binário original é substituído por um novo binário, a DACL do binário original deve ser copiada e aplicada ao novo binário. Isso poderá falhar se o usuário não tiver acesso READ_DAC no binário original.|  
|**VSP2009**|Não é possível definir atributos de segurança em \<name>. Código de erro \<error number><br /><br /> Este aviso ocorre se o usuário não tem a permissão WRITE_DAC. Durante o processo de instrumentação, o criador de perfil tenta preservar a DACL original para o binário. Porque o binário original é substituído por um novo binário, a DACL do binário original deve ser copiada e aplicada ao novo binário. Isso poderá falhar se o usuário não tiver acesso WRITE_DAC no novo binário.|  
|**VSP2010**|Não há funções especificamente selecionadas para instrumentação por causa das opções -INCLUDE/-EXCLUDE|  
|**VSP2011**|Include/Exclude funcspec \<name> não corresponde a qualquer função|  
|**VSP2012**|A imagem não contém qualquer código que pode ser instrumentado para cobertura de código.<br /><br /> O criador de perfil não instrumenta o seguinte tipo de código:<br /><br /> - Funções de CRT estáticas<br />- Métodos gerenciados atribuídos com NonUserCodeAttribute<br />- Métodos gerenciados atribuídos com DebuggerHiddenAttribute<br />- Blocos MASM<br /><br /> Esse aviso será gerado se, após a filtragem, não houver nenhum código restante.|  
|**VSP2013**|Instrumentar esta imagem requer que ela seja executada como um processo de 32 bits. Os sinalizadores de cabeçalho CLR foram atualizados para refletir isso.<br /><br /> O criador de perfil modifica o binário para que os sistemas operacionais de 64 bits pode abrir o processo de 32 bits no emulador WOW64. Para bibliotecas (DLLs) isso pode falhar se eles são carregados em um processo de 64 bits existente. Este aviso notifica o usuário da dependência.|  
|**VSP2014**|A imagem instrumentada resultante parece ser inválida e poderá não ser executada.<br /><br /> Essa mensagem ocorre quando o assembly instrumentado final tem um cabeçalho PE inválido.|  
  
## <a name="see-also"></a>Consulte também  
 [VSInstr](../profiling/vsinstr.md)