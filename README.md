# utl_clinical_n_percent_crosstab
Minimum lines of code to produce a clinical N(PCT) crosstab report for demographic variables.

    ```  N(PCT) demographic crosstab - How to stack demographic variables                                                                                             ```
    ```                                                                                                                                                               ```
    ```     for more flexible solutuons see                                                                                                                           ```
    ```     https://github.com/rogerjdeangelis/utl_flexible_proc_report                                                                                               ```
    ```     https://github.com/rogerjdeangelis/utl_clinical_report                                                                                                    ```
    ```     https://github.com/rogerjdeangelis/utl_crosstab_dataset_3_lines_of_code                                                                                   ```
    ```                                                                                                                                                               ```
    ```      N Percent crosstab in a minimum lines of code(LOC).                                                                                                      ```
    ```      Demographic table                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```           MAJOR        MINOR       VACINATED    NOT_VACINATED  TOTAL                                                                                          ```
    ```                                                                                                                                                               ```
    ```           AGEGROUP     18-39       9(64%)       5(36%)         14(100%)                                                                                       ```
    ```                        40-64       1(33%)       2(67%)         3(100%)                                                                                        ```
    ```                        40-65       2(67%)       1(33%)         3(100%)                                                                                        ```
    ```                        40-66       1(33%)       2(67%)         3(100%)                                                                                        ```
    ```                        65+         4(44%)       5(56%)         9(100%)                                                                                        ```
    ```                                                                                                                                                               ```
    ```           ETHNICITY    Hispanic    1(10%)       9(90%)         10(100%)                                                                                       ```
    ```                                                                                                                                                               ```
    ```      WORKING CODE                                                                                                                                             ```
    ```      ============                                                                                                                                             ```
    ```        proc transpose data=have out=havxpo;                                                                                                                   ```
    ```           by patient_id Vaccine_Flag;                                                                                                                         ```
    ```           var Race Gender Ethnicity AgeGroup;                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```        WORK.HAVXPO total obs=128                                                                                                                              ```
    ```        PATIENT_    VACCINE_                                                                                                                                   ```
    ```          ID         FLAG      _NAME_       COL1                                                                                                               ```
    ```                                                                                                                                                               ```
    ```           1           1       RACE         AmericanIndian                                                                                                     ```
    ```           1           1       GENDER       F                                                                                                                  ```
    ```           1           1       ETHNICITY    Hispanic                                                                                                           ```
    ```           1           1       AGEGROUP     18-39                                                                                                              ```
    ```           2           0       RACE         Asian                                                                                                              ```
    ```           2           0       GENDER       M                                                                                                                  ```
    ```           2           0       ETHNICITY    Non-Hispanic                                                                                                       ```
    ```                                                                                                                                                               ```
    ```        proc corresp data=havadd all dimens=1 print=both;                                                                                                      ```
    ```        tables   mjrMnr, vaccine_flag;                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```        mjrMnr=catx('@',_name_,col1);                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```        XPO total obs=18                                                                                                                                       ```
    ```        Obs    LABEL              _0    _1     _0pct      _1pct    SUM                                                                                         ```
    ```                                                                                                                                                               ```
    ```          1    AGEGROUP@18-39      9     5    64.286     35.714     14                                                                                         ```
    ```          2    AGEGROUP@40-64      1     2    33.333     66.667      3                                                                                         ```
    ```          3    AGEGROUP@40-65      2     1    66.667     33.333      3                                                                                         ```
    ```         ...                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```        Vacinated     = cats(put(_0,4.),'(',put(coalesce(_0pct,0),3.),'%)');                                                                                   ```
    ```        Not_vacinated = cats(put(_1,4.),'(',put(coalesce(_1pct,0),3.),'%)');                                                                                   ```
    ```        Total         = cats(put(sum,4.),'(100%)');                                                                                                            ```
    ```        Major=scan(label,1,'@');                                                                                                                               ```
    ```        Minor=scan(label,2,'@');                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```        Up to 40 obs from havNpc total obs=17                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```                                                   NOT_                                                                                                        ```
    ```        Obs    MAJOR        MINOR   VACINATED    VACINATED     TOTAL                                                                                           ```
    ```                                                                                                                                                               ```
    ```          1    AGEGROUP     18-39    9(64%)       5(36%)      14(100%)                                                                                         ```
    ```          2    AGEGROUP     40-64    1(33%)       2(67%)      3(100%)                                                                                          ```
    ```          3    AGEGROUP     40-65    2(67%)       1(33%)      3(100%)                                                                                          ```
    ```          4    AGEGROUP     40-66    1(33%)       2(67%)      3(100%)                                                                                          ```
    ```                                                                                                                                                               ```
    ```        proc report data=havNpc nowd;                                                                                                                          ```
    ```          cols Major Minor Vacinated Not_vacinated Total;                                                                                                      ```
    ```          define major / order;                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```           MAJOR        MINOR       VACINATED    NOT_VACINATED  TOTAL                                                                                          ```
    ```                                                                                                                                                               ```
    ```           AGEGROUP     18-39       9(64%)       5(36%)         14(100%)                                                                                       ```
    ```                        40-64       1(33%)       2(67%)         3(100%)                                                                                        ```
    ```                        40-65       2(67%)       1(33%)         3(100%)                                                                                        ```
    ```                        40-66       1(33%)       2(67%)         3(100%)                                                                                        ```
    ```                        65+         4(44%)       5(56%)         9(100%)                                                                                        ```
    ```           ETHNICITY    Hispanic    1(10%)       9(90%)         10(100%) .                                                                                     ```
    ```                        NA          6(67%)       3(33%)         9(100%)                                                                                        ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/z5PzGH                                                                                                                                        ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/How-to-stack-summary-table/m-p/406256                                                                    ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```    WORK.HAVE total obs=32                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```     PATIENT_                                                              FOLLOWUP_    VACCINE_                                                               ```
    ```        ID     RACE              GENDER    ETHNICITY       AGEGROUP           FLAG        FLAG                                                                 ```
    ```                                                                                                                                                               ```
    ```         1     AmericanIndian      F       Hispanic         18-39              1            1                                                                  ```
    ```         2     Asian               M       Non-Hispanic     18-39              0            0                                                                  ```
    ```         3     Black               F       NA               40-64              0            0                                                                  ```
    ```         4     White               NA      Hispanic         65+                1            1                                                                  ```
    ```         5     Multi-Race          F       Non-Hispanic     18-39              0            0                                                                  ```
    ```         6     NA                  M       Hispanic         18-39              1            1                                                                  ```
    ```         7     AmericanIndian      F       Non-Hispanic     40-65              0            1                                                                  ```
    ```         8     Asian               F       NA               65+                1            1                                                                  ```
    ```       ...                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```  WANT                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```      MAJOR        MINOR               VACINATED    NOT_VACINATED  TOTAL                                                                                       ```
    ```                                                                                                                                                               ```
    ```      AGEGROUP     18-39               9(64%)       5(36%)         14(100%)                                                                                    ```
    ```                   40-64               1(33%)       2(67%)         3(100%)                                                                                     ```
    ```                   40-65               2(67%)       1(33%)         3(100%)                                                                                     ```
    ```                   40-66               1(33%)       2(67%)         3(100%)                                                                                     ```
    ```                   65+                 4(44%)       5(56%)         9(100%)                                                                                     ```
    ```      ETHNICITY    Hispanic            1(10%)       9(90%)         10(100%)                                                                                    ```
    ```                   NA                  6(67%)       3(33%)         9(100%)                                                                                     ```
    ```                   Non-Hispanic        10(77%)      3(23%)         13(100%)                                                                                    ```
    ```      GENDER       F                   13(68%)      6(32%)         19(100%)                                                                                    ```
    ```                   M                   4(40%)       6(60%)         10(100%)                                                                                    ```
    ```                   NA                  0(0%)        3(100%)        3(100%)                                                                                     ```
    ```      RACE         AmericanIndian      5(71%)       2(29%)         7(100%)                                                                                     ```
    ```                   Asian               4(57%)       3(43%)         7(100%)                                                                                     ```
    ```                   Black               5(56%)       4(44%)         9(100%)                                                                                     ```
    ```                   Multi-Race          3(100%)      0(0%)          3(100%)                                                                                     ```
    ```                   NA                  0(0%)        3(100%)        3(100%)                                                                                     ```
    ```                   White               0(0%)        3(100%)        3(100%)                                                                                     ```
    ```                                                                                                                                                               ```
    ```  *                _                _       _                                                                                                                  ```
    ```   _ __ ___   __ _| | _____      __| | __ _| |_ __ _                                                                                                           ```
    ```  | '_ ` _ \ / _` | |/ / _ \    / _` |/ _` | __/ _` |                                                                                                          ```
    ```  | | | | | | (_| |   <  __/   | (_| | (_| | || (_| |                                                                                                          ```
    ```  |_| |_| |_|\__,_|_|\_\___|    \__,_|\__,_|\__\__,_|                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data have;                                                                                                                                                   ```
    ```     informat Race Gender Ethnicity AgeGroup $24.;                                                                                                             ```
    ```     input patient_ID Race Gender Ethnicity AgeGroup Followup_Flag Vaccine_Flag;                                                                               ```
    ```  cards4;                                                                                                                                                      ```
    ```  1 AmericanIndian F Hispanic 18-39 1 1                                                                                                                        ```
    ```  2 Asian M Non-Hispanic 18-39 0 0                                                                                                                             ```
    ```  3 Black F NA 40-64 0 0                                                                                                                                       ```
    ```  4 White NA Hispanic 65+ 1 1                                                                                                                                  ```
    ```  5 Multi-Race F Non-Hispanic 18-39 0 0                                                                                                                        ```
    ```  6 NA M Hispanic 18-39 1 1                                                                                                                                    ```
    ```  7 AmericanIndian F Non-Hispanic 40-65 0 1                                                                                                                    ```
    ```  8 Asian F NA 65+ 1 1                                                                                                                                         ```
    ```  9 Black M Non-Hispanic 18-39 0 1                                                                                                                             ```
    ```  10 AmericanIndian F NA 18-39 1 0                                                                                                                             ```
    ```  11 Asian M Hispanic 40-66 1 0                                                                                                                                ```
    ```  12 Black F Non-Hispanic 65+ 0 1                                                                                                                              ```
    ```  13 Black F NA 40-64 0 1                                                                                                                                      ```
    ```  14 White NA Hispanic 65+ 1 1                                                                                                                                 ```
    ```  15 Multi-Race F Non-Hispanic 18-39 0 0                                                                                                                       ```
    ```  16 NA M Hispanic 18-39 1 1                                                                                                                                   ```
    ```  17 AmericanIndian F Non-Hispanic 40-65 0 0                                                                                                                   ```
    ```  18 Asian F NA 65+ 1 0                                                                                                                                        ```
    ```  19 Black M Non-Hispanic 18-39 0 0                                                                                                                            ```
    ```  20 AmericanIndian F NA 18-39 0 0                                                                                                                             ```
    ```  21 Asian M Hispanic 40-66 1 1                                                                                                                                ```
    ```  22 Black F Non-Hispanic 65+ 0 0                                                                                                                              ```
    ```  23 Black F NA 40-64 0 1                                                                                                                                      ```
    ```  24 White NA Hispanic 65+ 1 1                                                                                                                                 ```
    ```  25 Multi-Race F Non-Hispanic 18-39 0 0                                                                                                                       ```
    ```  26 NA M Hispanic 18-39 1 1                                                                                                                                   ```
    ```  27 AmericanIndian F Non-Hispanic 40-65 0 0                                                                                                                   ```
    ```  28 Asian F NA 65+ 1 0                                                                                                                                        ```
    ```  29 Black M Non-Hispanic 18-39 0 0                                                                                                                            ```
    ```  30 AmericanIndian F NA 18-39 0 0                                                                                                                             ```
    ```  31 Asian M Hispanic 40-66 1 1                                                                                                                                ```
    ```  32 Black F Non-Hispanic 65+ 0 0                                                                                                                              ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  proc transpose data=have out=havxpo;                                                                                                                         ```
    ```  by patient_id Vaccine_Flag ;                                                                                                                                 ```
    ```  var Race Gender Ethnicity AgeGroup;                                                                                                                          ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  data havadd;                                                                                                                                                 ```
    ```   set havxpo;                                                                                                                                                 ```
    ```   mjrMnr=catx('@',_name_,col1);                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  ods exclude all;                                                                                                                                             ```
    ```  ods output observed      =xpocnt;                                                                                                                            ```
    ```  ods output rowprofilespct=xporowpct;                                                                                                                         ```
    ```  proc corresp data=havadd all dimens=1 print=both;                                                                                                            ```
    ```   tables   mjrMnr, vaccine_flag;                                                                                                                              ```
    ```  run;quit;                                                                                                                                                    ```
    ```  ods select all;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```  data havNpc(where=(label ne 'Sum'));                                                                                                                         ```
    ```    length Major Minor label Vacinated Not_vacinated Total $32.;                                                                                               ```
    ```    merge xpocnt xpoRowPct(rename=(_1=_1pct _0=_0pct));                                                                                                        ```
    ```    Vacinated     = cats(put(_0,4.),'(',put(coalesce(_0pct,0),3.),'%)');                                                                                       ```
    ```    Not_vacinated = cats(put(_1,4.),'(',put(coalesce(_1pct,0),3.),'%)');                                                                                       ```
    ```    Total         = cats(put(sum,4.),'(100%)');                                                                                                                ```
    ```    Major=scan(label,1,'@');                                                                                                                                   ```
    ```    Minor=scan(label,2,'@');                                                                                                                                   ```
    ```    keep Major Minor label Vacinated Not_vacinated Total;                                                                                                      ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  proc report data=havNpc nowd;                                                                                                                                ```
    ```    cols Major Minor Vacinated Not_vacinated Total;                                                                                                            ```
    ```    define major / order;                                                                                                                                      ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```

