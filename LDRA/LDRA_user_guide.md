# Set 생성
1. Multiple files(Add/Edit/Delete Sets) 선택 -> Select/Create/Delete Set 창 나옴
2. Select / Create Set 에 Set명 입력 후 하단의 Create 선택
- Set property 선택
  - Group : ex) single file 여러개, 파일 - 파일 연관 없음
  - System : ex) 이 set만 소스코드들 모두를 exe파일로 만든다고 생각, 관계 
- Add 선택 후 파일 불러오기 -> OK 선택
- " TBvison has found to analysis results for the selected source.
   Do you wish to run Static analyse to produce the required result? " - > No 선택 (아직 어떠한 설정도 하지 않았기 때문에)
                                                                                                                                                                                               
# Analysis Scope
- 정적 분석 및 동적 분석 진행 전에 고려해야 하는 다음과 같은 사항을 말함
  - 분석에 필요한 include path 와 define 심볼은 무엇이 있는가
  - 분석해야 하는 헤더파일은 무엇이 있는가
  - 분석에서 제외해야 하는 헤더파일이 있는가
- 위와 같은 사항들을 반영하지 않고 분석을 진행하면 결과가 제대로 나오지 않을 가능성이 높음

# Analysis Scope Setting
![스크린샷 2024-04-09 144750](https://github.com/2sahee/TIL/assets/119823052/aae84af6-863b-43a4-a173-fa75bc2e406b)
</br>
- Sysppvar.dat
  - 분석 수행 전 define 되어야 하는 모든 심볼들의 리스트 파일
- Sysearch.dat
  - 분석 수행 전 확장이 필요한 모든 헤더파일 경로 리스트 및 특정 헤더파일에 대한 분석 여부 설정 파일


## LDRA info


### Analysis Scope
분석 범위에는 다음이 포함됩니다.

1) 분석 대상으로 선택한 소스 파일.</br>
이는 파일 선택 대화 상자 또는 설정된 프로세스에 파일 추가를 통해 사용자가 제어합니다.</br>

2) 파일 포함 설정.
사용자는 확인란을 사용하여 포함 파일 처리를 끌 수 있으며, 이 경우 선택한 소스 파일만 분석됩니다.</br>
포함 파일 처리가 켜져 있는 경우 LDRA 테스트베드 정적 분석은 따옴표 안에 포함된 경우 상위 파일의 디렉터리와 관련된 모든 헤더 파일을 포함합니다.</br>

#include "header.h"

INI 파일 플래그 SHORTEN_SEARCH_RELATIVE_TO_MAIN_FILE=TRUE 또는 FALSE를 설정하여 "조부모" 디렉터리 검색을 활성화/비활성화합니다.</br>
추가 포함 경로가 지정되었거나 다음과 같이 꺾쇠 괄호가 사용되는 상황의 경우:</br>

#include <header2.h>

그런 다음 포함 파일 디렉터리를 지정하는 항목이 데이터 파일 sysearch.dat에 필요합니다.</br>
이 데이터 파일의 형식은 중요하며 모든 열은 한 줄에 있어야 합니다.</br>
이 데이터 파일을 사용하는 것은 환경이나 컴파일러 명령줄 등에서 포함 디렉터리를 지정하는 것과 유사합니다.</br>
시스템(꺾쇠 괄호)이 포함된 sysearch.dat 경로만 사용하려면(즉, 상위 파일과 관련된 검색 없음) INI 플래그를 SHORTEN_FORCE_SYS_SEARCH=TRUE로 설정하십시오.</br>
자세한 내용은 사용 설명서의 파일 포함을 참조하세요.</br>

3) 매크로 확장 설정.</br>
소스 코드의 매크로는 컴파일러 명령줄에서 정의하거나 IDE를 사용하여 대화형으로 정의하거나 컴파일러에서 미리 정의할 수 있습니다.</br>
이러한 상황에서 LDRA Testbed에서는 이 정보를 데이터 파일 sysppvar.dat에 배치해야 합니다.</br>
이를 통해 도구의 매크로 확장 기능이 컴파일러와 동일한 정보를 가지며 동일한 버전의 코드를 처리할 수 있습니다.</br>
LDRA Testbed가 분석하지 않는 헤더 파일에도 매크로를 정의할 수 있습니다.</br>
이 상황에서는 도구가 이러한 값을 선택할 수 있도록 정의를 sysppvar.dat에 배치할 수 있습니다.</br>




### Macros and Sysppvar
소스 코드의 매크로는 컴파일러 명령줄에서 정의하거나 IDE를 사용하여 대화형으로 정의하거나 컴파일러에서 미리 정의할 수 있습니다.</br>
이러한 상황에서 LDRA Testbed에서는 이 정보를 데이터 파일 sysppvar.dat에 배치해야 합니다.</br>
이를 통해 도구의 매크로 확장 기능이 컴파일러와 동일한 정보를 가지며 동일한 버전의 코드를 처리할 수 있습니다.</br>
LDRA Testbed가 분석하지 않는 헤더 파일에도 매크로를 정의할 수 있습니다.</br>
이 상황에서는 도구가 이러한 값을 선택할 수 있도록 정의를 sysppvar.dat에 배치할 수 있습니다.</br>

## Data file search
sysearch(파일 경로 포함) 또는 sysppvar(매크로 정의)인 경우</br>
데이터 파일이 지정되지 않은 경우 정적 분석은 사용 가능한 최상의 기본 파일, 검색 중 다음 순서로:</br>
1) 현재 소스 파일 디렉터리
2) LDRA Testbed가 시작된 디렉토리
3) LDRA Testbed 설치 디렉터리

## Expanding includes and Sysearch
사용자는 확인란을 사용하여 포함 파일 처리를 끌 수 있으며, 이 경우 선택한 소스 파일만 분석됩니다.</br>
포함 파일 처리가 켜져 있는 경우 LDRA 테스트베드 정적 분석은 따옴표 안에 포함된 경우 상위 파일의 디렉터리와 관련된 모든 헤더 파일을 포함합니다.</br>

#include "header.h"

INI 파일 플래그 SHORTEN_SEARCH_RELATIVE_TO_MAIN_FILE=TRUE 또는 FALSE를 설정하여 "grandparent" 디렉터리 검색을 활성화/비활성화합니다.</br>
추가 포함 경로가 지정되었거나 다음과 같이 꺾쇠 괄호가 사용되는 상황의 경우:</br>

#include <header2.h>

그런 다음 포함 파일 디렉터리를 지정하는 항목이 데이터 파일 sysearch.dat에 필요합니다.</br>
이 데이터 파일의 형식은 중요하며 모든 열은 한 줄에 있어야 합니다.</br>
이 데이터 파일을 사용하는 것은 환경이나 컴파일러 명령줄 등에서 포함 디렉터리를 지정하는 것과 유사합니다.</br>
시스템(꺾쇠 괄호)이 포함된 sysearch.dat 경로만 사용하려면(즉, 상위 파일과 관련된 검색 없음) INI 플래그SHORTEN_FORCE_SYS_SEARCH=TRUE를 설정하십시오.</br>




# 코딩룰 설정
### MISRA / DAPA / CWE 중 필요한 코딩룰 물어보고, CWE가 필요하다면 버전 특정된게 있냐 물어봄 -> 추후에 매핑테이블이랑 dat파일 만들어준다고 함
  - MISRA : 자동차 모델 기반의 코딩 규칙. 
  - DAPA : 무기체계 소프트웨어 코딩 규칙 Software Coding Rule Guide(SCR-G) 방위사업청
- 코딩룰 고르는 법
1) Code Review Options 창 열기
2) Programming Standads Model 탭에서 분석에 사용 될 코딩 규칙 설정
3) Data Files 탭에서 분석에 사용 될 rule dat file 선택 가능, edit 누르면 modifier 정보 편집 가




# 메트릭 
## 제한값을 무기체계 메뉴얼 따르냐고 물어봄 -> 이것도 추후에 무기체계 메뉴얼 제한값대로 설정된 파일 보내줄테니 그거 적용하면 그 제한값대로 레포트 나옴





# 정적분석 (Static Analysis)
### Select Analysis 
![스크린샷 2024-04-09 173500](https://github.com/2sahee/TIL/assets/119823052/0cbd1a7e-c34f-42bf-a688-931d4c779b56)
</br>
- Main Static Analysis
  - 분석에 용이한 형태로 코드를 재구성한다.
  - programming standards 위반을 검출한다.
  - static Call graph 를 작성한다.
- Complexity Analysis
  - 복잡도 계산
- Static Data Flow Analysis
  - 데이터 흐름 분석 및 변수 사용과 관련된 분석
- Cross Reference
  - 함수 Call 관계와 사용된 변수를 분석
- Information Flow Analysis
  - 변수들 간의 상호관계에 대해 분석
  - procedure 간의 의존성 분석
- Data Object Analysis
  - Static Data Flow Analysis, Cross Reference 및
  - Information Flow Analysis 통해 특정 변수에 대한 레포트 생성

##


