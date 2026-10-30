[← 포트폴리오](../README.md)

# 잔해 속의 숨 · Breath In The Rubble

**지진 현장에 매몰된 사람의 시점에서 주변 도구를 활용하는 VR 생존 시뮬레이션입니다.**

이동할 수 없는 좁은 공간에서 휴대폰의 빛과 불안정한 통신 및 손이 닿는 물건으로 상황을 파악하는 경험을 제작하고 있습니다.

| 항목 | 내용 |
| --- | --- |
| 제작 형태 | 1인 기획·제작 |
| 핵심 콘셉트 | 매몰된 사람의 제한된 시점과 도구 상호작용 |
| 플레이 형태 | 앉은 시점의 1인칭 VR · 이동·텔레포트 제한 |
| 현재 상태 | 휴대폰과 매몰 공간 중심의 핵심 상호작용 프로토타입 |
| 대상 기기 | 미정 · OpenXR 기반 구성과 PC Editor 시험 경로 |
| 공개 자료 | [개발 저장소와 실행 안내](https://github.com/mooner1213/BreathInTheRubble) |

## 제약을 활용한 경험 설계

| 설계 선택 | 의도한 경험 |
| --- | --- |
| 움직일 수 없는 좁은 잔해 공간 | 손이 닿는 범위의 물건과 환경을 살피기 |
| 라이트와 긴급전화 중심의 휴대폰 | 익숙한 도구로 주변 탐색과 구조 요청 시도 |
| 무신호·연결 실패와 수신 회복 | 연결을 기다리고 다시 시도하는 불확실성 |
| 라이트·통화에 따른 배터리 소모 | 도구 사용 상태와 남은 자원 확인 |
| 먼지와 콘크리트·철근 디테일 | 매몰 공간의 밀도와 현장 분위기 표현 |

위 내용은 기획 의도입니다. 실제 사용자 시험으로 긴장감이나 몰입 효과가 입증됐다는 의미는 아닙니다.

## 현재 제작한 상호작용

| 기능 | 현재 범위 |
| --- | --- |
| 휴대폰 발견 | 지연 후 점등과 경고음 및 화면 빛 변화 |
| 라이트 | 후면 라이트 켜기·끄기와 화면 버튼 |
| 긴급전화 | SOS → 119 번호 화면 → 통화 시도. 실패·재시도·취소·연결 상태 |
| 수신 상태 | 무신호에서 불안정한 수신을 거쳐 회복하는 임시 시간 기반 진행 |
| 배터리 | 라이트·통화 상태에 따른 소모와 잔량 표시 |
| 물통 | 잡을 수 있는 밀봉 PET 물통과 기울기에 따라 수평을 유지하는 액체 표현 |
| 공간 | 좁은 매몰 공간과 잔해·먼지·표면 디테일 |

긴급전화는 게임 내부의 통화 상태 시뮬레이션입니다. 실제 전화 연결 기능이 아닙니다. 물통의 마시기·따르기는 아직 제작하지 않았습니다.

## 현재 확인 가능한 플레이 흐름

휴대폰의 점등과 경고음으로 도구의 위치를 확인하고 잡은 뒤 라이트로 주변을 살핍니다. SOS 화면에서 통화를 시도하고 수신 상태에 따라 실패·재시도·연결 결과를 확인합니다. 물통은 잡기와 액체 표현을 확인할 수 있습니다.

이 흐름은 현재 상호작용을 설명합니다. 각성·여진·고립·구조의 4단계 전체 스토리와 구조대 대화·최종 구조 연출은 아직 통합 완료된 상태가 아닙니다.

## 제작 자료와 시험 범위

- [현재 씬 · ConfinedPrototype](https://github.com/mooner1213/BreathInTheRubble/blob/main/Assets/_Project/Scenes/ConfinedPrototype.unity)
- [긴급전화·수신 변화 기록](https://github.com/mooner1213/BreathInTheRubble/blob/main/AgentScripts/EmergencyCallGuide.md)
- [공간·물통 제작 기록](https://github.com/mooner1213/BreathInTheRubble/blob/main/AgentScripts/ConfinedSpaceReport.md)
- [배터리 기록](https://github.com/mooner1213/BreathInTheRubble/blob/main/AgentScripts/PhoneBatteryGuide.md)
- [PC 입력 시험 안내](https://github.com/mooner1213/BreathInTheRubble/blob/main/AgentScripts/DesktopPhoneTestGuide.md)

제작 보고서에는 Unity 컴파일과 Editor·시뮬레이터 시험 기록이 있습니다. 실제 HMD 시험과 장시간 성능 측정은 해당 보고서 기준으로 아직 수행하지 않았습니다.

실행 시에는 Unity 6000.3.22f1에서 `Assets/_Project/Scenes/ConfinedPrototype.unity`를 엽니다. 현재 빌드 설정은 기존 SampleScene을 가리키므로 빌드 전에 플레이 씬을 지정해야 합니다. 세부 조작은 개발 저장소 README에서 확인할 수 있습니다.

## 다음 제작 범위

스토리 단계와 수신 상태를 연결하고 구조대 대화와 구조 연출을 통합할 계획입니다. 이후 대상 기기를 확정해 실제 HMD에서 조작과 공간 표현을 확인해야 합니다.

[← 대표 프로젝트 목록](../README.md)
