# MAINFRAME - JCL


# ⚡ JCL

- Referencias e Exemplos de Códigos em JCL

## 1. JCL para criar um(s) conjunto(s) de dados PS

```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//*******************************************************************************
//** JCL TO CREATE A PS DATASET
//*******************************************************************************
//STEP001  EXEC PGM=IEFBR14
//DD1      DD DSN=RACFID.IBMMF.PS1,
//            DISP=(MOD,CATLG,DELETE),
//            SPACE=(TRK,(10,100),RLSE),
//            DCB=(LRECL=80,RECFM=FB,BLKSIZE=800,DSORG=PS)
//*
//DD2      DD DSN=RACFID.IBMMF.PS2,
//            DISP=(MOD,CATLG,DELETE),
//            SPACE=(TRK,(10,100),RLSE),
//            DCB=(LRECL=80,RECFM=FB,BLKSIZE=800,DSORG=PS)
//*
```

## 2. JCL para excluir um(s) conjunto(s) de dados PS

```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//*******************************************************************************
//* JCL TO DELETE A PS DATASET
//*******************************************************************************
//STEP001  EXEC PGM=IEFBR14
//DD1      DD DSN=RACFID.IBMMF.PS1,
//         DISP=(OLD,DELETE,DELETE)
//*
//DD2      DD DSN=RACFID.IBMMF.PS2,
//            DISP=(OLD,DELETE,DELETE)
//*
```

## 3. JCL para criar um(s) conjunto(s) de dados PDS

```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//*******************************************************************************
//* JCL TO CREATE A PDS DATASET
//*******************************************************************************
//STEP001  EXEC PGM=IEFBR14
//DD1      DD DSN=RACFID.IBMMF.PDS1,
//            DISP=(NEW,CATLG,DELETE),
//            SPACE=(CYL,(10,100,4),RLSE),
//            DCB=(LRECL=80,BLKSIZE=800,RECFM=FB,DSORG=PO)
//*
//STEP002  EXEC PGM=IEFBR14
//DD2      DD DSN=RACFID.IBMMF.PDS2,
//            DISP=(NEW,CATLG,DELETE),
//            SPACE=(CYL,(10,100,4),RLSE),
//            DCB=(LRECL=80,BLKSIZE=800,RECFM=FB,DSORG=PO)
//*

```
## 4. JCL para excluir um(s) conjunto(s) de dados PDS

```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//*******************************************************************************
//* JCL TO DELETE A PDS DATASET
//*******************************************************************************
//STEP001  EXEC PGM=IEFBR14
//DD1      DD DSN=RACFID.IBMMF.PDS1,
//            DISP=(OLD,DELETE,DELETE)
//*
//STEP002  EXEC PGM=IEFBR14
//DD1      DD DSN=RACFID.IBMMF.PDS2,
//            DISP=(OLD,DELETE,DELETE)
//*

```

## 5. JCL para criar um(s) membro(s) do conjunto de dados PDS

```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ********************************
  //* JCL PARA CRIAR UM MEMBRO DO CONJUNTO DE DADOS PDS
  //************************************************ ********************************
  //STEP001 EXEC PGM=IEBGENER
  //SYSUT1DD*
  //SYSUT2 DD DSN=RACFID.IBMMF.PDS(MEMBER1),
  //DISP=SHR
  //SYSIN DD DUMMY
  //SYSPRINT DD SYSOUT=*
  //*
  //STEP002 EXEC PGM=IEBGENER
  //SYSUT1DD*
  //SYSUT2 DD DSN=RACFID.IBMMF.PDS(MEMBER1),
  //DISP=SHR
  //SYSIN DD DUMMY
  //SYSPRINT DD SYSOUT=*
  //*
 ```
## 6. JCL para excluir um(s) membro(s) do conjunto de dados PDS (Partitioned Dataset)

```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ********************************
  //* JCL PARA EXCLUIR UM MEMBRO DO CONJUNTO DE DADOS PDS
  //************************************************ ********************************
  //STEP001 EXEC PGM=IDCAMS
  //DD1 DD DSN=RACFID.IBMMF.PDS,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSIN DD *
   EXCLUIR ARQUIVO 'RACFID.IBMMF.PDS(MEMBER1)'(DD1)
  /*
  //STEP002 EXEC PGM=IDCAMS
  //DD1 DD DSN=RACFID.IBMMF.PDS,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSIN DD *
    EXCLUIR ARQUIVO 'RACFID.IBMMF.PDS(MEMBER2)' (DD1)
  /*
  
  ```
## 7. JCL para criar uma(s) base(s) de GDG (Group Data Group)

```JCL
    // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
    //************************************************ ********************************
    //* JCL PARA CRIAR UMA BASE DE GDG
    //************************************************ ********************************
    //STEP001 EXEC PGM=IDCAMS
    //SYSPRINT DD SYSOUT=*
    //SYSIN DD *
      DEFINE GDG(NAME(RACFID.IBMMF.BASE1) -
                 LIMIT(7) -
                 NOTEMPTY -
                 SCRATCH
    /*
    //STEP002 EXEC PGM=IDCAMS
    //SYSPRINT DD SYSOUT=*
    //SYSIN DD *
      DEFINE GDG(NAME(RACFID.IBMMF.BASE2) -
                 LIMIT(7) -
                 NOTEMPTY -
                 SCRATCH
    /*
    
```
## 8. JCL para criar uma(s) geração(ões) de GDG

```JCL
    // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
    //************************************************ ********************************
    //* JCL PARA CRIAR UMA GERAÇÃO DE GDG
    //************************************************ ********************************
    //STEP001 EXEC PGM=IEFBR14
    //SYSPRINT DD SYSOUT=*
    //DD1 DD DSN=RACFID.IBMMF.GDG(+1),
    // DISP=(NEW,CATLG,DELETE),
    // SPACE=(TRK,(100,100),RLSE),
    // DCB=(LRECL=80,RECFM=FB,BLKSIZE=800,DSORG=PS)
    //*
    //DD2 DD DSN=RACFID.IBMMF.GDG(+1),
    // DISP=(NEW,CATLG,DELETE),
    // SPACE=(TRK,(100,100),RLSE),
    // DCB=(LRECL=80,RECFM=FB,BLKSIZE=800,DSORG=PS)
    //*
 ```
## 9. JCL para excluir uma(s) base(s) de GDG
```JCL
      // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
      //************************************************ ********************************
      //* JCL PARA EXCLUIR UMA BASE GDG
      //************************************************ ********************************
      //STEP001 EXEC PGM=IDCAMS
      //SYSPRINT DD SYSOUT=*
      //SYSIN DD *
        DELETE (RACFID.IBMMF.BASE1) -
                GDD -
                FORCE
      /*
      //STEP002 EXEC PGM=IDCAMS
      //SYSPRINT DD SYSOUT=*
      //SYSIN DD *
        DELETE (RACFID.IBMMF.BASE2) -
                GDD -
                FORCE
      /*
      
 ```
## 10. JCL para excluir uma(s) geração(ões) de GDG

```JCL
      // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
      //************************************************ ************************************
      //* JCL PARA EXCLUIR UMA GERAÇÃO DE UM GDG
      //************************************************ ************************************
      //STEP001 EXEC PGM=IEFBR14
      //DD1 DD DSN=RACFID.IBMMF.BASE1.G0001V00,
      // DISP=(OLD,DELETE,DELETE)
      //*
      //DD2 DD DSN=RACFID.IBMMF.BASE2.G0001V00,
      // DISP=(OLD,DELETE,DELETE)
```

## 11. JCL para excluir todas as gerações de GDG
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA EXCLUIR UMA GERAÇÃO DE UM GDG
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEFBR14
  //DD1 DD DSN=RACFID.IBMMF.BASE1,
  // DISP=(OLD,DELETE,DELETE)
  //*
  //DD2 DD DSN=RACFID.IBMMF.BASE2,
  // DISP=(OLD,DELETE,DELETE)
```
## 12. JCL para criar um VSAM - ESDS
  
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA CRIAR um VSAM - ESDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //SYSIN DD *
    DEFINE CLUSTER (-
            NAME(RACFID.IBMMF.ESDS) -
            NONINDEXED -
            RECSZ(200 200) -
            FREESPACE(10 10) -
            CISZ(8192) -
            TRACKS(20 20) -
            VOLUME(IBMSYS)
  /*
```
## 13. JCL para criar um VSAM - KSDS

```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA CRIAR um VSAM - KSDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //SYSIN DD *
    DEFINE CLUSTER (-
           NAME(RACFID.IBMMF.KSDS) -
           INDEXED -
           KEYS(5 0) -
           RECSZ(200 200) -
           FREESPACE(10 20) -
           TRACKS(50 30) -
           CISZ(4096) -
           VOLUME(IBMSYS))
  /*
  ```
## 14. JCL para criar um VSAM - RRDS

```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA CRIAR um VSAM - RRDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //SYSIN DD *
     DEFINE CLUSTER (-
     NAME(RACFID.IBMMF.RRDS) -
     NUMBERED -
     RECSZ(200 200) -
     CISZ(4096) -
     TRACKS(20 20) -
     FREESPACE(10 10) -
     VOLUME(IBMSYS))
  /*
```

## 15. JCL para criar um VSAM - LDS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA CRIAR um VSAM - LDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //SYSIN DD *
    DEFINE CLUSTER (-
    NAME(RACFID.IBMMF.LDS) -
    LINEAR -
    CISZ(4096) -
    TRACKS(20 20) -
    VOLUME(IBMSYS)
  /*
  ```
## 16. JCL para LISTCAT um VSAM
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA LISTCAT A VSAM
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //SYSIN DD *
    LISTCAT ENTRY(RACFID.IBMMF.ESDS) -
    ALL
  /*
  ```
## 17. JCL REPRO – Copiar de PS para ESDS
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL REPRO – CÓPIA DE PS PARA ESDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //*
  //PSFILE DD DSN=RACFID.IBMMF.PS,
  //DISP=SHR
  //ESDSFILE DD DSN=RACFID.IBMMF.ESDS,
  //DISP=SHR
  //SYSIN DD *
     REPRO INFILE (PSFILE) -
           OUTFILE(ESDSFILE)
  /*
 ```
## 18. JCL REPRO - Copiar de PS PARA KSDS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL REPRO - CÓPIA DE PS PARA KSDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //*
  //PSFILE DD DSN=RACFID.IBMMF.PS,
  //DISP=SHR
  //KSDSFILE DD DSN=RACFID.IBMMF.KSDS,
  //DISP=SHR
  //SYSIN DD *
    REPRO INFILE (PSFILE) -
          OUTFILE(KSDSFILE)
  /*
  ```
## 19. JCL REPRO - Copiar de KSDS PARA PS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL REPRO - CÓPIA DE KSDS PARA PS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //*
  //KSFILE DD DSN=RACFID.IBMMF.KSDS,
  //DISP=SHR
  //PSFILE DD DSN=RACFID.IBMMF.PS,
  //DISP=SHR
  //*
  //SYSIN DD *
    REPRO INFILE(KSFILE) -
          OUTFILE(PSFILE)
  /*
  ```
## 20. JCL REPRO - copie de PS para RRDS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL REPRO - CÓPIA DE PS PARA RRDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //*
  //PSFILE DD DSN=RACFID.IBMMF.PS,
  //DISP=SHR
  //RRDSFILE DD DSN=RACFID.IBMMF.RRDS,
  //DISP=SHR
  //*
  //SYSIN DD *
    REPRO INFILE (PSFILE) -
          OUTFILE(RRDSFILE)
  /*
```
## 21. JCL REPRO – cópia de ESDS para ESDS
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL REPRO - CÓPIA DE ESDS PARA ESDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //*
  //ESDS1 DD DSN=RACFID.IBMMF.ESDS1,
  //DISP=SHR
  //ESDS2 DD DSN=RACFID.IBMMF.ESDS2,
  //DISP=SHR
  //*
  //SYSIN DD *
    REPRO INFILE(ESDS1) -
          OUTFILE(ESDS2)
  /*
 ```
## 22. JCL REPRO – cópia de RRDS para RRDS
 ```JCL 
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL REPRO - CÓPIA DE RRDS PARA RRDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IDCAMS
  //SYSPRINT DD SYSOUT=*
  //*
  //RRDS1 DD DSN=RECFID.IBMMF.RRDS1,
  //DISP=SHR
  //RRDS2 DD DSN=RECFID.IBMMF.RRDS2,
  //DISP=SHR
  //*
  //SYSIN DD *
     REPRO INFILE(RRDS1) -
           OUTFILE(RRDS2)
  /*
 ```
## 23. JCL para copiar todos os membros de um PDS para outro PDS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COPIAR TODOS OS MEMBROS DE UM PDS PARA OUTRO PDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBCOPY
  //DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <--- INPUT DATASET
  //DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <--- CONJUNTO DE DADOS DE SAÍDA
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    COPY INDD=DD1
        OUTDD=DD2
  /*
 ```
## 24. JCL para copiar todos os membros de um PDS para outro PDS usando SYSUT
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//************************************************ ************************************
//* JCL PARA COPIAR TODOS OS MEMBROS DE UM PDS PARA OUTRO PDS USANDO O SYSUT
//************************************************ ************************************
//STEP001 EXEC PGM=IEBCOPY
//SYSUT1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <--- INPUT DATASET
//SYSUT2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <--- CONJUNTO DE DADOS DE SAÍDA
//*
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD DUMMY

```
## 25. JCL para copiar um membro específico de um PDS para outro PDS
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//************************************************ ************************************
//* JCL PARA COPIAR MEMBRO ESPECÍFICO DE UM PDS PARA OUTRO PDS
//************************************************ ************************************
//STEP001 EXEC PGM=IEBCOPY
//DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <--- INPUT DATASET
//DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <--- CONJUNTO DE DADOS DE SAÍDA
//*
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  COPY INDD=DD1
      OUTDD=DD2
      SELECT MEMBER=(MEMBER8,MEMBER3,MEMBER4)
/*
```
## 26. JCL para copiar dois membros PDS para um PDS
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//************************************************ ************************************
//* JCL PARA COPIAR DOIS PDS MEMBRO PARA UM PDS
//************************************************ ************************************
//STEP001 EXEC PGM=IEBCOPY
//DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <--- INPUT DATASET
//DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <--- INPUT DATASET
//DD3 DD DSN=RACFID.IBMMF.PDS3,DISP=SHR <--- CONJUNTO DE DADOS DE SAÍDA
//*
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  COPY INDD=DD1
       INDD=DD2
      OUTDD=DD3
/*
```
## 27. JCL para copiar um membro específico de dois PDS para um PDS
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//**************************************************** ********************************
//* JCL PARA COPIAR MEMBRO ESPECÍFICO DE DOIS PDS PARA UM PDS
//**************************************************** ********************************
//STEP001 EXEC PGM=IEBCOPY
//DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <--- INPUT DATASET
//DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <--- INPUT DATASET
//DD3 DD DSN=RACFID.IBMMF.PDS3,DISP=SHR <--- CONJUNTO DE DADOS DE SAÍDA
//*
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  COPY INDD=DD1
       INDD=DD2
      OUTDD=DD3
      SELECT MEMBER=(MEMBER1,MEMBER5,MEMBER9)
/*
```
## 28. JCL para renomear membro ao copiar PDS para PDS
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //**************************************************** ********************************
  //* JCL PARA RENOMEAR MEMBRO AO COPIAR PDS PARA PDS
  //**************************************************** ********************************
  //STEP001 EXEC PGM=IEBCOPY
  //DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <-- INPUT DATASET
  //DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <-- INPUT DATASET
  //DD3 DD DSN=RACFID.IBMMF.PDS3,DISP=SHR <-- CONJUNTO DE DADOS DE SAÍDA
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    COPY INDD=DD1
         INDD=DD2
         OUTDD=DD3
    SELECT MEMBER=((MEMBER1,NEW1),MEMBER2)
  /*
  ```
## 29. JCL para substituir membro ao copiar PDS para PDS
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//**************************************************** ********************************
//* JCL PARA SUBSTITUIR MEMBRO AO COPIAR PDS PARA PDS
//**************************************************** ********************************
//STEP001 EXEC PGM=IEBCOPY
//DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <-- INPUT DATASET
//DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <-- INPUT DATASET
//DD3 DD DSN=RACFID.IBMMF.PDS3,DISP=SHR <-- CONJUNTO DE DADOS DE SAÍDA
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  COPY INDD=DD1
       INDD=DD2
      OUTDD=DD3
    SELECT MEMBER=((MEMBER2,,R))
/*
```
## 30. JCL para excluir/omitir membros ao copiar PDS para PDS
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //**************************************************** ********************************
  //* JCL PARA EXCLUIR/OMITIR MEMBROS AO COPIAR PDS PARA PDS
  //**************************************************** ********************************
  //STEP001 EXEC PGM=IEBCOPY
  //DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <-- INPUT DATASET
  //DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <-- CONJUNTO DE DADOS DE SAÍDA
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    COPY INDD=DD1
        OUTDD=DD2
    EXCLUDE MEMBER=(MEMBER6,MEMBER3)
  /*
```
## 31. JCL para renomear e substituir ao copiar PDS para PDS
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA RENOMEAR E SUBSTITUIR AO COPIAR PDS PARA PDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBCOPY
  //DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <-- INPUT DATASET
  //DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <-- CONJUNTO DE DADOS DE SAÍDA
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    COPY INDD=DD1
        OUTDD=DD2
    SELECT MEMBER=((MEMBER1,MEMBER2,R))
  /*
 ```
## 32. JCL para comparar conjuntos de dados PS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COMPARAR OS CONJUNTOS DE DADOS PS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBCOMPR
  //SYSUT1 DD DSN=RACFID.IBMMF.PS1,DISP=SHR <--- DATASETS TO COMPARE
  //SYSUT2 DD DSN=RACFID.IBMMF.PS2,DISP=SHR <--- DATASETS TO COMPARE
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    COMPARE TIPORG=PS
  /*
 ```
## 33. JCL para comparar conjuntos de dados PDS
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COMPARAR CONJUNTOS DE DADOS PDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBCOMPR
  //SYSUT1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <--- DATASETS TO COMPARE
  //SYSUT2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <--- DATASETS TO COMPARE
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    COMPARE TIPORG=PO
  /*
 ```
## 34. JCL para copiar todo o trabalho em outro conjunto de dados
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COPIAR TODO O JOB PARA OUTRO CONJUNTO DE DADOS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBEDIT
  //SYSUT1 DD DSN=RACFID.IBMMF.PS1,DISP=SHR
  //SYSUT2 DD DSN=RACFID.IBMMF.PS2,DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    EDIT START=COPY1
  /*
 ```
## 35. JCL para copiar vários trabalhos em outro conjunto de dados
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//************************************************ ************************************
//* JCL PARA COPIAR MÚLTIPLOS TRABALHOS EM OUTRO CONJUNTO DE DADOS
//************************************************ ************************************
//STEP001 EXEC PGM=IEBEDIT
//SYSUT1 DD DSN=RACFID.IBMMF.PS1,DISP=SHR
//SYSUT2 DD DSN=RACFID.IBMMF.PS2,DISP=SHR
//*
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  EDIT START=COPY1
  EDIT START=COPY2
/*
```
## 36. JCL para copiar etapas usando o comando INCLUDE e EXCLUDE
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//************************************************ ************************************
//* JCL PARA COPIAR STEPS USANDO o comando INCLUDE e EXCLUDE
//************************************************ ************************************
//STEP001 EXEC PGM=IEBEDIT
//SYSUT1 DD DSN=RACFID.IBMMF.PS1,DISP=SHR
//SYSUT2 DD DSN=RACFID.IBMMF.PS2,DISP=SHR
//*
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  EDIT START=COPY1,TYPE=EXCLUDE,STEPNAME=STEPB
  EDIT START=COPY2,TYPE=INCLUDE,STEPNAME=STEPA
/*
```
37. JCL para copiar etapas usando o membro POSITION
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COPIAR ETAPAS USINF POSIÇÃO MEMBRO
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBEDIT
  //SYSUT1 DD DSN=RACFID.IBMMF.PS1,DISP=SHR
  //SYSUT2 DD DSN=RACFID.IBMMF.PS2,DISP=SHR
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    EDIT START=COPY1,TYPE=POSITION,STEPNAME=STEPC
  /*
  ```
## 38. JCL para mesclar conjuntos de dados
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA MERGE DATASETS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBCOPY
  //DD1 DD DSN=RACFID.IBMMF.PDS1,DISP=SHR <-- INPUT DATASET
  //DD2 DD DSN=RACFID.IBMMF.PDS2,DISP=SHR <-- INPUT DATASET
  //DD3 DD DSN=RACFID.IBMMF.PDS3,DISP=SHR <-- CONJUNTO DE DADOS DE SAÍDA
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
     COPY OUTDD=DD3
     INDD=DD1
     INDD=DD2
  /*
 ```
## 39. JCL para compactar um PDS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COMPRIMIR UM PDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEBCOPY
  //DD1 DD DSN=RACFID.IBMMF.PDS,DISP=SHR <-- DATASET TO COMPRESS
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    COPY INDD=DD1
        OUTDD=DD1
  /*
 ```
## 40. JCL para listar um PDS
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA LISTAR UM PDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEHLIST
  //DD1 DD UNIT=DISK,VOLUME=SER=IBMMFVOL,DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    LISTPDS DSNAME=RACFID.IBMMF.PDS,
            VOLUME=DISCO=IBMMFVOL
  /*
```
## 41. JCL para listar um VTOC
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//************************************************ ************************************
//* JCL PARA LISTAR UM VTOC
//************************************************ ************************************
//STEP001 EXEC PGM=IEHLIST
//DD1 DD UNIT=DISK,VOLUME=SER=IBMMFVOL,DISP=SHR
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  LISTVTOC FORMAT,
          VOLUME=DISK=IBMMFVOL
/*
```
## 42. JCL para RISCAR um conjunto de dados
```JCL
// JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
//************************************************ ************************************
//* JCL PARA RASGAR UM CONJUNTO DE DADOS
//************************************************ ************************************
//STEP001 EXEC PGM=IEHPROGM
//DD1 DD UNIT=DISK,VOLUME=SER=IBMMFVOL,DISP=SHR
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSIN DD *
  SCRATCH DSNAME=RACFID.IBMMF.PS,VOL=DISK=IBMMFVOL
/*
```
## 43. JCL para UNCATALOG um conjunto de dados
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL TO UNCATALOG um dataset
  //************************************************ ************************************
  //STEP001 EXEC PGM=IEHPROGM
  //DD1 DD UNIT=DISK,VOLUME=SER=IBMMFVOL,DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    UNCATLG DSNAME=RACFID.IBMMF.PS
  /*
  ```
## 44. JCL para classificar um único campo
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR UM ÚNICO CAMPO
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(1,10,CH,A)
  /*
  ```
## 45. JCL para classificar vários campos
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR UM CAMPO MÚLTIPLO
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(1,10,CH,A,30,5,CH,D)
  /*
  ```
## 46. JCL para SORT vários campos usando a palavra-chave FORMAT
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR MÚLTIPLOS CAMPOS USANDO PALAVRA-CHAVE DE FORMATO
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FORMAT=CH,FIELDS=(1,10,D,30,5,D)
  /*
  ```
## 47. JCL para classificar o registro em ordem crescente
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR O REGISTRO EM ORDEM ASCENDENTE
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(1,10,CH,A)
  /*
 ```
## 48. JCL para classificar o registro em ordem decrescente
 ```JCL 
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR O REGISTRO EM ORDEM DESCENDENTE
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(40,5,CH,D)
  /*
 ```
## 49. JCL para copiar um conjunto de dados usando SORT
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COPIAR UM DATASET USANDO SORT
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    OPTION COPY
  /*
  ```
## 50. JCL para classificar o registro com a condição INCLUDE
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR O REGISTRO COM INCLUIR CONDIÇÃO
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(1,10,CH,A)
    INCLUDE COND=(20,5,CH,EQ,C'IBMMF')
  /*
```
## 51. JCL para classificar o registro com INCLUDE muitas condições
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR O REGISTRO COM INCLUIR MUITAS CONDIÇÕES
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(1,10,CH,A)
    INCLUDE COND=(25,4,CH,EQ,C'2020',OR,50,1,CH,NE,C'F')
  /*
```  
## 52. JCL para classificar o registro com condição de omissão
```JCL 
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR O REGISTRO COM OMITIR CONDIÇÃO
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(1,10,CH,A)
    INCLUDE COND=(1,2,CH,EQ,C'NY',OR,1,2,CH,EQ,C'NJ')
  /*
```  
## 53. JCL para classificar o registro com o campo OUTREC
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR O REGISTRO COM OUTREC FIELDS
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(10,4,BI,D)
    OUTREC FIELDS=(1,20,30,50)
  /*
  ```
## 54. JCL para copiar um conjunto de dados usando SORT OUTREC com FINDREP
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COPIAR UM CONJUNTO DE DADOS USANDO SORT OUTREC COM FINDREP
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    OPTION COPY
    OUTREC FINDREP=(IN=C'MAINFRAME TUTORIAL',OUT=C'APRENDA COBOL')
  /*
  ```
## 55. JCL para classificar o registro e escrever OUTREC em colunas específicas
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA ORDENAR O REGISTRO E ESCREVER OUTREC EM COLUNAS ESPECÍFICAS
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,
  //DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  //DISP=SHR
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    SORT FIELDS=(1,4,BI,A)
    OUTREC BUILD=(20:2,4,30:10,70)
  /*
  ```
## 56. JCL para registro de arquivo SPLIT com base na condição
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA DIVIDIR O REGISTRO DE ARQUIVO COM BASE NA CONDIÇÃO
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOF01 DD DSN=RACFID.IBMMF.NY,DISP=SHR
  //SORTOF02 DD DSN=RACFID.IBMMF.PL,DISP=SHR
  //SORTOF03 DD DSN=RACFID.IBMMF.NJ.DISP=SHR
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    OPTION COPY
    OUTFIL FILES=01,INCLUDE=(23,2,CH,EQ,C'NY')
    OUTFIL FILES=02,INCLUDE=(23,2,CH,EQ,C'PL')
    OUTFIL FILES=03,INCLUDE=(23,2,CH,EQ,C'NJ')
  /*
  ```
## 57. JCL para DIVIDIR um conjunto de dados em partes iguais
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA DIVIDIR UM CONJUNTO DE DADOS EM PARTES IGUAIS
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOF01 DD DSN=RACFID.IBMMF.OUTPUT1,DISP=SHR
  //SORTOF02 DD DSN=RACFID.IBMMF.OUTPUT2,DISP=SHR
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    OPTION COPY
    OUTFIL FILES=(01,02),SPLIT
  /*
  ```
## 58. JCL para SORT para várias cópias usando OUTFIL
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT PARA MÚLTIPLAS CÓPIAS USANDO OUTFIL
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOF01 DD DSN=RACFID.IBMMF.OUT1,DISP=SHR
  //SORTOF02 DD DSN=RACFID.IBMMF.OUT2,DISP=SHR
  //SORTOF03 DD DSN=RACFID.IBMMF.OUT3.DISP=SHR
  //*
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    OPTION COPY
    OUTFIL FILES=(01,02,03)
  /*
  ```
## 59. JCL para remover registro duplicado do conjunto de dados
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA REMOVER REGISTRO DUPLICADO DO CONJUNTO DE DADOS
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,DISP=SHR
  //SYSIN DD *
    SORT FIELDS=(1,15,ZD,A)
    SUM FIELDS=NONE
  /*
 ```
## 60. JCL para COPIAR apenas os primeiros 100 registros no conjunto de dados
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA Copiar APENAS OS PRIMEIROS 100 REGISTROS NO CONJUNTO DE DADOS
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RECFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,DISP=SHR
  //SYSIN DD *
    OPTION COPY, STOPAFT=50
  /*
 ```
## 61. JCL para substituir o conteúdo do registro de entrada
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA SUBSTITUIR O CONTEÚDO DO REGISTRO DE ENTRADA
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RECFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,DISP=SHR
  //SYSIN DD *
    OPTION COPY
    INREC OVERLAY=(47:1,6)
  /*
  ```
## 62. Condição JCL SORT IF
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT IF CONDITION
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SORTIN DD *
  123456789012345 ---> Coluna
  HEADRselect
  DETAIL
  TRIALselect
  /*
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // DCB=*.SYSUT1,SPACE=(CYL,(50,1),RLSE)
  //SYSPRINT DD SYSOUT=*
  //SYSOUT DD SYSOUT=*
  //SYSIN DD *
    INREC IFTHEN=(WHEN=(6,1,CH,NE,C' '),BUILD=(1:1,15),
           IFTHEN=(WHEN=(6,1,CH,EQ,C' '),BUILD=(1:1,5,7:C'RECORD')
    OPTION COPY
  /*
  ```
## 63. JCL para converter um conjunto de dados FB para VB
```JCL  
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA CONVERTER UM CONJUNTO DE DADOS FB PARA VB
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.FBIN,DISP=SHR
  //VBOUT DD DSN=RACFID.IBMMF.VBOUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    OUTFIL FNAMES=VBOUT,FTOV
  /*
  ```
## 64. JCL para converter um conjunto de dados VB para FB
 ```JCL 
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA CONVERTER UM CONJUNTO DE DADOS VB PARA FB
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.VBIN,DISP=SHR <-- LRECL=104
  //FBOUT DD DSN=RACFID.IBMMF.FBOUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    OUTFIL FNAMES=FBOUT,VTOF,OUTREC=(5.100)
  /*
  ```
## 65. JCL para copiar o conjunto de dados usando ICETOOL
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL PARA COPIAR CONJUNTO DE DADOS USANDO ICETOOL
  //************************************************ ************************************
  //STEP001 EXEC PGM=ICETOOL
  //TOOLMSG DD SYSOUT=*
  //DFSMSG DD SYSOUT=*
  //*
  //INPUT  DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //OUTPUT DD DSN=RACFID.IBMMF.OUTPUT,DISP=(NEW,CATLG),
  // DCB=(*.INPUT1)
  //*
  //TOOLIN DD *
    COPY FROM(INPUT) TO (OUTPUT)
  /*
  ```
## 66. JCL SORT - Omitir dados numéricos
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT - OMITIR DADOS NUMÉRICOS
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(1,3,FS,NE,NUM)
  /*
  ```
Se o valor no campo (1,3,FS) não for igual (NE) a numerics(NUM), esses registros serão incluídos no conjunto de dados de saída.
O registro no conjunto de dados de saída serão aqueles em que o campo não possui números (um caractere diferente de 0 a 9 em algum lugar no campo).

## 67. JCL SORT - Incluir dados numéricos
 ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT - INCLUIR DADOS NUMÉRICOS
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(1,3,FS,EQ,NUM)
  /*
  ```
Se o valor no campo (1,3,FS) for igual (EQ) a numerics(NUM), esses registros serão incluídos no conjunto de dados de saída.

## 68. JCL SORT - Inclui dados de caracteres maiúsculos (A-Z)
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT - INCLUIR DADOS DE CARACTERES MAIÚSCULOS (A-Z)
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(5,10,BI,EQ,UC)
  /*
  ```
A instrução INCLUDE inclui registros que possuem caracteres maiúsculos (A-Z) nas posições 5 a 15.

## 69. JCL SORT - Incluir caracteres minúsculos Data(a-z)
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT - INCLUIR DADOS DE CARACTERES MINÚSCULOS (a-z)
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(5,10,BI,EQ,LC)
  /*
  ```
A instrução INCLUDE inclui registros que possuem caracteres minúsculos (a-z) nas posições 5 a 15.

## 70. JCL SORT - Inclui dados de caracteres maiúsculos e minúsculos (A-Z, a-z)
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT - INCLUIR DADOS DE CARACTERES MAIÚSCULOS E MINÚSCULOS (A-Z, a-z)
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(5,10,BI,EQ,MC)
  /*
  ```
A instrução INCLUDE inclui registros que possuem caracteres maiúsculos e minúsculos (A-Z, a-z) nas posições 5 a 15.

## 71. JCL SORT - Incluir caracteres maiúsculos e numéricos Dados (A-Z, 0-9)
  
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT - INCLUI MAIÚSCULAS E DADOS DE CARACTERES NUMÉRICOS (A-Z, 0-9)
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(5,10,BI,EQ,UN)
  /*
 ```
A instrução INCLUDE inclui registros que possuem caracteres maiúsculos e numéricos (A-Z, 0-9) nas posições 5 a 15.

## 72. JCL SORT - Inclui dados de caracteres minúsculos e numéricos (a-z, 0-9)
  ```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //************************************************ ************************************
  //* JCL SORT - INCLUIR MINÚSCULAS E DADOS DE CARACTERES NUMÉRICOS (a-z, 0-9)
  //************************************************ ************************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(5,10,BI,EQ,LN)
  /*
  ```
A instrução INCLUDE inclui registros que possuem caracteres minúsculos e numéricos (a-z, 0-9) nas posições 5 a 15.

## 73. JCL SORT - Inclui dados de caracteres maiúsculos, minúsculos e numéricos (A-Z, a-z, 0-9)
```JCL
  // JOBNAME JOB (ACCT),'NOME DO JOB', MSGCLASS=X, NOTIFY=SEU-USUARIO
  //**************************************************** ********************************
  //* JCL SORT - INCLUI MAIÚSCULAS, MINÚSCULAS E DADOS DE CARACTERES NUMÉRICOS (A-Z, a-z, 0-9)
  //**************************************************** ********************************
  //STEP001 EXEC PGM=SORT
  //SYSOUT DD SYSOUT=*
  //SORTIN DD DSN=RACFID.IBMMF.INPUT,DISP=SHR
  //SORTOUT DD DSN=RACFID.IBMMF.OUTPUT,
  // DISP=(NEW,CATLG,DELETE),
  // UNIT=3390,SPACE=(CIL,(5,5))
  //SYSIN DD *
    OPTION COPY
    INCLUDE COND=(5,10,BI,EQ,MN)
  /*
  ```
A instrução INCLUDE inclui registros que possuem caracteres maiúsculos, minúsculos e numéricos (A-Z, a-z, 0-9) nas posições 5 a 15.
