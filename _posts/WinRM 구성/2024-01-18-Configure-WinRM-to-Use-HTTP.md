---
title: HTTP를 사용하도록 WinRM 구성
categories: [Windows]
tags: [Windows, winrm]
---

상황 설명

## Target 서버 설정
로컬 컴퓨터 관리자 계정으로 실행되는 명령 프롬프트에서 다음 명령을 실행합니다.

1. 기본 WinRM 구성 값을 설정하려면 다음 명령을 실행합니다.
```console
winrm quickconfig
```
2. (선택 사항) 수신기가 작동 중인지 확인하고 기본 포트를 확인하려면 다음 명령을 실행합니다.
```console
winrm e winrm/config/listener
```
기본 포트는 HTTP의 경우 5985이며 HTTPS의 경우 5986입니다.
3. WinRM 서비스에서 기본 인증을 사용하도록 설정합니다.
+ 기본 인증이 허용되는지 여부를 확인하려면 다음 명령을 실행합니다.
```console
winrm get winrm/config/service
```
+ 기본 인증을 사용하도록 설정하려면 다음 명령을 실행합니다.
```console
winrm set winrm/config/service/auth @{Basic="true"}
```
4. WinRM 서비스에서 암호화되지 않은 데이터의 전송을 허용하려면 다음 명령을 실행합니다.
```console
winrm set winrm/config/service @{AllowUnencrypted="true"}
```
5. WinRM 서비스의 채널 바인딩 토큰 강화 수준이 강화로 설정된 경우 해당 값을 낮음으로 변경합니다.
```console
winrm set winrm/config/service/auth @{CbtHardeningLevel="relaxed"}
```

## Client 서버 설정
로컬 컴퓨터 관리자 계정으로 실행되는 명령 프롬프트에서 다음 명령을 실행합니다.

1. WinRM 클라이언트에서 기본 인증을 사용하도록 설정합니다.
+ 기본 인증이 허용되는지 여부를 확인하려면 다음 명령을 실행합니다.
```console
winrm get winrm/config/client
```
+ 기본 인증을 사용하도록 설정하려면 다음 명령을 실행합니다.
```console
winrm set winrm/config/client/auth @{Basic="true"}
```
2. WinRM 클라이언트에서 암호화되지 않은 데이터의 전송을 허용하려면 다음 명령을 실행합니다.
```console
winrm set winrm/config/client @{AllowUnencrypted="true"}
```
3. WinRM 호스트 시스템이 외부 도메인에 있는 경우, 신뢰할 수 있는 호스트를 지정하려면 다음 명령을 실행합니다.
```console
winrm set winrm/config/client @{TrustedHosts="host1, host2, host3"}
```
4. WinRM 서비스에 대한 연결을 테스트하려면 다음 명령을 실행합니다.
```console
winrm identify -r:http://winrm_server:5985 -auth:basic -u:user_name -p:password -encoding:utf-8
```

## 참조
<https://docs.vmware.com/kr/vRealize-Orchestrator/8.11/com.vmware.vrealize.orchestrator-use-plugins.doc/GUID-D4ACA4EF-D018-448A-866A-DECDDA5CC3C1.html>{:target="_blank"}

<https://svrforum.com/software/76940>{:target="_blank"}

<https://techexpert.tips/ko/powershell-ko/%ED%8C%8C%EC%9B%8C%EC%89%98-winrm%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9B%90%EA%B2%A9-%EB%AA%85%EB%A0%B9/>{:target="_blank"}
