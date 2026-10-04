# KKACHI 설치와 배포

**현재 버전: 0.1.0-beta.1 · macOS 12 이상 Apple Silicon·Intel, Windows x64 베타.** Mac은 ad-hoc 서명만 있으며 Apple Developer ID 서명·공증은 없습니다. Windows 설치 파일은 배포자 서명이 없습니다.

## 사용자가 설치하는 방법

### Homebrew · Apple Silicon / Intel macOS

```bash
brew install --cask djfksjd/kkachi/kkachi

# 새 버전으로 업데이트
brew upgrade --cask djfksjd/kkachi/kkachi
```

Cask는 Mac 종류에 맞는 DMG를 선택하고 버전별 SHA-256을 검증합니다. macOS 보안 설정을 끄거나 격리 속성을 삭제하지 않습니다. Homebrew 자체가 필요한 경우 [공식 설치 안내](https://brew.sh/)를 참고하세요.

### 설치 파일 다운로드

[0.1.0-beta.1 릴리스](https://github.com/djfksjd/kkachi-releases/releases/tag/v0.1.0-beta.1)에서 Apple Silicon은 `KKACHI-0.1.0-beta.1-macos-arm64.dmg`, Intel은 `KKACHI-0.1.0-beta.1-macos-x64.dmg`를 받습니다. DMG를 열고 `KKACHI.app`을 응용 프로그램 폴더로 옮깁니다.

첫 실행 때 확인되지 않은 개발자 안내가 나오면 앱을 한 번 연 뒤 **시스템 설정 → 개인정보 보호 및 보안 → 그래도 열기**를 선택합니다. [Apple의 앱 열기 안내](https://support.apple.com/102445)를 따르세요. “손상된 앱” 등 다른 오류가 나오면 보안 기능을 해제하지 말고 릴리스 저장소에 보고해 주세요.

GitHub CLI로 다운로드할 수도 있습니다. 베타는 prerelease이므로 버전을 명시합니다.

```bash
gh release download v0.1.0-beta.1 --repo djfksjd/kkachi-releases \
  --pattern 'KKACHI-0.1.0-beta.1-macos-arm64.dmg' --dir "$HOME/Downloads"
```

### Windows · x64

[베타 릴리스](https://github.com/djfksjd/kkachi-releases/releases/tag/v0.1.0-beta.1)의 `KKACHI-0.1.0-beta.1-windows-x64-setup.exe`를 실행하고 설치 안내를 따릅니다. 설치 위치를 선택할 수 있고, 시작 메뉴와 바탕화면에서 KKACHI를 열 수 있습니다.

PowerShell로 다운로드하고 SHA-256을 확인한 뒤 설치 화면을 열 수도 있습니다.

```powershell
$version = '0.1.0-beta.1'
$file = "KKACHI-$version-windows-x64-setup.exe"
$base = "https://github.com/djfksjd/kkachi-releases/releases/download/v$version"
$folder = Join-Path $env:TEMP ("KKACHI-" + [guid]::NewGuid().ToString('N'))
New-Item -ItemType Directory -Path $folder | Out-Null
$installer = Join-Path $folder $file
Invoke-WebRequest "$base/$file" -OutFile $installer
$checksumFile = Join-Path $folder 'SHA256SUMS.txt'
Invoke-WebRequest "$base/SHA256SUMS.txt" -OutFile $checksumFile
$checksums = Get-Content -LiteralPath $checksumFile -Raw
$lines = @($checksums -split '\r?\n' | Where-Object { $_.EndsWith("  $file") })
if ($lines.Count -ne 1 -or $lines[0] -notmatch '^[a-f0-9]{64}  ') { throw '체크섬 항목을 확인할 수 없습니다.' }
$expected = $lines[0].Substring(0, 64)
if ((Get-FileHash $installer -Algorithm SHA256).Hash.ToLowerInvariant() -ne $expected) { throw '다운로드 파일의 SHA-256이 일치하지 않습니다.' }
Start-Process -FilePath $installer -Wait
```

서명은 GitHub 업로드나 일반 EXE 설치의 필수 조건이 아닙니다. 미서명 앱은 SmartScreen의 **Windows의 PC 보호** 안내가 나올 수 있습니다. 출처와 체크섬을 확인했고 **추가 정보 → 실행** 선택지가 표시되는 경우 앱별 실행을 선택할 수 있습니다. **Windows 11 Smart App Control이나 회사 보안 정책은 실행을 막을 수 있으며**, 그런 환경에는 정책에 맞는 서명된 배포가 필요합니다. 보안 기능을 끄는 설치 명령은 제공하지 않습니다. [Microsoft 안내](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/smartscreen-reputation)를 참고하세요.

### 베타의 지원 범위

- 앱 내부 자동 업데이트는 제공하지 않습니다. Homebrew 또는 새 설치 파일로 업데이트합니다.
- KKACHI 자체 관리형 AI와 API 키(BYOK) 방식은 비활성화되어 있습니다. Claude·Codex(ChatGPT)·Gemini 구독 계정 연결 경로는 별도로 지원하며, 실제 실행에는 해당 계정 연결과 권한이 필요합니다.
- HWPX의 외부 뷰어 검증은 미완료이며 외부 전달 검증을 생략하지 않습니다. 로컬 내부 검토본과 공식 제출본을 구분합니다.
- README 화면은 실제 앱의 예시 계정·내장 데모 자료입니다. 신규 설치에는 해당 예시 프로젝트가 자동으로 들어가지 않습니다.
