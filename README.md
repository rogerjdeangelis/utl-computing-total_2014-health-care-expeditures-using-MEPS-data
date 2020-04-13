# utl-computing-total_2014-health-care-expeditures-using-MEPS-data
Computing total 2014 health care expeditures using MEPS data
    Computing total 2014 health care expeditures using MEPS data

    github
    https://tinyurl.com/rmqc3u6
    https://github.com/rogerjdeangelis/utl-computing-total_2014-health-care-expeditures-using-MEPS-data

    see
    https://github.com/HHS-AHRQ/MEPS/blob/master/SAS/README.md

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;
    Go to
    https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_detail.jsp?cboPufNumber=HC-171

    Click on
    Data File, SAS transport format      ZIP (12 MB) / EXE (7.5 MB)

    Copy from downloaded file to d:/ssp/h171.ssp

    Convert transport file to SAS datasets;

    options ls=max;
    FILENAME in_h171 'd:\ssp\h171.ssp';

    proc xcopy in = in_h171 out = WORK IMPORT;
    run;

    113   options ls=max;
    114   FILENAME in_h171 'd:\ssp\h171.ssp';
    115   proc xcopy in = in_h171 out = WORK IMPORT;
    116   run;

    NOTE: Input library IN_H171 is sequential.
    NOTE: Copying IN_H171.H171 to WORK.H171 (memtype=DATA).
    NOTE: There were 34875 observations read from the data set IN_H171.H171.
    NOTE: The data set WORK.H171 has 34875 observations and 1838 variables.
    NOTE: PROCEDURE XCOPY used (Total process time):
          real time           2.74 seconds
          cpu time            2.71 seconds

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;


                        Data Summary

    Number of Strata                                 165
    Number of Clusters                               366
    Number of Observations                         34875
    Number of Observations Used                    33162
    Number of Obs with Nonpositive Weights          1713
    Sum of Weights                             318440423


                               Statistics

                                                           Std Error
    Variable    Label                            Sum          of Sum
    ----------------------------------------------------------------
    TOTEXP14    TOTAL HEALTH CARE       1.4993648E12     49778703162
                EXP 14
    ----------------------------------------------------------------

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    proc surveymeans data = h171 sum;
      stratum VARSTR;
      cluster VARPSU;
      weight PERWT14F;
      var TOTEXP14;
    run;

    *_                   _     _        _     _
    (_)_ __  _ __  _   _| |_  | |_ __ _| |__ | | ___
    | | '_ \| '_ \| | | | __| | __/ _` | '_ \| |/ _ \
    | | | | | |_) | |_| | |_  | || (_| | |_) | |  __/
    |_|_| |_| .__/ \__,_|\__|  \__\__,_|_.__/|_|\___|
            |_|
    ;

    Middle Observation(17437 ) of h171 - Total Obs 34,875


     -- CHARACTER --

                        Sample
    Variable      Type  Value     LABEL

    DUPERSID        C8  49607105  PERSON ID (DUID + PID)
    FAMID31         C2  A         FAMILY ID (STUDENT MERGED IN) - R3/1
    FAMID42         C2  A         FAMILY ID (STUDENT MERGED IN) - R4/2
    FAMID53         C2  A         FAMILY ID (STUDENT MERGED IN) - R5/3
    FAMID14         C2  A         FAMILY ID (STUDENT MERGED IN) - 12/31/14
    FAMIDYR         C2  A         ANNUAL FAMILY IDENTIFIER
    CPSFAMID        C2  A         CPSFAMID
    RULETR31        C2  A         RU LETTER - R3/1
    RULETR42        C2  A         RU LETTER - R4/2
    RULETR53        C2  A         RU LETTER - R5/3
    RULETR14        C2  A         RU LETTER AS OF 12/31/14
    RURSLT31        C2  60        RU RESULT - R3/1
    RURSLT42        C2  60        RU RESULT - R4/2
    RURSLT53        C2  60        RU RESULT - R5/3
    HIEUIDX         C7  49607A1   HIEU IDENTIFIER
    TOTOBS          C1  34,875    TOTOBS


     -- NUMERIC --
                        Sample                                                                    Sample
    Variable      Type  Value     LABEL                                       Variable      Type  Value     LABEL

    DUID            N6  49607     DWELLING UNIT ID                            HPEMY14         N4  2         HOLDER OF EMPL UNION INS IN MAY14
    PID             N4  105       PERSON NUMBER                               HPEJU14         N4  2         HOLDER OF EMPL UNION INS IN JUN14
    PANEL           N4  18        PANEL NUMBER                                HPEJL14         N4  2         HOLDER OF EMPL UNION INS IN JUL14
                                                                              HPEAU14         N4  2         HOLDER OF EMPL UNION INS IN AUG14
    FCSZ1231        N4  5         FAM SIZE RESPONDING 12/31 CPS FAMILY        HPESE14         N4  2         HOLDER OF EMPL UNION INS IN SEP14
    FCRP1231        N4  0         REF PERSON OF 12/31 CPS FAMILY              HPEOC14         N4  2         HOLDER OF EMPL UNION INS IN OCT14
    RUSIZE31        N4  5         RU SIZE - R3/1                              HPENO14         N4  2         HOLDER OF EMPL UNION INS IN NOV14
    RUSIZE42        N4  5         RU SIZE - R4/2                              HPEDE14         N4  2         HOLDER OF EMPL UNION INS IN DEC14
    RUSIZE53        N4  5         RU SIZE - R5/3                              HPDJA14         N4  -1        HOLDER OF PRIV INS (SOURCE UNKNWN) JAN14
    RUSIZE14        N4  5         RU SIZE AS OF 12/31/14                      HPDFE14         N4  -1        HOLDER OF PRIV INS (SOURCE UNKNWN) FEB14
    RUCLAS31        N4  1         RU FIELDED AS:STANDARD/NEW/STUDENT-R3/1     HPDMA14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) MAR14
    RUCLAS42        N4  1         RU FIELDED AS:STANDARD/NEW/STUDENT-R4/2     HPDAP14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) APR14
    RUCLAS53        N4  1         RU FIELDED AS:STANDARD/NEW/STUDENT-R5/3     HPDMY14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) MAY14
    RUCLAS14        N4  1         RU FIELDED AS:STANDARD/NEW/STUD-12/31/14    HPDJU14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) JUN14
    FAMSZE31        N4  5         RU SIZE INCLUDING STUDENTS - R3/1           HPDJL14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) JUL14
    FAMSZE42        N4  5         RU SIZE INCLUDING STUDENTS - R4/2           HPDAU14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) AUG14
    FAMSZE53        N4  5         RU SIZE INCLUDING STUDENTS - R5/3           HPDSE14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) SEP14
    FAMSZE14        N4  5         RU SIZE INCLUDING STUDENT AS OF 12/31/14    HPDOC14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) OCT14
    FMRS1231        N4  1         MEMBER OF RESPONDING 12/31 FAMILY           HPDNO14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) NOV14
    FAMS1231        N4  5         FAMILY SIZE OF RESPONDING 12/31 FAMILY      HPDDE14         N4  2         HOLDER OF PRIV INS (SOURCE UNKNWN) DEC14
    FAMSZEYR        N4  5         SIZE OF RESPONDING ANNUALIZED FAMILY        HPNJA14         N4  -1        HOLDER OF NONGROUP INS IN JAN14
    FAMRFPYR        N4  0         REFERENCE PERSON OF ANNUALIZED FAMILY       HPNFE14         N4  -1        HOLDER OF NONGROUP INS IN FEB14
    REGION31        N4  4         CENSUS REGION - R3/1                        HPNMA14         N4  2         HOLDER OF NONGROUP INS IN MAR14
    REGION42        N4  4         CENSUS REGION - R4/2                        HPNAP14         N4  2         HOLDER OF NONGROUP INS IN APR14
    REGION53        N4  4         CENSUS REGION - R5/3                        HPNMY14         N4  2         HOLDER OF NONGROUP INS IN MAY14
    REGION14        N4  4         CENSUS REGION AS OF 12/31/14                HPNJU14         N4  2         HOLDER OF NONGROUP INS IN JUN14
    REFPRS31        N4  101       REFERENCE PERSON AT - R3/1                  HPNJL14         N4  2         HOLDER OF NONGROUP INS IN JUL14
    REFPRS42        N4  101       REFERENCE PERSON AT - R4/2                  HPNAU14         N4  2         HOLDER OF NONGROUP INS IN AUG14
    REFPRS53        N4  101       REFERENCE PERSON AT - R5/3                  HPNSE14         N4  2         HOLDER OF NONGROUP INS IN SEP14
    REFPRS14        N4  101       REFERENCE PERSON AS OF 12/31/14             HPNOC14         N4  2         HOLDER OF NONGROUP INS IN OCT14
    RESP31          N4  2         1ST RESPONDENT INDICATOR FOR R3/1           HPNNO14         N4  2         HOLDER OF NONGROUP INS IN NOV14
    RESP42          N4  2         1ST RESPONDENT INDICATOR FOR R4/2           HPNDE14         N4  2         HOLDER OF NONGROUP INS IN DEC14
    RESP53          N4  2         1ST RESPONDENT INDICATOR FOR R5/3           HPOJA14         N4  -1        HOLDER OF OTHER GROUP INS IN JAN14
    RESP14          N4  2         1ST RESPONDENT INDICATOR AS OF 12/31/14     HPOFE14         N4  -1        HOLDER OF OTHER GROUP INS IN FEB14
    PROXY31         N4  1         WAS RESPONDENT A PROXY IN R3/1              HPOMA14         N4  2         HOLDER OF OTHER GROUP INS IN MAR14
    PROXY42         N4  1         WAS RESPONDENT A PROXY IN R4/2              HPOAP14         N4  2         HOLDER OF OTHER GROUP INS IN APR14
    PROXY53         N4  1         WAS RESPONDENT A PROXY IN R5/3              HPOMY14         N4  2         HOLDER OF OTHER GROUP INS IN MAY14
    PROXY14         N4  1         WAS RESPONDENT A PROXY AS OF 12/31/14       HPOJU14         N4  2         HOLDER OF OTHER GROUP INS IN JUN14
    INTVLANG        N4  1         LANGUAGE INTERVIEW WAS COMPLETED            HPOJL14         N4  2         HOLDER OF OTHER GROUP INS IN JUL14
    BEGRFM31        N4  3         R3/1 REFERENCE PERIOD BEGIN DATE: MONTH     HPOAU14         N4  2         HOLDER OF OTHER GROUP INS IN AUG14
    BEGRFY31        N5  2014      R3/1 REFERENCE PERIOD BEGIN DATE: YEAR      HPOSE14         N4  2         HOLDER OF OTHER GROUP INS IN SEP14
    ENDRFM31        N4  4         R3/1 REFERENCE PERIOD END DATE: MONTH       HPOOC14         N4  2         HOLDER OF OTHER GROUP INS IN OCT14
    ENDRFY31        N5  2014      R3/1 REFERENCE PERIOD END DATE: YEAR        HPONO14         N4  2         HOLDER OF OTHER GROUP INS IN NOV14
    BEGRFM42        N4  4         R4/2 REFERENCE PERIOD BEGIN DATE: MONTH     HPODE14         N4  2         HOLDER OF OTHER GROUP INS IN DEC14
    BEGRFY42        N5  2014      R4/2 REFERENCE PERIOD BEGIN DATE: YEAR      HPSJA14         N4  -1        HOLDER OF SELF-EMP-1 INS IN JAN14
    ENDRFM42        N4  9         R4/2 REFERENCE PERIOD END DATE: MONTH       HPSFE14         N4  -1        HOLDER OF SELF-EMP-1 INS IN FEB14
    ENDRFY42        N5  2014      R4/2 REFERENCE PERIOD END DATE: YEAR        HPSMA14         N4  2         HOLDER OF SELF-EMP-1 INS IN MAR14
    BEGRFM53        N4  9         R5/3 REFERENCE PERIOD BEGIN DATE: MONTH     HPSAP14         N4  2         HOLDER OF SELF-EMP-1 INS IN APR14
    BEGRFY53        N5  2014      R5/3 REFERENCE PERIOD BEGIN DATE: YEAR      HPSMY14         N4  2         HOLDER OF SELF-EMP-1 INS IN MAY14
    ENDRFM53        N4  12        R5/3 REFERENCE PERIOD END DATE: MONTH       HPSJU14         N4  2         HOLDER OF SELF-EMP-1 INS IN JUN14
    ENDRFY53        N5  2014      R5/3 REFERENCE PERIOD END DATE: YEAR        HPSJL14         N4  2         HOLDER OF SELF-EMP-1 INS IN JUL14
    ENDRFM14        N4  12        2014 REFERENCE PERIOD END DATE: MONTH       HPSAU14         N4  2         HOLDER OF SELF-EMP-1 INS IN AUG14
    ENDRFY14        N5  2014      2014 REFERENCE PERIOD END DATE: YEAR        HPSSE14         N4  2         HOLDER OF SELF-EMP-1 INS IN SEP14
    KEYNESS         N4  1         PERSON KEY STATUS                           HPSOC14         N4  2         HOLDER OF SELF-EMP-1 INS IN OCT14
    INSCOP31        N4  3         INSCOPE - R3/1                              HPSNO14         N4  2         HOLDER OF SELF-EMP-1 INS IN NOV14
    INSCOP42        N4  1         INSCOPE - R4/2                              HPSDE14         N4  2         HOLDER OF SELF-EMP-1 INS IN DEC14
    INSCOP53        N4  1         INSCOPE - R5/3                              HPXJA14         N4  -1        HOLDER OF PRIV INS THROUGH EXCH IN JAN14
    INSCOP14        N4  1         INSCOPE - R5/3 START THROUGH 12/31/14       HPXFE14         N4  -1        HOLDER OF PRIV INS THROUGH EXCH IN FEB14
    INSC1231        N4  1         INSCOPE STATUS ON 12/31/14                  HPXMA14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN MAR14
    INSCOPE         N4  1         WAS PERSON EVER INSCOPE IN 2014             HPXAP14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN APR14
    ELGRND31        N4  1         ELIGIBILITY - R3/1                          HPXMY14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN MAY14
    ELGRND42        N4  1         ELIGIBILITY - R4/2                          HPXJU14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN JUN14
    ELGRND53        N4  1         ELIGIBILITY - R5/3                          HPXJL14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN JUL14
    ELGRND14        N4  1         ELIGIBILITY STATUS AS OF 12/31/14           HPXAU14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN AUG14
    PSTATS31        N4  51        PERSON DISPOSITION STATUS - R3/1            HPXSE14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN SEP14
    PSTATS42        N4  11        PERSON DISPOSITION STATUS - R4/2            HPXOC14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN OCT14
    PSTATS53        N4  11        PERSON DISPOSITION STATUS - R5/3            HPXNO14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN NOV14
    AGE31X          N4  0         AGE - R3/1 (EDITED/IMPUTED)                 HPXDE14         N4  2         HOLDER OF PRIV INS THROUGH EXCH IN DEC14
    AGE42X          N4  0         AGE - R4/2 (EDITED/IMPUTED)                 HPRJA14         N4  -1        HOLDER OF PRIVATE INSURANCE IN JAN14
    AGE53X          N4  0         AGE - R5/3 (EDITED/IMPUTED)                 HPRFE14         N4  -1        HOLDER OF PRIVATE INSURANCE IN FEB14
    AGE14X          N4  0         AGE AS OF 12/31/14 (EDITED/IMPUTED)         HPRMA14         N4  2         HOLDER OF PRIVATE INSURANCE IN MAR14
    AGELAST         N4  0         PERSON'S AGE LAST TIME ELIGIBLE             HPRAP14         N4  2         HOLDER OF PRIVATE INSURANCE IN APR14
    DOBMM           N4  3         DATE OF BIRTH: MONTH                        HPRMY14         N4  2         HOLDER OF PRIVATE INSURANCE IN MAY14
    DOBYY           N5  2014      DATE OF BIRTH: YEAR                         HPRJU14         N4  2         HOLDER OF PRIVATE INSURANCE IN JUN14
    SEX             N4  2         SEX                                         HPRJL14         N4  2         HOLDER OF PRIVATE INSURANCE IN JUL14
    RACEV1X         N4  1         RACE (EDITED/IMPUTED)                       HPRAU14         N4  2         HOLDER OF PRIVATE INSURANCE IN AUG14
    RACEV2X         N4  1         RACE (EDITED/IMPUTED)                       HPRSE14         N4  2         HOLDER OF PRIVATE INSURANCE IN SEP14
    RACEAX          N4  3         ASIAN AMONG RACES RPTD (EDITED/IMPUTED)     HPROC14         N4  2         HOLDER OF PRIVATE INSURANCE IN OCT14
    RACEBX          N4  3         BLACK AMONG RACES RPTD (EDITED/IMPUTED)     HPRNO14         N4  2         HOLDER OF PRIVATE INSURANCE IN NOV14
    RACEWX          N4  1         WHITE AMONG RACES RPTD (EDITED/IMPUTED)     HPRDE14         N4  2         HOLDER OF PRIVATE INSURANCE IN DEC14
    RACETHX         N4  2         RACE/ETHNICITY (EDITED/IMPUTED)             INSJA14X        N4  -1        COVR BY HOSP/MED INS IN JAN14 (ED)
    HISPANX         N4  2         HISPANIC ETHNICITY (EDITED/IMPUTED)         INSFE14X        N4  -1        COVR BY HOSP/MED INS IN FEB14 (ED)
    HISPNCAT        N4  9         HISPANIC ETHNICITY (EDITED/IMPUTED)         INSMA14X        N4  2         COVR BY HOSP/MED INS IN MAR14 (ED)
    MARRY31X        N4  6         MARITAL STATUS - R3/1 (EDITED/IMPUTED)      INSAP14X        N4  1         COVR BY HOSP/MED INS IN APR14 (ED)
    MARRY42X        N4  6         MARITAL STATUS - R4/2 (EDITED/IMPUTED)      INSMY14X        N4  1         COVR BY HOSP/MED INS IN MAY14 (ED)
    MARRY53X        N4  6         MARITAL STATUS - R5/3 (EDITED/IMPUTED)      INSJU14X        N4  1         COVR BY HOSP/MED INS IN JUN14 (ED)
    MARRY14X        N4  6         MARITAL STATUS-12/31/14 (EDITED/IMPUTED)    INSJL14X        N4  1         COVR BY HOSP/MED INS IN JUL14 (ED)
    SPOUID31        N4  997       SPOUSE ID - R3/1                            INSAU14X        N4  1         COVR BY HOSP/MED INS IN AUG14 (ED)
    SPOUID42        N4  997       SPOUSE ID - R4/2                            INSSE14X        N4  1         COVR BY HOSP/MED INS IN SEP14 (ED)
    SPOUID53        N4  997       SPOUSE ID - R5/3                            INSOC14X        N4  1         COVR BY HOSP/MED INS IN OCT14 (ED)
    SPOUID14        N4  997       SPOUSE ID - 12/31/14                        INSNO14X        N4  1         COVR BY HOSP/MED INS IN NOV14 (ED)
    SPOUIN31        N4  3         MARITAL STATUS W/SPOUSE PRESENT-R3/1        INSDE14X        N4  1         COVR BY HOSP/MED INS IN DEC14 (ED)
    SPOUIN42        N4  3         MARITAL STATUS W/SPOUSE PRESENT-R4/2        PRVEV14         N4  1         EVER HAVE PRIVATE INSURANCE DURING 14
    SPOUIN53        N4  3         MARITAL STATUS W/SPOUSE PRESENT-R5/3        TRIEV14         N4  2         EVER HAVE TRICARE/CHAMPVA DURING 14
    SPOUIN14        N4  3         MARITAL STATUS W/SPOUSE PRESENT-12/31/14    MCREV14         N4  2         EVER HAVE MEDICARE DURING 14 (ED)
    EDUYRDG         N4  10        YEAR OF EDUCATION OR HIGHEST DEGREE         MCDEV14         N4  2         EVER HAVE MEDICAID/SCHIP DURING 14 (ED)
    EDUCYR          N4  -1        YEARS OF EDUC WHEN FIRST ENTERED MEPS       OPAEV14         N4  2         EVER HAVE OTHER PUBLIC A INS DURING 14
    EDRECODE        N4  -1        EDUCATION RECODE (EDITED)                   OPBEV14         N4  2         EVER HAVE OTHER PUBLIC B INS DURING 14
    FTSTU31X        N4  -1        STUDENT STATUS IF AGES 17-23 - R3/1         UNINS14         N4  2         UNINSURED ALL OF 14
    FTSTU42X        N4  -1        STUDENT STATUS IF AGES 17-23 - R4/2         INSCOV14        N4  1         HEALTH INSURANCE COVERAGE INDICATOR 14
    FTSTU53X        N4  -1        STUDENT STATUS IF AGES 17-23 - R5/3         INSURC14        N4  1         FULL YEAR INSURANCE COVERAGE STATUS 2014
    FTSTU14X        N4  -1        STUDENT STATUS IF AGES 17-23 - 12/31/14     TRIST31X        N4  3         COVERED BY TRICARE STANDARD - R3/1
    ACTDTY31        N4  3         MILITARY FULL-TIME ACTIVE DUTY - R3/1       TRIST42X        N4  3         COVERED BY TRICARE STANDARD - R4/2
    ACTDTY42        N4  3         MILITARY FULL-TIME ACTIVE DUTY - R4/2       TRIST14X        N4  3         COVERED BY TRICARE STANDARD - 12/31/14
    ACTDTY53        N4  3         MILITARY FULL-TIME ACTIVE DUTY - R5/3       TRIPR31X        N4  3         COVERED BY TRICARE PRIME - R3/1
    HONRDC31        N4  3         HONORABLY DISCHARGED FROM MILITARY          TRIPR42X        N4  3         COVERED BY TRICARE PRIME - R4/2
    HONRDC42        N4  3         HONORABLY DISCHARGED FROM MILITARY          TRIPR14X        N4  3         COVERED BY TRICARE PRIME - 12/31/14
    HONRDC53        N4  3         HONORABLY DISCHARGED FROM MILITARY          TRIEX31X        N4  3         COVERED BY TRICARE EXTRA - R3/1
    REFRL31X        N4  4         RELATION TO REF PERS- R3/1 (EDIT/IMP)       TRIEX42X        N4  3         COVERED BY TRICARE EXTRA - R4/2
    REFRL42X        N4  4         RELATION TO REF PERS- R4/2 (EDIT/IMP)       TRIEX14X        N4  3         COVERED BY TRICARE EXTRA - 12/31/14
    REFRL53X        N4  4         RELATION TO REF PERS- R5/3 (EDIT/IMP)       TRILI31X        N4  3         COVERED BY TRICARE FOR LIFE - R3/1
    REFRL14X        N4  4         RELATION TO REF PERS-12/31/14 (EDIT/IMP)    TRILI42X        N4  3         COVERED BY TRICARE FOR LIFE - R4/2
    OTHLANG         N4  -1        IN FAMILY WITH SOMEONE SPKNG OTHER LANG     TRILI14X        N4  3         COVERED BY TRICARE FOR LIFE - 12/31/14
    LANGSPK         N4  -1        LANGUAGE SPOKEN AT HOME OTHER THAN ENGL     TRICH31X        N4  3         COVERED BY CHAMPVA - R3/1
    HWELLSPE        N4  -1        HOW WELL PERSON SPEAKS ENGLISH              TRICH42X        N4  3         COVERED BY CHAMPVA - R4/2
    BORNUSA         N4  1         PERSON BORN IN THE US                       TRICH14X        N4  3         COVERED BY TRICARE CHAMPVA - 12/31/14
    YRSINUS         N4  -1        YEARS PERSON LIVED IN THE US                MCRPD31         N4  3         COV BY MEDICARE PMED BENEFIT - R3/1
    MOPID31X        N4  102       PID OF PERSON'S MOM - RD 3/1                MCRPD42         N4  3         COV BY MEDICARE PMED BENEFIT - R4/2
    MOPID42X        N4  102       PID OF PERSON'S MOM - RD 4/2                MCRPD14         N4  3         COV BY MEDICARE PMED BENEFIT - 12/31/14
    MOPID53X        N4  102       PID OF PERSON'S MOM - RD 5/3                MCRPD31X        N4  3         COV BY MEDICARE PMED BENEFIT - R3/1 (ED)
    DAPID31X        N4  101       PID OF PERSON'S DAD - RD 3/1                MCRPD42X        N4  3         COV BY MEDICARE PMED BENEFIT - R4/2 (ED)
    DAPID42X        N4  101       PID OF PERSON'S DAD - RD 4/2                MCRPD14X        N4  3         COV BY MCARE PMED BENEFIT-12/31/14 (ED)
    DAPID53X        N4  101       PID OF PERSON'S DAD - RD 5/3                MCRPB31         N4  3         COV BY MEDICARE PART B - R3/1
    RTHLTH31        N4  1         PERCEIVED HEALTH STATUS - RD 3/1            MCRPB42         N4  3         COV BY MEDICARE PART B - R4/2
    RTHLTH42        N4  1         PERCEIVED HEALTH STATUS - RD 4/2            MCRPB14         N8  3         COV BY MEDICARE PART B - 12/31/14
    RTHLTH53        N4  1         PERCEIVED HEALTH STATUS - RD 5/3            MCRPHO31        N4  3         COV BY MEDICARE MANAGED CARE - R3/1
    MNHLTH31        N4  1         PERCEIVED MENTAL HEALTH STATUS - RD 3/1     MCRPHO42        N4  3         COV BY MEDICARE MANAGED CARE - R4/2
    MNHLTH42        N4  1         PERCEIVED MENTAL HEALTH STATUS - RD 4/2     MCRPHO14        N4  3         COV BY MEDICARE MANAGED CARE - 12/31/14
    MNHLTH53        N4  1         PERCEIVED MENTAL HEALTH STATUS - RD 5/3     MCDHMO31        N4  3         COVERED BY MEDICAID OR SCHIP HMO - R3/1
    HIBPDX          N4  -1        HIGH BLOOD PRESSURE DIAG (>17)              MCDHMO42        N4  3         COVERED BY MEDICAID OR SCHIP HMO - R4/2
    HIBPAGED        N4  -1        AGE OF DIAGNOSIS-HIGH BLOOD PRESSURE        MCDHMO14        N4  3         COVRED BY MEDICAID OR SCHIP HMO-12/31/14
    BPMLDX          N4  -1        MULT DIAG HIGH BLOOD PRESS (>17)            MCDMC31         N4  3         COV BY MCAID/SCHIP GATEKEEPER PLAN-R3/1
    CHDDX           N4  -1        CORONARY HRT DISEASE DIAG (>17)             MCDMC42         N4  3         COV BY MCAID/SCHIP GATEKEEPER PLAN-R4/2
    CHDAGED         N4  -1        AGE OF DIAGNOSIS-CORONARY HEART DISEASE     MCDMC14         N4  3         COV BY MCAID/SCHIP GTKEEPR PLAN-12/31/14
    ANGIDX          N4  -1        ANGINA DIAGNOSIS (>17)                      PRVHMO31        N4  3         COVERED BY PRIVATE HMO - R3/1
    ANGIAGED        N4  -1        AGE OF DIAGNOSIS-ANGINA                     PRVHMO42        N4  2         COVERED BY PRIVATE HMO - R4/2
    MIDX            N4  -1        HEART ATTACK (MI) DIAG (>17)                PRVHMO14        N4  2         COVERED BY PRIVATE HMO - 12/31/14
    MIAGED          N4  -1        AGE OF DIAGNOSIS-HEART ATTACK(MI)           FSAGT31         N4  1         ANYONE IN RU HAVE FSA - R3/1
    OHRTDX          N4  -1        OTHER HEART DISEASE DIAG (>17)              HASFSA31        N4  -1        PERSON IS FSA HOLDER - R3/1
    OHRTAGED        N4  -1        AGE OF DIAGNOSIS-OTHER HEART DISEASE        FSAAMT31        N8  2         FSA TOTAL AMOUNT FOR RU - R3/1
    STRKDX          N4  -1        STROKE DIAGNOSIS (>17)                      PROBPY42        N4  -8        FAMILY HAVING PROB PAYING MEDICAL BILLS
    STRKAGED        N4  -1        AGE OF DIAGNOSIS-STROKE                     CRFMPY42        N4  -8        FAMILY MED BILLS BEING PAID OVER TIME
    EMPHDX          N4  -1        EMPHYSEMA DIAGNOSIS (>17)                   PYUNBL42        N4  -8        UNABLE TO PAY FAMILY MEDICAL BILLS
    EMPHAGED        N4  -1        AGE OF DIAGNOSIS-EMPHYSEMA                  PREVCOVR        N4  -1        PER COV BY INS IN PREV 2 YRS-PNL 19 ONLY
    CHBRON31        N4  -1        CHRONC BRONCHITS LAST 12 MTHS (>17)-R3/1    COVRMM          N4  -1        MONTH MOST RECENTLY COVERED-PNL 19 ONLY
    CHBRON53        N4  -1        CHRONC BRONCHITS LAST 12 MTHS (>17)-R5/3    COVRYY          N5  -1        YEAR MOST RECENTLY COVERED-PANEL 19 ONLY
    CHOLDX          N4  -1        HIGH CHOLESTEROL DIAGNOSIS (>17)            WASESTB         N4  -1        WAS PREV INS BY EMPL OR UNION-PN 19 ONLY
    CHOLAGED        N4  -1        AGE OF DIAGNOSIS-HIGH CHOLESTEROL           WASMCARE        N4  -1        WAS PREV INS BY MEDICARE-PANEL 19 ONLY
    CANCERDX        N4  -1        CANCER DIAGNOSIS (>17)                      WASMCAID        N4  -1        WAS PREV INS BY MCAID/SCHIP-PNL 19 ONLY
    CABLADDR        N8  -1        CANCER DIAGNOSED - BLADDER (>17)            WASCHAMP        N4  -1        WAS PREV INS TRICARE/CHAMPVA-PNL 19 ONLY
    CABREAST        N4  -1        CANCER DIAGNOSED - BREAST (>17)             WASVA           N4  -1        WAS PREV INS VA/MILITAR CARE-PNL 19 ONLY
    CACERVIX        N4  -1        CANCER DIAGNOSED - CERVIX (>17)             WASPRIV         N4  -1        WAS PREV INS GRP/ASSOC/INS CO-PN 19 ONLY
    CACOLON         N4  -1        CANCER DIAGNOSED - COLON (>17)              WASOTGOV        N4  -1        WAS PREV INS BY OTH GOV PRG-PNL 19 ONLY
    CALUNG          N4  -1        CANCER DIAGNOSED - LUNG (>17)               WASAFDC         N4  -1        WAS PREV INS BY PUBLIC AFDC-PNL 19 ONLY
    CALYMPH         N4  -1        CANCER DIAGNOSED - LYMPHOMA (>17)           WASSSI          N4  -1        WAS PREV INS BY SSI PROGRAM-PNL 19 ONLY
    CAMELANO        N4  -1        CANCER DIAGNOSED - MELANOMA (>17)           WASSTAT1        N4  -1        WAS PREV INS BY STAT PROG 1-PNL 19 ONLY
    CAOTHER         N4  -1        CANCER DIAGNOSED - OTHER (>17)              WASSTAT2        N4  -1        WAS PREV INS BY STAT PROG 2-PNL 19 ONLY
    CAPROSTA        N4  -1        CANCER DIAGNOSED - PROSTATE (>17)           WASSTAT3        N4  -1        WAS PREV INS BY STAT PROG 3-PNL 19 ONLY
    CASKINNM        N4  -1        CANCER DIAGNOSED - SKIN-NONMELANO (>17)     WASSTAT4        N4  -1        WAS PREV INS BY STAT PROG 4-PNL 19 ONLY
    CASKINDK        N4  -1        CANCER DIAGNOSED-SKIN-UNKNOWN TYPE (>17)    WASOTHER        N4  -1        WAS PREV INS BY OTH SOURCE-PANEL 19 ONLY
    CAUTERUS        N4  -1        CANCER DIAGNOSED - UTERUS (>17)             NOINSBEF        N4  -1        EVR WOUT HLTH INSR PREV YR-PANEL 19 ONLY
    DIABDX          N4  -1        DIABETES DIAGNOSIS (>17)                    NOINSTM         N4  -1        # WKS/MON WOUT HLTH INS PRV YR-PN 19 ONL
    DIABAGED        N4  -1        AGE OF DIAGNOSIS-DIABETES                   NOINUNIT        N4  -1        UNIT OF TIME WOUT HLTH INS-PANEL 19 ONLY
    JTPAIN31        N4  -1        JOINT PAIN LAST 12 MONTHS (>17) - RD 3/1    MORECOVR        N4  -1        COV BY MOR COMPR PL PREV 2 YR-PN 19 ONLY
    JTPAIN53        N4  -1        JOINT PAIN LAST 12 MONTHS (>17) - RD 5/3    INSENDMM        N4  -1        MONTH MOST RECENTLY COVD-PANEL 19 ONLY
    ARTHDX          N4  -1        ARTHRITIS DIAGNOSIS (>17)                   INSENDYY        N5  -1        YEAR MOST RECENTLY COVD-PANEL 19 ONLY
    ARTHTYPE        N4  -1        TYPE OF ARTHRITIS DIAGNOSED (>17)           TRICR31X        N4  2         COV BY TRICR/CHAMV - R3/1 INT DT (ED)
    ARTHAGED        N4  -1        AGE OF DIAGNOSIS-ARTHRITIS                  TRICR42X        N4  2         COV BY TRICR/CHAMV - R4/2 INT DT (ED)
    ASTHDX          N4  2         ASTHMA DIAGNOSIS                            TRICR53X        N4  2         COV BY TRICR/CHAMV 12-31/R3 INT DT (ED)
    ASTHAGED        N4  -1        AGE OF DIAGNOSIS-ASTHMA                     TRICR14X        N4  2         COV BY TRICR/CHAMV - 12/31/14 (ED)
    ASSTIL31        N4  -1        DOES PERSON STILL HAVE ASTHMA-RD3/1         TRIAT31X        N4  2         ANY TIME COV TRICARE/CHAMPVA - R3/1
    ASSTIL53        N4  -1        DOES PERSON STILL HAVE ASTHMA - RD 5/3      TRIAT42X        N4  2         ANY TIME COV TRICARE/CHAMPVA - R4/2
    ASATAK31        N4  -1        ASTHMA ATTACK LAST 12 MOS - RD3/1           TRIAT53X        N4  2         ANY TIME COV TRICARE/CHAMPVA - R5/3
    ASATAK53        N4  -1        ASTHMA ATTACK LAST 12 MOS - RD 5/3          TRIAT14X        N4  2         ANY TIME COV TRICARE/CHAMPVA - 12/31/14
    ASTHEP31        N4  -1        WHEN WAS LAST EPISODE OF ASTHMA - RD 3/1    MCAID31         N4  2         COV BY MEDICAID OR SCHIP - R3/1 INT DT
    ASTHEP53        N4  -1        WHEN WAS LAST EPISODE OF ASTHMA - RD 5/3    MCAID42         N4  2         COV BY MEDICAID OR SCHIP - R4/2 INT DT
    ASACUT53        N4  -1        USED ACUTE PRES INHALER LAST 3 MOS-RD5/3    MCAID53         N4  2         COV BY MEDICAID OR SCHIP 12-31/R3 INT DT
    ASMRCN53        N4  -1        USED>3ACUTE CN PRES INH LAST 3 MOS-RD5/3    MCAID14         N4  2         COV BY MEDICAID OR SCHIP - 12/31/14
    ASPREV53        N4  -1        EVER USED PREV DAILY ASTHMA MEDS -RD 5/3    MCAID31X        N4  2         COV BY MEDICAID/SCHIP - R3/1 INT DT (ED)
    ASDALY53        N4  -1        NOW TAKE PREV DAILY ASTHMA MEDS - RD 5/3    MCAID42X        N4  2         COV BY MEDICAID/SCHIP - R4/2 INT DT (ED)
    ASPKFL53        N4  -1        HAVE PEAK FLOW METER AT HOME - RD 5/3       MCAID53X        N4  2         COV MEDICAID/SCHIP 12-31/R3 INT DT(ED)
    ASEVFL53        N4  -1        EVER USED PEAK FLOW METER - RD 5/3          MCAID14X        N4  2         COV BY MEDICAID OR SCHIP - 12/31/14 (ED)
    ASWNFL53        N4  -1        WHEN LAST USED PEAK FLOW METER - RD 5/3     MCARE31         N4  2         COV BY MEDICARE - R3/1 INT DT
    ADHDADDX        N4  -1        ADHDADD DIAGNOSIS (5-17)                    MCARE42         N4  2         COV BY MEDICARE - R4/2 INT DT
    ADHDAGED        N4  -1        AGE OF DIAGNOSIS-ADHD/ADD                   MCARE53         N4  2         COV BY MEDICARE 12-31/R3 INT DT
    PREGNT31        N4  -1        PREGNANT DURING REF PERIOD - RD 3/1         MCARE14         N4  2         COV BY MEDICARE - 12/31/14
    PREGNT42        N4  -1        PREGNANT DURING REF PERIOD - RD 4/2         MCARE31X        N4  2         COV BY MEDICARE - R3/1 INT DT (ED)
    PREGNT53        N4  -1        PREGNANT DURING REF PERIOD - RD 5/3         MCARE42X        N4  2         COV BY MEDICARE - R4/2 INT DT (ED)
    IADLHP31        N4  2         IADL SCREENER - RD 3/1                      MCARE53X        N4  2         COV BY MEDICARE 12-31/R3 INT DT(ED)
    IADLHP53        N4  2         IADL SCREENER - RD 5/3                      MCARE14X        N4  2         COV BY MEDICARE - 12/31/14 (ED)
    ADLHLP31        N4  2         ADL SCREENER - RD 3/1                       MCDAT31X        N4  2         ANY TIME COV MEDICAID OR SCHIP - R3/1
    ADLHLP53        N4  2         ADL SCREENER - RD 5/3                       MCDAT42X        N4  2         ANY TIME COV MEDICAID OR SCHIP - R4/2
    AIDHLP31        N4  2         USED ASSISTIVE DEVICES - RD 3/1             MCDAT53X        N4  2         ANY TIME COV MEDICAID OR SCHIP - R5/3
    AIDHLP53        N4  2         USED ASSISTIVE DEVICES - RD 5/3             MCDAT14X        N4  2         ANY TIME COV MEDICAID OR SCHIP-12/31/14
    WLKLIM31        N4  2         LIMITATION IN PHYSICAL FUNCTIONING-RD3/1    OTPAAT31        N4  2         ANY TIME COV OT GOV MCAID/SCHIP HMO-R3/1
    WLKLIM53        N4  2         LIMITATION IN PHYSICAL FUNCTIONING-RD5/3    OTPAAT42        N4  2         ANY TIME COV OT GOV MCAID/SCHIP HMO-R4/2
    LFTDIF31        N4  -1        DIFFICULTY LIFTING 10 POUNDS - RD 3/1       OTPAAT53        N4  2         ANY TIME COV OT GOV MCAID/SCHIP HMO-R5/3
    LFTDIF53        N4  -1        DIFFICULTY LIFTING 10 POUNDS - RD 5/3       OTPAAT14        N4  2         ANY COV OT GOV MCAID/SCHIP HMO-12/31/14
    STPDIF31        N4  -1        DIFFICULTY WALKING UP 10 STEPS - RD 3/1     OTPBAT31        N4  2         ANY COV OT GOV NOT MCAID/SCHIP HMO-R3/1
    STPDIF53        N4  -1        DIFFICULTY WALKING UP 10 STEPS - RD 5/3     OTPBAT42        N4  2         ANY COV OT GOV NOT MCAID/SCHIP HMO-R4/2
    WLKDIF31        N4  -1        DIFFICULTY WALKING 3 BLOCKS - RD 3/1        OTPBAT53        N4  2         ANY COV OT GOV NOT MCAID/SCHIP HMO-R5/3
    WLKDIF53        N4  -1        DIFFICULTY WALKING 3 BLOCKS - RD 5/3        OTPBAT14        N4  2         ANY CV OT GV NT MCAID/SCHIP HMO-12/31/14
    MILDIF31        N4  -1        DIFFICULTY WALKING A MILE - RD 3/1          OTPUBA31        N4  2         COV/PAY OTH GOV MCAID/SCHIP HMO-R3/1 INT
    MILDIF53        N4  -1        DIFFICULTY WALKING A MILE - RD 5/3          OTPUBA42        N4  2         COV/PAY OTH GOV MCAID/SCHIP HMO-R4/2 INT
    STNDIF31        N4  -1        DIFFICULTY STANDING 20 MINUTES - RD 3/1     OTPUBA53        N4  2         COV/PAY OTH GOV MCAID/SCHIP HMO 12-31/R3
    STNDIF53        N4  -1        DIFFICULTY STANDING 20 MINUTES - RD 5/3     OTPUBA14        N4  2         COV/PAY OTH GOV MCAID/SCHIP HMO-12/31/14
    BENDIF31        N4  -1        DIFFICULTY BENDING/STOOPING - RD 3/1        OTPUBB31        N4  2         COV OTH GOV NOT MCAID/SCHIP HMO-R3/1 INT
    BENDIF53        N4  -1        DIFFICULTY BENDING/STOOPING - RD 5/3        OTPUBB42        N4  2         COV OTH GOV NOT MCAID/SCHIP HMO-R4/2 INT
    RCHDIF31        N4  -1        DIFFICULTY REACHING OVERHEAD - RD 3/1       OTPUBB53        N4  2         COV OTH GOV NOT MCAID/SCHIP HMO 12-31/R3
    RCHDIF53        N4  -1        DIFFICULTY REACHING OVERHEAD - RD 5/3       OTPUBB14        N4  2         COV OTH GOV NOT MCAID/SCHIP HMO-12/31/14
    FNGRDF31        N4  -1        DIFFICULTY USING FINGERS TO GRASP-RD 3/1    PRIDK31         N4  2         COV BY PRIV INS (DK PLAN) - R3/1 INT
    FNGRDF53        N4  -1        DIFFICULTY USING FINGERS TO GRASP-RD 5/3    PRIDK42         N4  2         COV BY PRIV INS (DK PLAN) - R4/2 INT
    ACTLIM31        N4  -1        ANY LIMITATION WORK/HOUSEWRK/SCHL-RD 3/1    PRIDK53         N4  2         COV BY PRIV INS (DK PLAN) 12-31/R3 INT
    ACTLIM53        N4  -1        ANY LIMITATION WORK/HOUSEWRK/SCHL-RD 5/3    PRIDK14         N4  2         COV BY PRIV INS (DK PLAN) - 12/31/14
    WRKLIM31        N4  -1        WORK LIMITATION - RD 3/1                    PRIEU31         N4  2         COV BY EMPL/UNION GRP INS - R3/1 INT DT
    WRKLIM53        N4  -1        WORK LIMITATION - RD 5/3                    PRIEU42         N4  1         COV BY EMPL/UNION GRP INS - R4/2 INT DT
    HSELIM31        N4  -1        HOUSEWORK LIMITATION - RD 3/1               PRIEU53         N4  1         COV BY EMPL/UNION GRP INS 12-31/R3 INT
    HSELIM53        N4  -1        HOUSEWORK LIMITATION - RD 5/3               PRIEU14         N4  1         COV BY EMPL/UNION GRP INS - 12/31/14
    SCHLIM31        N4  -1        SCHOOL LIMITATION - RD 3/1                  PRING31         N4  2         COV BY NON-GROUP INS - R3/1 INT DT
    SCHLIM53        N4  -1        SCHOOL LIMITATION - RD 5/3                  PRING42         N4  2         COV BY NON-GROUP INS - R4/2 INT DT
    UNABLE31        N4  -1        COMPLETELY UNABLE TO DO ACTIVITY-RD 3/1     PRING53         N4  2         COV BY NON-GROUP INS 12-31/R3 INT DT
    UNABLE53        N4  -1        COMPLETELY UNABLE TO DO ACTIVITY-RD 5/3     PRING14         N4  2         COV BY NON-GROUP INS - 12/31/14
    SOCLIM31        N4  2         SOCIAL LIMITATIONS - RD 3/1                 PRIOG31         N4  2         COV BY OTHER GROUP INS - R3/1 INT DT
    SOCLIM53        N4  2         SOCIAL LIMITATIONS - RD 5/3                 PRIOG42         N4  2         COV BY OTHER GROUP INS - R4/2 INT DT
    COGLIM31        N4  -1        COGNITIVE LIMITATIONS - RD 3/1              PRIOG53         N4  2         COV BY OTHER GROUP INS 12-31/R3 INT DT
    COGLIM53        N4  -1        COGNITIVE LIMITATIONS - RD 5/3              PRIOG14         N4  2         COV BY OTHER GROUP INS - 12/31/14
    DFHEAR42        N4  -1        SERIOUS DIFFICULTY HEARING-RD 4/2           PRIS31          N4  2         COV BY SELF-EMP-1 INS - R3/1 INT DT
    DEAF42          N4  -1        PERSON IS DEAF - RD 4/2                     PRIS42          N4  2         COV BY SELF-EMP-1 INS - R4/2 INT DT
    DFSEE42         N4  -1        SERIOUS DIFFICULTY SEE W/GLASSES-RD 4/2     PRIS53          N4  2         COV BY SELF-EMP-1 INS 12-31/R3 INT DT
    BLIND42         N4  -1        PERSON IS BLIND - RD 4/2                    PRIS14          N4  2         COV BY SELF-EMP-1 INS - 12/31/14
    DFCOG42         N4  -1        SERIOUS COGNITIVE DIFFICULTIES-RD 4/2       PROUT31         N4  2         COV BY SOMEONE OUT OF RU - R3/1 INT
    DFWLKC42        N4  -1        SERIOUS DIFCULTY WLK/CLIMB STAIRS-RD 4/2    PROUT42         N4  2         COV BY SOMEONE OUT OF RU - R4/2 INT
    DFDRSB42        N4  -1        DIFFICULTY DRESSING/BATHING-RD 4/2          PROUT53         N4  2         COV BY SOMEONE OUT OF RU 12-31/R3 INT DT
    DFERND42        N4  -1        DIFFICULTY DOING ERRANDS ALONE-RD 4/2       PROUT14         N4  2         COV BY SOMEONE OUT OF RU - 12/31/14
    HEARAD42        N4  2         PERSON WEARS HEARING AID - RD 4/2           PRSTX31         N4  2         COV BY PRIV EXCHANGE INS -R3/1 INT DT
    WRGLAS42        N4  2         WEARS EYEGLASSES OR CONTACTS - RD 4/2       PRSTX42         N4  2         COV BY PRIV EXCHANGE INS -R4/2 INT DT
    ANYLMT14        N4  -9        ANY LIMITATION IN P18R3,4,5/P19R1,2,3       PRSTX53         N4  2         PRIV EXCHANGE INS ON 12-31 R5/R3 INT DT
    CHPMED42        N4  2         CSHCN:CHILD NEEDS PRESCRB MED(0-17)-R4/2    PRSTX14         N4  2         PRIV EXCHANGE INSURANCE ON 12/31/14
    CHPMHB42        N4  -1        CSHCN:PMED FOR HLTH/BEHV COND(0-17)-R4/2    PRIV31          N4  2         COV BY PRIV HLTH INS - R3/1 INT DATE
    CHPMCN42        N4  -1        CSHCN:PMED COND LAST 12+ MOS (0-17)-R4/2    PRIV42          N4  1         COV BY PRIV HLTH INS - R4/2 INT DATE
    CHSERV42        N4  2         CSHCN:CHLD NEEDS MED&OTH SERV(0-17)-R4/2    PRIV53          N4  1         COV BY PRIV HLTH INS 12-31/R3 INT DATE
    CHSRHB42        N4  -1        CSHCN:SERV FOR HLTH/BEHV COND(0-17)-R4/2    PRIV14          N4  1         COV BY PRIV HLTH INS - 12/31/14
    CHSRCN42        N4  -1        CSHCN:SERV COND LAST 12+ MOS (0-17)-R4/2    PRIVAT31        N4  2         ANY TIME COV PRIVATE INS - R3/1
    CHLIMI42        N4  2         CSHCN:LIMITED IN ANY WAY (0-17)-R4/2        PRIVAT42        N4  1         ANY TIME COV PRIVATE INS - R4/2
    CHLIHB42        N4  -1        CSHCN:LIMT FOR HLTH/BEHV COND(0-17)-R4/2    PRIVAT53        N4  1         ANY TIME COV PRIVATE INS - R5/3
    CHLICO42        N4  -1        CSHCN:LIMIT COND LAST 12+MOS (0-17)-R4/2    PRIVAT14        N4  1         ANY TIME COV PRIVATE INS - 12/31/14
    CHTHER42        N4  2         CSHCN:CHLD NEEDS SPEC THERAPY(0-17)-R4/2    PUB31X          N4  2         COV BY PUBLIC INS - R3/1 INT DT (ED)
    CHTHHB42        N4  -1        CSHCN:SPEC THER FOR HLTH+COND(0-17)-R4/2    PUB42X          N4  2         COV BY PUBLIC INS - R4/2 INT DT (ED)
    CHTHCO42        N4  -1        CSHCN:THER COND LAST 12+ MOS (0-17)-R4/2    PUB53X          N4  2         COV BY PUBLIC INS 12-31/R3 INT DT (ED)
    CHCOUN42        N4  2         CSHCN:CHILD NEEDS COUNSELING (0-17)-R4/2    PUB14X          N4  2         COV BY PUBLIC INS - 12/31/14 (ED)
    CHEMPB42        N4  -1        CSHCN:COUNS PROB LAST 12+MOS (0-17)-R4/2    PUBAT31X        N4  2         ANY TIME COV BY PUBLIC - R3/1
    CSHCN42         N4  2         CSHCN:CHILD W/SPEC HC NEEDS (0-17)-R4/2     PUBAT42X        N4  2         ANY TIME COV BY PUBLIC - R4/2
    MOMPRO42        N4  -1        PROBLEM GETTING ALONG W/MOM (5-17)-R4/2     PUBAT53X        N4  2         ANY TIME COV BY PUBLIC - R5/3
    DADPRO42        N4  -1        PROBLEM GETTING ALONG W/DAD (5-17)-R4/2     PUBAT14X        N4  2         ANY TIME COV BY PUBLIC - 12/31/14
    UNHAP42         N4  -1        PROBLEM FEELING UNHAPPY/SAD (5-17)-R4/2     INS31X          N4  2         INSURED - R3/1 INT DATE (ED)
    SCHLBH42        N4  -1        PROBLEM BEHAVIOR AT SCHOOL (5-17)-R4/2      INS42X          N4  1         INSURED - R4/2 INT DATE (ED)
    HAVFUN42        N4  -1        PROBLEM HAVING FUN (5-17) - R4/2            INS53X          N4  1         INSURED 12-31/R3 INT DATE (ED)
    ADUPRO42        N4  -1        PRBLM GETTING ALONG W/ADULTS (5-17)-R4/2    INS14X          N4  1         INSURED - 12/31/14 (ED)
    NERVAF42        N4  -1        PRBLM FEELING NERVOUS/AFRAID (5-17)-R4/2    INSAT31X        N4  2         INSURED ANY TIME IN R3/1
    SIBPRO42        N4  -1        PRBLM GETTING ALONG W/SIBS (5-17)-R4/2      INSAT42X        N4  1         INSURED ANY TIME IN R4/2
    KIDPRO42        N4  -1        PRBLM GETTING ALONG W/KIDS (5-17)-R4/2      INSAT53X        N4  1         INSURED ANY TIME IN R5/3
    SPRPRO42        N4  -1        PROBLEM W/SPORTS/HOBBIES (5-17)-R4/2        INSAT14X        N4  1         INSURED ANY TIME IN R5/R3 UNTIL 12/31/14
    SCHPRO42        N4  -1        PROBLEM WITH SCHOOLWORK (5-17)-R4/2         STAPR31         N4  2         COV BY STATE-SPEC PROG - R3/1 INT DT
    HOMEBH42        N4  -1        PROBLEM W/BEHAVIOR AT HOME (5-17)-R4/2      STAPR42         N4  2         COV BY STATE-SPEC PROG - R4/2 INT DT
    TRBLE42         N4  -1        PRBLM STAY OUT OF TROUBLE (5-17)-R4/2       STAPR53         N4  2         COV BY STATE-SPEC PROG 12-31/R3 INT DT
    CHILCR42        N4  2         CAHPS:12MOS:ILL/INJ NEED CARE(0-17)-R4/2    STAPR14         N4  2         COV BY STATE-SPEC PROG - 12/31/14
    CHILWW42        N4  -1        CAHPS:12MOS:ILL CARE WHN WNTD(0-17)-R4/2    STPRAT31        N4  2         ANY TIME COVERAGE BY STATE INS - R3/1
    CHRTCR42        N4  1         CAHPS:12MOS:MAKE ROUT CARE APT(0-17)R4/2    STPRAT42        N4  2         ANY TIME COVERAGE BY STATE INS - R4/2
    CHRTWW42        N4  4         CAHPS:12MOS:ROUT APT WHN WNTD(0-17)-R4/2    STPRAT53        N4  2         ANY TIME COVERAGE BY STATE INS - R5/3
    CHAPPT42        N4  1         CAHPS:12MOS:# OF OFF/CLIN APTS(0-17)R4/2    STPRAT14        N4  2         ANY TIME COV BY STATE INS - 12/31/14
    CHNDCR42        N4  1         CAHPS:12MOS:NEED ANY CARE/TRT(0-17)-R4/2    DENTIN31        N4  2         DENTAL INSURANCE - RD 3/1
    CHENEC42        N4  4         CAHPS:12MOS:EASY GET NEC CARE (0-17)R4/2    DENTIN42        N4  1         DENTAL INSURANCE - RD 4/2
    CHLIST42        N4  4         CAHPS:12MOS:CHLD DR LSN TO YOU(0-17)R4/2    DENTIN53        N4  1         DENTAL INSURANCE - RD 5/3
    CHEXPL42        N4  4         CAHPS:12MOS:CHLD DR EXPL THNG(0-17)R4/2     DNTINS31        N4  2         DENTAL INS - RD 3/1 IN 14
    CHRESP42        N4  4         CAHPS:12MOS:CHLD'S DR SHW RESP(0-17)R4/2    DNTINS14        N4  1         DENTAL INS - R5/R3 UNTIL 12/31/14
    CHPRTM42        N4  4         CAHPS:12MOS:CHILD DR ENGH TIME(0-17)R4/2    PMEDIN31        N4  2         PRESCRIPTION DRUG INSURANCE - RD 3/1
    CHHECR42        N4  10        CAHPS:12MOS:RATE CHLD HLT CARE(0-17)R4/2    PMEDIN42        N4  1         PRESCRIPTION DRUG INSURANCE - RD 4/2
    CHSPEC42        N4  2         CAHPS:12MOS:CHLD NEEDED SPEC(0-17)R4/2      PMEDIN53        N4  1         PRESCRIPTION DRUG INSURANCE - RD 5/3
    CHEYRE42        N4  -1        CAHPS:12MOS:ESY W/RFR TO SPEC(0-17)-R4/2    PMDINS31        N4  2         PMED INS - RD 3/1 IN 14
    MESHGT42        N4  1         DOCTOR EVER MEASURED HEIGHT (0-17)-R4/2     PMDINS14        N4  1         PMED INS - R5/R3 UNTIL 12/31/14
    WHNHGT42        N4  1         WHEN DOCTOR MEASURED HEIGHT (0-17)-R4/2     PMEDUP31        N4  -1        HAS USUAL 3RD PARTY PAYER FOR PMEDS-R3/1
    MESWGT42        N4  1         DOCTOR EVER MEASURED WEIGHT (0-17)-R4/2     PMEDUP42        N4  1         HAS USUAL 3RD PARTY PAYER FOR PMEDS-R4/2
    WHNWGT42        N4  1         WHEN DOCTOR MEASURED WEIGHT (0-17)-R4/2     PMEDUP53        N4  1         HAS USUAL 3RD PARTY PAYER FOR PMEDS-R5/3
    CHBMIX42        N8  -1        CHILD'S BODY MASS INDEX (6-17)-R4/2         PMEDPY31        N4  -1        USUAL 3RD PARTY PAYER FOR PMEDS - R3/1
    MESVIS42        N4  -1        DOCTOR CHECKED CHILD'S VISION (3-6)-R4/2    PMEDPY42        N4  1         USUAL 3RD PARTY PAYER FOR PMEDS - R4/2
    MESBPR42        N4  -1        DR CHECKED BLOOD PRESSURE (2-17)-R4/2       PMEDPY53        N4  1         USUAL 3RD PARTY PAYER FOR PMEDS - R5/3
    WHNBPR42        N4  -1        WHEN DR CHECKED BLOOD PRESS (2-17)-R4/2     TOTTCH14        N8  3894      TOTAL HEALTH CARE CHARGES 14, EXCL RX
    DENTAL42        N4  -1        DR ADVISE REG DENTAL CHECKUP (2-17)-R4/2    TOTEXP14        N8  2162      TOTAL HEALTH CARE EXP 14
    WHNDEN42        N4  -1        WHEN DR ADVISE DENT CHECKUP (2-17)-R4/2     TOTSLF14        N8  424       TOTAL AMT PAID BY SELF/FAMILY 14
    EATHLT42        N4  -1        DR ADVISE EAT HEALTHY (2-17)-R4/2           TOTMCR14        N8  0         TOTAL AMT PAID BY MEDICARE 14
    WHNEAT42        N4  -1        WHEN DR ADVISE EAT HEALTHY (2-17)-R4/2      TOTMCD14        N8  0         TOTAL AMT PAID BY MEDICAID 14
    PHYSCL42        N4  -1        DR ADVISE EXERCISE (2-17)-R4/2              TOTPRV14        N8  1738      TOTAL AMT PAID BY PRIVATE INS 14
    WHNPHY42        N4  -1        WHEN DR ADVISE EXERCISE (2-17)-R4/2         TOTVA14         N8  0         TOTAL AMT PAID BY VA/CHAMPVA 14
    SAFEST42        N4  1         DR ADVISE CHLD SAFETY SEAT (WT<=40)-R4/2    TOTTRI14        N8  0         TOTAL AMT PAID BY TRICARE 14
    WHNSAF42        N4  1         WHEN DR ADVISE SAFETY SEAT (WT<=40)-R4/2    TOTOFD14        N8  0         TOTAL AMT PAID BY OTHER FEDERAL 14
    BOOST42         N4  -1        DR ADVISE BOOSTER SEAT (40<WT<=80)-R4/2     TOTSTL14        N8  0         TOTAL AMT PAID BY OTH ST/LOCAL 14
    WHNBST42        N4  -1        WHN DR ADVISE BOOST SEAT(40<WT<=80)-R4/2    TOTWCP14        N8  0         TOTAL AMT PAID BY WORKERS COMP 14
    LAPBLT42        N4  -1        DR ADVISE LAP/SHOULDER BELT (80<WT)-R4/2    TOTOPR14        N8  0         TOTAL AMT PAID BY OTHER PRIVATE 14
    WHNLAP42        N4  -1        WHN DR ADVISE LAP/SHLDR BLT (80<WT)-R4/2    TOTOPU14        N8  0         TOTAL AMT PAID BY OTHER PUBLIC 14
    HELMET42        N4  -1        DR ADVISE BIKE HELMET (2-17)-R4/2           TOTOSR14        N8  0         TOTAL AMT PAID BY OTHER SOURCES 14
    WHNHEL42        N4  -1        WHEN DR ADVISE BIKE HELMET (2-17)-R4/2      TOTPTR14        N8  1738      TOTAL AMT PAID BY PRV & TRI 14
    NOSMOK42        N4  2         DR ADVISE SMKG IN HOME IS BAD(0-17)-R4/2    TOTOTH14        N8  0         TOTAL AMT PAID BY OTH COMBINED 14
    WHNSMK42        N4  -1        WHN DR ADVIS SMKG IN HOME BAD(0-17)-R4/2    OBTOTV14        N4  3         # OFFICE-BASED PROVIDER VISITS 14
    TIMALN42        N4  -1        DOCTOR SPEND ANY TIME ALONE (12-17)-R4/2    OBVTCH14        N8  3894      OFFICE-BASED PROVIDER VISIT CHARGES 14
    DENTCK53        N4  -1        HOW OFTEN DENTAL CHECK-UP - RD 5/3          OBVEXP14        N8  2150      TOTAL OFFICE-BASED EXP 14
    BPCHEK53        N4  -1        TIME SNCE LST BLOOD PRES CHK (>17)-RD5/3    OBVSLF14        N8  412       ALL OFFICE VISITS - SELF/FAMILY AMT 14
    CHOLCK53        N4  -1        HOW LNG CHOLEST LST CHCK (>17) - RD 5/3     OBVMCR14        N8  0         ALL OFFICE VISITS - MEDICARE AMT 14
    CHECK53         N4  -1        HOW LNG LST ROUTNE CHECKUP (>17)-RD 5/3     OBVMCD14        N8  0         ALL OFFICE VISITS - MEDICAID AMT 14
    NOFAT53         N4  -1        RESTRICT HGH FAT/CHOLES FOOD (>17)-RD5/3    OBVPRV14        N8  1738      ALL OFFICE VISITS - PRIVATE INS AMT 14
    EXRCIS53        N4  -1        ADVISED TO EXERCISE MORE (>17) - RD 5/3     OBVVA14         N8  0         ALL OFFICE VISITS-VA/CHAMPVA AMT 14
    FLUSHT53        N4  -1        HOW LNG LAST FLU VACINATION (>17)-RD 5/3    OBVTRI14        N8  0         ALL OFFICE VISITS-TRICARE AMT 14
    ASPRIN53        N4  -1        TKE ASPIRN EVERY (OTHR) DAY (>17)-RD 5/3    OBVOFD14        N8  0         ALL OFFICE VISITS-OTHER FEDERAL AMT 14
    NOASPR53        N4  -1        TAKING ASPIRIN UNSAFE (>17) - RD 5/3        OBVSTL14        N8  0         ALL OFFICE VISITS-OTH ST/LOCAL AMT 14
    STOMCH53        N4  -1        TKE ASPRN UNSAFE B/C STOMCH (>17)-RD 5/3    OBVWCP14        N8  0         ALL OFFICE VISITS - WORKERS COMP AMT 14
    LSTETH53        N4  -1        LOST ALL UPPR AND LOWR TEETH (>17)-RD5/3    OBVOPR14        N8  0         ALL OFFICE VISITS - OTH PRIVATE AMT 14
    PSA53           N4  -1        HOW LONG SINCE LAST PSA (>39) - RD 5/3      OBVOPU14        N8  0         ALL OFFICE VISITS - OTH PUBLIC AMT 14
    HYSTER53        N4  -1        HAD A HYSTERECTOMY (>17) - RD 5/3           OBVOSR14        N8  0         ALL OFF VSTS - OTH UNCLASS SRCE AMT 14
    PAPSMR53        N4  -1        HOW LNG LST PAP SMEAR TST (>17) - RD 5/3    OBVPTR14        N8  1738      ALL OFFICE VISITS - PRV & TRI AMT 14
    BRSTEX53        N4  -1        HOW LNG SNCE LST BREAST EXAM (>17)-RD5/3    OBVOTH14        N8  0         ALL OFFICE VISITS - OTH COMBINED AMT 14
    MAMOGR53        N4  -1        HOW LNG SNCE LST MAMMOGRAM (>29) - RD5/3    OBDRV14         N4  3         # OFFICE-BASED PHYSICIAN VISITS 14
    BSTST53         N4  -1        MST RCNT BLD STOOL TST HME KIT(>39)-R5/3    OBDTCH14        N8  3894      OFFICE-BASED PHYSICIAN VISIT CHARGES 14
    BSTSRE53        N4  -1        RSN HAVE BLD STOOL TST (>39)-R5/3           OBDEXP14        N8  2150      TOTAL OFF-BASED DR EXP 14
    CLNTST53        N4  -1        MOST RECENT COLONOSCOPY (>39) - R5/3        OBDSLF14        N8  412       DR OFFICE VISITS - SELF/FAMILY AMT 14
    CLNTRE53        N4  -1        RSN HAVE COLONOSCOPY (>39)-R5/3             OBDMCR14        N8  0         DR OFFICE VISITS - MEDICARE AMT 14
    SGMTST53        N4  -1        MOST RECENT SIGMOIDOSCOPY (>39) - R5/3      OBDMCD14        N8  0         DR OFFICE VISITS - MEDICAID AMT 14
    SGMTRE53        N4  -1        RSN HAVE SIGMOIDOSCOPY (>39)-R5/3           OBDPRV14        N8  1738      DR OFFICE VISITS - PRIVATE INS AMT 14
    PHYEXE53        N4  -1        MOD/VIG PHYS EXEC 5X WK (>17) - RD 5/3      OBDVA14         N8  0         DR OFFICE VISITS - VA/CHAMPVA AMT 14
    BMINDX53        N8  -1        ADULT BODY MASS INDEX (>17) - RD 5/3        OBDTRI14        N8  0         DR OFFICE VISITS - TRICARE AMT 14
    SEATBE53        N4  -1        WEARS SEAT BELT (>15) - RD 5/3              OBDOFD14        N8  0         DR OFFICE VISITS - OTHER FEDERAL AMT 14
    SAQELIG         N4  0         ELIGIBILITY STATUS FOR SAQ                  OBDSTL14        N8  0         DR OFFICE VISITS - OTH ST/LOCAL AMT 14
    ADPRX42         N4  -1        SAQ: RELATIONSHIP OF PROXY TO ADULT         OBDWCP14        N8  0         DR OFFICE VISITS - WORKERS COMP AMT 14
    ADILCR42        N4  -1        SAQ 12MOS: ILL/INJURY NEEDING IMMED CARE    OBDOPR14        N8  0         DR OFFICE VISITS - OTH PRIVATE AMT 14
    ADILWW42        N4  -1        SAQ 12 MOS: GOT CARE WHEN NEEDED ILL/INJ    OBDOPU14        N8  0         DR OFFICE VISITS - OTH PUBLIC AMT 14
    ADRTCR42        N4  -1        SAQ 12 MOS: MADE APPT ROUTINE MED CARE      OBDOSR14        N8  0         DR OFF VSTS - OTH UNCLASS SRCE AMT 14
    ADRTWW42        N4  -1        SAQ 12 MOS: GOT MED APPT WHEN WANTED        OBDPTR14        N8  1738      DR OFFICE VISITS - PRV & TRI AMT 14
    ADAPPT42        N4  -1        SAQ 12 MOS: # VISITS TO MED OFF FOR CARE    OBDOTH14        N8  0         DR OFFICE VISITS - OTH COMBINED AMT 14
    ADNDCR42        N4  -1        SAQ 12MOS: NEED ANY CARE, TEST, TREATMNT    OBOTHV14        N4  0         # OFFICE-BASED NON-PHYSICAN VISITS 14
    ADEGMC42        N4  -1        SAQ 12MOS: EASY GETTING NEEDED MED CARE     OBOTCH14        N8  0         OFFICE-BASED NON-DR VISIT CHARGES 14
    ADLIST42        N4  -1        SAQ 12 MOS: DOCTOR LISTENED TO YOU          OBOEXP14        N8  0         TOTAL OFF-BASED NON-DR EXP 14
    ADEXPL42        N4  -1        SAQ 12 MOS: DOC EXPLAINED SO UNDERSTOOD     OBOSLF14        N8  0         NON-DR OFF VISTS - SELF/FAMILY AMT 14
    ADRESP42        N4  -1        SAQ 12 MOS: DR SHOWED RESPECT               OBOMCR14        N8  0         NON-DR OFF VISTS - MEDICARE AMT 14
    ADPRTM42        N4  -1        SAQ 12 MOS: DR SPENT ENUF TIME WITH YOU     OBOMCD14        N8  0         NON-DR OFF VISTS - MEDICAID AMT 14
    ADINST42        N4  -1        SAQ 12 MOS: DR GAVE SPCIFC INSTRCTNS        OBOPRV14        N8  0         NON-DR OFF VISTS - PRIVATE INS AMT 14
    ADEZUN42        N4  -1        SAQ 12 MOS: DR GIVEN INSTR. EZ UNDRSTD      OBOVA14         N8  0         NON-DR OFF VISTS - VA/CHAMPVA AMT 14
    ADTLHW42        N4  -1        SAQ 12 MOS: DR ASKED R DESC HOW FOLLOW      OBOTRI14        N8  0         NON-DR OFF VISTS - TRICARE AMT 14
    ADFFRM42        N4  -1        SAQ 12 MOS: HAD TO FILL OUT/SIGN FORMS      OBOOFD14        N8  0         NON-DR OFF VISTS - OTHER FEDERAL AMT 14
    ADFHLP42        N4  -1        SAQ 12 MOS: OFFRD HELP FILLING OUT FORMS    OBOSTL14        N8  0         NON-DR OFF VISTS - OTH ST/LOCAL AMT 14
    ADHECR42        N4  -1        SAQ 12 MOS: RATING OF HEALTH CARE           OBOWCP14        N8  0         NON-DR OFF VISTS - WORKERS COMP AMT 14
    ADSMOK42        N4  -1        SAQ: CURRENTLY SMOKE                        OBOOPR14        N8  0         NON-DR OFF VISTS - OTH PRIVATE AMT 14
    ADNSMK42        N4  -1        SAQ 12MOS: DR ADVISED TO QUIT SMOKING       OBOOPU14        N8  0         NON-DR OFF VISTS - OTH PUBLIC AMT 14
    ADDRBP42        N4  -1        SAQ 2 YRS: DR CHECKED BLOOD PRESSURE        OBOOSR14        N8  0         NON-DR OF VSTS - OTH UNCLASS SRCE AMT 14
    ADSPEC42        N4  -1        SAQ 12 MOS: NEEDED TO SEE SPECIALIST        OBOPTR14        N8  0         NON-DR OFF VISTS - PRV & TRI AMT 14
    ADESSP42        N4  -1        SAQ 12MOS: HOW ESY TO SEE SPECIALIST        OBOOTH14        N8  0         NON-DR OFF VISTS - OTH COMBINED AMT 14
    ADGENH42        N4  -1        SAQ: HEALTH IN GENERAL SF-12V2              OBCHIR14        N4  0         # OFFICE-BASED CHIROPRACTOR VISITS 14
    ADDAYA42        N4  -1        SAQ: HLTH LIMITS MOD ACTIVITIES SF-12V2     OBCTCH14        N8  0         OFFICE-BASED CHIRO VISIT CHARGES 14
    ADCLIM42        N4  -1        SAQ: HLTH LIMITS CLIMBING STAIRS SF-12V2    OBCEXP14        N8  0         TOTAL OFF-BASED CHIRO EXP 14
    ADPALS42        N4  -1        SAQ 4WKS:ACCMP LESS B/C PHY PRBS SF-12V2    OBCSLF14        N8  0         CHIRO OFF VISITS - SELF/FAMILY AMT 14
    ADPWLM42        N4  -1        SAQ 4WKS:WORK LIMT B/C PHY PROBS SF-12V2    OBCMCR14        N8  0         CHIRO OFF VISITS - MEDICARE AMT 14
    ADMALS42        N4  -1        SAQ 4WKS:ACCMP LESS B/C MNT PRBS SF-12V2    OBCMCD14        N8  0         CHIRO OFF VISITS - MEDICAID AMT 14
    ADMWLM42        N4  -1        SAQ 4WKS:WORK LIMT B/C MNT PROBS SF-12V2    OBCPRV14        N8  0         CHIRO OFF VISITS - PRIVATE INS AMT 14
    ADPAIN42        N4  -1        SAQ 4WKS:PAIN LIMITS NORMAL WORK SF-12V2    OBCVA14         N8  0         CHIRO OFF VISITS - VA/CHAMPVA AMT 14
    ADCAPE42        N4  -1        SAQ 4WKS: FELT CALM/PEACEFUL SF-12V2        OBCTRI14        N8  0         CHIRO OFF VISITS - TRICARE AMT 14
    ADNRGY42        N4  -1        SAQ 4WKS: HAD A LOT OF ENERGY SF-12V2       OBCOFD14        N8  0         CHIRO OFF VISITS - OTHER FEDERAL AMT 14
    ADDOWN42        N4  -1        SAQ 4WKS: FELT DOWNHEARTED/DEPR SF-12V2     OBCSTL14        N8  0         CHIRO OFF VISITS - OTH ST/LOCAL AMT 14
    ADSOCA42        N4  -1        SAQ 4WKS: HLTH STOPPED SOC ACTIV SF-12V2    OBCWCP14        N8  0         CHIRO OFF VISITS - WORKERS COMP AMT 14
    PCS42           N8  -1        SAQ:PHY COMPONENT SUMMRY SF-12V2 IMPUTED    OBCOPR14        N8  0         CHIRO OFF VISTS - OTHR PRIVATE AMT 14
    MCS42           N8  -1        SAQ:MNT COMPONENT SUMMRY SF-12V2 IMPUTED    OBCOPU14        N8  0         CHIRO OFF VISTS - OTHR PUBLIC AMT 14
    SFFLAG42        N4  -1        SAQ: PCS/MCS IMPUTATION FLAG SF-12V2        OBCOSR14        N8  0         CHIRO OFF VSTS-OTHR UNCLASS SRCE AMT 14
    ADNERV42        N4  -1        SAQ 30 DAYS: HOW OFTEN FELT NERVOUS         OBCPTR14        N8  0         CHIRO OFF VISITS - PRV & TRI AMT 14
    ADHOPE42        N4  -1        SAQ 30 DAYS: HOW OFTEN FELT HOPELESS        OBCOTH14        N8  0         CHIRO OFF VISITS -OTH COMBINED AMT 14
    ADREST42        N4  -1        SAQ 30 DAYS: HOW OFTEN FELT RESTLESS        OBNURS14        N4  0         # OFF-BASED NURSE/PRACTITIONER VISITS 14
    ADSAD42         N4  -1        SAQ 30 DAYS: HOW OFTEN FELT SAD             OBNTCH14        N8  0         OFFICE-BASED NURSE/PRAC VISIT CHARGES 14
    ADEFRT42        N4  -1        SAQ 30 DAYS: HOW OFTN EVRYTHNG AN EFFORT    OBNEXP14        N8  0         TOTAL OFF-BASED NURSE/PRAC 14
    ADWRTH42        N4  -1        SAQ 30 DAYS: HOW OFTEN FELT WORTHLESS       OBNSLF14        N8  0         NURSE/PRAC OFF VISITS-SELF/FAMILY AMT 14
    K6SUM42         N4  -1        SAQ 30 DAYS: OVERALL RATING OF FEELINGS     OBNMCR14        N8  0         NURSE/PRAC OFF VISITS - MEDICARE AMT 14
    ADINTR42        N4  -1        SAQ 2 WKS: LITTLE INTEREST IN THINGS        OBNMCD14        N8  0         NURSE/PRAC OFF VSTS - MEDICAID AMT 14
    ADDPRS42        N4  -1        SAQ 2 WKS: FELT DOWN/DEPRESSED/HOPELESS     OBNPRV14        N8  0         NURSE/PRAC OFF VSTS-PRIVATE INS AMT 14
    PHQ242          N4  -1        SAQ 2 WKS: OVERALL RATING OF FEELINGS       OBNVA14         N8  0         NURSE/PRAC OFF VSTS - VA/CHAMPVA AMT 14
    ADINSA42        N4  -1        SAQ: DO NOT NEED HEALTH INSURANCE           OBNTRI14        N8  0         NURSE/PRAC OFF VSTS - TRICARE AMT 14
    ADINSB42        N4  -1        SAQ: HEALTH INSURANCE NOT WORTH COST        OBNOFD14        N8  0         NURSE/PRAC OFF VSTS-OTHER FEDERAL AMT 14
    ADRISK42        N4  -1        SAQ: MORE LIKELY TO TAKE RISKS              OBNSTL14        N8  0         NURSE/PRAC OFF VSTS-OTH ST/LOCAL AMT 14
    ADOVER42        N4  -1        SAQ: CAN OVERCOME ILLS WITHOUT MED HELP     OBNWCP14        N8  0         NURSE/PRAC OFF VSTS-WORKERS COMP AMT 14
    ADCMPM42        N4  -1        SAQ: DATE COMPLETED - MONTH                 OBNOPR14        N8  0         NURSE/PRAC OFF VSTS - OTH PRIVATE AMT 14
    ADCMPY42        N5  -1        SAQ: DATE COMPLETED - YEAR                  OBNOPU14        N8  0         NURSE/PRAC OFF VSTS - OTH PUBLIC AMT 14
    ADLANG42        N4  -1        SAQ: LANGUAGE OF SAQ INTERVIEW              OBNOSR14        N8  0         NRS/PR OFF VSTS-OTH UNCLASS SRCE AMT 14
    DSDIA53         N4  -1        DCS: DIABETES DIAGNOSIS BY HEALTH PROF      OBNPTR14        N8  0         NURSE/PRAC OFF VSTS - PRV & TRI AMT 14
    DSA1C53         N4  -1        DCS: TIMES TESTED FOR A-ONE-C IN 2013       OBNOTH14        N8  0         NURSE/PRAC OFF VSTS-OTH COMBINED AMT 14
    DSFT1553        N4  -1        DCS: HAD FEET CHECKED DURING 2015           OBOPTO14        N4  0         # OFF-BASED OPTOMETRIST VISITS 14
    DSFT1453        N4  -1        DCS: HAD FEET CHECKED DURING 2014           OBETCH14        N8  0         OFFICE-BASED OPTOMTRIST VISIT CHARGES 14
    DSFT1353        N4  -1        DCS: HAD FEET CHECKED DURING 2013           OBEEXP14        N8  0         TOTAL OFF-BASED OPTOMETRIST EXP 14
    DSFB1353        N4  -1        DCS: HAD FEET CHECKED BEFORE 2013           OBESLF14        N8  0         OPTOMETRIST OFF VSTS-SELF/FAMILY AMT 14
    DSFTNV53        N4  -1        DCS: NEVER HAD FEET CHECKED                 OBEMCR14        N8  0         OPTOMETRIST OFF VSTS - MEDICARE AMT 14
    DSEY1553        N4  -1        DCS: DILATED EYE EXAM IN 2015               OBEMCD14        N8  0         OPTOMETRIST OFF VSTS - MEDICAID AMT 14
    DSEY1453        N4  -1        DCS: DILATED EYE EXAM IN 2014               OBEPRV14        N8  0         OPTOMETRIST OFF VSTS-PRIVATE INS AMT 14
    DSEY1353        N4  -1        DCS: DILATED EYE EXAM IN 2013               OBEVA14         N8  0         OPTOMETRIST OFF VSTS - VA/CHAMPVA AMT 14
    DSEB1353        N4  -1        DCS: DILATED EYE EXAM BEFORE 2013           OBETRI14        N8  0         OPTOMETRIST OFF VSTS - TRICARE AMT 14
    DSEYNV53        N4  -1        DCS: NEVER HAD DILATED EYE EXAM             OBEOFD14        N8  0         OPTOMETRIST OFF VSTS-OTH FEDERAL AMT 14
    DSCH1553        N4  -1        DCS: BLOOD CHOLESTEROL CHECKED IN 2015      OBESTL14        N8  0         OPTOMETRIST OFF VSTS-OTH ST/LOCL AMT 14
    DSCH1453        N4  -1        DCS: BLOOD CHOLESTEROL CHECKED IN 2014      OBEWCP14        N8  0         OPTOMETRIST OFF VSTS-WORKERS COMP AMT 14
    DSCH1353        N4  -1        DCS: BLOOD CHOLESTEROL CHECKED IN 2013      OBEOPR14        N8  0         OPTOMETRIST OFF VSTS-OTH PRIVATE AMT 14
    DSCB1353        N4  -1        DCS: BLOOD CHOLESTEROL CHECKED BEF 2013     OBEOPU14        N8  0         OPTOMETRIST OFF VSTS - OTH PUBLIC AMT 14
    DSCHNV53        N4  -1        DCS: NEVER HAD BLOOD CHOLESTEROL CHECKED    OBEOSR14        N8  0         OPTOM OFF VSTS-OTH UNCLASS SRCE AMT 14
    DSFL1553        N4  -1        DCS: GOT FLU VACCINATION IN 2015            OBEPTR14        N8  0         OPTOMETRIST OFF VSTS - PRV & TRI AMT 14
    DSFL1453        N4  -1        DCS: GOT FLU VACCINATION IN 2014            OBEOTH14        N8  0         OPTOMETRIST OFF VSTS-OTH COMBINED AMT 14
    DSFL1353        N4  -1        DCS: GOT FLU VACCINATION IN 2013            OBASST14        N4  0         # OFF-BASED PHYSICIAN ASSIST VISITS 14
    DSVB1353        N4  -1        DCS: GOT FLU VACCINATION BEFORE 2013        OBATCH14        N8  0         OFFICE-BASED PHYS ASST VISIT CHARGES 14
    DSFLNV53        N4  -1        DCS: NEVER GOT FLU VACCINATION              OBAEXP14        N8  0         TOTAL OFF-BASED PHYS ASS T EXP 14
    DSKIDN53        N4  -1        DCS: HAS DIABETES CAUSED KIDNEY PROBLEMS    OBASLF14        N8  0         PHYS ASS T OFF VSTS - SELF/FAMILY AMT 14
    DSEYPR53        N4  -1        DCS: HAS DIABETES CAUSED EYE PROBS          OBAMCR14        N8  0         PHYS ASS T OFF VSTS - MEDICARE AMT 14
    DSDIET53        N4  -1        DCS: TREAT DIABETES W/DIET MODIFICATION     OBAMCD14        N8  0         PHYS ASS T OFF VSTS - MEDICAID AMT 14
    DSMED53         N4  -1        DCS: TREAT DIABETES W/MEDS BY MOUTH         OBAPRV14        N8  0         PHYS ASS T OFF VSTS - PRIVATE INS AMT 14
    DSINSU53        N4  -1        DCS: TREAT DIABETES W/INSULIN INJECTIONS    OBAVA14         N8  0         PHYS ASS T OFF VSTS - VA/CHAMPVA AMT 14
    DSCPCP53        N4  -1        DCS: LEARNED CARE FROM PRIMARY CARE PROV    OBATRI14        N8  0         PHYS ASS T OFF VSTS - TRICARE AMT 14
    DSCNPC53        N4  -1        DCS: LEARNED CARE FROM OTHER PROVIDER       OBAOFD14        N8  0         PHYS ASS T OFF VSTS - OTHER FED AMT 14
    DSCPHN53        N4  -1        DCS: LEARN CARE FROM PHONE CALL W/PROV      OBASTL14        N8  0         PHYS ASS T OFF VSTS - OTH ST/LOCL AMT 14
    DSCINT53        N4  -1        DCS: LEARNED CARE FROM READING INTERNET     OBAWCP14        N8  0         PHYS ASS T OFF VSTS-WORKERS COMP AMT 14
    DSCGRP53        N4  -1        DCS: LEARNED CARE BY TAKING GROUP CLASS     OBAOPR14        N8  0         PHYS ASS T OFF VSTS - OTH PRIVATE AMT 14
    DSCONF53        N4  -1        DCS: CONFIDENT TAKING CARE OF DIABETES      OBAOPU14        N8  0         PHYS ASS T OFF VSTS - OTH PUBLIC AMT 14
    DSPRX53         N4  -1        DCS: WAS RESPONDENT A PROXY                 OBAOSR14        N8  0         P A OFF VSTS - OTH UNCLASS SRCE AMT 14
    DDNWRK31        N4  -1        # DAYS MISSED WORK DUE TO ILL/INJ (RD31)    OBAPTR14        N8  0         PHYS ASST OFF VSTS - PRV & TRI AMT 14
    DDNWRK42        N4  -1        # DAYS MISSED WORK DUE TO ILL/INJ (RD42)    OBAOTH14        N8  0         PHYS ASST OFF VSTS - OTH COMBINED AMT 14
    DDNWRK53        N4  -1        # DAYS MISSED WORK DUE TO ILL/INJ (RD53)    OBTHER14        N4  0         # OFF-BASED PT/OT VISITS 14
    DDNSCL31        N4  -1        # DAYS MISSD SCHOOL DUE TO ILL/INJ(RD31)    OBTTCH14        N8  0         OFFICE-BASED PT/OC VISIT CHARGES 14
    DDNSCL42        N4  -1        # DAYS MISSD SCHOOL DUE TO ILL/INJ(RD42)    OBTEXP14        N8  0         TOT OFF-BASED PT EXP 14
    DDNSCL53        N4  -1        # DAYS MISSD SCHOOL DUE TO ILL/INJ(RD53)    OBTSLF14        N8  0         PT/OT OFF VISITS - SELF/FAMILY AMT 14
    OTHDYS31        N4  -1        MISS ANY WORK DAY TO CARE FOR OTH (RD31)    OBTMCR14        N8  0         PT/OT OFF VISITS - MEDICARE AMT 14
    OTHDYS42        N4  -1        MISS ANY WORK DAY TO CARE FOR OTH (RD42)    OBTMCD14        N8  0         PT/OT OFF VISITS - MEDICAID AMT 14
    OTHDYS53        N4  -1        MISS ANY WORK DAY TO CARE FOR OTH (RD53)    OBTPRV14        N8  0         PT/OT OFF VISITS - PRIVATE INS AMT 14
    OTHNDD31        N4  -1        # DAY MISSED WORK TO CARE FOR OTH (RD31)    OBTVA14         N8  0         PT/OT OFF VISITS - VA/CHAMPVA AMT 14
    OTHNDD42        N4  -1        # DAY MISSED WORK TO CARE FOR OTH (RD42)    OBTTRI14        N8  0         PT/OT OFF VISITS - TRICARE AMT 14
    OTHNDD53        N4  -1        # DAY MISSED WORK TO CARE FOR OTH (RD53)    OBTOFD14        N8  0         PT/OT OFF VISITS - OTHER FED AMT 14
    ACCELI42        N4  1         PERS ELIGIBLE FOR ACCESS SUPPLEMENT-R4/2    OBTSTL14        N8  0         PT/OT OFF VISITS - OTH ST/LOCL AMT 14
    HAVEUS42        N4  1         AC05 DOES PERSON HAVE USC PROVIDER-R4/2     OBTWCP14        N8  0         PT/OT OFF VISITS - WORKERS COMP AMT 14
    YNOUSC42        N4  -1        AC07 MAIN REAS PERS DOESNT HAVE USC-R4/2    OBTOPR14        N8  0         PT/OT OFF VISITS - OTH PRIVATE AMT 14
    NOREAS42        N4  -1        AC08 OTH REAS NO USC:NO OTH REASONS-R4/2    OBTOPU14        N8  0         PT/OT OFF VISITS - OTH PUBLIC AMT 14
    SELDSI42        N4  -1        AC08 OTH REAS NO USC:SELDM/NEV SICK-R4/2    OBTOSR14        N8  0         PT/OT OFF VSTS-OTH UNCLASS SRCE AMT 14
    NEWARE42        N4  -1        AC08 OTH REAS NO USC:RECENTLY MOVED-R4/2    OBTPTR14        N8  0         PT/OT OFF VISITS - PRV & TRI AMT 14
    DKWHRU42        N4  -1        AC08 OTH REAS NO USC:DK WHERE TO GO-R4/2    OBTOTH14        N8  0         PT/OT OFF VISITS - OTH COMBINED AMT 14
    USCNOT42        N4  -1        AC08 OTH REAS NO USC: USC NOT AVAIL-R4/2    OPTOTV14        N4  0         # OUTPATIENT DEPT PROVIDER VISITS 14
    PERSLA42        N4  -1        AC08 OTH REAS NO USC: LANGUAGE-R4/2         OPTTCH14        N8  0         OPD FACILITY + DR VISIT CHARGES - 14
    DIFFPL42        N4  -1        AC08 OTH REAS NO USC:DIFFRNT PLACES-R4/2    OPTEXP14        N8  0         TOTAL OUTPATIENT FAC + DR EXP 14
    INSRPL42        N4  -1        AC08 OTH REAS NO USC:JUST CHNGD INS-R4/2    OPTSLF14        N8  0         ALL OPD VSTS-SELF/FAMILY AMT-(FAC+DR) 14
    MYSELF42        N4  -1        AC08 OTH REAS NO USC:NO DOC/TRT SLF-R4/2    OPTMCR14        N8  0         ALL OPD VSTS-MEDICARE AMT-(FAC+DR) 14
    CARECO42        N4  -1        AC08 OTH REAS NO USC:COST OF MED CR-R4/2    OPTMCD14        N8  0         ALL OPD VSTS-MEDICAID AMT-(FAC+DR) 14
    NOHINS42        N4  -1        AC08 OTH REAS NO USC:NO HLTH INSRNC-R4/2    OPTPRV14        N8  0         ALL OPD VSTS-PRIV INS AMT-(FAC+DR) 14
    OTHINS42        N4  -1        AC08 OTH REAS NO USC: INS RELATED-R4/2      OPTVA14         N8  0         ALL OPD VSTS-VA/CHAMPVA AMT-(FAC+DR) 14
    JOBRSN42        N4  -1        AC08 OTH REAS NO USC: JOB RELATED-R4/2      OPTTRI14        N8  0         ALL OPD VSTS-TRICARE AMT-(FAC+DR) 14
    NEWDOC42        N4  -1        AC08 OTH REAS NO USC: LOOKNG FOR DR-R4/2    OPTOFD14        N8  0         ALL OPD VSTS-OTHER FED AMT-(FAC+DR) 14
    DOCELS42        N4  -1        AC08 OTH REAS NO USC: DR ELSEWHERE-R4/2     OPTSTL14        N8  0         ALL OPD VST-OTH ST/LOCAL AMT(FAC+DR) 14
    NOLIKE42        N4  -1        AC08 OTH REAS NO USC: DONT LIKE DRS-R4/2    OPTWCP14        N8  0         ALL OPD VST-WORKRS COMP AMT-(FAC+DR) 14
    HEALTH42        N4  -1        AC08 OTH REAS NO USC: HLTH RELATED-R4/2     OPTOPR14        N8  0         ALL OPD VSTS-OTH PRIVATE AMT-(FAC+DR) 14
    KNOWDR42        N4  -1        AC08 OTH REAS NO USC: KNOWS/IS A DR-R4/2    OPTOPU14        N8  0         ALL OPD VSTS-OTH PUBLIC AMT-(FAC+DR) 14
    ONJOB42         N4  -1        AC08 OTH REAS NO USC: DR AT WORK-R4/2       OPTOSR14        N8  0         ALL OPD VST-OTH UNCLS SRC AMT(FAC+DR) 14
    NOGODR42        N4  -1        AC08 OTH REAS NO USC: WONT GO TO DR-R4/2    OPTPTR14        N8  0         ALL OPD VISITS-PRV & TRI AMT (FAC+DR) 14
    TRANS42         N4  -1        AC08 OTH REAS NO USC: TRANSPRT/TIME-R4/2    OPTOTH14        N8  0         ALL OPD VSTS-OTH COMBINED AMT(FAC+DR) 14
    CLINIC42        N4  -1        AC08 OTH REAS NO USC: HOSP/ER/CLNIC-R4/2    OPFTCH14        N8  0         OPD PROVIDER VISIT CHARGES - FAC 14
    OTHREA42        N4  -1        AC08 OTH REAS NO USC: OTHER REASON-R4/2     OPFEXP14        N8  0         TOTAL OUTPATIENT FACILITY EXP 14
    PROVTY42        N4  3         PROVIDER TYPE-R4/2                          OPFSLF14        N8  0         ALL OPD VISITS-SELF/FAMILY AMT-FAC 14
    PLCTYP42        N4  3         USC TYPE OF PLACE-R4/2                      OPFMCR14        N8  0         ALL OPD VISITS-MEDICARE AMT-FAC 14
    TMTKUS42        N4  1         AC13 HOW LONG IT TAKES GET TO USC-R4/2      OPFMCD14        N8  0         ALL OPD VISITS-MEDICAID AMT-FAC 14
    TYPEPE42        N4  3         USC TYPE OF PROVIDER-R4/2                   OPFPRV14        N8  0         ALL OPD VISITS-PRIV INS AMT-FAC 14
    LOCATN42        N4  1         USC LOCATION-R4/2                           OPFVA14         N8  0         ALL OPD VISITS-VA/CHAMPVA AMT-FAC 14
    HSPLAP42        N4  2         AC18 IS PROVIDER HISPANIC OR LATINO-R4/2    OPFTRI14        N8  0         ALL OPD VISITS-TRICARE AMT-FAC 14
    WHITPR42        N4  1         AC19 IS PROVIDER WHITE-R4/2                 OPFOFD14        N8  0         ALL OPD VISITS-OTHER FED AMT-FAC 14
    BLCKPR42        N4  2         AC19 IS PROVIDER BLACK/AFRICAN AMER-R4/2    OPFSTL14        N8  0         ALL OPD VISITS-OTH ST/LOCAL AMT-FAC 14
    ASIANP42        N4  2         AC19 IS PROVIDER ASIAN-R4/2                 OPFWCP14        N8  0         ALL OPD VISITS-WORKERS COMP AMT-FAC 14
    NATAMP42        N4  2         AC19 IS PROVIDER NATIVE AMERICAN-R4/2       OPFOPR14        N8  0         ALL OPD VISITS - OTH PRIVATE AMT-FAC 14
    PACISP42        N4  2         AC19 IS PROVIDER OTH PACIFIC ISLNDR-R4/2    OPFOPU14        N8  0         ALL OPD VISITS - OTH PUBLIC AMT-FAC 14
    OTHRCP42        N4  2         AC19 IS PROVIDER SOME OTHER RACE-R4/2       OPFOSR14        N8  0         ALL OPD VSTS-OTH UNCLASS SRCE AMT-FAC 14
    GENDRP42        N4  2         AC20 IS PROVIDER MALE OR FEMALE-R4/2        OPFPTR14        N8  0         ALL OPD VISITS - PRV & TRI AMT-FAC 14
    MINORP42        N4  1         AC22 GO TO USC FOR NEW HEALTH PROB-R4/2     OPFOTH14        N8  0         ALL OPD VISITS - OTH COMBINED AMT-FAC 14
    PREVEN42        N4  1         AC22 GO TO USC FOR PRVNTVE HLT CARE-R4/2    OPDEXP14        N8  0         TOTAL OUTPATIENT PROVIDER EXP 14
    REFFRL42        N4  1         AC22 GO TO USC FOR REFERRALS-R4/2           OPDTCH14        N8  0         OPD PROVIDER VISIT CHARGES - DR 14
    ONGONG42        N4  1         AC22 GO TO USC FOR ONGOING HLTH PRB-R4/2    OPDSLF14        N8  0         ALL OPD VISITS-SELF/FAMILY AMT-DR 14
    PHNREG42        N4  4         AC23 HOW DIFF CONTACT USC BY PHONE-R4/2     OPDMCR14        N8  0         ALL OPD VISITS-MEDICARE AMT-DR 14
    OFFHOU42        N4  2         AC24 USC HAS OFFCE HRS NGHTS/WKENDS-R4/2    OPDMCD14        N8  0         ALL OPD VISITS-MEDICAID AMT-DR 14
    AFTHOU42        N4  -8        AC25 HOW DIFF CONTACT USC AFT HOURS-R4/2    OPDPRV14        N8  0         ALL OPD VISITS-PRIV INS AMT-DR 14
    TREATM42        N4  1         AC26 PROV ASK ABOUT OTH TREATMENTS-R4/2     OPDVA14         N8  0         ALL OPD VISITS-VA/CHAMPVA AMT-DR 14
    RESPCT42        N4  4         AC27 PROV SHOWS RESPECT FOR TRTMNTS-R4/2    OPDTRI14        N8  0         ALL OPD VISITS-TRICARE AMT-DR 14
    DECIDE42        N4  4         AC28 PROV ASKS PERS TO HELP DECIDE-R4/2     OPDOFD14        N8  0         ALL OPD VISITS-OTHER FED AMT-DR 14
    EXPLOP42        N4  1         AC30 PROV EXPLNS OPTIONS TO PERS-R4/2       OPDSTL14        N8  0         ALL OPD VISITS-OTH ST/LOCAL AMT-DR 14
    PRVSPK42        N4  -1        AC31 PROV SPEAKS PERSON'S LANGUAGE-R4/2     OPDWCP14        N8  0         ALL OPD VISITS-WORKERS COMP AMT-DR 14
    MDUNAB42        N4  2         UNABLE TO GET NECESSRY MEDICAL CARE-R4/2    OPDOPR14        N8  0         ALL OPD VISITS - OTH PRIVATE AMT-DR 14
    MDUNRS42        N4  -1        AC34 RSN UNABLE GET NECSRY MED CARE-R4/2    OPDOPU14        N8  0         ALL OPD VISITS-OTH PUBLIC AMT-DR 14
    MDDLAY42        N4  2         DELAYED IN GETTING NECSRY MED CARE-R4/2     OPDOSR14        N8  0         ALL OPD VSTS-OTH UNCLASS SRCE AMT-DR 14
    MDDLRS42        N4  -1        AC38 RSN DLAYD GETTING NEC MED CARE-R4/2    OPDPTR14        N8  0         ALL OPD VISITS-PRV & TRI AMT -DR 14
    DNUNAB42        N4  2         UNABLE TO GET NECESSARY DENTAL CARE-R4/2    OPDOTH14        N8  0         ALL OPD VISITS-OTH COMBINED AMT-DR 14
    DNUNRS42        N4  -1        AC42 RSN UNABLE GET NCSRY DENT CARE-R4/2    OPDRV14         N4  0         # OUTPATIENT DEPT PHYSICIAN VISITS 14
    DNDLAY42        N4  2         DELAYED IN GETTING NEC DENTAL CARE-R4/2     OPVTCH14        N8  0         OPD PHYSICIAN VISIT CHARGES - FAC 14
    DNDLRS42        N4  -1        AC46 RSN DLAYD GETTNG NEC DENT CARE-R4/2    OPVEXP14        N8  0         TOTAL OUTPATIENT PHYSICIAN - FAC EXP 14
    PMUNAB42        N4  2         UNABLE TO GET NECESSARY PRES MED-R4/2       OPVSLF14        N8  0         OPD DR VISITS-SELF/FAMILY AMT-FAC 14
    PMUNRS42        N4  -1        AC50 RSN UNABLE TO GET NEC PRES MED-R4/2    OPVMCR14        N8  0         OPD DR VISITS-MEDICARE AMT-FAC 14
    PMDLAY42        N4  2         DELAYED IN GETTING NECSRY PRES MED-R4/2     OPVMCD14        N8  0         OPD DR VISITS-MEDICAID AMT-FAC 14
    PMDLRS42        N4  -1        AC54 RSN DLAYD GETTING NEC PRES MED-R4/2    OPVPRV14        N8  0         OPD DR VISITS-PRIV INS AMT-FAC 14
    RNDFLG31        N4  -1        DATA COLLECTION ROUND FOR RD 3/1 CMJ        OPVVA14         N8  0         OPD DR VISITS-VA/CHAMPVA AMT-FAC 14
    MORJOB31        N4  -1        HAS MORE THAN ONE JOB RD 3/1 INT DATE       OPVTRI14        N8  0         OPD DR VISITS-TRICARE AMT-FAC 14
    MORJOB42        N4  -1        HAS MORE THAN ONE JOB RD 4/2 INT DATE       OPVOFD14        N8  0         OPD DR VISITS-OTHER FED AMT-FAC 14
    MORJOB53        N4  -1        HAS MORE THAN ONE JOB RD 5/3 INT DATE       OPVSTL14        N8  0         OPD DR VISITS-OTH ST/LOCAL AMT-FAC 14
    EVRWRK          N4  -1        EVER WRKD FOR PAY IN LIFE AS OF 12/31/14    OPVWCP14        N8  0         OPD DR VISITS-WORKERS COMP AMT-FAC 14
    HRWG31X         N8  -1        HOURLY WAGE RD 3/1 CMJ (IMP)                OPVOPR14        N8  0         OPD DR VISITS - OTH PRIVATE AMT-FAC 14
    HRWG42X         N8  -1        HOURLY WAGE RD 4/2 CMJ (IMP)                OPVOPU14        N8  0         OPD DR VISITS-OTH PUBLIC AMT-FAC 14
    HRWG53X         N8  -1        HOURLY WAGE RD 5/3 CMJ (IMP)                OPVOSR14        N8  0         OPD DR VSTS-OTH UNCLASS SRCE AMT-FAC 14
    HRWGIM31        N4  0         HRWG31X IMPUTATION FLAG                     OPVPTR14        N8  0         OPD DR VISITS - PRV & TRI AMT-FAC 14
    HRWGIM42        N4  0         HRWG42X IMPUTATION FLAG                     OPVOTH14        N8  0         OPD DR VISITS - OTH COMBINED AMT-FAC 14
    HRWGIM53        N4  0         HRWG53X IMPUTATION FLAG                     OPSEXP14        N8  0         TOTAL OUTPATIENT PHYSICIAN - DR EXP 14
    HRHOW31         N4  -1        HOW HOURLY WAGE WAS CALCULATED RD 3/1       OPSTCH14        N8  0         OPD PHYSICIAN VISIT CHARGES - DR 14
    HRHOW42         N4  -1        HOW HOURLY WAGE WAS CALCULATED RD 4/2       OPSSLF14        N8  0         OPD DR VISITS-SELF/FAMILY AMT-DR 14
    HRHOW53         N4  -1        HOW HOURLY WAGE WAS CALCULATED RD 5/3       OPSMCR14        N8  0         OPD DR VISITS-MEDICARE AMT-DR 14
    DIFFWG31        N4  -1        PERSONS WAGES DIFFERENT THIS RD31 AT CMJ    OPSMCD14        N8  0         OPD DR VISITS-MEDICAID AMT-DR 14
    DIFFWG42        N4  -1        PERSONS WAGES DIFFERENT THIS RD42 AT CMJ    OPSPRV14        N8  0         OPD DR VISITS-PRIV INS AMT-DR 14
    DIFFWG53        N4  -1        PERSONS WAGES DIFFERENT THIS RD53 AT CMJ    OPSVA14         N8  0         OPD DR VISITS-VA/CHAMPVA AMT-DR 14
    NHRWG31         N8  -1        UPDATED HRLY WAGE RD 3/1 CMJ (EDITED)       OPSTRI14        N8  0         OPD DR VISITS-TRICARE AMT-DR 14
    NHRWG42         N8  -1        UPDATED HRLY WAGE RD 4/2 CMJ (EDITED)       OPSOFD14        N8  0         OPD DR VISITS-OTHER FED AMT-DR 14
    NHRWG53         N8  -1        UPDATED HRLY WAGE RD 5/3 CMJ (EDITED)       OPSSTL14        N8  0         OPD DR VISITS-OTH ST/LOCAL AMT-DR 14
    HOUR31          N4  -1        HOURS PER WEEK AT RD 3/1 CMJ                OPSWCP14        N8  0         OPD DR VISITS-WORKERS COMP AMT-DR 14
    HOUR42          N4  -1        HOURS PER WEEK AT RD 4/2 CMJ                OPSOPR14        N8  0         OPD DR VISITS - OTH PRIVATE AMT-DR 14
    HOUR53          N4  -1        HOURS PER WEEK AT RD 5/3 CMJ                OPSOPU14        N8  0         OPD DR VISITS-OTH PUBLIC AMT-DR 14
    TEMPJB31        N4  -1        IS CMJ A TEMPORARY JOB RD 3/1               OPSOSR14        N8  0         OPD DR VSTS-OTH UNCLASS SRCE AMT-DR 14
    TEMPJB42        N4  -1        IS CMJ A TEMPORARY JOB RD 4/2               OPSPTR14        N8  0         OPD DR VISITS - PRV & TRI AMT-DR 14
    TEMPJB53        N4  -1        IS CMJ A TEMPORARY JOB RD 5/3               OPSOTH14        N8  0         OPD DR VISITS -OTH COMBINED AMT-DR 14
    SSNLJB31        N4  -1        IS CMJ A SEASONAL JOB RD 3/1                OPOTHV14        N4  0         # OUTPATIENT DEPT NON-DR VISITS 14
    SSNLJB42        N4  -1        IS CMJ A SEASONAL JOB RD 4/2                OPOTCH14        N8  0         OPD NON-PHYS VISIT CHARGES - FAC 14
    SSNLJB53        N4  -1        IS CMJ A SEASONAL JOB RD 5/3                OPOEXP14        N8  0         TOTAL OUTPATIENT NON-DR - FAC EXP 14
    SELFCM31        N4  -1        SELF-EMPLOYED AT RD 3/1 CMJ                 OPOSLF14        N8  0         OPD NON-DR VISITS-SELF/FAM AMT-FAC 14
    SELFCM42        N4  -1        SELF-EMPLOYED AT RD 4/2 CMJ                 OPOMCR14        N8  0         OPD NON-DR VISITS-MEDICARE AMT-FAC 14
    SELFCM53        N4  -1        SELF-EMPLOYED AT RD 5/3 CMJ                 OPOMCD14        N8  0         OPD NON-DR VISITS-MEDICAID AMT-FAC 14
    DISVW31X        N4  -1        DISAVOWED HEALTH INS AT RD 3/1 CMJ (ED)     OPOPRV14        N8  0         OPD NON-DR VISITS-PRIV INS AMT-FAC 14
    DISVW42X        N4  -1        DISAVOWED HEALTH INS AT RD 4/2 CMJ (ED)     OPOVA14         N8  0         OPD NON-DR VISITS-VA/CHAMPVA AMT-FAC 14
    DISVW53X        N4  -1        DISAVOWED HEALTH INS AT RD 5/3 CMJ (ED)     OPOTRI14        N8  0         OPD NON-DR VISITS-TRICARE AMT-FAC 14
    CHOIC31         N4  -1        CHOICE OF HEALTH PLANS AT RD 3/1 CMJ        OPOOFD14        N8  0         OPD NON-DR VISITS-OTHER FED AMT-FAC 14
    CHOIC42         N4  -1        CHOICE OF HEALTH PLANS AT RD 4/2 CMJ        OPOSTL14        N8  0         OPD NON-DR VISITS-OTH ST/LOC AMT-FAC 14
    CHOIC53         N4  -1        CHOICE OF HEALTH PLANS AT RD 5/3 CMJ        OPOWCP14        N8  0         OPD NON-DR VISITS-WRKRS COMP AMT-FAC 14
    INDCAT31        N4  -1        INDUSTRY GROUP RD 3/1 CMJ                   OPOOPR14        N8  0         OPD NON-DR VISITS-OTH PRIVATE AMT-FAC 14
    INDCAT42        N4  -1        INDUSTRY GROUP RD 4/2 CMJ                   OPOOPU14        N8  0         OPD NON-DR VISITS-OTH PUBLIC AMT-FAC 14
    INDCAT53        N4  -1        INDUSTRY GROUP RD 5/3 CMJ                   OPOOSR14        N8  0         OPD NON-DR VSTS-OT UNCLAS SRC AMT-FAC 14
    NUMEMP31        N4  -1        NUMBER OF EMPLOYEES AT RD 3/1 CMJ           OPOPTR14        N8  0         OPD NON-DR VISITS - PRV & TRI AMT-FAC 14
    NUMEMP42        N4  -1        NUMBER OF EMPLOYEES AT RD 4/2 CMJ           OPOOTH14        N8  0         OPD NON-DR VISITS-OTH COMBINED AM-FAC 14
    NUMEMP53        N4  -1        NUMBER OF EMPLOYEES AT RD 5/3 CMJ           OPPEXP14        N8  0         TOTAL OUTPATIENT NON-DR - DR EXP 14
    MORE31          N4  -1        RD 3/1 CMJ FIRM HAS MORE THAN 1 LOCAT       OPPTCH14        N8  0         OPD NON-PHYS VISIT CHARGES - DR 14
    MORE42          N4  -1        RD 4/2 CMJ FIRM HAS MORE THAN 1 LOCAT       OPPSLF14        N8  0         OPD NON-DR VISITS-SELF/FAM AMT-DR 14
    MORE53          N4  -1        RD 5/3 CMJ FIRM HAS MORE THAN 1 LOCAT       OPPMCR14        N8  0         OPD NON-DR VISITS-MEDICARE AMT-DR 14
    UNION31         N4  -1        UNION STATUS AT RD 3/1 CMJ                  OPPMCD14        N8  0         OPD NON-DR VISITS-MEDICAID AMT-DR 14
    UNION42         N4  -1        UNION STATUS AT RD 4/2 CMJ                  OPPPRV14        N8  0         OPD NON-DR VISITS-PRIV INS AMT-DR 14
    UNION53         N4  -1        UNION STATUS AT RD 5/3 CMJ                  OPPVA14         N8  0         OPD NON-DR VISITS-VA/CHAMPVA AMT-DR 14
    NWK31           N4  -1        REASON NOT WORKING DURING RD 3/1            OPPTRI14        N8  0         OPD NON-DR VISITS-TRICARE AMT-DR 14
    NWK42           N4  -1        REASON NOT WORKING DURING RD 4/2            OPPOFD14        N8  0         OPD NON-DR VISITS-OTHER FED AMT-DR 14
    NWK53           N4  -1        REASON NOT WORKING DURING RD 5/3            OPPSTL14        N8  0         OPD NON-DR VISITS-OTH ST/LOC AMT-DR 14
    CHGJ3142        N4  -1        CHANGED JOB BETWEEN RD 3/1 AND RD 4/2       OPPWCP14        N8  0         OPD NON-DR VISITS-WRKRS COMP AMT-DR 14
    CHGJ4253        N4  -1        CHANGED JOB BETWEEN RD 4/2 AND RD 5/3       OPPOPR14        N8  0         OPD NON-DR VISITS-OTH PRIVATE AMT-DR 14
    YCHJ3142        N4  -1        WHY CHNGD JOB BETWEEN RD 3/1 AND RD 4/2     OPPOPU14        N8  0         OPD NON-DR VISITS-OTH PUBLIC AMT-DR 14
    YCHJ4253        N4  -1        WHY CHNGD JOB BETWEEN RD 4/2 AND RD 5/3     OPPOSR14        N8  0         OPD NON-DR VSTS-OT UNCLAS SRC AMT-DR 14
    STJBMM31        N4  -1        MONTH STARTED RD 3/1 CMJ                    OPPPTR14        N8  0         OPD NON-DR VISITS - PRV & TRI AMT-DR 14
    STJBYY31        N5  -1        YEAR STARTED RD 3/1 CMJ                     OPPOTH14        N8  0         OPD NON-DR VISITS-OTH COMBINED AMT-DR 14
    STJBMM42        N4  -1        MONTH STARTED RD 4/2 CMJ                    AMCHIR14        N4  0         # CHIROPRACTR VSTS (OFF+OUTPAT), 2014
    STJBYY42        N5  -1        YEAR STARTED RD 4/2 CMJ                     AMCTCH14        N8  0         CHIRO AMBULATORY VISIT CHARGES 14
    STJBMM53        N4  -1        MONTH STARTED RD 5/3 CMJ                    AMCEXP14        N8  0         TOTL AMBULTRY (OB+OP) CHIRO EXP 14
    STJBYY53        N5  -1        YEAR STARTED RD 5/3 CMJ                     AMCSLF14        N8  0         CHIRO AMB VISITS - SELF/FAMILY AMT 14
    EVRETIRE        N4  -1        PERSON HAS EVER RETIRED                     AMCMCR14        N8  0         CHIRO AMB VISITS - MEDICARE AMT 14
    OCCCAT31        N4  -1        OCCUPATION GROUP RD 3/1 CMJ                 AMCMCD14        N8  0         CHIRO AMB VISITS - MEDICAID AMT 14
    OCCCAT42        N4  -1        OCCUPATION GROUP RD 4/2 CMJ                 AMCPRV14        N8  0         CHIRO AMB VISITS - PRIVATE INS AMT 14
    OCCCAT53        N4  -1        OCCUPATION GROUP RD 5/3 CMJ                 AMCVA14         N8  0         CHIRO AMB VISITS - VA/CHAMPVA AMT 14
    PAYVAC31        N4  -1        PAID VACATION AT RD 3/1 CMJ                 AMCTRI14        N8  0         CHIRO AMB VISITS-TRICARE AMT 14
    PAYVAC42        N4  -1        PAID VACATION AT RD 4/2 CMJ                 AMCOFD14        N8  0         CHIRO AMB VISITS - OTHER FEDERAL AMT 14
    PAYVAC53        N4  -1        PAID VACATION AT RD 5/3 CMJ                 AMCSTL14        N8  0         CHIRO AMB VISITS - OTH ST/LOCAL AMT 14
    SICPAY31        N4  -1        PAID SICK LEAVE AT RD 3/1 CMJ               AMCWCP14        N8  0         CHIRO AMB VISITS-WORKERS COMP AMT 14
    SICPAY42        N4  -1        PAID SICK LEAVE AT RD 4/2 CMJ               AMCOPR14        N8  0         CHIRO AMB VISITS - OTH PRIVATE AMT 14
    SICPAY53        N4  -1        PAID SICK LEAVE AT RD 5/3 CMJ               AMCOPU14        N8  0         CHIRO AMB VISITS - OTH PUBLIC AMT 14
    PAYDR31         N4  -1        PAID LEAVE TO VISIT DR RD 3/1 CMJ           AMCOSR14        N8  0         CHIR AMB VSTS - OTH UNCLASS SRCE AMT 14
    PAYDR42         N4  -1        PAID LEAVE TO VISIT DR RD 4/2 CMJ           AMCPTR14        N8  0         CHIRO AMB VISITS -PRV & TRI AMT 14
    PAYDR53         N4  -1        PAID LEAVE TO VISIT DR RD 5/3 CMJ           AMCOTH14        N8  0         CHIRO AMB VISITS - OTH COMBINED AMT 14
    RETPLN31        N4  -1        PENSION PLAN AT RD 3/1 CMJ                  AMNURS14        N4  0         # AMB NURSE/PRCTITIONR VSTS(OB+OP) 14
    RETPLN42        N4  -1        PENSION PLAN AT RD 4/2 CMJ                  AMNTCH14        N8  0         NRS/PRAC AMBULATORY VISIT CHARGES 14
    RETPLN53        N4  -1        PENSION PLAN AT RD 5/3 CMJ                  AMNEXP14        N8  0         TOTL AMBULTRY (OB+OP) NURSE/PRAC EXP 14
    BSNTY31         N4  -1        SOLE PROP, PARTNER, CORP, RD 3/1 CMJ        AMNSLF14        N8  0         NRS/PRAC AMB VSTS - SELF/FAMILY AMT 14
    BSNTY42         N4  -1        SOLE PROP, PARTNER, CORP, RD 4/2 CMJ        AMNMCR14        N8  0         NRS/PRAC AMB VSTS - MEDICARE AMT 14
    BSNTY53         N4  -1        SOLE PROP, PARTNER, CORP, RD 5/3 CMJ        AMNMCD14        N8  0         NRS/PRAC AMB VSTS - MEDICAID AMT 14
    JOBORG31        N4  -1        PRIV (PROFIT,NONPROFIT) GOV RD 3/1 CMJ      AMNPRV14        N8  0         NRS/PRAC AMB VSTS - PRIV INS AMT 14
    JOBORG42        N4  -1        PRIV (PROFIT,NONPROFIT) GOV RD 4/2 CMJ      AMNVA14         N8  0         NRS/PRAC AMB VSTS-VA/CHAMPVA AMT 14
    JOBORG53        N4  -1        PRIV (PROFIT,NONPROFIT) GOV RD 5/3 CMJ      AMNTRI14        N8  0         NRS/PRAC AMB VSTS-TRICARE AMT 14
    HELD31X         N4  -1        HEALTH INSUR HELD FROM RD 3/1 CMJ (ED)      AMNOFD14        N8  0         NRS/PRAC AMB VSTS-OTHER FEDERAL AMT 14
    HELD42X         N4  -1        HEALTH INSUR HELD FROM RD 4/2 CMJ (ED)      AMNSTL14        N8  0         NRS/PRAC AMB VSTS-OTH ST/LOCAL AMT 14
    HELD53X         N4  -1        HEALTH INSUR HELD FROM RD 5/3 CMJ (ED)      AMNWCP14        N8  0         NRS/PRAC AMB VSTS-WORKERS COMP AMT 14
    OFFER31X        N4  -1        HEALTH INSUR OFFERED BY RD 3/1 CMJ (ED)     AMNOPR14        N8  0         NRS/PRAC AMB VSTS - OTH PRIVATE AMT 14
    OFFER42X        N4  -1        HEALTH INSUR OFFERED BY RD 4/2 CMJ (ED)     AMNOPU14        N8  0         NRS/PRAC AMB VSTS - OTH PUBLIC AMT 14
    OFFER53X        N4  -1        HEALTH INSUR OFFERED BY RD 5/3 CMJ (ED)     AMNOSR14        N8  0         NRS/PR AMB VSTS - OTH UNCLAS SRCE AMT 14
    OFREMP31        N4  -1        EMPLOYER OFFERS HEALTH INS RD 3/1 CMJ       AMNPTR14        N8  0         NRS/PRAC AMB VSTS - PRV & TRI AMT 14
    OFREMP42        N4  -1        EMPLOYER OFFERS HEALTH INS RD 4/2 CMJ       AMNOTH14        N8  0         NRS/PRAC AMB VSTS - OTH COMBINED AMT 14
    OFREMP53        N4  -1        EMPLOYER OFFERS HEALTH INS RD 5/3 CMJ       AMOPTO14        N4  0         # AMB OPTOMETRIST VSTS (OB+OP) 14
    EMPST31         N4  -1        EMPLOYMENT STATUS RD 3/1                    AMETCH14        N8  0         OPTOMETRIST AMBULATORY VISIT CHARGES 14
    EMPST42         N4  -1        EMPLOYMENT STATUS RD 4/2                    AMEEXP14        N8  0         TOTL AMBULTRY (OB+OP) OPTOMETRIST EXP 14
    EMPST53         N4  -1        EMPLOYMENT STATUS RD 5/3                    AMESLF14        N8  0         OPTMTRIST AMB VSTS - SELF/FAMILY AMT 14
    EMPST31H        N4  -1        EMPLOYMENT STATUS RD 3/1 (IMP)              AMEMCR14        N8  0         OPTMTRIST AMB VSTS - MEDICARE AMT 14
    EMPST42H        N4  -1        EMPLOYMENT STATUS RD 4/2 (IMP)              AMEMCD14        N8  0         OPTMTRIST AMB VSTS - MEDICAID AMT 14
    EMPST53H        N4  -1        EMPLOYMENT STATUS RD 5/3 (IMP)              AMEPRV14        N8  0         OPTMTRIST AMB VSTS - PRIVATE INS AMT 14
    SLFCM31H        N4  -1        SELF-EMPLOYED AT RD 3/1 CMJ (IMP)           AMEVA14         N8  0         OPTMTRIST AMB VSTS-VA/CHAMPVA AMT 14
    SLFCM42H        N4  -1        SELF-EMPLOYED AT RD 4/2 CMJ (IMP)           AMETRI14        N8  0         OPTMTRIST AMB VSTS-TRICARE AMT 14
    SLFCM53H        N4  -1        SELF-EMPLOYED AT RD 5/3 CMJ (IMP)           AMEOFD14        N8  0         OPTMTRIST AMB VSTS-OTHER FED AMT 14
    NMEMP31H        N4  -1        NUMBER OF EMPLOYEES AT RD 3/1 CMJ (IMP)     AMESTL14        N8  0         OPTMTRIST AMB VSTS-OTH ST/LOCAL AMT 14
    NMEMP42H        N4  -1        NUMBER OF EMPLOYEES AT RD 4/2 CMJ (IMP)     AMEWCP14        N8  0         OPTMTRIST AMB VSTS-WORKERS COMP AMT 14
    NMEMP53H        N4  -1        NUMBER OF EMPLOYEES AT RD 5/3 CMJ (IMP)     AMEOPR14        N8  0         OPTMTRIST AMB VSTS - OTH PRIVATE AMT 14
    MORE31H         N4  -1        RD 3/1 CMJ FIRM MORE THAN 1 LOCAT (IMP)     AMEOPU14        N8  0         OPTMTRIST AMB VSTS - OTH PUBLIC AMT 14
    MORE42H         N4  -1        RD 4/2 CMJ FIRM MORE THAN 1 LOCAT (IMP)     AMEOSR14        N8  0         OPTOM AMB VSTS - OTH UNCLAS SRCE AMT 14
    MORE53H         N4  -1        RD 5/3 CMJ FIRM MORE THAN 1 LOCAT (IMP)     AMEPTR14        N8  0         OPTMTRIST AMB VSTS - PRV & TRI AMT 14
    INDCT31H        N4  -1        INDUSTRY GROUP RD 3/1 CMJ (IMP)             AMEOTH14        N8  0         OPTMTRIST AMB VSTS - OTH COMBINED AMT 14
    INDCT42H        N4  -1        INDUSTRY GROUP RD 4/2 CMJ (IMP)             AMASST14        N4  0         # PHYSICIAN ASS T VSTS (OFF+OUPAT), 2014
    INDCT53H        N4  -1        INDUSTRY GROUP RD 5/3 CMJ (IMP)             AMATCH14        N8  0         PHYS ASS T AMBULATORY VISIT CHARGES 14
    OCCCT31H        N4  -1        OCCUPATION GROUP RD 3/1 CMJ (IMP)           AMAEXP14        N8  0         TOTL AMBULTRY (OB+OP) PHYS ASS T EXP 14
    OCCCT42H        N4  -1        OCCUPATION GROUP RD 4/2 CMJ (IMP)           AMASLF14        N8  0         PHYS ASS T AMB VSTS-SELF/FAMILY AMT 14
    OCCCT53H        N4  -1        OCCUPATION GROUP RD 5/3 CMJ (IMP)           AMAMCR14        N8  0         PHYS ASS T AMB VSTS-MEDICARE AMT 14
    HOUR31H         N4  -1        HOURS PER WEEK AT RD 3/1 CMJ (IMP)          AMAMCD14        N8  0         PHYS ASS T AMB VSTS-MEDICAID AMT 14
    HOUR42H         N4  -1        HOURS PER WEEK AT RD 4/2 CMJ (IMP)          AMAPRV14        N8  0         PHYS ASS T AMB VSTS-PRIVATE INS AMT 14
    HOUR53H         N4  -1        HOURS PER WEEK AT RD 5/3 CMJ (IMP)          AMAVA14         N8  0         PHYS ASS T AMB VSTS-VA/CHAMPVA AMT 14
    JBORG31H        N4  -1        PRV, ST-LC GOV, FED GOV RD 3/1 CMJ (IMP)    AMATRI14        N8  0         PHYS ASS T AMB VSTS-TRICARE AMT 14
    JBORG42H        N4  -1        PRV, ST-LC GOV, FED GOV RD 4/2 CMJ (IMP)    AMAOFD14        N8  0         PHYS ASS T AMB VSTS - OTHER FED AMT 14
    JBORG53H        N4  -1        PRV, ST-LC GOV, FED GOV RD 5/3 CMJ (IMP)    AMASTL14        N8  0         PHYS ASS T AMB VSTS-OTH ST/LOCL AMT 14
    UNION31H        N4  -1        UNION STATUS AT RD 3/1 CMJ (IMP)            AMAWCP14        N8  0         PHYS ASS T AMB VSTS-WRKERS COMP AMT 14
    UNION42H        N4  -1        UNION STATUS AT RD 4/2 CMJ (IMP)            AMAOPR14        N8  0         PHYS ASS T AMB VSTS - OTH PRIVATE AMT 14
    UNION53H        N4  -1        UNION STATUS AT RD 5/3 CMJ (IMP)            AMAOPU14        N8  0         PHYS ASS T AMB VSTS - OTH PUBLIC AMT 14
    BSNTY31H        N4  -1        SOL PROP, PRTNR, CORP, RD 3/1 CMJ (IMP)     AMAOSR14        N8  0         P A AMB VSTS - OTH UNCLASS SRCE AMT 14
    BSNTY42H        N4  -1        SOL PROP, PRTNR, CORP, RD 4/2 CMJ (IMP)     AMAPTR14        N8  0         PHYS ASS T AMB VSTS - PRV & TRI AMT 14
    BSNTY53H        N4  -1        SOL PROP, PRTNR, CORP, RD 5/3 CMJ (IMP)     AMAOTH14        N8  0         PHYS ASS T AMB VSTS-OTH COMBINED AMT 14
    HRWG31H         N8  -1        HOURLY WAGE RD 3/1 CMJ (IMP)                AMTHER14        N4  0         # AMB PT/OT THRPY VISITS (OB+OP) 14
    HRWG42H         N8  -1        HOURLY WAGE RD 4/2 CMJ (IMP)                AMTTCH14        N8  0         PT/OC AMBULATORY VISIT CHARGES 14
    HRWG53H         N8  -1        HOURLY WAGE RD 5/3 CMJ (IMP)                AMTEXP14        N8  0         TOTL AMBULTRY (OB+OP) PT/OT EXP 14
    CMJHLD31        N4  -1        HLTH INSUR HELD FROM RD 3/1 CMJ (PRPL)      AMTSLF14        N8  0         PT/OT AMB VISITS-SELF/FAMILY AMT 14
    CMJHLD42        N4  -1        HLTH INSUR HELD FROM RD 4/2 CMJ (PRPL)      AMTMCR14        N8  0         PT/OT AMB VISITS-MEDICARE AMT 14
    CMJHLD53        N4  -1        HLTH INSUR HELD FROM RD 5/3 CMJ (PRPL)      AMTMCD14        N8  0         PT/OT AMB VISITS-MEDICAID AMT 14
    OFFER31H        N4  -1        HEALTH INSUR OFFERED BY RD 3/1 CMJ (IMP)    AMTPRV14        N8  0         PT/OT AMB VISITS-PRIVATE INS AMT 14
    OFFER42H        N4  -1        HEALTH INSUR OFFERED BY RD 4/2 CMJ (IMP)    AMTVA14         N8  0         PT/OT AMB VISITS-VA/CHAMPVA AMT 14
    OFFER53H        N4  -1        HEALTH INSUR OFFERED BY RD 5/3 CMJ (IMP)    AMTTRI14        N8  0         PT/OT AMB VISITS-TRICARE AMT 14
    OFEMP31H        N4  -1        EMP OFFERS HEALTH INS RD 3/1 CMJ (IMP)      AMTOFD14        N8  0         PT/OT AMB VISITS - OTHER FED AMT 14
    OFEMP42H        N4  -1        EMP OFFERS HEALTH INS RD 4/2 CMJ (IMP)      AMTSTL14        N8  0         PT/OT AMB VISITS-OTH ST/LOCL AMT 14
    OFEMP53H        N4  -1        EMP OFFERS HEALTH INS RD 5/3 CMJ (IMP)      AMTWCP14        N8  0         PT/OT AMB VISITS-WORKERS COMP AMT 14
    PYVAC31H        N4  -1        PAID VACATION AT RD 3/1 CMJ (IMP)           AMTOPR14        N8  0         PT/OT AMB VISITS - OTH PRIVATE AMT 14
    PYVAC42H        N4  -1        PAID VACATION AT RD 4/2 CMJ (IMP)           AMTOPU14        N8  0         PT/OT AMB VISITS-OTH PUBLIC AMT 14
    PYVAC53H        N4  -1        PAID VACATION AT RD 5/3 CMJ (IMP)           AMTOSR14        N8  0         PT/OT AMB VSTS-OTH UNCLAS SRCE AMT 14
    SCPAY31H        N4  -1        PAID SICK LEAVE AT RD 3/1 CMJ (IMP)         AMTPTR14        N8  0         PT/OT AMB VISITS -PRV & TRI AMT 14
    SCPAY42H        N4  -1        PAID SICK LEAVE AT RD 4/2 CMJ (IMP)         AMTOTH14        N8  0         PT/OT AMB VISITS - OTH COMBINED AMT 14
    SCPAY53H        N4  -1        PAID SICK LEAVE AT RD 5/3 CMJ (IMP)         AMTOTC14        N4  0         # CALLS W/OFFICE & OUPAT DEPTS, 2014
    PAYDR31H        N4  -1        PAID LEAVE TO VISIT DR RD 3/1 CMJ (IMP)     AMDRC14         N4  0         # CALLS W/OFF & OUTPAT PHYSICIANS, 2014
    PAYDR42H        N4  -1        PAID LEAVE TO VISIT DR RD 4/2 CMJ (IMP)     ERTOT14         N4  0         # EMERGENCY ROOM VISITS 14
    PAYDR53H        N4  -1        PAID LEAVE TO VISIT DR RD 5/3 CMJ (IMP)     ERTTCH14        N8  0         ER FACILITY + DR VISIT CHARGES 14
    RTPLN31H        N4  -1        PENSION PLAN AT RD 3/1 CMJ (IMP)            ERTEXP14        N8  0         TOTAL ER FACILITY + DR EXP 14
    RTPLN42H        N4  -1        PENSION PLAN AT RD 4/2 CMJ (IMP)            ERTSLF14        N8  0         ER-SELF/FAMILY AMT-(FAC+DR) 14
    RTPLN53H        N4  -1        PENSION PLAN AT RD 5/3 CMJ (IMP)            ERTMCR14        N8  0         ER-MEDICARE AMT-(FAC+DR) 14
    AFDC14          N4  -1        DID PERSON'S CHECK INCLUDE TANF             ERTMCD14        N8  0         ER-MEDICAID AMT-(FAC+DR) 14
    FILEDR14        N4  2         HAS PERSON FILED A FED INCOME TAX RETURN    ERTPRV14        N8  0         ER-PRIV INS AMT-(FAC+DR) 14
    WILFIL14        N4  2         WILL PERSON FILE FED INCOME TAX RETURN      ERTVA14         N8  0         ER-VA/CHAMPVA AMT-(FAC+DR) 14
    FLSTAT14        N4  -1        PERSON'S FILING STATUS                      ERTTRI14        N8  0         ER-TRICARE AMT-(FAC+DR) 14
    FILER14         N4  -1        PRIMARY OR SECONDARY FILER                  ERTOFD14        N8  0         ER-OTHER FED AMT-(FAC+DR) 14
    JTINRU14        N4  -1        JOINT FILER'S MEMBERSHIP IN RU              ERTSTL14        N8  0         ER-OTH ST/LOCAL AMT-(FAC+DR) 14
    JNTPID14        N4  -1        PID OF SECONDARY FILER                      ERTWCP14        N8  0         ER-WORKERS COMP AMT-(FAC+DR) 14
    CLMDEP14        N4  -1        DID/WILL PERS CLAIM DEPENDENTS ON RETURN    ERTOPR14        N8  0         ER-OTH PRIVATE AMT-(FAC+DR) 14
    DEPDNT14        N4  1         PERSON IS FLAGGED A DEPENDENT               ERTOPU14        N8  0         ER-OTH PUBLIC AMT-(FAC+DR) 14
    DPINRU14        N4  -1        DEPENDENTS IN/OUT OF RU                     ERTOSR14        N8  0         ER-OTH UNCLASS SRCE AMT-(FAC+DR) 14
    DPOTSD14        N4  -1        HOW MANY DEPENDENTS LIVE OUTSIDE RU         ERTPTR14        N8  0         ER-PRV & TRI AMT (FAC+DR) 14
    TAXFRM14        N4  -1        TAX FORM PERSON WILL FILE                   ERTOTH14        N8  0         ER -OTH COMBINED AMT (FAC+DR) 14
    CLMHIP14        N4  -1        DID/WILL PERS DEDUCT HEALTH INSUR. PREM.    ERFTCH14        N8  0         ER FACILITY VISIT CHARGES 14
    EICRDT14        N4  -1        DID/WILL PERS RECEIVE EARNED INC CREDIT     ERFEXP14        N8  0         TOTAL ER FACILITY EXP 14
    FOODST14        N4  2         DID ANYONE PURCHASE FOOD STAMPS             ERFSLF14        N8  0         ER-SELF/FAMILY AMT - FAC 14
    FOODMN14        N4  -1        NUMBER OF MONTHS FOOD STAMPS PURCHASED      ERFMCR14        N8  0         ER-MEDICARE AMT - FAC 14
    FOODVL14        N8  -1        MONTHLY VALUE OF FOOD STAMPS                ERFMCD14        N8  0         ER-MEDICAID AMT - FAC 14
    TTLP14X         N8  0         PERSON'S TOTAL INCOME                       ERFPRV14        N8  0         ER-PRIVATE INS AMT - FAC 14
    FAMINC14        N8  250000    FAMILY'S TOTAL INCOME                       ERFVA14         N8  0         ER-VA/CHAMPVA AMT - FAC 14
    POVCAT14        N4  5         FAMILY INC AS % OF POVERTY LINE - CATEGO    ERFTRI14        N8  0         ER-TRICARE AMT - FAC 14
    POVLEV14        N8  884.89    FAMILY INC AS % OF POVERTY LINE - CONTIN    ERFOFD14        N8  0         ER-OTHER FEDERAL AMT - FAC 14
    WAGEP14X        N8  0         PERSON'S WAGE INCOME                        ERFSTL14        N8  0         ER-OTH ST/LOCAL AMT - FAC 14
    WAGIMP14        N4  1         WAGE IMPUTATION FLAG                        ERFWCP14        N8  0         ER-WORKERS COMP AMT - FAC 14
    BUSNP14X        N8  0         PERSON'S BUSINESS INCOME                    ERFOPR14        N8  0         ER-OTHER PRIVATE AMT - FAC 14
    BUSIMP14        N4  1         BUSINESS INCOME IMPUTATION FLAG             ERFOPU14        N8  0         ER-OTHER PUBLIC AMT - FAC 14
    UNEMP14X        N8  0         PERSON'S UNEMPLOYMENT COMP INCOME           ERFOSR14        N8  0         ER-OTH UNCLASS SRCE AMT - FAC 14
    UNEIMP14        N4  1         UNEMPLOYMENT IMPUTATION FLAG                ERFPTR14        N8  0         ER-PRV & TRI AMT - FAC 14
    WCMPP14X        N8  0         PERSON'S WORKERS' COMPENSATION              ERFOTH14        N8  0         ER-OTH COMBINED AMT - FAC 14
    WCPIMP14        N4  1         WORKERS' COMP IMPUTATION FLAG               ERDEXP14        N8  0         TOTAL EMERGENCY ROOM DR EXP 14
    INTRP14X        N8  0         PERSON'S INTEREST INCOME                    ERDTCH14        N8  0         ER DOCTOR VISIT CHARGES 14
    INTIMP14        N4  1         INTEREST INCOME IMPUTATION FLAG             ERDSLF14        N8  0         ER-SELF/FAMILY AMT - DR 14
    DIVDP14X        N8  0         PERSON'S DIVIDEND INCOME                    ERDMCR14        N8  0         ER-MEDICARE AMT - DR 14
    DIVIMP14        N4  1         DIVIDEND INCOME IMPUTATION FLAG             ERDMCD14        N8  0         ER-MEDICAID AMT - DR 14
    SALEP14X        N8  0         PERSON'S SALES INCOME                       ERDPRV14        N8  0         ER-PRIVATE INS AMT - DR 14
    SALIMP14        N4  1         SALES INCOME IMPUTATION FLAG                ERDVA14         N8  0         ER-VA/CHAMPVA AMT - DR 14
    PENSP14X        N8  0         PERSON'S PENSION INCOME                     ERDTRI14        N8  0         ER-TRICARE AMT - DR 14
    PENIMP14        N4  1         PENSION INCOME IMPUTATION FLAG              ERDOFD14        N8  0         ER-OTHER FED AMT - DR 14
    SSECP14X        N8  0         PERSON'S SOCIAL SECURITY INCOME             ERDSTL14        N8  0         ER-OTH ST/LOCAL AMT - DR 14
    SSCIMP14        N4  1         SOCIAL SECURITY INCOME IMPUTATION FLAG      ERDWCP14        N8  0         ER-WORKERS COMP AMT - DR 14
    TRSTP14X        N8  0         PERSON'S TRUST/RENT INCOME                  ERDOPR14        N8  0         ER - OTHER PRIVATE AMT - DR 14
    TRTIMP14        N4  1         TRUST INCOME IMPUTATION FLAG                ERDOPU14        N8  0         ER - OTHER PUBLIC AMT - DR 14
    VETSP14X        N8  0         PERSON'S VETERAN'S INCOME                   ERDOSR14        N8  0         ER-OTH UNCLASS SRCE AMT - DR 14
    VETIMP14        N4  1         VETERAN'S INCOME IMPUTATION FLAG            ERDPTR14        N8  0         ER-PRV & TRI AMT - DR 14
    IRASP14X        N8  0         PERSON'S IRA INCOME                         ERDOTH14        N8  0         ER-OTH COMBINED AMT - DR 14
    IRAIMP14        N4  1         IRA INCOME IMPUTATION FLAG                  IPZERO14        N4  0         # ZERO-NIGHT HOSPITAL STAYS 14
    ALIMP14X        N8  0         PERSON'S ALIMONY INCOME                     ZIFTCH14        N8  0         ZERO-NITE IP STAY CHARGES - FAC 14
    ALIIMP14        N4  1         ALIMONY INCOME IMPUTATION FLAG              ZIFEXP14        N8  0         TOTAL ZERO-NITE STAYS FAC EXP 14
    CHLDP14X        N8  0         PERSON'S CHILD SUPPORT                      ZIFSLF14        N8  0         ZERO-NITE IP STAZ-SELF/FAM AMT-FAC 14
    CHLIMP14        N4  1         CHILD SUPPORT IMPUTATION FLAG               ZIFMCR14        N8  0         ZERO-NITE IP STAZ-MEDICARE AMT-FAC 14
    CASHP14X        N8  0         PERSON'S OTHER REGULAR CASH CONTRIBUTION    ZIFMCD14        N8  0         ZERO-NITE IP STAZ-MEDICAID AMT-FAC 14
    CSHIMP14        N4  1         CASH CONTRIBUTION IMPUTATION FLAG           ZIFPRV14        N8  0         ZERO-NITE IP STAZ-PRIV INS AMT-FAC 14
    SSIP14X         N8  0         PERSON'S SSI                                ZIFVA14         N8  0         ZERO-NITE IP STAZ-VA/CHAMPVA AMT-FAC 14
    SSIIMP14        N4  1         SSI IMPUTATION FLAG                         ZIFTRI14        N8  0         ZERO-NITE IP STAZ-TRICARE AMT-FAC 14
    PUBP14X         N8  0         PERSON'S PUBLIC ASSISTANCE                  ZIFOFD14        N8  0         ZERO-NITE IP STAZ-OTHER FED AMT-FAC 14
    PUBIMP14        N4  1         PUBLIC ASSISTANCE IMPUTATION FLAG           ZIFSTL14        N8  0         ZERO-NITE IP STAZ-OTH ST/LOC AMT-FAC 14
    OTHRP14X        N8  0         PERSON'S OTHER INCOME                       ZIFWCP14        N8  0         ZERO-NITE IP STAZ-WRKERS COMP AMT-FAC 14
    OTHIMP14        N4  1         OTHER INCOME IMPUTATION FLAG                ZIFOPR14        N8  0         ZERO-NITE IP STAZ-OTH PRIVATE AMT-FAC 14
    TRIJA14X        N4  -1        COVERED BY TRICARE/CHAMPVA IN JAN14 (ED)    ZIFOPU14        N8  0         ZERO-NITE IP STAZ-OTH PUBLIC AMT-FAC 14
    TRIFE14X        N4  -1        COVERED BY TRICARE/CHAMPVA IN FEB14 (ED)    ZIFOSR14        N8  0         ZERO-NITE IP STAZ-UNCLAS SRCE AMT-FAC 14
    TRIMA14X        N4  2         COVERED BY TRICARE/CHAMPVA IN MAR14 (ED)    ZIFPTR14        N8  0         ZERO-NITE IP STAZ-PRV & TRI AMT-FAC 14
    TRIAP14X        N4  2         COVERED BY TRICARE/CHAMPVA IN APR14(ED)     ZIFOTH14        N8  0         ZERO-NITE IP STAZ-OTH COMBINE AMT-FAC 14
    TRIMY14X        N4  2         COVERED BY TRICARE/CHAMPVA IN MAY14 (ED)    ZIDEXP14        N8  0         TOTAL ZERO-NITE STAZ DR 14
    TRIJU14X        N4  2         COVERED BY TRICARE/CHAMPVA IN JUN14 (ED)    ZIDTCH14        N8  0         ZERO-NITE IP STAY CHARGES - DR 14
    TRIJL14X        N4  2         COVERED BY TRICARE/CHAMPVA IN JUL14 (ED)    ZIDSLF14        N8  0         ZERO-NITE IP STAZ-SELF/FAM AMT-DR 14
    TRIAU14X        N4  2         COVERED BY TRICARE/CHAMPVA IN AUG14 (ED)    ZIDMCR14        N8  0         ZERO-NITE IP STAZ-MEDICARE AMT-DR 14
    TRISE14X        N4  2         COVERED BY TRICARE/CHAMPVA IN SEP14 (ED)    ZIDMCD14        N8  0         ZERO-NITE IP STAZ-MEDICAID AMT-DR 14
    TRIOC14X        N4  2         COVERED BY TRICARE/CHAMPVA IN OCT14 (ED)    ZIDPRV14        N8  0         ZERO-NITE IP STAZ-PRIV INS AMT-DR 14
    TRINO14X        N4  2         COVERED BY TRICARE/CHAMPVA IN NOV14 (ED)    ZIDVA14         N8  0         ZERO-NITE IP STAZ-VA/CHAMPVA AMT-DR 14
    TRIDE14X        N4  2         COVERED BY TRICARE/CHAMPVA IN DEC14 (ED)    ZIDTRI14        N8  0         ZERO-NITE IP STAZ-TRICARE AMT-DR 14
    MCRJA14         N4  -1        COVERED BY MEDICARE IN JAN14                ZIDOFD14        N8  0         ZERO-NITE IP STAZ-OTHER FED AMT-DR 14
    MCRFE14         N4  -1        COVERED BY MEDICARE IN FEB14                ZIDSTL14        N8  0         ZERO-NITE IP STAZ-OTH ST/LOC AMT-DR 14
    MCRMA14         N4  2         COVERED BY MEDICARE IN MAR14                ZIDWCP14        N8  0         ZERO-NITE IP STAZ-WRKERS COMP AMT-DR 14
    MCRAP14         N4  2         COVERED BY MEDICARE IN APR14                ZIDOPR14        N8  0         ZERO-NITE IP STAZ-OTH PRIVATE AMT-DR 14
    MCRMY14         N4  2         COVERED BY MEDICARE IN MAY14                ZIDOPU14        N8  0         ZERO-NITE IP STAZ-OTH PUBLIC AMT-DR 14
    MCRJU14         N4  2         COVERED BY MEDICARE IN JUN14                ZIDOSR14        N8  0         ZERO-NITE IP STAZ-UNCLAS SRCE AMT-DR 14
    MCRJL14         N4  2         COVERED BY MEDICARE IN JUL14                ZIDPTR14        N8  0         ZERO-NITE IP STAZ-PRV & TRI AMT-DR 14
    MCRAU14         N4  2         COVERED BY MEDICARE IN AUG14                ZIDOTH14        N8  0         ZERO-NITE IP STAZ-OTH COMBINED AMT-DR 14
    MCRSE14         N4  2         COVERED BY MEDICARE IN SEP14                IPDIS14         N4  0         # HOSPITAL DISCHARGES, 2014
    MCROC14         N4  2         COVERED BY MEDICARE IN OCT14                IPTEXP14        N8  0         TOT HOSP IP FACILITY + DR EXP 14
    MCRNO14         N4  2         COVERED BY MEDICARE IN NOV14                IPTTCH14        N8  0         IP HOSP STAY CHARGES (FAC+DR) 14
    MCRDE14         N4  2         COVERED BY MEDICARE IN DEC14                IPTSLF14        N8  0         IP HOSP STAZ-SELF/FAMILY AMT-(FAC+DR) 14
    MCRJA14X        N4  -1        COVERED BY MEDICARE IN JAN14 (ED)           IPTMCR14        N8  0         IP HOSP STAZ-MEDICARE AMT-(FAC+DR) 14
    MCRFE14X        N4  -1        COVERED BY MEDICARE IN FEB14 (ED)           IPTMCD14        N8  0         IP HOSP STAZ-MEDICAID AMT-(FAC+DR) 14
    MCRMA14X        N4  2         COVERED BY MEDICARE IN MAR14 (ED)           IPTPRV14        N8  0         IP HOSP STAZ-PRIV INS AMT-(FAC+DR) 14
    MCRAP14X        N4  2         COVERED BY MEDICARE IN APR14 (ED)           IPTVA14         N8  0         IP HOSP STAZ-VA/CHAMPVA AMT-(FAC+DR) 14
    MCRMY14X        N4  2         COVERED BY MEDICARE IN MAY14 (ED)           IPTTRI14        N8  0         IP HOSP STAZ-TRICARE AMT-(FAC+DR) 14
    MCRJU14X        N4  2         COVERED BY MEDICARE IN JUN14 (ED)           IPTOFD14        N8  0         IP HOSP STAZ-OTHER FED AMT-(FAC+DR) 14
    MCRJL14X        N4  2         COVERED BY MEDICARE IN JUL14 (ED)           IPTSTL14        N8  0         IP HSP STAZ-OTH ST/LOCAL AMT-(FAC+DR) 14
    MCRAU14X        N4  2         COVERED BY MEDICARE IN AUG14 (ED)           IPTWCP14        N8  0         IP HOSP STAZ-WRKRS COMP AMT-(FAC+DR) 14
    MCRSE14X        N4  2         COVERED BY MEDICARE IN SEP14 (ED)           IPTOPR14        N8  0         IP HOSP STAZ-OTH PRIVATE AMT-(FAC+DR) 14
    MCROC14X        N4  2         COVERED BY MEDICARE IN OCT14 (ED)           IPTOPU14        N8  0         IP HOSP STAZ-OTH PUBLIC AMT-(FAC+DR) 14
    MCRNO14X        N4  2         COVERED BY MEDICARE IN NOV14 (ED)           IPTOSR14        N8  0         IP HSP STAZ-OTH UNCLS SRC AMT(FAC+DR) 14
    MCRDE14X        N4  2         COVERED BY MEDICARE IN DEC14 (ED)           IPTPTR14        N8  0         IP HOSP STAZ-PRV & TRI AMT-(FAC+DR) 14
    MCDJA14         N4  -1        COV BY MEDICAID OR SCHIP IN JAN14           IPTOTH14        N8  0         IP HOSP STAZ-OTH COMBINED AMT(FAC+DR) 14
    MCDFE14         N4  -1        COV BY MEDICAID OR SCHIP IN FEB14           IPFEXP14        N8  0         TOT HOSP IP FACILITY EXP-INC 0 NITES 14
    MCDMA14         N4  2         COV BY MEDICAID OR SCHIP IN MAR14           IPFTCH14        N8  0         IP HOSP STAY CHARGES - FAC 14
    MCDAP14         N4  2         COV BY MEDICAID OR SCHIP IN APR14           IPFSLF14        N8  0         IP HOSP STAZ-SELF/FAMILY AMT-FAC 14
    MCDMY14         N4  2         COV BY MEDICAID OR SCHIP IN MAY14           IPFMCR14        N8  0         IP HOSP STAZ-MEDICARE AMT-FAC 14
    MCDJU14         N4  2         COV BY MEDICAID OR SCHIP IN JUN14           IPFMCD14        N8  0         IP HOSP STAZ-MEDICAID AMT-FAC 14
    MCDJL14         N4  2         COV BY MEDICAID OR SCHIP IN JUL14           IPFPRV14        N8  0         IP HOSP STAZ-PRIV INS AMT-FAC 14
    MCDAU14         N4  2         COV BY MEDICAID OR SCHIP IN AUG14           IPFVA14         N8  0         IP HOSP STAZ-VA/CHAMPVA AMT-FAC 14
    MCDSE14         N4  2         COV BY MEDICAID OR SCHIP IN SEP14           IPFTRI14        N8  0         IP HOSP STAZ-TRICARE AMT-FAC 14
    MCDOC14         N4  2         COV BY MEDICAID OR SCHIP IN OCT14           IPFOFD14        N8  0         IP HOSP STAZ-OTHER FED AMT-FAC 14
    MCDNO14         N4  2         COV BY MEDICAID OR SCHIP IN NOV14           IPFSTL14        N8  0         IP HOSP STAZ-OTH ST/LOCAL AMT-FAC 14
    MCDDE14         N4  2         COV BY MEDICAID OR SCHIP IN DEC14           IPFWCP14        N8  0         IP HOSP STAZ-WORKERS COMP AMT-FAC 14
    MCDJA14X        N4  -1        COV BY MEDICAID OR SCHIP IN JAN14 (ED)      IPFOPR14        N8  0         IP HOSP STAZ - OTH PRIVATE AMT-FAC 14
    MCDFE14X        N4  -1        COV BY MEDICAID OR SCHIP IN FEB14 (ED)      IPFOPU14        N8  0         IP HOSP STAZ - OTH PUBLIC AMT-FAC 14
    MCDMA14X        N4  2         COV BY MEDICAID OR SCHIP IN MAR14 (ED)      IPFOSR14        N8  0         IP HOSP STAZ-OT UNCLASS SRCE AMT-FAC 14
    MCDAP14X        N4  2         COV BY MEDICAID OR SCHIP IN APR14 (ED)      IPFPTR14        N8  0         IP HOSP STAZ-PRV & TRI AMT-FAC 14
    MCDMY14X        N4  2         COV BY MEDICAID OR SCHIP IN MAY14 (ED)      IPFOTH14        N8  0         IP HOSP STAZ-OTH COMBINED AMT-FAC 14
    MCDJU14X        N4  2         COV BY MEDICAID OR SCHIP IN JUN14 (ED)      IPDEXP14        N8  0         TOTL HOSP STAZ DR EXP 14
    MCDJL14X        N4  2         COV BY MEDICAID OR SCHIP IN JUL14 (ED)      IPDTCH14        N8  0         IP HOSP STAY CHARGES - DR 14
    MCDAU14X        N4  2         COV BY MEDICAID OR SCHIP IN AUG14 (ED)      IPDSLF14        N8  0         IP HOSP STAZ-SELF/FAMILY AMT-DR 14
    MCDSE14X        N4  2         COV BY MEDICAID OR SCHIP IN SEP14 (ED)      IPDMCR14        N8  0         IP HOSP STAZ-MEDICARE AMT- DR 14
    MCDOC14X        N4  2         COV BY MEDICAID OR SCHIP IN OCT14 (ED)      IPDMCD14        N8  0         IP HOSP STAZ-MEDICAID AMT-DR 14
    MCDNO14X        N4  2         COV BY MEDICAID OR SCHIP IN NOV14 (ED)      IPDPRV14        N8  0         IP HOSP STAZ-PRIV INS AMT-DR 14
    MCDDE14X        N4  2         COV BY MEDICAID OR SCHIP IN DEC14 (ED)      IPDVA14         N8  0         IP HOSP STAZ-VA/CHAMPVA AMT-DR 14
    OPAJA14         N4  -1        COV BY OTHER PUBLIC A INS IN JAN14          IPDTRI14        N8  0         IP HOSP STAZ-TRICARE AMT-DR 14
    OPAFE14         N4  -1        COV BY OTHER PUBLIC A INS IN FEB14          IPDOFD14        N8  0         IP HOSP STAZ-OTHER FED AMT-DR 14
    OPAMA14         N4  2         COV BY OTHER PUBLIC A INS IN MAR14          IPDSTL14        N8  0         IP HOSP STAZ-OTH ST/LOCAL AMT-DR 14
    OPAAP14         N4  2         COV BY OTHER PUBLIC A INS IN APR14          IPDWCP14        N8  0         IP HOSP STAZ-WORKERS COMP AMT-DR 14
    OPAMY14         N4  2         COV BY OTHER PUBLIC A INS IN MAY14          IPDOPR14        N8  0         IP HOSP STAZ - OTH PRIVATE AMT-DR 14
    OPAJU14         N4  2         COV BY OTHER PUBLIC A INS IN JUN14          IPDOPU14        N8  0         IP HOSP STAZ - OTH PUBLIC AMT-DR 14
    OPAJL14         N4  2         COV BY OTHER PUBLIC A INS IN JUL14          IPDOSR14        N8  0         IP HOSP STAZ-OT UNCLASS SORCE AMT-DR 14
    OPAAU14         N4  2         COV BY OTHER PUBLIC A INS IN AUG14          IPDPTR14        N8  0         IP HOSP STAZ-PRV & TRI AMT-DR 14
    OPASE14         N4  2         COV BY OTHER PUBLIC A INS IN SEP14          IPDOTH14        N8  0         IP HOSP STAZ-OTH COMBINED AMT-DR 14
    OPAOC14         N4  2         COV BY OTHER PUBLIC A INS IN OCT14          IPNGTD14        N4  0         # NIGHTS IN HOSP FOR DISCHARGES, 2014
    OPANO14         N4  2         COV BY OTHER PUBLIC A INS IN NOV14          DVTOT14         N4  0         # DENTAL CARE VISITS 14
    OPADE14         N4  2         COV BY OTHER PUBLIC A INS IN DEC14          DVTTCH14        N8  0         TOTAL DENTAL CARE VISIT CHARGES 14
    OPBJA14         N4  -1        COV BY OTHER PUBLIC B INS IN JAN14          DVTEXP14        N8  0         TOTAL DENTAL CARE EXP 14
    OPBFE14         N4  -1        COV BY OTHER PUBLIC B INS IN FEB14          DVTSLF14        N8  0         ALL DENTAL CARE - SELF/FAMILY AMT 14
    OPBMA14         N4  2         COV BY OTHER PUBLIC B INS IN MAR14          DVTMCR14        N8  0         ALL DENTAL CARE - MEDICARE AMT 14
    OPBAP14         N4  2         COV BY OTHER PUBLIC B INS IN APR14          DVTMCD14        N8  0         ALL DENTAL CARE - MEDICAID AMT 14
    OPBMY14         N4  2         COV BY OTHER PUBLIC B INS IN MAY14          DVTPRV14        N8  0         ALL DENTAL CARE - PRIVATE INS AMT 14
    OPBJU14         N4  2         COV BY OTHER PUBLIC B INS IN JUN14          DVTVA14         N8  0         ALL DENTAL CARE - VA/CHAMPVA AMT 14
    OPBJL14         N4  2         COV BY OTHER PUBLIC B INS IN JUL14          DVTTRI14        N8  0         ALL DENTAL CARE - TRICARE AMT 14
    OPBAU14         N4  2         COV BY OTHER PUBLIC B INS IN AUG14          DVTOFD14        N8  0         ALL DENTAL CARE - OTHER FEDRL AMT 14
    OPBSE14         N4  2         COV BY OTHER PUBLIC B INS IN SEP14          DVTSTL14        N8  0         ALL DENTAL CARE - OTH ST/LOCAL AMT 14
    OPBOC14         N4  2         COV BY OTHER PUBLIC B INS IN OCT14          DVTWCP14        N8  0         ALL DENTAL CARE - WORKERS COMP AMT 14
    OPBNO14         N4  2         COV BY OTHER PUBLIC B INS IN NOV14          DVTOPR14        N8  0         ALL DENTAL CARE - OTH PRIVATE AMT 14
    OPBDE14         N4  2         COV BY OTHER PUBLIC B INS IN DEC14          DVTOPU14        N8  0         ALL DENTAL CARE - OTH PUBLIC AMT 14
    STAJA14         N4  -1        COVERED BY OTHER STATE PROG IN JAN14        DVTOSR14        N8  0         ALL DENT CARE-OT UNCLASS SRCE AMT 14
    STAFE14         N4  -1        COVERED BY OTHER STATE PROG IN FEB14        DVTPTR14        N8  0         ALL DENTAL CARE - PRV & TRI AMT 14
    STAMA14         N4  2         COVERED BY OTHER STATE PROG IN MAR14        DVTOTH14        N8  0         ALL DENTAL CARE - OTH COMBINED AMT 14
    STAAP14         N4  2         COVERED BY OTHER STATE PROG IN APR14        DVGEN14         N4  0         # GENERAL DENTIST VISITS 14
    STAMY14         N4  2         COVERED BY OTHER STATE PROG IN MAY14        DVGTCH14        N8  0         GENERAL DENTAL CARE VISIT CHARGES 14
    STAJU14         N4  2         COVERED BY OTHER STATE PROG IN JUN14        DVGEXP14        N8  0         TOTAL GENERAL DENTIST EXP 14
    STAJL14         N4  2         COVERED BY OTHER STATE PROG IN JUL14        DVGSLF14        N8  0         GNRL DENTAL VISITS - SELF/FAM AMT 14
    STAAU14         N4  2         COVERED BY OTHER STATE PROG IN AUG14        DVGMCR14        N8  0         GNRL DENTAL VISITS - MEDICARE AMT 14
    STASE14         N4  2         COVERED BY OTHER STATE PROG IN SEP14        DVGMCD14        N8  0         GNRL DENTAL VISITS - MEDICAID AMT 14
    STAOC14         N4  2         COVERED BY OTHER STATE PROG IN OCT14        DVGPRV14        N8  0         GNRL DENTAL VISITS - PRIVATE INS AMT 14
    STANO14         N4  2         COVERED BY OTHER STATE PROG IN NOV14        DVGVA14         N8  0         GNRL DENTAL VISITS - VA/CHAMPVA AMT 14
    STADE14         N4  2         COVERED BY OTHER STATE PROG IN DEC14        DVGTRI14        N8  0         GNRL DENTAL VISITS-TRICARE AMT 14
    PUBJA14X        N4  -1        COVR BY ANY PUBLIC INS IN JAN14 (ED)        DVGOFD14        N8  0         GNRL DENTAL VISITS - OTHER FED AMT 14
    PUBFE14X        N4  -1        COVR BY ANY PUBLIC INS IN FEB14 (ED)        DVGSTL14        N8  0         GNRL DENTAL VISITS - OTH ST/LOCAL AMT 14
    PUBMA14X        N4  2         COVR BY ANY PUBLIC INS IN MAR14 (ED)        DVGWCP14        N8  0         GNRL DENTAL VISITS - WORKERS COMP AMT 14
    PUBAP14X        N4  2         COVR BY ANY PUBLIC INS IN APR14 (ED)        DVGOPR14        N8  0         GNRL DENTAL VISITS - OTH PRIVATE AMT 14
    PUBMY14X        N4  2         COVR BY ANY PUBLIC INS IN MAY14 (ED)        DVGOPU14        N8  0         GNRL DENTAL VISITS - OTH PUBLIC AMT 14
    PUBJU14X        N4  2         COVR BY ANY PUBLIC INS IN JUN14 (ED)        DVGOSR14        N8  0         GNRL DENT VSTS - OT UNCLASS SRCE AMT 14
    PUBJL14X        N4  2         COVR BY ANY PUBLIC INS IN JUL14 (ED)        DVGPTR14        N8  0         GNRL DENTAL VISITS - PRV & TRI AMT 14
    PUBAU14X        N4  2         COVR BY ANY PUBLIC INS IN AUG14 (ED)        DVGOTH14        N8  0         GNRL DENTAL VISITS - OTH COMBINED AMT 14
    PUBSE14X        N4  2         COVR BY ANY PUBLIC INS IN SEP14 (ED)        DVORTH14        N4  0         # ORTHODONTIST VISITS 14
    PUBOC14X        N4  2         COVR BY ANY PUBLIC INS IN OCT14 (ED)        DVOTCH14        N8  0         ORTHODONTIST VISIT CHARGES 14
    PUBNO14X        N4  2         COVR BY ANY PUBLIC INS IN NOV14 (ED)        DVOEXP14        N8  0         TOTAL ORTHODONTIST EXP 14
    PUBDE14X        N4  2         COVR BY ANY PUBLIC INS IN DEC14 (ED)        DVOSLF14        N8  0         ORTHODONTIST VISITS - SELF/FAMILY AMT 14
    PEGJA14         N4  -1        COVERED BY EMPL UNION INS IN JAN14          DVOMCR14        N8  0         ORTHODONTIST VISITS - MEDICARE AMT 14
    PEGFE14         N4  -1        COVERED BY EMPL UNION INS IN FEB14          DVOMCD14        N8  0         ORTHODONTIST VISITS - MEDICAID AMT 14
    PEGMA14         N4  2         COVERED BY EMPL UNION INS IN MAR14          DVOPRV14        N8  0         ORTHODONTIST VISITS - PRIVATE INS AMT 14
    PEGAP14         N4  1         COVERED BY EMPL UNION INS IN APR14          DVOVA14         N8  0         ORTHODONTIST VISITS-VA/CHAMPVA AMT 14
    PEGMY14         N4  1         COVERED BY EMPL UNION INS IN MAY14          DVOTRI14        N8  0         ORTHODONTIST VISITS-TRICARE AMT 14
    PEGJU14         N4  1         COVERED BY EMPL UNION INS IN JUN14          DVOOFD14        N8  0         ORTHODONTIST VISITS-OTHR FED AMT 14
    PEGJL14         N4  1         COVERED BY EMPL UNION INS IN JUL14          DVOSTL14        N8  0         ORTHODONTIST VISITS-OTHR ST/LOCAL AMT 14
    PEGAU14         N4  1         COVERED BY EMPL UNION INS IN AUG14          DVOWCP14        N8  0         ORTHODONTIST VISITS-WORKERS COMP AMT 14
    PEGSE14         N4  1         COVERED BY EMPL UNION INS IN SEP14          DVOOPR14        N8  0         ORTHODONTIST VISITS-OTHR PRIVATE AMT 14
    PEGOC14         N4  1         COVERED BY EMPL UNION INS IN OCT14          DVOOPU14        N8  0         ORTHODONTIST VISITS-OTHR PUBLIC AMT 14
    PEGNO14         N4  1         COVERED BY EMPL UNION INS IN NOV14          DVOOSR14        N8  0         ORTHODONT VSTS - OT UNCLASS SRCE AMT 14
    PEGDE14         N4  1         COVERED BY EMPL UNION INS IN DEC14          DVOPTR14        N8  0         ORTHODONTIST VISITS - PRV & TRI AMT 14
    PDKJA14         N4  -1        COVR BY PRIV INS (SOURCE UNKNWN) JAN14      DVOOTH14        N8  0         ORTHODONTIST VISITS-OTH COMBINED AMT 14
    PDKFE14         N4  -1        COVR BY PRIV INS (SOURCE UNKNWN) FEB14      HHTOTD14        N4  0         # HOME HEALTH PROVIDER DAYS, 2014
    PDKMA14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) MAR14      HHAGD14         N4  0         # AGENCY HOME HEALTH PROVIDER DAYS 14
    PDKAP14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) APR14      HHATCH14        N8  0         HOME HEALTH AGENCY VISIT CHARGES 14
    PDKMY14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) MAY14      HHAEXP14        N8  0         TOTAL HOME HEALTH AGENCY EXP 14
    PDKJU14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) JUN14      HHASLF14        N8  0         HOME HLTH AGENCY - SELF/FAMILY AMT 14
    PDKJL14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) JUL14      HHAMCR14        N8  0         HOME HLTH AGENCY - MEDICARE AMT 14
    PDKAU14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) AUG14      HHAMCD14        N8  0         HOME HLTH AGENCY - MEDICAID AMT 14
    PDKSE14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) SEP14      HHAPRV14        N8  0         HOME HLTH AGENCY - PRIVATE INS AMT 14
    PDKOC14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) OCT14      HHAVA14         N8  0         HOME HLTH AGENCY-VA/CHAMPVA AMT 14
    PDKNO14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) NOV14      HHATRI14        N8  0         HOME HLTH AGENCY-TRICARE AMT 14
    PDKDE14         N4  2         COVR BY PRIV INS (SOURCE UNKNWN) DEC14      HHAOFD14        N8  0         HOME HLTH AGENCY - OTHER FED AMT 14
    PNGJA14         N4  -1        COVERED BY NONGROUP INS IN JAN14            HHASTL14        N8  0         HOME HLTH AGENCY-OTHR ST/LOCAL AMT 14
    PNGFE14         N4  -1        COVERED BY NONGROUP INS IN FEB14            HHAWCP14        N8  0         HOME HLTH AGENCY - WORKERS COMP AMT 14
    PNGMA14         N4  2         COVERED BY NONGROUP INS IN MAR14            HHAOPR14        N8  0         HOME HLTH AGENCY - OTH PRIVATE AMT 14
    PNGAP14         N4  2         COVERED BY NONGROUP INS IN APR14            HHAOPU14        N8  0         HOME HLTH AGENCY - OTH PUBLIC AMT 14
    PNGMY14         N4  2         COVERED BY NONGROUP INS IN MAY14            HHAOSR14        N8  0         H HLTH AGENCY - OT UNCLASS SRCE AMT 14
    PNGJU14         N4  2         COVERED BY NONGROUP INS IN JUN14            HHAPTR14        N8  0         HOME HLTH AGENCY - PRV & TRI AMT 14
    PNGJL14         N4  2         COVERED BY NONGROUP INS IN JUL14            HHAOTH14        N8  0         HOME HLTH AGENCY - OTH COMBINED AMT 14
    PNGAU14         N4  2         COVERED BY NONGROUP INS IN AUG14            HHINDD14        N4  0         # NON-AGENCY HOME HEALTH PROVIDR DAYS 14
    PNGSE14         N4  2         COVERED BY NONGROUP INS IN SEP14            HHNTCH14        N8  0         HOME HEALTH NON-AGENCY VISIT CHARGES 14
    PNGOC14         N4  2         COVERED BY NONGROUP INS IN OCT14            HHNEXP14        N8  0         TOTAL HOME HEALTH NON-AGNCY EXP 14
    PNGNO14         N4  2         COVERED BY NONGROUP INS IN NOV14            HHNSLF14        N8  0         HOME HLTH NON-AGNCY - SELF/FAM AMT 14
    PNGDE14         N4  2         COVERED BY NONGROUP INS IN DEC14            HHNMCD14        N8  0         HOME HLTH NON-AGNCY - MEDICAID AMT 14
    POGJA14         N4  -1        COVERED BY OTHER GROUP INS IN JAN14         HHNMCR14        N8  0         HOME HLTH NON-AGNCY - MEDICARE AMT 14
    POGFE14         N4  -1        COVERED BY OTHER GROUP INS IN FEB14         HHNPRV14        N8  0         HOME HLTH NON-AGNCY - PRIV INS AMT 14
    POGMA14         N4  2         COVERED BY OTHER GROUP INS IN MAR14         HHNVA14         N8  0         HOME HLTH NON-AGNCY-VA/CHAMPVA AMT 14
    POGAP14         N4  2         COVERED BY OTHER GROUP INS IN APR14         HHNTRI14        N8  0         HOME HLTH NON-AGNCY-TRICARE AMT 14
    POGMY14         N4  2         COVERED BY OTHER GROUP INS IN MAY14         HHNOFD14        N8  0         HOME HLTH NON-AGNCY-OTHR FED AMT 14
    POGJU14         N4  2         COVERED BY OTHER GROUP INS IN JUN14         HHNSTL14        N8  0         HOME HLTH NON-AGNCY-OTHR ST/LOCL AMT 14
    POGJL14         N4  2         COVERED BY OTHER GROUP INS IN JUL14         HHNWCP14        N8  0         HOME HLTH NON-AGNCY-WORKERS COMP AMT 14
    POGAU14         N4  2         COVERED BY OTHER GROUP INS IN AUG14         HHNOPR14        N8  0         HOME HLTH NON-AGNCY-OTH PRIVATE AMT 14
    POGSE14         N4  2         COVERED BY OTHER GROUP INS IN SEP14         HHNOPU14        N8  0         HOME HLTH NON-AGNCY-OTH PUBLIC AMT 14
    POGOC14         N4  2         COVERED BY OTHER GROUP INS IN OCT14         HHNOSR14        N8  0         H HLTH NON-AGNCY-OT UNCLASS SRCE AMT 14
    POGNO14         N4  2         COVERED BY OTHER GROUP INS IN NOV14         HHNPTR14        N8  0         HOME HLTH NON-AGNCY - PRV & TRI AMT 14
    POGDE14         N4  2         COVERED BY OTHER GROUP INS IN DEC14         HHNOTH14        N8  0         HOME HLTH NON-AGNCY-OTH COMBINED AMT 14
    PRSJA14         N4  -1        COVERED BY SELF-EMP-1 INS IN JAN14          HHINFD14        N4  0         # INFORMAL HOME HEALTH PROVIDER DAYS 14
    PRSFE14         N4  -1        COVERED BY SELF-EMP-1 INS IN FEB14          VISEXP14        N8  0         TOTAL GLASSES/CONTACT LENS EXP 14
    PRSMA14         N4  2         COVERED BY SELF-EMP-1 INS IN MAR14          VISTCH14        N8  0         GLASSES/CONTACT LENSES CHARGES 14
    PRSAP14         N4  2         COVERED BY SELF-EMP-1 INS IN APR14          VISSLF14        N8  0         GLASSES/CNTCT LENSES -SELF/FAM AMT 14
    PRSMY14         N4  2         COVERED BY SELF-EMP-1 INS IN MAY14          VISMCR14        N8  0         GLASSES/CNTCT LENSES-MEDICARE AMT 14
    PRSJU14         N4  2         COVERED BY SELF-EMP-1 INS IN JUN14          VISMCD14        N8  0         GLASSES/CNTCT LENSES-MEDICAID AMT 14
    PRSJL14         N4  2         COVERED BY SELF-EMP-1 INS IN JUL14          VISPRV14        N8  0         GLASSES/CNTCT LENSES-PRIV INS AMT 14
    PRSAU14         N4  2         COVERED BY SELF-EMP-1 INS IN AUG14          VISVA14         N8  0         GLASSES/CNTCT LENSES-VA/CHAMPVA AMT 14
    PRSSE14         N4  2         COVERED BY SELF-EMP-1 INS IN SEP14          VISTRI14        N8  0         GLASSES/LENSES-TRICARE AMT 14
    PRSOC14         N4  2         COVERED BY SELF-EMP-1 INS IN OCT14          VISOFD14        N8  0         GLASSES/CNTCT LENSES-OTHR FED AMT 14
    PRSNO14         N4  2         COVERED BY SELF-EMP-1 INS IN NOV14          VISSTL14        N8  0         GLASSES/CNTCT LENSES-OTH ST/LOCL AMT 14
    PRSDE14         N4  2         COVERED BY SELF-EMP-1 INS IN DEC14          VISWCP14        N8  0         GLASSES/CNTCT LENSES-WORKERS COMP AMT 14
    POUJA14         N4  -1        COVERED BY HOLDER OUTSIDE OF RU IN JAN14    VISOPR14        N8  0         GLASSES/CNTCT LENSES-OTH PRIVATE AMT 14
    POUFE14         N4  -1        COVERED BY HOLDER OUTSIDE OF RU IN FEB14    VISOPU14        N8  0         GLASSES/CNTCT LENSES-OTH PUBLIC AMT 14
    POUMA14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN MAR14    VISOSR14        N8  0         GLASES/CNTCT LENSE-OT UNCLAS SRCE AMT 14
    POUAP14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN APR14    VISPTR14        N8  0         GLASSES/CNTCT LENSES-PRV & TRI AMT 14
    POUMY14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN MAY14    VISOTH14        N8  0         GLASSES/CNTCT LENSES-OTH COMBINED AMT 14
    POUJU14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN JUN14    OTHTCH14        N8  0         OTHER EQUP/SUPPLIES CHARGES 14
    POUJL14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN JUL14    OTHEXP14        N8  0         TOT OTHER EQUIP/SPLY (EXCL DIAB) EXP 14
    POUAU14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN AUG14    OTHSLF14        N8  0         OTHER EQUP/SUPPLIES-SELF/FAM AMT 14
    POUSE14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN SEP14    OTHMCR14        N8  0         OTHER EQUP/SUPPLIES-MEDICARE AMT 14
    POUOC14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN OCT14    OTHMCD14        N8  0         OTHER EQUP/SUPPLIES-MEDICAID AMT 14
    POUNO14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN NOV14    OTHPRV14        N8  0         OTHER EQUP/SUPPLIES-PRIV INS AMT 14
    POUDE14         N4  2         COVERED BY HOLDER OUTSIDE OF RU IN DEC14    OTHVA14         N8  0         OTHER EQUP/SUPPLY-VA/CHAMPVA AMT 14
    PRXJA14         N4  -1        COV BY PRIV INS THROUGH EXCHNG IN JAN14     OTHTRI14        N8  0         OTHER EQUP/SUPPLY-TRICARE AMT 14
    PRXFE14         N4  -1        COV BY PRIV INS THROUGH EXCHNG IN FEB14     OTHOFD14        N8  0         OTHER EQUP/SUPPLIES-OTHR FEDRL AMT 14
    PRXMA14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN MAR14     OTHSTL14        N8  0         OTHER EQUP/SUPPLY-OTHR ST/LOCAL AMT 14
    PRXAP14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN APR14     OTHWCP14        N8  0         OTHER EQUP/SUPPLY - WORKERS COMP AMT 14
    PRXMY14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN MAY14     OTHOPR14        N8  0         OTHER EQUP/SUPPLY-OTH PRIVATE AMT 14
    PRXJU14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN JUN14     OTHOPU14        N8  0         OTHER EQUP/SUPPLY - OTH PUBLIC AMT 14
    PRXJL14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN JUL14     OTHOSR14        N8  0         OTH EQUP/SUPLY - OT UNCLASS SRCE AMT 14
    PRXAU14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN AUG14     OTHPTR14        N8  0         OTHER EQUP/SUPPLY - PRV & TRI AMT 14
    PRXSE14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN SEP14     OTHOTH14        N8  0         OTHER EQUP/SUPPLY - OTH COMBINED AMT 14
    PRXOC14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN OCT14     RXTOT14         N4  2         # PRESC MEDS INCL REFILLS 14
    PRXNO14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN NOV14     RXEXP14         N8  12        TOTAL RX-EXP 14
    PRXDE14         N4  2         COV BY PRIV INS THROUGH EXCHNG IN DEC14     RXSLF14         N8  12        TOTAL RX-SELF/FAMILY AMT 14
    PRIJA14         N4  -1        COVERED BY PRIVATE INS IN JAN14             RXMCR14         N8  0         TOTAL RX-MEDICARE AMT 14
    PRIFE14         N4  -1        COVERED BY PRIVATE INS IN FEB14             RXMCD14         N8  0         TOTAL RX-MEDICAID AMT 14
    PRIMA14         N4  2         COVERED BY PRIVATE INS IN MAR14             RXPRV14         N8  0         TOTAL RX-PRIVATE INS AMT 14
    PRIAP14         N4  1         COVERED BY PRIVATE INS IN APR14             RXVA14          N8  0         TOTAL RX-VA/CHAMPVA AMT 14
    PRIMY14         N4  1         COVERED BY PRIVATE INS IN MAY14             RXTRI14         N8  0         TOTAL RX-TRICARE AMT 14
    PRIJU14         N4  1         COVERED BY PRIVATE INS IN JUN14             RXOFD14         N8  0         TOTAL RX-OTHER FED AMT 14
    PRIJL14         N4  1         COVERED BY PRIVATE INS IN JUL14             RXSTL14         N8  0         TOTAL RX-OTHER ST/LOCAL AMT 14
    PRIAU14         N4  1         COVERED BY PRIVATE INS IN AUG14             RXWCP14         N8  0         TOTAL RX-WORKERS COMP AMT 14
    PRISE14         N4  1         COVERED BY PRIVATE INS IN SEP14             RXOPR14         N8  0         TOTAL RX-OTH PRIVATE AMT 14
    PRIOC14         N4  1         COVERED BY PRIVATE INS IN OCT14             RXOPU14         N8  0         TOTAL RX-OTH PUBLIC AMT 14
    PRINO14         N4  1         COVERED BY PRIVATE INS IN NOV14             RXOSR14         N8  0         TOT RX-OTH UNCLASS SRCE AMT 14
    PRIDE14         N4  1         COVERED BY PRIVATE INS IN DEC14             RXPTR14         N8  0         TOTAL RX-PRV & TRI AMT 14
    HPEJA14         N4  -1        HOLDER OF EMPL UNION INS IN JAN14           RXOTH14         N8  0         TOTAL RX-OTH COMBINED AMT 14
    HPEFE14         N4  -1        HOLDER OF EMPL UNION INS IN FEB14           PERWT14F        N8  19170.747 FINAL PERSON WEIGHT, 2014
    HPEMA14         N4  2         HOLDER OF EMPL UNION INS IN MAR14           FAMWT14F        N8  15785.670 FINAL FAMILY WEIGHT, 2014
    HPEAP14         N4  2         HOLDER OF EMPL UNION INS IN APR14           FAMWT14C        N8  15785.670 POV ADJ FAMILY WGT-CPS FAM ON 12/31/14
                                                                              SAQWT14F        N8  0         FINAL SAQ PERSON WEIGHT, 2014
                                                                              DIABW14F        N8  0         FINAL DIABETES CARE SUPPLEMENT WEIGHT
                                                                              VARSTR          N5  1117      VARIANCE ESTIMATION STRATUM - 2014
                                                                              VARPSU          N4  3         VARIANCE ESTIMATION PSU - 2014




