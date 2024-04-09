## Set 생성
1. Multiple files(Add/Edit/Delete Sets) 선택 -> Select/Create/Delete Set 창 나옴
2. Select / Create Set 에 Set명 입력 후 하단의 Create 선택
- Set property 선택
  - Group : ex) single file 여러개, 파일 - 파일 연관 없음
  - System : ex) 이 set만 소스코드들 모두를 exe파일로 만든다고 생각, 관계 
- Add 선택 후 파일 불러오기 -> OK 선택
- " TBvison has found to analysis results for the selected source.
   Do you wish to run Static analyse to produce the required result? " - > No 선택 (아직 어떠한 설정도 하지 않았기 때문에)
                                                                                                                                                                                               
## Analysis Scope
- 정적 분석 및 동적 분석 진행 전에 고려해야 하는 다음과 같은 사항을 말함
  - 분석에 필요한 include path 와 define 심볼은 무엇이 있는가
  - 분석해야 하는 헤더파일은 무엇이 있는가
  - 분석에서 제외해야 하는 헤더파일이 있는가
- 위와 같은 사항들을 반영하지 않고 분석을 진행하면 결과가 제대로 나오지 않을 가능성이 높음

## Analysis Scope Setting
![스크린샷 2024-04-09 144750](https://github.com/2sahee/TIL/assets/119823052/aae84af6-863b-43a4-a173-fa75bc2e406b)
</br>
- Sysppvar.dat
  - 분석 수행 전 define 되어야 하는 모든 심볼들의 리스트 파일
- Sysearch.dat
  - 분석 수행 전 확장이 필요한 모든 헤더파일 경로 리스트 및 특정 헤더파일에 대한 분석 여부 설정 파일
