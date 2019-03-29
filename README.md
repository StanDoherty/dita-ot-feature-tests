# dita-ot-feature-tests
This collection of sample files exercises features in DITA 1.3 as they are visible in a DITA-compliant editor (currently Oxygen Editor 21.0) and in DITA-OT output (currently dita-ot-3.3). 

Please feel free to download and test on your own.

If you want to update or augment what is here, please contact Stan Doherty at stan@modularwriting.com. Feedback and additional contributions are most welcome. 

## test_001: Changebar flagging in PDF output
*Goal*: The test_001 suite of files tests how to generate changebars in PDF output. 
*Results*: 
 * dita-ot-3.1.2 PDF: Fail - bundled Apache FOP processor does not currently support changebars.
 * dita-ot-3.2.0 PDF: Fail - bundled Apache FOP processor does not currently support changebars.
 * dita-ot-3.3.0 PDF: Fail - bundled Apache FOP processor does not currently support changebars.

## test_002: Image flagging in PDF and HTML5
*Goal*: The test_002 suite of files tests how to flag content with "start" and "end" images.  
*Results*:
 * dita-ot-3.x PDF: Pass
 * dita-ot-3.2.0 HTML5: Fail - with error
   [dita-ot-copy] Attempt to copy images\end_rev.jpg to 
   C:\git\dita-ot-feature-tests\output\html5\file:\C:\git\dita-ot-feature-tests\images\end_rev.jpg 
   using NIO Channels failed due to 'The filename, directory name, or volume label syntax is incorrect'.
   Falling back to streams.
   Error: The filename, directory name, or volume label syntax is incorrect
 * dita-ot-3.3.0 HTML5: Fail - with error
   [dita-ot-copy] Attempt to copy images\end_rev.jpg to C:\git\dita-ot-feature-tests\output\html5\file:\C:\git\dita-ot-feature-tests\images\end_rev.jpg using NIO Channels failed due to 'The filename, directory name, or volume label syntax is incorrect'.  Falling back to streams.
   Error: The filename, directory name, or volume label syntax is incorrect

## test_003: Content badging in PDF and HTML5
*Goal*: The test_003 suite of files tests how to use DITA flagging to insert content badges (icons+text) into generated content. 
*Results*: 
 * dita-ot-3.x PDF: Pass
 * dita-ot-3.x HTML5: Fail - with errors - see test_002
 

## test_004: Scoped key resolution in PDF and HTML5
*Goal*: The test_004 suite of files exercises the DITA 1.3 feature of scoped keys. 
*Results*: 
 * Unscoped (global) keys without any @keyscope definitions. 
   * Oxygen 21: Pass
   * dita-ot-3.x PDF: Pass
   * dita-ot-3.x HTML5: Pass 
 * Scoped key references using keyscope prefix, e.g. keyscope.keyname. 
   * Oxygen 21: Pass
   * dita-ot-3.x PDF: Pass
   * dita-ot-3.x HTML5: Pass 
 * Scoped key references with an inherited @keyscope from a branch map/topic (with NO mix of unscoped and scoped key definitions in the keyspace)using keyscope prefix, e.g. keyscope.keyname. 
   * Oxygen 21: Pass (with transient Java errors in the editor)
   * dita-ot-3.x PDF: Fail (inherited key values not in output) 
   * dita-ot-3.x HTML5: Fail (inherited key values not in output) 
 * Scoped key references with a mix of inherited @keyscopes defined in a branch map/topic AND unscoped key definitions in the keyspace). 
   * Oxygen 21: Fail (unscoped key values override branch-scoped values). No error.
   * dita-ot-3.x PDF: Fail (unscoped key values override branch-scoped values). No error. 
   * dita-ot-3.x HTML5: Fail (unscoped key values override branch-scoped values). No error. 
   TIP: Uncomment the unscoped key definition map.

## test_005: Branch filtering
*Goal*: The test_005 suite of files exercises the DITA 1.3 feature of branch filtering. There is one shared topic with separate paragraphs tagged with @product="red", @product="blue", and @product="green". This topic is built four times -- once without any ditaval filtering, and three times with specific red, green, and blue <ditavalref> references. There should be four different versions of the same shared topic in the PDF and HTML5 output. 
*Results*:   
 * PDF works as advertised. 
 * HTML5 works as advertised. 
 

 
