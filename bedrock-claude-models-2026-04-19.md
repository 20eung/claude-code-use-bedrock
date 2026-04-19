# AWS Bedrock Claude 모델 목록 (ap-northeast-2)

> 조회일: 2026-04-19  
> 리전: ap-northeast-2 (서울)  
> 명령어: `aws bedrock list-foundation-models --region ap-northeast-2`

## Claude 4.x 모델 (ACTIVE)

| 모델 ID | 모델명 | 상태 |
|---------|--------|------|
| `anthropic.claude-opus-4-7` | Claude Opus 4.7 | ACTIVE |
| `anthropic.claude-opus-4-6-v1` | Claude Opus 4.6 | ACTIVE |
| `anthropic.claude-opus-4-5-20251101-v1:0` | Claude Opus 4.5 | ACTIVE |
| `anthropic.claude-sonnet-4-6` | Claude Sonnet 4.6 | ACTIVE |
| `anthropic.claude-sonnet-4-5-20250929-v1:0` | Claude Sonnet 4.5 | ACTIVE |
| `anthropic.claude-sonnet-4-20250514-v1:0` | Claude Sonnet 4 | ACTIVE |
| `anthropic.claude-haiku-4-5-20251001-v1:0` | Claude Haiku 4.5 | ACTIVE |

## Claude 3.x 모델

| 모델 ID | 모델명 | 상태 |
|---------|--------|------|
| `anthropic.claude-3-5-sonnet-20241022-v2:0` | Claude 3.5 Sonnet v2 | ACTIVE |
| `anthropic.claude-3-5-sonnet-20240620-v1:0` | Claude 3.5 Sonnet | ACTIVE |
| `anthropic.claude-3-haiku-20240307-v1:0` | Claude 3 Haiku | ACTIVE |
| `anthropic.claude-3-haiku-20240307-v1:0:200k` | Claude 3 Haiku (200k) | ACTIVE |
| `anthropic.claude-3-7-sonnet-20250219-v1:0` | Claude 3.7 Sonnet | LEGACY |
| `anthropic.claude-3-sonnet-20240229-v1:0` | Claude 3 Sonnet | LEGACY |
| `anthropic.claude-3-sonnet-20240229-v1:0:28k` | Claude 3 Sonnet (28k) | LEGACY |
| `anthropic.claude-3-sonnet-20240229-v1:0:200k` | Claude 3 Sonnet (200k) | LEGACY |

---

## `global.` 접두사 — Inference Profile 사용 권장

### 직접 모델 ID vs. Inference Profile 비교

| 구분 | 직접 모델 ID | Inference Profile (`global.`) |
|------|-------------|-------------------------------|
| 예시 | `anthropic.claude-opus-4-7` | `global.anthropic.claude-opus-4-7` |
| 트래픽 처리 | `ap-northeast-2` 단일 리전 | 여러 리전 자동 분산 |
| 리전 장애 시 | 요청 실패 | 다른 리전으로 자동 전환 |
| 응답 속도 | 단일 리전 부하 | 부하 분산으로 지연 감소 |
| 유형 | Foundation Model | SYSTEM_DEFINED Inference Profile |

### Inference Profile 조회 명령어

```bash
aws bedrock list-inference-profiles --region ap-northeast-2 \
  --query "inferenceProfileSummaries[?contains(inferenceProfileId,'claude')].[inferenceProfileId,inferenceProfileName,type]" \
  --output table
```

조회 결과 (2026-04-19):

#### APAC 프로파일

| Inference Profile ID | 모델명 | 유형 |
|----------------------|--------|------|
| `apac.anthropic.claude-3-sonnet-20240229-v1:0` | APAC Anthropic Claude 3 Sonnet | SYSTEM_DEFINED |
| `apac.anthropic.claude-3-5-sonnet-20240620-v1:0` | APAC Anthropic Claude 3.5 Sonnet | SYSTEM_DEFINED |
| `apac.anthropic.claude-3-haiku-20240307-v1:0` | APAC Anthropic Claude 3 Haiku | SYSTEM_DEFINED |
| `apac.anthropic.claude-3-5-sonnet-20241022-v2:0` | APAC Anthropic Claude 3.5 Sonnet v2 | SYSTEM_DEFINED |
| `apac.anthropic.claude-3-7-sonnet-20250219-v1:0` | APAC Anthropic Claude 3.7 Sonnet | SYSTEM_DEFINED |
| `apac.anthropic.claude-sonnet-4-20250514-v1:0` | APAC Claude Sonnet 4 | SYSTEM_DEFINED |

#### GLOBAL 프로파일

| Inference Profile ID | 모델명 | 유형 |
|----------------------|--------|------|
| `global.anthropic.claude-opus-4-5-20251101-v1:0` | GLOBAL Anthropic Claude Opus 4.5 | SYSTEM_DEFINED |
| `global.anthropic.claude-haiku-4-5-20251001-v1:0` | Global Anthropic Claude Haiku 4.5 | SYSTEM_DEFINED |
| `global.anthropic.claude-sonnet-4-5-20250929-v1:0` | Global Claude Sonnet 4.5 | SYSTEM_DEFINED |
| `global.anthropic.claude-sonnet-4-6` | Global Anthropic Claude Sonnet 4.6 | SYSTEM_DEFINED |
| `global.anthropic.claude-opus-4-7` | Global Anthropic Claude Opus 4.7 | SYSTEM_DEFINED |
| `global.anthropic.claude-opus-4-6-v1` | Global Anthropic Claude Opus 4.6 | SYSTEM_DEFINED |

### `global.` 접두사를 써야 하는 이유

1. **고가용성**: 단일 리전 용량 부족 또는 장애 시 AWS가 자동으로 다른 리전(예: `us-east-1`, `eu-west-1`)으로 요청을 라우팅
2. **부하 분산**: 여러 리전에 트래픽을 분산하여 응답 지연 감소
3. **Anthropic 권장**: Bedrock + Claude Code 연동 시 Inference Profile 사용을 공식 권장
4. **비용 동일**: 직접 모델 ID와 동일한 요금 체계 적용

---

## Claude Code 환경변수 설정 예시

```bash
# Opus 4.7 사용 시 — global. 접두사 필수 (Inference Profile)
export ANTHROPIC_DEFAULT_OPUS_MODEL="global.anthropic.claude-opus-4-7"
export ANTHROPIC_MODEL="global.anthropic.claude-opus-4-7"

# Sonnet 4.6
export ANTHROPIC_DEFAULT_SONNET_MODEL="global.anthropic.claude-sonnet-4-6"

# Haiku 4.5
export ANTHROPIC_DEFAULT_HAIKU_MODEL="global.anthropic.claude-haiku-4-5-20251001-v1:0"
```

## settings.json 설정 예시

```json
{
  "model": "opus",
  "env": {
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "global.anthropic.claude-opus-4-7"
  }
}
```
