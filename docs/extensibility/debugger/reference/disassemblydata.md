---
title: DisassemblyData | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- DisassemblyData
helpviewer_keywords:
- DisassemblyData structure
ms.assetid: 10e70aa7-9381-40d3-bdd1-d2cad78ef16c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a7ab7b278c03d092e1e559f1eb74f5d6bdc86d85
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816842"
---
# <a name="disassemblydata"></a>DisassemblyData
Descreve uma instrução de desmontagem para o ambiente de desenvolvimento integrado (IDE) para exibir.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct tagDisassemblyData {   
   DISASSEMBLY_STREAM_FIELDS dwFields;  
   BSTR                      bstrAddress;  
   BSTR                      bstrAddressOffset;  
   BSTR                      bstrCodeBytes;  
   BSTR                      bstrOpcode;  
   BSTR                      bstrOperands;  
   BSTR                      bstrSymbol;  
   UINT64                    uCodeLocationId;  
   TEXT_POSITION             posBeg;  
   TEXT_POSITION             posEnd;  
   BSTR                      bstrDocumentUrl;  
   DWORD                     dwByteOffset;  
   DISASSEMBLY_FLAGS         dwFlags;  
} DisassemblyData;  
```  
  
```csharp  
public struct DisassemblyData {   
   public uint          dwFields;  
   public string        bstrAddress;  
   public string        bstrAddressOffset;  
   public string        bstrCodeBytes;  
   public string        bstrOpcode;  
   public string        bstrOperands;  
   public string        bstrSymbol;  
   public ulong         uCodeLocationId;  
   public TEXT_POSITION posBeg;  
   public TEXT_POSITION posEnd;  
   public string        bstrDocumentUrl;  
   public uint          dwByteOffset;  
   public uint          dwFlags;  
};  
```  
  
## <a name="members"></a>Membros  
 `dwFields`  
 O [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) constante que especifica quais campos são preenchidos.  
  
 `bstrAddress`  
 O endereço como um deslocamento de algum ponto de partida (geralmente o início da função associada).  
  
 `bstrCodeBytes`  
 Os bytes de código para essa instrução.  
  
 `bstrOpcode`  
 O código de operação para essa instrução.  
  
 `bstrOperands`  
 Os operandos para essa instrução.  
  
 `bstrSymbol`  
 O nome do símbolo, se houver, associado ao endereço (símbolos públicos, rótulo e assim por diante).  
  
 `uCodeLocationId`  
 O identificador de local de código para essa linha desmontado. Se o endereço de contexto de código de uma linha for maior que o endereço de contexto de código de outro, o identificador de local do código desmontado do primeiro também será maior que o identificador de local do código do segundo.  
  
 `posBeg`  
 O [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) que corresponde à posição em um documento em que os dados de desmontagem começam.  
  
 `posEnd`  
 O [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) que corresponde à posição em um documento em que os dados de desmontagem termina.  
  
 `bstrDocumentUrl`  
 Para documentos de texto que podem ser representados como nomes de arquivo, o `bstrDocumentUrl` campo é preenchido com o nome do arquivo onde a fonte pode ser encontrada, usando o formato `file://file name`.  
  
 Para documentos de texto que não podem ser representados como nomes de arquivo `bstrDocumentUrl` é um identificador exclusivo para o documento e o mecanismo de depuração deve implementar a [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md) método.  
  
 Este campo também pode conter informações adicionais sobre as somas de verificação. Consulte os comentários para obter detalhes.  
  
 `dwByteOffset`  
 O número de bytes que a instrução é desde o início da linha de código.  
  
 `dwFlags`  
 O [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md) constante que especifica quais sinalizadores estão ativos.  
  
## <a name="remarks"></a>Comentários  
 Cada `DisassemblyData` estrutura descreve uma instrução de desmontagem. Uma matriz dessas estruturas é retornada do [leitura](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) método.  
  
 O [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) estrutura é usada para documentos com base em texto apenas. O intervalo de código de origem para essa instrução é preenchido somente para a primeira instrução gerada a partir de uma instrução ou uma linha, por exemplo, quando `dwByteOffset == 0`.  
  
 Para documentos que são não textuais, um contexto de documento pode ser obtido a partir do código e o `bstrDocumentUrl` campo deve ser um valor nulo. Se o `bstrDocumentUrl` campo é o mesmo que o `bstrDocumentUrl` campo anterior `DisassemblyData` elemento da matriz, em seguida, defina o `bstrDocumentUrl` com um valor nulo.  
  
 Se o `dwFlags` campo tem o `DF_DOCUMENT_CHECKSUM` sinalizador definido, em seguida, as informações de soma de verificação adicional seguem a cadeia de caracteres apontada pelo `bstrDocumentUrl` campo. Especificamente, após o terminador de cadeia de caracteres nula, existe segue um GUID que identifica o algoritmo de soma de verificação, que por sua vez é seguido por um valor de 4 bytes indicando o número de bytes em que a soma de verificação e o que por sua vez é seguido pelos bytes da soma de verificação. Veja o exemplo neste tópico sobre como codificar e decodificar esse campo em [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)].  
  
## <a name="example"></a>Exemplo  
 O `bstrDocumentUrl` campo pode conter informações adicionais que não seja uma cadeia de caracteres se o `DF_DOCUMENT_CHECKSUM` sinalizador está definido. O processo de criar e ler essa cadeia de caracteres codificada é bem simples no [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]. No entanto, em [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)], é outra questão. Para aqueles que estão curiosos, o exemplo a seguir mostra uma maneira de criar a cadeia de caracteres codificada de [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] e uma maneira para decodificar a cadeia de caracteres codificada em [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)].  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
namespace MyNamespace  
{
    class MyClass  
    {  
        string EncodeData(string documentString,  
                          Guid checksumGuid,  
                          byte[] checksumData)  
        {  
            string returnString = documentString;  
  
            if (checksumGuid == null || checksumData == null)  
            {  
                // Nothing more to do. Just return the string.  
                return returnString;  
            }  
  
            returnString += '\0'; // separating null value  
  
            // Add checksum GUID to string.  
            byte[] guidDataArray  = checksumGuid.ToByteArray();  
            int    guidDataLength = guidDataArray.Length;  
            IntPtr pBuffer        = Marshal.AllocCoTaskMem(guidDataLength);  
            for (int i = 0; i < guidDataLength; i++)  
            {  
                Marshal.WriteByte(pBuffer, i, guidDataArray[i]);  
            }  
            // Copy guid data bytes to string as wide characters.  
            // Assumption: sizeof(char) == 2.  
            for (int i = 0; i < guidDataLength / sizeof(char); i++)  
            {  
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));  
            }  
  
            // Add checksum count (a 32-bit value).  
            Int32 checksumCount = checksumData.Length;  
            Marshal.StructureToPtr(checksumCount, pBuffer, true);  
            for (int i = 0; i < sizeof(Int32) / sizeof(char); i++)  
            {  
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));  
            }  
  
            // Add checksum data.  
            pBuffer = Marshal.AllocCoTaskMem(checksumCount);  
            for (int i = 0; i < checksumCount; i++)  
            {  
                Marshal.WriteByte(pBuffer, i, checksumData[i]);  
            }  
            for (int i = 0; i < checksumCount / sizeof(char); i++)  
            {  
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));  
            }  
            Marshal.FreeCoTaskMem(pBuffer);  
  
            return returnString;  
        }  
  
        void DecodeData(    string encodedString,  
                        out string documentString,  
                        out Guid   checksumGuid,  
                        out byte[] checksumData)  
       {  
           documentString = String.Empty;  
           checksumGuid = Guid.Empty;  
           checksumData = null;  
  
           IntPtr pBuffer = Marshal.StringToBSTR(encodedString);  
           if (null != pBuffer)  
           {  
               int bufferOffset = 0;  
  
               // Parse string out.  String is assumed to be Unicode.  
               documentString = Marshal.PtrToStringUni(pBuffer);  
               bufferOffset += (documentString.Length + 1) * sizeof(char);  
  
               // Parse Guid out.  
               // Read guid bytes from buffer and store in temporary  
               // buffer that contains only the guid bytes. Then the  
               // Marshal.PtrToStructure() can work properly.  
               byte[] guidDataArray  = checksumGuid.ToByteArray();  
               int    guidDataLength = guidDataArray.Length;  
               IntPtr pGuidBuffer    = Marshal.AllocCoTaskMem(guidDataLength);  
               for (int i = 0; i < guidDataLength; i++)  
               {  
                   Marshal.WriteByte(pGuidBuffer, i,  
                                     Marshal.ReadByte(pBuffer, bufferOffset + i));  
               }  
               bufferOffset += guidDataLength;  
               checksumGuid = (Guid)Marshal.PtrToStructure(pGuidBuffer, typeof(Guid));  
               Marshal.FreeCoTaskMem(pGuidBuffer);  
  
              // Parse out the number of checksum data bytes (always 32-bit value).  
              int dataCount = Marshal.ReadInt32(pBuffer, bufferOffset);  
              bufferOffset += sizeof(Int32);  
  
              // Parse out the checksum data.  
              checksumData = new byte[dataCount];  
              for (int i = 0; i < dataCount; i++)  
              {  
                  checksumData[i] = Marshal.ReadByte(pBuffer, bufferOffset + i);  
              }  
           }  
       }  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [Leitura](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)   
 [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)   
 [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
