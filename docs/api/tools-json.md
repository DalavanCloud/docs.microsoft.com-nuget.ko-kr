---
title: tools.json nuget.exe 버전 검색
description: 에 대 한 끝점
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546937"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.json nuget.exe 버전 검색

현재는 스크립팅 가능한 방식으로 컴퓨터에 최신 버전의 nuget.exe 가져오려면 몇 가지가 있습니다. 다운로드를 추출 하는 예를 들어 합니다 [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org에서 패키지 있습니다. Nuget.exe를 이미가지고 있다고 하거나 필요 하므로이 일부 복잡성 (에 대 한 `nuget.exe install`)는 기본 압축 풀기 도구를 사용 하 여.nupkg 압축을 풀고 이진 내부 찾을를 만들어야 합니다.

Nuget.exe가 이미 있는 경우 사용할 수도 있습니다 `nuget.exe update -self`이지만 nuget.exe의 기존 복사본을 포함 합니다.이 또한 해야 합니다. 이 방법은 또한 업데이트를 최신 버전입니다. 특정 버전을 사용 하 여를 허용 되지 않습니다.

`tools.json` 끝점 수 둘 다 부트스트래핑 문제를 해결 및 다운로드 nuget.exe의 버전 제어를 제공 합니다. 이 수 사용자 지정 스크립트 또는 CI/CD 환경에서 검색 하 고 릴리스된 모든 버전의 nuget.exe 다운로드 합니다.

합니다 `tools.json` 인증 되지 않은 HTTP 요청을 사용 하 여 끝점을 인출할 수 있습니다 (예: `Invoke-WebRequest` PowerShell에서 또는 `wget`). JSON 역직렬 변환기를 사용 하 여 구문 분석할 수 및 HTTP 요청을 인증 되지 않은 후속 nuget.exe 다운로드를 사용 하 여 Url 인출할 수도 있습니다.

사용 하 여 끝점을 인출할 수 있습니다는 `GET` 메서드:

    GET https://dist.nuget.org/tools.json

합니다 [JSON 스키마](http://json-schema.org/) 끝점 여기 제공 됩니다.

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>응답

응답은 모든 사용 가능한 버전의 nuget.exe 포함 하는 JSON 문서입니다.

루트 JSON 개체에는 다음과 같은 속성이 있습니다.

이름      | 형식             | 필수
--------- | ---------------- | --------
nuget.exe | 개체의 배열 | 예

각 개체는 `nuget.exe` 배열에는 다음 속성이 있습니다.

이름     | 형식   | 필수 | 노트
-------- | ------ | -------- | -----
버전  | string | 예      | SemVer 2.0.0 문자열
url      | string | 예      | 이 버전의 nuget.exe 다운로드 하는 것에 대 한 절대 URL
단계    | string | 예      | 열거형 문자열
업로드 | string | 예      | 버전을 사용할 수 있었던 경우의 대략적인 타임 스탬프를

배열의 항목 내림차순, SemVer 2.0.0 순서로 정렬 됩니다. 이 확인 하려면 최신 버전을 찾고 클라이언트의 부담을 줄일 것입니다. 

`stage` 속성 어떻게 vettect 도구의이 버전은 나타냅니다. 

단계              | 의미
------------------ | ------
EarlyAccessPreview | 에 표시 되지 않습니다 합니다 [웹 페이지 다운로드](https://www.nuget.org/downloads) 파트너가 유효성을 검사 해야 하 고
Released           | 다운로드 사이트에서 사용 가능 하지만 아직 광범위 소비에 대 한 권장
ReleasedAndBlessed | 다운로드 사이트에서 사용할 수 있는 사용에 대 한 것이 좋습니다.

최신 것에 대 한 한 가지 간단한 방법은 권장 버전이 있는 목록의 첫 번째 버전을 사용 하는 `stage` 의 값 `ReleasedAndBlessed`합니다.

합니다 `NuGet.CommandLine` nuget.org에서 패키지는 일반적으로 사용 하 여 업데이트만 `ReleasedAndBlessed` 버전입니다.

### <a name="sample-request"></a>샘플 요청

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [tools-json.json](./_data/tools-json.json)]
