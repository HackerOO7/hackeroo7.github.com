---
layout:     post
title:      ��������verifiedboot��system image
category:
    - Android
tags:
    - verifiedboot
---

## GetVerityTreeSize��GetVerityMetadataSize

`build_verity_tree -s 2046820352`

`build_verity_metadata.py -s 2046820352`

������������Դ���`./tools/releasetools/build_image.py`��.

��������ʵsystem�����Ĵ�С

## ����Ԥ���ռ��system.simg

Ҫ���´��system.simg��verity_tree��verity_metadataԤ�����ռ䣬`-l`ָ���Ĵ�СΪ��ʵsystem�ռ�Ĵ�С��ȥ��һ���ֱ�õ��Ĵ�С

## ����root_hash��verity_tree

`build_verity_tree -A aee087a5be3b982978c923f566a94613496b417f2af592639bc80d141e34dfe7 system.simg verity.img`

����`aee087a5be3b982978c923f566a94613496b417f2af592639bc80d141e34dfe7`��salt��`system.simg`��Ҫ��sparse image������verity.img.

�����������

`3a82cfc74206a6a8b467fb699022d86ea36dee48b04fc8b40585d2cad941f463 aee087a5be3b982978c923f566a94613496b417f2af592639bc80d141e34dfe7`

��һ�����Ǻ���Ҫ�õ���root_hashֵ.

## ����verity_metadata

`build_verity_metadata.py 2030665728 verity_metadata.img 3a82cfc74206a6a8b467fb699022d86ea36dee48b04fc8b40585d2cad941f463 aee087a5be3b982978c923f566a94613496b417f2af592639bc80d141e34dfe7 /dev/block/platform/msm_sdcc.1/by-name/system verity_signer verity.pk8`

���е�һ��������Ԥ���˿ռ���system��С������ķֱ���root_hash, salt,system�������ֻ���ķ�����signer_path,˽Կ. �������verity_metadata.img��32768���ֽ�32kb�ǹ̶�ֵ��

## �������յ�image

`append2simg system.simg verity_metadata.img`

`append2simg system.simg verity.img`

�ֱ���ǰ���������ɵ��ļ�.

## �ο�

* [Android secrue boot](http://blog.andrsec.com/android/2015/04/10/android-boot-verity.html)