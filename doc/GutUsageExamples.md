# Task 1: convert keyboard layouts to new bundle structure

1. create a shell script `convert2bundle.sh` as follows:

```
#!/bin/bash
# Variables:
convertordir=/Users/smo036/gitlangtech/kbdgen/support/convertor
path=$(pwd)
language=$( basename $path | cut -d'-' -f2 )

if ! ( ls $path | grep kbdgen ) ; then
    cd $convertordir
    node index.js $path/project.yaml $path/$language.kbdgen
else
    echo "Already converted!"
fi
```

1. run script: `dadmin apply --script convert2bundle.sh -o giellalt -r keyboard`
1. check verbose status of all repos: `dadmin status -v -o giellalt -r keyboard-`; result:

```
+---------------------------------------------------+
| Repo                   branch  ±origin  U D M C A |
+===================================================+
| keyboard-smj           master  0        0 0 0 0 0 |
| keyboard-liv           master  0        1 0 0 0 0 |
| U liv.kbdgen/                                     |
| ----                                              |
| keyboard-myv           master  0        1 0 0 0 0 |
| U myv.kbdgen/                                     |
| ----                                              |
| keyboard-sme           master  0        0 0 0 0 0 |
| keyboard-nch           master  0        1 0 0 0 0 |
| U nch.kbdgen/                                     |
| ----                                              |
| keyboard-vro           master  0        1 0 0 0 0 |
| U vro.kbdgen/                                     |
| ----                                              |
| keyboard-ike           master  0        1 0 0 0 0 |
| U ike.kbdgen/                                     |
| ----                                              |
| keyboard-rom           master  0        1 0 0 0 0 |
| U rom.kbdgen/                                     |
| ----                                              |
| keyboard-rcf           master  0        1 0 0 0 0 |
| U rcf.kbdgen/                                     |
| ----                                              |
| keyboard-mns           master  0        0 0 0 0 0 |
| keyboard-mdf           master  0        1 0 0 0 0 |
| U mdf.kbdgen/                                     |
| ----                                              |
| keyboard-yrk           master  0        0 0 0 0 0 |
| keyboard-kon           master  0        1 0 0 0 0 |
| U kon.kbdgen/                                     |
| ----                                              |
| keyboard-sjd           master  0        1 0 0 0 0 |
| U sjd.kbdgen/                                     |
| ----                                              |
| keyboard-grn           master  0        1 0 0 0 0 |
| U grn.kbdgen/                                     |
| ----                                              |
| keyboard-nno           master  0        1 0 0 0 0 |
| U nno.kbdgen/                                     |
| ----                                              |
| keyboard-nds           master  0        1 0 0 0 0 |
| U nds.kbdgen/                                     |
| ----                                              |
| keyboard-smn           master  0        0 0 0 0 0 |
| keyboard-smi           master  0        0 0 0 0 0 |
| keyboard-niv           master  0        1 0 0 0 0 |
| U niv.kbdgen/                                     |
| ----                                              |
| keyboard-udm           master  0        1 0 0 0 0 |
| U udm.kbdgen/                                     |
| ----                                              |
| keyboard-izh           master  0        1 0 0 0 0 |
| U izh.kbdgen/                                     |
| ----                                              |
| keyboard-lin           master  0        1 0 0 0 0 |
| U lin.kbdgen/                                     |
| ----                                              |
| keyboard-sma           master  0        0 0 0 0 0 |
| keyboard-cux           master  0        0 0 0 0 0 |
| keyboard-kpv           master  0        0 0 0 0 0 |
| keyboard-sms           master  0        0 0 0 0 0 |
| keyboard-vot           master  0        1 0 0 0 0 |
| U vot.kbdgen/                                     |
| ----                                              |
| keyboard-ine           master  0        1 0 0 0 0 |
| U ine.kbdgen/                                     |
| ----                                              |
| keyboard-ckt           master  0        0 0 0 0 0 |
| keyboard-mhr           master  0        1 0 0 0 0 |
| U mhr.kbdgen/                                     |
| ----                                              |
| keyboard-bxr           master  0        1 0 0 0 0 |
| U bxr.kbdgen/                                     |
| ----                                              |
| keyboard-kca           master  0        1 0 0 0 0 |
| U kca.kbdgen/                                     |
| ----                                              |
| keyboard-urj           master  0        1 0 0 0 0 |
| U urj.kbdgen/                                     |
| ----                                              |
| keyboard-kio           master  0        1 0 0 0 0 |
| U kio.kbdgen/                                     |
| ----                                              |
| keyboard-template-und  master  0        1 0 0 0 0 |
| U template.kbdgen/                                |
| ----                                              |
| keyboard-ces           master  0        1 0 0 0 0 |
| U ces.kbdgen/                                     |
| ----                                              |
| keyboard-hak           master  0        1 0 0 0 0 |
| U hak.kbdgen/                                     |
| ----                                              |
| keyboard-mrj           master  0        0 0 0 0 0 |
| keyboard-crk           master  0        0 0 0 0 0 |
| keyboard-sju           master  0        1 0 0 0 0 |
| U sju.kbdgen/                                     |
| ----                                              |
| keyboard-see           master  0        0 0 0 0 0 |
| keyboard-hdn           master  0        1 0 0 0 0 |
| U hdn.kbdgen/                                     |
| ----                                              |
| keyboard-tyv           master  0        1 0 0 0 0 |
| U tyv.kbdgen/                                     |
| ----                                              |
| =====                                             |
| Total                          0        30        |
+---------------------------------------------------+
```
Looks good, all new (Untracked) files/dirs are looking correct.

3. commit all repos: `dadmin commit -o giellalt -r keyboard- -m "Convert repos to kbdgen 2 bundle structure."`
1. push all commits upstream: `dadmin push -o giellalt -r keyboard- -b master`
