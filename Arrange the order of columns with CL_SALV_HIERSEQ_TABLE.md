Here is a minimal program to display a hierarchical-sequential ALV list with the class `CL_SALV_HIERSEQ_TABLE`, and define the order of columns, here shown for `CURRCODE` of the master table `SCARR`.

Before running this program, the program [`SAPBC_DATA_GENERATOR`]() must be run to fill the tables `SCARR` and `SPFLI`.

```
SELECT * FROM scarr INTO TABLE @DATA(scarr_s).
SELECT * FROM spfli INTO TABLE @DATA(spfli_s).

cl_salv_hierseq_table=>factory(
  EXPORTING
    t_binding_level1_level2 = VALUE #( ( master = 'CARRID' slave = 'CARRID' ) )
  IMPORTING
    r_hierseq               = DATA(gr_hierseq)
  CHANGING
    t_table_level1          = scarr_s
    t_table_level2          = spfli_s ).

gr_hierseq->get_columns( 1 )->set_column_position( columnname = 'CURRCODE' position = 2 ).

gr_hierseq->display( ).
```
