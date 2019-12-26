This explains how to transport a transport from one ABAP-based system to another, without using the SAP command `tp` (via command line).

When a transport request <SID>K9<NUMBER> is released, two files are written to the directory "DIR_TRANS" of the application server, that you may browse with the transaction code `AL11`, they are placed in two distinct subdirectories and named `cofiles/K9<NUMBER>.<SID>` and `data/R9<NUMBER>.<SID>`.
* Example: if the transport request is X20K900237, the two files are `cofiles/K900237.X20` and `data/R900237.X20`.

Copy these files to the application server where you want to import this transport request.
* If needed, you may use your laptop to store temporarily the files as a bridge between the two application servers. If you use SAP ERP or S/4HANA, you may use the transaction codes CG3Y and CG3Z to do that. If you know both the administrator user and password, you may use a FTP client to access the file system of the application server. If you're an ABAP developer you may also create an ABAP program to [[read or write the files|]].

Start the transaction STMS, open the import queue of the system in which you want to import the transport request; in the menu Extras – Other requests – Add, enter the ID of the transport request.

Refresh the list of transport requests in the import queue, you see the new transport request, click Import.

Sources:
* https://blogs.sap.com/2012/05/07/how-to-manually-import-transports-into-sap-without-using-command-line-tp/
* https://blogs.sap.com/2013/08/24/how-to-download-upload-transport-request-from-to-a-server/
* https://blogs.sap.com/2016/05/12/step-by-step-instruction-on-how-to-transfer-request-to-external-system/
* https://blogs.sap.com/2019/08/19/upload-a-sap-transport-request-made-easy/
* https://blogs.sap.com/2019/12/13/download-and-upload-the-abap-code/
