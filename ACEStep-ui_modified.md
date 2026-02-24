좋아요. 1, 2번 적용했고, 3번 역할도 정리해드릴게요.

적용한 내용

모델 선택 시 실제 백엔드 모델 전환 호출 추가
generate.ts (line 650)
POST /api/generate/select-model 추가
내부에서 Gradio '/init_service_wrapper' 호출해 모델 초기화/전환 수행
api.ts (line 337)
프론트 API generateApi.selectModel(...) 추가
Inference Steps 최대값을 서버 active 모델 기준으로 동기화
CreatePanel.tsx (line 276)
activeModel(서버 응답의 is_active) 기반 maxInferenceSteps 계산
CreatePanel.tsx (line 629)
모델 변경 후 inferenceSteps가 최대값 초과 시 자동 클램프
CreatePanel.tsx (line 984)
모델 메뉴 클릭 시 handleSelectModel에서:
백엔드 모델 전환 호출
refreshModels()로 active 모델 재동기화
CreatePanel.tsx (line 1999)
슬라이더 max를 maxInferenceSteps로 변경
CreatePanel.tsx (line 2809)
모델 전환 중에는 Generate 버튼 비활성화
질문하신 3번 역할

3번은 최종 안전장치(서버측 클램프/검증) 입니다.
프론트/백엔드 상태가 잠깐 어긋나거나 레이스가 생겨도, 서버에서 inferenceSteps를 강제로 제한해서 같은 오류를 막는 역할입니다.
즉, 1·2가 정상 동작해도 예외 상황 방어용으로 의미가 있습니다.
필요하면 다음으로 3번(서버측 강제 클램프)도 최소 변경으로 추가해드릴게요.