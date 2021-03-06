# utl_referencing_a_variable_from_another_dataset_in_a_macro
Referencing a variable from another dataset in a macro.    Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Referencing a variable from another dataset in a macro

    Print sashelp.class reports for each age in a control dataset

    github
    https://tinyurl.com/y7fd5bt3
    https://github.com/rogerjdeangelis/utl_referencing_a_variable_from_another_dataset_in_a_macro

    https://tinyurl.com/y7fz64kd
    https://communities.sas.com/t5/Base-SAS-Programming/referencing-a-variable-from-another-dataset-in-a-macro/m-p/470197


    INPUT  (macro and control dataset wit a list of ages)
    =====

     1, control datsset wil a list of ages
     2. sashelp.class
     3. prtx macro


     WORK.HAVE total obs=5

      Obs    AGE

       1      11
       2      12
       3      13
       4      14
       5      15

     %macro prtx(age);

        proc print data=sashelp.class(where=(age=&age));
        title "Report for age &age";

        run;quit;
     %mend prtx;


     SAMPLE OUTPUT

     Up to 40 obs from log total obs=5

     Obs    AGE    RC     STATUS

      1      11     0    Completed
      2      12     0    Completed
      3      13     0    Completed
      4      14     0    Completed
      5      15     0    Completed

     Report for age 11

     Obs     NAME     SEX    AGE    HEIGHT    WEIGHT

      11    Joyce      F      11     51.3      50.5
      18    Thomas     M      11     57.5      85.0

     ...

     Report for age 15

     Obs    NAME       SEX    AGE    HEIGHT    WEIGHT

       8    Janet       F      15     62.5      112.5
      14    Mary        F      15     66.5      112.0
      17    Ronald      M      15     67.0      133.0
      19    William     M      15     66.5      112.0


    PROCESS
    =======

      data log;

        set have;
        call symputx('age',age);

        rc=dosubl('
           %prtx(&age);
        ');

        if rc=0 then status="Completed";
        else status="Failed";

      run;quit;


    OUTPUT
    ======


     Up to 40 obs from log total obs=5

     Obs    AGE    RC     STATUS

      1      11     0    Completed
      2      12     0    Completed
      3      13     0    Completed
      4      14     0    Completed
      5      15     0    Completed

     Report for age 11

     Obs     NAME     SEX    AGE    HEIGHT    WEIGHT

      11    Joyce      F      11     51.3      50.5
      18    Thomas     M      11     57.5      85.0

     ...

     Report for age 15

     Obs    NAME       SEX    AGE    HEIGHT    WEIGHT

       8    Janet       F      15     62.5      112.5
      14    Mary        F      15     66.5      112.0
      17    Ronald      M      15     67.0      133.0
      19    William     M      15     66.5      112.0

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;


    data have;
     do age=11 to 15;
       output;
     end;
    run;quit;

     %macro prtx(age);

        proc print data=sashelp.class(where=(age=&age));
        title "Report for age &age";

        run;quit;
     %mend prtx;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    see process

