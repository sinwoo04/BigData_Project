# BigData_Project

## 주제: 교통 혼잡 예측
### 설명<br/>
시간대별 교통량 데이터를 기반으로 혼잡 시간대를 파악하고 시각화하여 교통 흐름의 주요 패턴 이해

### 데이터 분석 결과 예상
- 출퇴근 시간, 주말, 공휴일 등 특정 시간대의 교통량 증가

### 기대효과
1. 교통 효율성 개선
   - 실시간 교통 제어 : 교통 흐름 조절
   - 혼잡 예측 및 회피 경로 제공 : 운전자에게 실시간 우회 경로 제공
   - 대중교통 개선 : 대중교통 서비스의 시간표 및 경로를 효율적으로 조정
2. 정책 및 도시 계획 지원
   - 교통 인프라 확장 및 보수 계획 수립 : 도로확장, 신호체계 개선
3. 안정성 향상
   - 교통사고 감소 : 사고 지역 파악 및 예방 대책 수립
4. 스마트 도시 구현
   - IoT 및 AI 활용 : 교통 데이터를 활용한 스마트 교통 관리 시스템 구축

### 사용 데이터<br/>
View-T 3.0 인천광역시 고속도로 교통 혼잡 시간 데이터<br/>
https://viewt.ktdb.go.kr/cong/map/page.do

### 코드
```import pandas as pd
import matplotlib.pyplot as plt

# 데이터 로드
file_path = 'TrafficVolume.csv'  # 데이터 파일 경로
traffic_data = pd.read_csv(file_path)

# 1. 데이터 전처리
# 시간대 열(1시~24시)만 추출
time_columns = [str(i) + '시' for i in range(1, 25)]

# 열 이름 확인 및 정리
print("Before cleaning:", traffic_data.columns)
traffic_data.columns = traffic_data.columns.str.strip().str.replace(' ', '')
print("After cleaning:", traffic_data.columns)

traffic_data.columns = traffic_data.columns.str.strip()  # 앞뒤 공백 제거
traffic_data.columns = traffic_data.columns.str.replace(' ', '')  # 공백 전체 제거

time_columns = [col for col in traffic_data.columns if '시' in col]  # "시"가 포함된 열만 선택
print(time_columns)
traffic_data['평균 통행량'] = traffic_data[time_columns].mean(axis=1)

# 2. 혼잡 시간대 계산 (시간대별 평균값)
hourly_traffic = traffic_data[time_columns].mean()

# 3. 시각화
plt.figure(figsize=(12, 6))
plt.plot(hourly_traffic.index, hourly_traffic.values, marker='o', label='평균 통행량')
plt.title('시간대별 평균 교통량', fontsize=16)
plt.xlabel('시간대', fontsize=14)
plt.ylabel('평균 교통량', fontsize=14)
plt.grid(alpha=0.5)
plt.legend()
plt.xticks(rotation=45)
plt.show()
```

### 데이터 전처리
1. 열 이름 정리 : 불필요한 공백 제거 및 열 이름 간소화
2. 혼잡 시간대 열 추출 : 1시부터 24시까지 시간대를 나타내는 열만 선택
3. 평균 통행량 계산 : 각 시간대의 데이터를 평균 내어 '평균 통행량' 열 추가

### 시각화 결과
- x축 : 시간대(1시~24시)
- y축 : 평균 교통량 값
- 혼잡 시간대를 시각적으로 강조하여 한눈에 파악 가능
- '꺾은선 그래프' 형태로, 교통량의 증감 패턴을 쉽게 이해할 수 있음

### 해소방안
1. 교통 관리 시스템 최적화
   - 혼잡 구간 분산 : 데이터를 기반으로 혼잡 지역을 우회할 수 있는 대체 경로 실시간 제공
2. 대중교통 인프라 강화
   - 대중교통 우선 정책 : 버스 전용 차로 확대
   - 연계 교통망 구축 : 지하철, 버스, 자전거 공유 등 대중교통 수단 간 원활한 연계 시스템 확보
3. 교통 인프라 개선
   - 도로 확충 및 재설계 : 도로 확장 및 고가도로, 지하도로 설치
4. 스마트 기술 도입
   - 교통 데이터 플랫폼 구축 : IoT 센서를 통해 교통량, 사고 정보를 실시간 수집 및 공유
   - AI 기반 예측 시스템 : 교통 데이터를 분석하여 혼잡 예측 및 대응 방안 마련
5. 시민 의식 개선
   - 대중교통 및 친환경 이동 유도 캠페인
   - 운전자 교육 강화 : 교통 혼잡을 유발하는 행위에 대한 인식 개선
