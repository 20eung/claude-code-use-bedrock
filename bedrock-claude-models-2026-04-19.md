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

## Claude Code 환경변수 설정 예시

```bash
# Opus 4.7 사용 시 (settings.json env 키 또는 ~/.zshrc)
export ANTHROPIC_DEFAULT_OPUS_MODEL="anthropic.claude-opus-4-7"
export ANTHROPIC_MODEL="anthropic.claude-opus-4-7"

# Sonnet 4.6 (현재 기본값 유지)
export ANTHROPIC_DEFAULT_SONNET_MODEL="anthropic.claude-sonnet-4-6"

# Haiku 4.5 (현재 기본값 유지)
export ANTHROPIC_DEFAULT_HAIKU_MODEL="anthropic.claude-haiku-4-5-20251001-v1:0"
```

## settings.json 설정 예시

```json
{
  "model": "opus",
  "env": {
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "anthropic.claude-opus-4-7"
  }
}
```
