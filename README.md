# dita-ot-feature-tests
This collection of sample files exercises features in DITA 1.3 as they are visible in a DITA-compliant editor (currently Oxygen Editor 21.0) and in DITA-OT output (currently dita-ot-3.3). 

Please download and test on your own.

If you want to update or augment what is here, please contact Stan Doherty at stan@modularwriting.com. Feedback and additional contributions are most welcome. 

## test_001: Changebar flagging in PDF output
*Goal*: The test_001 suite of files tests how to generate changebars in PDF output. NOTE: The DITA0OT documentation is now explicit about changebars not being supported with OOTB DITA-OT.
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
 
## test_006: Multiple DITAVALs on command line
*Goal*: The test_006 suite of files exercises the DITA-OT command line option if specifying multiple DITAVAL files for the --filter argument.



MacOS and Linux require the colon (:) without quotation marks. 

*Results*:   
 * On Windows - success. Each --filter value (DITAVAL file) requires a semicolon (;) separator character AND (undocumented) surrounding quotation marks.  

```c:\dita-ot\bin\dita --input=./test_006_cli-ditavals.ditamap --format=html5 --output=output\html5 --filter="test_006_cli-ditavals_exclude-platform-red.ditaval;test_006_cli-ditavals_exclude-product-green.ditaval;test_006_cli-ditavals_exclude-audience-blue.ditaval"```

 
 * On Linux/MacOS - success. 

```./dita --input=./test_006_cli-ditavals.ditamap --format=html5 --output=output\html5 --filter=test_006_cli-ditavals_exclude-platform-red.ditaval;test_006_cli-ditavals_exclude-product-green.ditaval;test_006_cli-ditavals_exclude-audience-blue.ditaval```


## test_007: Prism-JS syntax highlighting for codeblocks
*Goal*: The test_007 exercises the Prism-JS DITA-OT plug-in. Once you have installed the plug-in, you can use the @outputclass attribute on &lt;codeblocks> to identify the syntax of that code sample. When you build PDF or HTML subsequently, the code within that &lt;codeblock> reflects basic industry highlighting. 
*Results*:   
 * The unmodified plug-in supports HTML. XML, CSS, JavaScript, and C syntax highlighting for both PDF2 and HTML5 transforms. 
 * A customized version of the plug-in is integrated with Oxygen and offers numerous other syntax options (provided you build through Oxygen's vesion of the DITA-OT). 
 
## test_011: Link crawl
Write-up forthcoming

## test_012: Extended codeblock processing
Write-up forthcoming
