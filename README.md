# Claude Code Use Amazon Bedrock

## 1. AWS Credentials

### Windows CMD:

```cmd
mkdir "USERPROFILE%\.aws" 2>NUL

(
echo [default]
echo region = ap-northeast-2
echo output = json
) > "%USERPROFILE%\.aws\config"

(
echo [default]
echo aws_access_key_id = YOUR_ACCESS_KEY_ID
echo aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
echo region = ap-northeast-2
) > "%USERPROFILE%\.aws\credentials"

(
echo [default]
echo region = ap-northeast-2
echo output = json
) > "%USERPROFILE%\.aws\config"

setx AWS_REGION "ap-northeast-2"
setx AWS_PROFILE "[default]"
setx PATH "%USERPROFILE%\.local\bin;%PATH%"

```

### Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path $env:USERPROFILE\.aws

@"
[default]
region = ap-northeast-2
output = json
"@ | Set-Content -Path $env:USERPROFILE\.aws\config -Encoding Ascii

@"
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
region = ap-northeast-2
"@ | Set-Content -Path $env:USERPROFILE\.aws\credentials -Encoding Ascii

@"
[default]
region = ap-northeast-2
output = json
"@ | Set-Content -Path $env:USERPROFILE\.aws\config -Encoding Ascii

setx AWS_REGION "ap-northeast-2"
setx AWS_PROFILE "[default]"

$CurrentPath = [Environment]::GetEnvironmentVariable("Path", "User")
$NewPath = $CurrentPath + ";$env:USERPROFILE\.local\bin"
[Environment]::SetEnvironmentVariable("Path", $NewPath, "User")

```

### macOS, Linux, WSL:

```bash
mkdir -p ~/.aws

cat <<EOF > ~/.aws/config
[default]
region = ap-northeast-2
output = json
EOF

cat <<EOF > ~/.aws/credentials
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
region = ap-northeast-2
EOF

chmod 600 ~/.aws/config
chmod 600 ~/.aws/credentials
chmod 700 ~/.aws

cat <<EOF >> ~/.bashrc
# Bedrock 엔진 활성화 (필수)
export CLAUDE_CODE_USE_BEDROCK=1

# 리전 설정 (Bedrock 모델 권한을 받은 리전 입력, 예: us-east-1)
export AWS_REGION=ap-northeast-2

# (선택) 프로필 이름이 default가 아니라면 지정
# export AWS_PROFILE=[default]
EOF

```

## 2. Claude Code Install

### Windows CMD:

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

### Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

### macOS, Linux, WSL:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

## 3. Claude Code 실행

반드시 새 cmd, powershell, bash 창을 열어서 실행할 것 

### Windows CMD:

```cmd
claude
```

### Windows PowerShell:

```powershell
claude
```

### macOS, Linux, WSL:

```bash
claude
```

## 4. n8n MCP/Skills 설치

프롬프트에서 아래 내용 입력

```text
n8n MCP와 n8n Skills를 이 프로젝트에서 활용할 수 있게 프로젝트단으로 설치해줘.

참고링크:
- https://github.com/czlonkowski/n8n-mcp
- https://github.com/czlonkowski/n8n-skills
```
