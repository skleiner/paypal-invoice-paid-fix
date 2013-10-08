paypal-invoice-paid-fix
=======================
Fix for when PayPal generates a message about an invoice is already paid.

two files to modify

*************************************************************************************************************************

catalog\includes\modules\payment\paypal_standard.php

change:

                          'invoice' => substr($cart_PayPal_Standard_ID, strpos($cart_PayPal_Standard_ID, '-')+1),
						  
to

                          'invoice' => 'A' .  substr($cart_PayPal_Standard_ID, strpos($cart_PayPal_Standard_ID, '-')+1),
						  
'A' can be any letter, such as 'B' or 'C' etc.

****************************************************************************************************************************
catalog\ext\modules\payment\paypal\standard_ipn.php

find:

    curl_close($ch);
  }
  
add this right after that code:

  $invoice_id = substr($HTTP_POST_VARS['invoice'],1);

  
then using search and replace change all subsequent instances in the existing code of 'invoice'

to 'invoice_id'

when done the only line that has 'invoice' in is what was added above

*****************************************************************************************************************************

good luck