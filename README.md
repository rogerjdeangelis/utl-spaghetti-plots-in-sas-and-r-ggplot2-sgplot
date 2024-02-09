# utl-spaghetti-plots-in-sas-and-r-ggplot2-sgplot
Spaghetti plots in sas and r ggplot2 sgplot 
    %let pgm=utl-spaghetti-plots-in-sas-and-r-ggplot2-sgplot;

    Spaghetti plots in sas and r ggplot2 sgplot

      SOLUTIONS

         1 sas sgplot
         2 r ggplot2

    github
    http://tinyurl.com/9z45v2js
    https://github.com/rogerjdeangelis/utl-spaghetti-plots-in-sas-and-r-ggplot2-sgplot

    for output graphs see

    http://tinyurl.com/347trda6
    https://github.com/rogerjdeangelis/utl-spaghetti-plots-in-sas-and-r-ggplot2-sgplot/blob/main/spaghetti_sas.pdf

    http://tinyurl.com/mun5h2sh
    https://github.com/rogerjdeangelis/utl-spaghetti-plots-in-sas-and-r-ggplot2-sgplot/blob/main/spaghetti_wps.pdf

    Also at

    SAS
    https://www.dropbox.com/s/u8x3ace457kwfxj/spaghetti_sas.pdf?dl=0
    R
    https://www.dropbox.com/s/ty8vcpqk9arcgbx/spaghetti_wps.pdf?dl=0

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /************************************************************************************************************************/
    /*                            |                                        |                                                */
    /*            INPUT           |             PROCESS                    |                    OUTPUT                      */
    /*                            |                                        |                                                */
    /*  TRT_                      |                                        |                                                */
    /* GROUP TIME SUBJECT RESULTS | SAS SGLOT                              |                    TIME                        */
    /*                            |                                        |         2         4         6         8        */
    /*   1     2    100      20   | proc sgplot data=sd1.have;             |        -+---------+---------+---------+---     */
    /*   1     4    100      30   | title "Study Results Treatment Group"; |     50 +                            /*   + 50  */
    /*   1     6    100      35   | series x=time y=results/ group=subject |        |                    Time1  /     |     */
    /*   1     8    100      50   | grouplc=trt_group name="grouping";     |        |               *-----*----*      |     */
    /*   1     2    200      40   | keylegend "grouping" / type=linecolor; |     45 + \  Time 5    /               *  + 45  */
    /*  ....                      |                                        |        |  \          /               /   |     */
    /*                            |  R GGPLOT2                             |        |   \        /               /    |     */
    /*                            |  =========                             |     40 +    \      /               /     + 40  */
    /*                            |  ggplot(have, aes(x=TIME, y=RESULTS    |        |     \    /               /      |     */
    /*                            |     ,color=factor(SUBJECT))) +         |  R     |      \  /      Time 2   /       |     */
    /*                            |      geom_line() + geom_point() +      |  E  35 +*------\*   +-----------+      + + 35  */
    /*                            |      theme_bw();                       |  S     |        \  /   *\     *\      /  |     */
    /*                            |                                        |  U     |+ Time 4 \/   /  \   /  \    /   |     */
    /*                            |                                        |  L  30 + \       /\  /  + \ /    \  /    + 30  */
    /*                            |                                        |  T     |  \     /  */  / \ *      \/     |     */
    /*                            |                                        |  S     |   \   /      /   \       /\     |     */
    /*                            |                                        |    25 +    \ /      /     \     /  \    + 25   */
    /*                            |                                        |        |     /\     /       \   /    \   |     */
    /*                            |                                        |        |    /  \   /  Time 3 \ /      \  |     */
    /*                            |                                        |     20 +   /    \ /           +        * + 20  */
    /*                            |                                        |        |  /      +                       |     */
    /*                            |                                        |        | /                               |     */
    /*                            |                                        |     15 +/                                + 15  */
    /*                            |                                        |        -+---------+---------+---------+---     */
    /*                            |                                        |         2         4         6         8        */
    /*                            |                                        |                                                */
    /*                            |                                        |                   TIME                         */
    /*                            |                                        |                                                */
    /************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */


    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
    infile ft15f001;
    input trt_group time subject results @@;
    parmcards4;
    1 2 100 20 1 4 100 30 1 6 100 35 1 8 100 50
    1 2 200 40 1 4 200 25 1 6 200 40 1 8 200 30
    1 2 300 25 1 4 300 40 1 6 300 45 1 8 300 55
    2 2 400 15 2 4 400 35 2 6 400 50 2 8 400 45
    2 2 500 35 2 4 500 35 2 6 500 20 2 8 500 35
    ;;;;
    run;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  d:/sd1/have.sas7bdat total obs=20                                                                                     */
    /*                                                                                                                        */
    /*          TRT_                                                                                                          */
    /*  Obs    GROUP    TIME    SUBJECT    RESULTS                                                                            */
    /*                                                                                                                        */
    /*    1      1        2       100         20                                                                              */
    /*    2      1        4       100         30                                                                              */
    /*    3      1        6       100         35                                                                              */
    /*    4      1        8       100         50                                                                              */
    /*    5      1        2       200         40                                                                              */
    /*  ...                                                                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                                   _       _
    / |  ___  __ _ ___   ___  __ _ _ __ | | ___ | |_
    | | / __|/ _` / __| / __|/ _` | `_ \| |/ _ \| __|
    | | \__ \ (_| \__ \ \__ \ (_| | |_) | | (_) | |_
    |_| |___/\__,_|___/ |___/\__, | .__/|_|\___/ \__|
                             |___/|_|
    */

    options orientation=portrait;
    ods graphics on / height=9in width=7in;
    ods pdf file="d:/pdf/spaghetti_sas.pdf";
    proc sgplot data=sd1.have;
    title "Study Results by Treatment Group";
    series x=time y=results/ group=subject
    grouplc=trt_group name="grouping";
    keylegend "grouping" / type=linecolor;
    run;quit;
    ods pdf close;

    /*___                             _       _   ____
    |___ \   _ __    __ _  __ _ _ __ | | ___ | |_|___ \
      __) | | `__|  / _` |/ _` | `_ \| |/ _ \| __| __) |
     / __/  | |    | (_| | (_| | |_) | | (_) | |_ / __/
    |_____| |_|     \__, |\__, | .__/|_|\___/ \__|_____|
                    |___/ |___/|_|
    */

    %utl_rbegin;
    parmcards4;
    library(ggplot2);
    library(haven);
    have<-read_sas("d:/sd1/have.sas7bdat");
    pdf("d:/pdf/spaghetti_r.pdf");
    ggplot(have, aes(x=TIME, y=RESULTS, color=factor(SUBJECT))) +
      geom_line() + geom_point() +
      theme_bw();
    ;;;;
    %utl_rend;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  d:/sd1/have.sas7bdat total obs=20                                                                                     */
    /*                                                                                                                        */
    /*          TRT_                                                                                                          */
    /*  Obs    GROUP    TIME    SUBJECT    RESULTS                                                                            */
    /*                                                                                                                        */
    /*    1      1        2       100         20                                                                              */
    /*    2      1        4       100         30                                                                              */
    /*    3      1        6       100         35                                                                              */
    /*    4      1        8       100         50                                                                              */
    /*    5      1        2       200         40                                                                              */
    /*  ...                                                                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
