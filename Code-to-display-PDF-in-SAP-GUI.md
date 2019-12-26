The principle is to use the [[HTML Viewer]], a Windows control provided with SAP GUI for Windows, which is connected to a simplified but powerful browser provided with Windows (Microsoft).

# Smallest use case
Display a small PDF ([[Code of the smallest PDF (binary format)]]) [[without dynpro|Trick to use Control Framework "without dynpro"]]:
```
REPORT.
" paste here the code of the class lcl_smallest_pdf_binary
" paste here the code of the class lcl_pdf_in_sap_gui
PARAMETERS dummy.
AT SELECTION-SCREEN OUTPUT.
  lcl_pdf_in_sap_gui=>show( container = cl_gui_container=>screen0 pdf = lcl_smallest_pdf_binary=>get( ) ).
```

# Code of class lcl_pdf_in_sap_gui
```
CLASS lcl_pdf_in_sap_gui DEFINITION.
  PUBLIC SECTION.
    CLASS-METHODS show IMPORTING container TYPE REF TO cl_gui_container pdf TYPE xstring.
ENDCLASS.
CLASS lcl_pdf_in_sap_gui IMPLEMENTATION.
  METHOD show.

    DATA(lo_pdf_object) = NEW cl_gui_html_viewer( parent = cl_gui_container=>screen0 ).

    DATA(lt_solix) = cl_bcs_convert=>xstring_to_solix( pdf ).
    DATA(lv_size) = xstrlen( pdf ).
    DATA(lv_url) = VALUE char255( ).
    lo_pdf_object->load_data(
      EXPORTING
        type                   = 'application'  " 'text'
        subtype                = 'pdf'          " 'HTML'
        size                   = lv_size
      IMPORTING
        assigned_url           = lv_url
      CHANGING
        data_table             = lt_solix ).

    lo_pdf_object->show_data( lv_url ).

  ENDMETHOD.
ENDCLASS.
```
