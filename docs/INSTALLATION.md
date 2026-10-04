# KKACHI 설치와 배포

현재 첫 설치 파일을 준비하고 있습니다. 기존 2026-07-29 로컬 패키지는 최신 버전으로 배포하지 않습니다. 아래 사용자 설치 명령은 검증된 첫 릴리스와 Homebrew Cask를 발행한 뒤 사용할 수 있습니다.

## 사용자가 설치하는 방법

### Homebrew · macOS

```bash
brew install --cask djfksjd/kkachi/kkachi

# 새 버전으로 업데이트
brew upgrade --cask djfksjd/kkachi/kkachi
```

Apple Silicon과 Intel에 맞는 DMG를 선택하고 SHA-256을 검증합니다. macOS 보안 설정을 끄거나 격리 속성을 삭제하는 명령은 사용하지 않습니다.

### 설치 파일 다운로드

[공개 릴리스 목록](https://github.com/djfksjd/kkachi-releases/releases)에서 자신의 플랫폼에 맞는 파일을 선택합니다.

- macOS: DMG를 열고 `KKACHI.app`을 응용 프로그램 폴더로 옮깁니다.
- Windows: `windows-x64-setup.exe`를 실행합니다.

GitHub CLI가 설치되어 있다면 릴리스 발행 후 아래 명령으로 파일을 받을 수도 있습니다.

```bash
# Apple Silicon macOS
gh release download --repo djfksjd/kkachi-releases \
  --pattern 'KKACHI-*-macos-arm64.dmg' --dir "$HOME/Downloads"

# Intel macOS
gh release download --repo djfksjd/kkachi-releases \
  --pattern 'KKACHI-*-macos-x64.dmg' --dir "$HOME/Downloads"

# Windows PowerShell
gh release download --repo djfksjd/kkachi-releases --pattern 'KKACHI-*-windows-x64-setup.exe' --dir "$env:USERPROFILE\Downloads"
```

