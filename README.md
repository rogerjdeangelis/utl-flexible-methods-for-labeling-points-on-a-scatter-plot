# utl-flexible-methods-for-labeling-points-on-a-scatter-plot
utl-flexible-methods-for-labeling-points-on-a-scatter-plot

    Flexible methods for labeling points on a scatter plot

        Three Solutions

               a. Ascii plot
               b. SGplot
               c. Gplot

    This is worth a reminder

    gplot graph
    https://tinyurl.com/wqj4xu7
    https://github.com/rogerjdeangelis/utl-flexible-methods-for-labeling-points-on-a-scatter-plot/blob/master/gplot_scatter.png

    sgplot graph
    https://tinyurl.com/tuf8gvl
    https://github.com/rogerjdeangelis/utl-flexible-methods-for-labeling-points-on-a-scatter-plot/blob/master/sgplot_scattert.pdf

    github
    https://tinyurl.com/vta6wzo
    https://github.com/rogerjdeangelis/utl-flexible-methods-for-labeling-points-on-a-scatter-plot

    SAS Forum
    https://tinyurl.com/rg9h728
    https://communities.sas.com/t5/SAS-Programming/How-to-label-some-points-in-a-scatter-plot-with-a-character-name/m-p/610651

    Draycut
    https://communities.sas.com/t5/user/viewprofilepage/user-id/31304

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
       input name $ X Y;
    cards4;
    Ann 1 1
    Barb 2 2
    Cat 3 3
    Doug 4 4
    Ed 5 5
    Fran 6 6
    Gary 7 7
    Hal 8 8
    Izy 9 9
    Joan 10 10
    Kate 11 11
    ;;;;
    run;quit;

     WORK.HAVE total obs=11

      NAME     X     Y

      Ann      1     1
      Barb     2     2
      Cat      3     3
      Doug     4     4
      Ed       5     5
      Fran     6     6
      Gary     7     7
      Hal      8     8
      Izy      9     9
      Joan    10    10
      Kate    11    11

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    gplot graph
    https://tinyurl.com/wqj4xu7

    sgplot graph
    https://tinyurl.com/tuf8gvl

    options ls=64 ps=32;
    proc plot data=have;
      plot y*x='*' $ name/box;
    run;quit;


                Plot of Y*X$NAME.  Symbol used is '*'.


           1    2    3    4    5    6    7    8    9   10   11
        ---+----+----+----+----+----+----+----+----+----+----+---
      Y |                                                       |
     11 +                                               Kate *  + 11
        |                                                       |
     10 +                                               * Joan  + 10
        |                                                       |
      9 +                                          * Izy        +  9
        |                                                       |
      8 +                                     * Hal             +  8
        |                                                       |
      7 +                                * Gary                 +  7
        |                                                       |
      6 +                           * Fran                      +  6
        |                                                       |
      5 +                      * Ed                             +  5
        |                                                       |
      4 +                 * Doug                                +  4
        |                                                       |
      3 +            * Cat                                      +  3
        |                                                       |
      2 +       * Barb                                          +  2
        |                                                       |
      1 +  * Ann                                                +  1
        |                                                       |
        ---+----+----+----+----+----+----+----+----+----+----+---
           1    2    3    4    5    6    7    8    9   10   11

                                    X
    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __  ___
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/

      __ _      __ _ ___  ___(_|_)  _ __ | | ___ | |_
     / _` |    / _` / __|/ __| | | | '_ \| |/ _ \| __|
    | (_| |_  | (_| \__ \ (__| | | | |_) | | (_) | |_
     \__,_(_)  \__,_|___/\___|_|_| | .__/|_|\___/ \__|
                                   |_|
    ;

    data have;
       input name $ X Y;
    cards4;
    Ann 1 1
    Barb 2 2
    Cat 3 3
    Doug 4 4
    Ed 5 5
    Fran 6 6
    Gary 7 7
    Hal 8 8
    Izy 9 9
    Joan 10 10
    Kate 11 11
    ;;;;
    run;quit;

    *_                        _       _
    | |__     ___  __ _ _ __ | | ___ | |_
    | '_ \   / __|/ _` | '_ \| |/ _ \| __|
    | |_) |  \__ \ (_| | |_) | | (_) | |_
    |_.__(_) |___/\__, | .__/|_|\___/ \__|
                  |___/|_|
    ;

    options ls=64 ps=32;
    proc plot data=have;
      plot y*x='*' $ name/box;
    run;quit;

    ods graphics on / reset width=10in height=8in;
    options orientation=landscape;
    ods pdf file="d:/pdf/scattert.pdf";

    proc sgplot data=have;
         scatter x=x y=y / datalabel=name
               DATALABELATTRS=(Color=Black Family="Arial" Size=12);
    run;quit;
    ods graphics off;
    ods pdf close;

    *                     _       _
      ___      __ _ _ __ | | ___ | |_
     / __|    / _` | '_ \| |/ _ \| __|
    | (__ _  | (_| | |_) | | (_) | |_
     \___(_)  \__, | .__/|_|\___/ \__|
              |___/|_|
    ;


    data labels;
      length text $4;
      retain xsys ysys '2' hsys '3' function 'label' position '2' style '"calibri"';
      set have;
       text = name;
    run;quit;

    filename outfile "d:/png/scatter.png";
    goptions
          reset=global
          gsfmode = replace
          device  = png
          gsfname = outfile
          vsize=8in
          hsize=10in
          htext=12pt ;
    run;quit;

    symbol v=dot h=2;
    proc gplot data=have anno=labels;
    plot y*x;
    run;quit;


