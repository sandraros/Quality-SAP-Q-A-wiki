This is the minimal program to display an ALV grid control in SAP GUI (ALV grid displayed inside a container, not fullscreen), with the counter of rows.

The counter of rows is automatically updated if some rows are filtered or if sorting and subtotal columns are changed.

It's possible to hide the counter column by clicking the button Aggregations > Count, and get the counter back by clicking it again.

```
DATA go_alv TYPE REF TO cl_gui_alv_grid.
TYPES: BEGIN OF ty_sflight.
        INCLUDE TYPE sflight.
        TYPES: count TYPE i,
       END OF ty_sflight.
DATA gt_sflight TYPE TABLE OF ty_sflight.
DATA gt_fieldcat TYPE TABLE OF lvc_s_fcat.

PARAMETERS dummy.

AT SELECTION-SCREEN OUTPUT.
  IF go_alv IS NOT BOUND.
    CALL FUNCTION 'LVC_FIELDCATALOG_MERGE'
      EXPORTING
        i_structure_name       = 'SFLIGHT'
      CHANGING
        ct_fieldcat            = gt_fieldcat
      EXCEPTIONS
        inconsistent_interface = 1
        program_error          = 2.
    APPEND VALUE #( fieldname = 'COUNT' col_pos = 4 no_out = ' ' ) TO gt_fieldcat.
    CREATE OBJECT go_alv
      EXPORTING
        i_parent = cl_gui_container=>screen0.
    SELECT * FROM sflight INTO CORRESPONDING FIELDS OF TABLE gt_sflight.
    go_alv->set_table_for_first_display(
        EXPORTING
          is_layout       = VALUE #( countfname = 'COUNT' )
        CHANGING
          it_outtab       = gt_sflight
          IT_FIELDCATALOG = gt_fieldcat ).
  ENDIF.
```
