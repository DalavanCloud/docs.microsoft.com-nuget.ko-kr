---
title: NuGet 2.8.5 릴리스 정보
description: NuGet 2.8.5 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820081"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 릴리스 정보

[NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 릴리스 정보](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 2015 년 3 월 30 일에 발표 되었습니다. 한 부분 업데이트는 우리의 2.8.3 일부와 VSIX 대상 수정 합니다.

NuGet 패키지 관리자 대화 상자에 대 한 지원이 추가 되었습니다이 릴리스에서 [DNX 대상 프레임 워크 모니커](https://github.com/aspnet/dnx)합니다.  지원 되는 이러한 새 프레임 워크 모니커는 다음과 같습니다.

* **core50** -는 'base' 대상 Core CLR 호환 되는 프레임 워크 모니커 (TFM).
* **dnx452** -전체 4.5.2를 사용 하 여 A TFM DNX 기반 특정 앱의 프레임 워크 버전
* **dnx46** -4.6 전체 버전의 framework 사용 하 여 A TFM DNX 기반 특정 앱
* **dnxcore50** -Core 5.0 버전의 framework 사용 하 여 A TFM DNX 기반 특정 앱

FSharp 프로젝트에 제대로 설치에서 금지 패키지 하 한 버그 수정:

https://nuget.codeplex.com/workitem/4400