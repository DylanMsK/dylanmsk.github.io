---
title: SemVer - 버전 표기법
date: 2022-09-01 09:00:00 +9000
description: 'Software 버전 관리 규칙에 대해 알아보자'
categories: [DevOps, Common]
tags: [semver, version, semantic versioning]
published: true
pin: false
img_path: /assets/img/posts/semver/
---

이번 글에서는 버전 관리에 대해 알아보려고 한다.  

버전 관리를 함으로써 얻을 수 있는 **장점**은 아래와 같다.  
1.  그동안 개발해 온 히스토리를 한 눈에 파악할 수 있다.
2.  프로그램에서 사용된 오픈소스 또는 라이브러리의 의존성 관계를 확립할 수 있다.
3.  팀 프로젝트시 상대방과 원활한 코드 병합이 가능하다.  

위와 같은 장점이 있듯이 물론 **단점**도 있다.  
1.  프로그램 개발에 있어 버전 관리라는 추가적인 리소스가 투입된다.
2.  의존성 지옥에 빠져 프로젝트 진행에 제한이 올 수 있다.

버전 관리는 어디까지나 효율적인 소프트웨어 관리를 위함 **선택 사항일 뿐 강제 사항이 아니다.**  
때문에 개인별, 회사별, 그리고 소프트웨어별로 버전 형식이 다를 수도 있으며,  
무엇을 콕 집어 정답이다 라고 말 할수 없다.

하지만 버전 관리를 더 효율적으로 운영하기 위한 목적 하에 다양한 커뮤니티 개발자들과 소프트웨어 거장들의 수많은 시도가 있었다.  
다양한 시도로 현재 가장 많이 사용하는 버저닝 규칙인 **유의적 버전 명세(Semantic Versioning)** 가 등장하게 되었다.

SemVer는 Github의 공동창업자인 [톰 프레스턴-베르너](https://tom.preston-werner.com/)가 만든 기준으로 그 효율성을 인정 받아 많은 소프트웨어가 SemVer 기준을 채택하고 있다.

## 유의적 버전(SemVer)이란?

요약하자면 버전을 아래와 같이 표현하는 방식을 말한다.
![semver](semver.png)
- Major: 신규 업데이트로 인해 기존 버전과 호환되지 않는다면 major를 한 단계 올린다.
- Minor: 신규 기능이 추가되거나 기존 기능이 사라졌지만 기존 버전과 호환이 된다면 minor를 한 단계 올린다.
- Patch: 기존 버전에서의 버그를 수정하였거나 동일한 기능의 코드 리팩토링이 발생했다면 patch를 한 단계 올린다.
- Label: 정식 배포 전 버전이나 빌드 메타데이터를 위한 label로, 아스키(ASCII) 문자로 표현한다.

공식 SemVer 명세는 총 11개의 규칙으로 이루어져 있으며, 혼동하기 쉬운 몇 가지 규칙에 대해서 정리한다.

### 1. 기본 버저닝은 X.Y.Z 형태로 한다.

> A normal version number MUST take the form X.Y.Z where X, Y, and Z are non-negative integers, and MUST NOT contain leading zeroes. X is the major version, Y is the minor version, and Z is the patch version. Each element MUST increase numerically.
> {:.prompt-info}

보통의 버저닝은 X.Y.Z 형태로 하며, 반드시 X, Y, Z는 **0으로 시작되지 않는 자연수**여야 한다.  
또한 **각각의 숫자는 반드시 증가하는 수**여야 합니다.

예를 들면, **1.9.0 → 1.10.0 → 1.11.0** 방식으로 버저닝이 되어야 한다.

### 2. 이미 배포된 버전은 롤백을 금지한다.

> Once a versioned package has been released, the contents of that version MUST NOT be modified. Any modifications MUST be released as a new version.

특정 버전이 배포된 후에는 어떤 일이 있어도 해당 버전의 내용을 변경해서는 안된다.

예를들어 **1.0.1 → 1.0.2** 로 버그가 수정되어 배포되었다고 가정할 때, 개발자의 실수로 배포중 오타가 기입되어 배포가 되었더라도 이미 배포된 1.0.2를 철회하고 오타 수정 후 다시 1.0.2로 배포하면 안된다.

기능상 전혀 문제가 없는 오타를 수정했다고 하더라도 **동일 버전으로 재배포는 절대 금지**하며, 어떻게 해서든 코드를 수정해서 배포해야 한다면 반드시 버전을 한 단계 더 올린 1.0.3으로 배포해야 한다.

### 3. 상위 버전을 올릴 때 하위버전은 0으로 초기화 한다.

> Major version X (X.y.z | X > 0) MUST be incremented if any backwards incompatible changes are introduced to the public API. It MAY also include minor and patch level changes. Patch and minor version MUST be reset to 0 when major version is incremented.

기존의 공개된 API(X > 0)와 호환되지 않는 변화가 있을때는 반드시 Major 버전을 올린다.  
이때 Minor와, Patch는 반드시 0으로 초기화 한다.

마찬가지로 Minor를 올리는 경우에는 Patch를 0으로 초기화 한다.

예를 들면,
-   Major 버전업의 경우 **0.8.24 → 1.0.0**
-   Minor 버전업의 경우 **0.8.24 → 0.9.0**

<br>
>지금까지 규칙은 나름 직관적이어서 이해가 쉬웠지만 앞으로의 내용은 정말 헷갈릴 수 있다. 
{: .prompt-warning }

### 4. Pre-release 버전 표기법

> A pre-release version MAY be denoted by appending a hyphen and a series of dot separated identifiers immediately following the patch version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Numeric identifiers MUST NOT include leading zeroes. Pre-release versions have a lower precedence than the associated normal version. A pre-release version indicates that the version is unstable and might not satisfy the intended compatibility requirements as denoted by its associated normal version.

Pre-release 버전 표기 방식은 Patch 버전의 뒤에 하이픈 기호(-)를 붙히고 마침표(.)로 구분된 식별자를 더해서 표기한다.  
이때 식별자는 반드시 한 글자 이상의 ASCII 문자와 숫자, 하이픈으로만 구성된다[0-9A-Za-z-].

또한, X.Y.Z 형태의 보통 버전 표기법과 마찬가지로 숫자 앞에는 0을 붙혀서는 안된다.

예를 들면,
-   1.0.0-alpha
-   1.0.0-alpha.1
-   1.0.0-0.3.7
-   1.0.0-x.7.z.92
-   1.0.0-x-y-z.–.

Pre-release 버전은 정식 배포된 버전 아니다.  
때문에 연관된 일반 버전과 호환성 이슈가 있을 수 있어 사용시 유의해야 한다.

그리고 버전 간의 우선순위에 있어서 관련한 보통 버전보다 우선순위가 낮다.

### 5. Build metadata 표기법

> Build metadata MAY be denoted by appending a plus sign and a series of dot separated identifiers immediately following the patch or pre-release version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Build metadata MUST be ignored when determining version precedence. Thus two versions that differ only in the build metadata, have the same precedence.

Build metadata는 patch 버전이나, pre-release 버전 뒤에 더하기(+) 기호를 붙혀 표현할 수 있다.  
pre-relase 버전과 마찬가지로 한글자 이상의 ASCII 문자와 숫자, 하이픈만 식별자로 사용 가능하다.

예를 들면,
-   1.0.0-alpha+001
-   1.0.0+20130313144700
-   1.0.0-beta+exp.sha.5114f85.

Build metadata는 버전 간의 우선순위가 없기 때문에 build metadata가 다른 동일한 버전의 우선순위는 같다.

### 6. 버전 간의 우선순위 비교

> Precedence refers to how versions are compared to each other when ordered.

1.  Precedence MUST be calculated by separating the version into major, minor, patch and pre-release identifiers in that order (Build metadata does not figure into precedence).
2.  Precedence is determined by the first difference when comparing each of these identifiers from left to right as follows: Major, minor, and patch versions are always compared numerically.
3.  When major, minor, and patch are equal, a pre-release version has lower precedence than a normal version:
4.  Precedence for two pre-release versions with the same major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found as follows: 4-1. Identifiers consisting of only digits are compared numerically. 4-2. Identifiers with letters or hyphens are compared lexically in ASCII sort order. 4-3. Numeric identifiers always have lower precedence than non-numeric identifiers. 4-4. A larger set of pre-release fields has a higher precedence than a smaller set, if all of the preceding identifiers are equal.

버전 간의 순서는 Major, Minor, Patch, pre-release의 식별자를 기준으로 우선순위를 정렬할 수 있다.  
이때 빌드 메타데이터는 우선순위에 영향을 주지 않으므로 정렬에서 제외한다.

1.  X.Y.Z 형태의 일반 버전의 경우
    -   1.0.0 < 2.0.0 < 2.1.0 < 2.1.1.
2.  동일한 일반 버전에서 pre-release 버전이 표기된 경우
    -   1.0.0-alpha < 1.0.0.
3.  동일한 일반 버전에서 pre-release 버전 간의 경우
    -   숫자로만 구성된 식별자는 수의 크기로 비교하고, 알파벳이나 하이픈이 포함된 경우에는 아스키 문자열로 정렬한다.
    -   숫자로만 구성된 식별자는 어떤 경우에도 문자와 하이픈이 있는 식별자보다 낮은 우선순위로 여긴다.
    -   식별자가 모두 같은 pre-release 버전의 경우에는 필드 수가 많은 쪽이 더 높은 우선순위를 가진다.
    -   1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

여기까지 혼동하기 쉬운 Semver의 몇 가지 버전 명명법에 대해 정리해 봤다.

단순히 일반 버전 표기법으로 버전을 관리하면 정말 쉬웠지만, pre-release 버전과 빌드 메타데이터를 버전에 표현하는 순간부터 개발자와 사용자 모두 혼동스러워 일반 표기법으로만 버전을 관리하는 경우도 있다.

## Reference
1.  [Semantic Versioning 2.0.0](https://semver.org/)
2.  [다양한 소프트웨어 버전 명명 (Software versioning)](https://blog.sonim1.com/243)
3.  [버전 표기법 (SemVer) 기초개념 알려드림. 5분 순삭.](https://www.youtube.com/watch?v=FPSZ9ao9cFo)
4.  [Semantic Versioning 소개](https://spoqa.github.io/2012/12/18/semantic-versioning.html)