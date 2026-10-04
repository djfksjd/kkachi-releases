# KKACHI 설치와 배포

**현재 버전: 0.1.0-beta.1 · macOS Apple Silicon 전용 베타.** Apple Developer ID 서명과 공증이 없습니다. Intel macOS와 Windows 설치 파일은 아직 제공하지 않습니다.

## 사용자가 설치하는 방법

### Homebrew · Apple Silicon macOS

```bash
brew install --cask djfksjd/kkachi/kkachi

# 새 버전으로 업데이트
brew upgrade --cask djfksjd/kkachi/kkachi
```

Cask는 버전별 DMG의 SHA-256을 검증합니다. macOS 보안 설정을 끄거나 격리 속성을 삭제하지 않습니다. Homebrew 자체가 필요한 경우 [공식 설치 안내](https://brew.sh/)를 참고하세요.

### 설치 파일 다운로드

[0.1.0-beta.1 릴리스](https://github.com/djfksjd/kkachi-releases/releases/tag/v0.1.0-beta.1)에서 `KKACHI-0.1.0-beta.1-macos-arm64.dmg`를 받습니다. DMG를 열고 `KKACHI.app`을 응용 프로그램 폴더로 옮깁니다.

첫 실행 때 확인되지 않은 개발자 안내가 나오면 앱을 한 번 연 뒤 **시스템 설정 → 개인정보 보호 및 보안 → 그래도 열기**를 선택합니다. [Apple의 앱 열기 안내](https://support.apple.com/102445)를 따르세요. “손상된 앱” 등 다른 오류가 나오면 보안 기능을 해제하지 말고 릴리스 저장소에 보고해 주세요.

GitHub CLI로 다운로드할 수도 있습니다. 베타는 prerelease이므로 버전을 명시합니다.

```bash
gh release download v0.1.0-beta.1 --repo djfksjd/kkachi-releases \
  --pattern 'KKACHI-0.1.0-beta.1-macos-arm64.dmg' --dir "$HOME/Downloads"
```

### 베타의 지원 범위

- 앱 내부 자동 업데이트는 제공하지 않습니다. Homebrew 또는 새 설치 파일로 업데이트합니다.
- 현재 공개 배포의 관리형 AI와 BYOK AI 실행은 비활성화되어 있습니다. AI 공급자 연결 화면이 곧 모든 실행 기능을 사용할 수 있다는 뜻은 아닙니다.
- HWPX의 외부 뷰어 검증은 미완료이며 외부 전달 검증을 생략하지 않습니다. 로컬 내부 검토본과 공식 제출본을 구분합니다.
- README 화면은 실제 앱의 예시 계정·내장 데모 자료입니다. 신규 설치에는 해당 예시 프로젝트가 자동으로 들어가지 않습니다.

