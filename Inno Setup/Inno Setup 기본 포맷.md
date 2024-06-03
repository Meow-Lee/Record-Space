- - - 
```javascript
#define MyAppName "wsserver" // 프로그램 이름 정의
#define MyAppVersion "1.5" // 프로그램 버전 정의
#define MyAppPublisher "My Company, Inc." // 프로그램 배포자 정의
#define MyAppURL "https://www.example.com/" // 프로그램 URL 정의
#define MyAppExeName "MyProg.exe" // 실행 파일의 이름 정의
// 프로그램과 연관된 파일의 이름을 wsserver File로 정의
#define MyAppAssocName MyAppName + " File"
#define MyAppAssocExt ".myp" // 프로그램과 연관된 파일의 확장자를 .myp로 정의
// 프로그램과 연관된 파일의 레지스트리 키 정의하며, 공백 제거 후 확장자를 추가
#define MyAppAssocKey StringChange(MyAppAssocName, " ", "") + MyAppAssocExt

// 설치
[Setup]
AppId={{A06266B8-23E0-4F26-93D1-5B95B6C32BB8} // 이 애플리케이션의 고유 식별자 GUID
AppName={#MyAppName} // 애플리케이션의 이름을 이전에 정의한 MyAppName 매크로로 설정
AppVersion={#MyAppVersion} // 애플리케이션 버전
AppPublisher={#MyAppPublisher} // 배포자 정의
AppPublisherURL={#MyAppURL} // 배포자 URL
AppSupportURL={#MyAppURL} // 지원 URL
AppUpdatesURL={#MyAppURL} // 업데이트 URL
DefaultDirName=C:\Program Files (x86)\{#MyAppName} // 애플리케이션 설치 기본 디렉토리
// 파일 연결 변경 허용/프로그램 설치 후 파일 확장자와 이 프로그램 간의 연관을 설정
ChangesAssociations=yes
DisableProgramGroupPage=yes // 시작메뉴에 프로그램 그룹 만들지 않음
OutputBaseFilename=mysetup // 생성되는 설치 파일의 기본 이름을 mysetup으로 설정
Compression=lzma // 설치 파일 압축하는 방법
SolidCompression=yes // Solid 압축을 활성화하여 설치 파일 크기를 최적화
WizardStyle=modern // 설치 마법사의 스타일을 현대적인 스타일로 설정

// 언어
[Languages]
// 설치 프로그램 언어 설정, 사용할 언어 파일 지정
Name: "english"; MessagesFile: "compiler:Default.isl"

// 설치 프로그램에 대한 작업 정의
[Tasks]
// 작업의 이름 정의(데스크톱 아이콘 만드는 작업)
// 작업의 설명 정의(설치 마법사에서 사용자에게 표시됨)
// 작업이 속하는 그룹의 설명을 정의
// 작업을 기본적으로 선택되지 않도록 설정(checked면 기본적으로 선택되어 설치됨)
Name: "desktopicon"; Description: "{cm:CreateDesktopIcon}"; GroupDescription: "{cm:AdditionalIcons}"; Flags: unchecked

// 설치할 파일 지정
[Files]
// 설치할 파일의 원본 경로
// 파일을 설치할 대상 디렉토리 지정
Source: "C:\Program Files (x86)\Inno Setup 6\Examples\{#MyAppExeName}"; DestDir: "{app}"; Flags: ignoreversion
Source: "C:\Users\이명모\Documents\vscode_workspace\wsserver\target\release\*"; DestDir: "{app}"; Flags: ignoreversion recursesubdirs createallsubdirs

[Registry]
Root: HKA; Subkey: "Software\Classes\{#MyAppAssocExt}\OpenWithProgids"; ValueType: string; ValueName: "{#MyAppAssocKey}"; ValueData: ""; Flags: uninsdeletevalue
Root: HKA; Subkey: "Software\Classes\{#MyAppAssocKey}"; ValueType: string; ValueName: ""; ValueData: "{#MyAppAssocName}"; Flags: uninsdeletekey
Root: HKA; Subkey: "Software\Classes\{#MyAppAssocKey}\DefaultIcon"; ValueType: string; ValueName: ""; ValueData: "{app}\{#MyAppExeName},0"
Root: HKA; Subkey: "Software\Classes\{#MyAppAssocKey}\shell\open\command"; ValueType: string; ValueName: ""; ValueData: """{app}\{#MyAppExeName}"" ""%1"""
Root: HKA; Subkey: "Software\Classes\Applications\{#MyAppExeName}\SupportedTypes"; ValueType: string; ValueName: ".myp"; ValueData: ""

// 아이콘
[Icons]
// 시작 메뉴에 추가될 프로그램의 항목 이름 정의
// 시작메뉴 항목이 클릭되었을 때 실행될 파일의 경로
Name: "{autoprograms}\{#MyAppName}"; Filename: "{app}\{#MyAppExeName}"
// 데스크톱에 추가될 프로그램의 바로 가기의 이름 정의
// 바로가기가 클릭되었을 때 실행될 파일의 경로를 지정
// 데스크톱에 바로 가기를 만들기 위한 작업 설정
Name: "{autodesktop}\{#MyAppName}"; Filename: "{app}\{#MyAppExeName}"; Tasks: desktopicon

// 설치 시 실행해야 하는 파일 실행
[Run]
// 실행할 파일의 경로
Filename: "{app}\{#MyAppExeName}";
// 설치 완료 후에 실행되는 프로그램의 설명 제공
Description: "{cm:LaunchProgram,{#StringChange(MyAppName, '&', '&&')}}";
// 프로그램 실행의 특정 동작 지정
Flags: nowait postinstall skipifsilent

```