---
title: NumericScale y Precision propiedades (VC ++) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- NumericScale property [ADO], VC++ example
- Precision property [ADO], VC++ example
ms.assetid: 55d91ba8-4d80-4df6-af8e-060a19ddc138
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70a751db424cec07a0ac617b3620316a07936400
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917962"
---
# <a name="numericscale-and-precision-properties-example-vc"></a>Ejemplo de las propiedades NumericScale y Precision (VC ++)
Este ejemplo se usa el [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) y [precisión](../../../ado/reference/ado-api/precision-property-ado.md) propiedades para mostrar la escala numérica y la precisión de los campos de la ***descuentos*** tabla de la  ***Pubs*** base de datos.  
  
```cpp
// BeginNumericScaleCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void NumericScaleX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   NumericScaleX();  
   ::CoUninitialize();  
}  
  
void NumericScaleX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace  
   _RecordsetPtr pRstDiscounts = NULL;  
   FieldsPtr fldTemp = NULL;  
  
   // Define Other Variables  
   _variant_t Index;  
   Index.vt = VT_I2;  
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open recordset.  
      TESTHR(pRstDiscounts.CreateInstance(__uuidof(Recordset)));  
      pRstDiscounts->Open("discounts", strCnn, adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      // Display numeric scale and precision of numeric and small integer fields.  
      fldTemp = pRstDiscounts->GetFields();  
  
      for (short int intLoop = 0 ; intLoop < (int)fldTemp->GetCount() ; intLoop++ ) {  
         Index.iVal = intLoop;  
  
         if ( (fldTemp->GetItem(Index)->Type == adNumeric) ||   
            (fldTemp->GetItem(Index)->Type == adSmallInt) ) {   
            printf("Field: %s\n" , (LPCSTR)fldTemp->GetItem(Index)->GetName());  
            printf("Numeric scale: %d\n", fldTemp->GetItem(Index)->GetNumericScale());  
            printf("Precision: %d\n", fldTemp->GetItem(Index)->GetPrecision());  
         }  
      }  
   }  
   catch(_com_error &e) {      
      // Display errors, if any. Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstDiscounts->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
  
   // Clean up objects before exit.  
   if (pRstDiscounts)  
      if (pRstDiscounts->State == adStateOpen)  
         pRstDiscounts->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [NumericScale (propiedad, ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)   
 [Propiedad Precision (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
