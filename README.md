# 불법 우회전 차량 단속 시스템
단속 및 과태료 부과 시스템 개발
## 목차
* [프로젝트 개요](#프로젝트-개요)
* [팀구성 및 역할](#팀구성-및-역할)
* [데이터 개요](#데이터-개요)
* [개발과정](#개발과정)
* [기대효과](#기대효과)
## 프로젝트 개요
* 도로교통법 개정으로 우회전 위반차량 단속 필요
* 단속 시행 결과 전년도 동기간 우회전 교통사고 51.3% 감소

![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/e9a8a162-2a16-4091-8057-55b7845b52b0)

### 프로젝트 목표
* 교차로 내 불법 우회전 차량 단속 시스템을 개발하여 교차로 내 보행자의 안전성을 향상하고자 함

### 우회전 위반 감지 process
![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/589c908d-2cf9-465c-9c57-17cfdb4ee46e)
### 결과
![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/9e6aecbb-6634-437c-8307-6c6b395e6937)
![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/a8fee6ad-e87a-4ed9-af3e-971f5d06f224)

* 총 86분 길이 영상에서 8번 위반사항 모두 감지
* 승용차, 승합차 범칙금 모두 맞게 분류
* 위반 내용 및 범칙금 엑셀 파일로 저장
  
## 팀구성 및 역할
* 이성수
  * 교차로 영상 데이터 EDA 및 이미지 전처리
  * 우회전 위반 감지 process 개발 및 모델 문제점 개선
  * 과태료 책정을 위한 승용차 및 승합차 분류 딥러닝 모델 개발
* 이종혁
  * YOLO 버전 및 트래커 비교 및 선정
  * 우회전 차량 인식 알고리즘 개발 및 모델 문제점 개선
  * 프로젝트 일정 및 미팅 관리
* 장호정
  * 우회전 관련 법규 확인
  * 교차로 영상 데이터 EDA 진행
  * 발표자료 제작 및 발표
* 정해찬
  * 모델 학습 데이터 수집
  * 오토바이, 보행자 분류 딥러닝 모델 개발
## 데이터 개요
* 출처 : 한양대학교 교통공학과
![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/d709ace7-d0e0-4f87-b2c0-9b9a376fced3)
* 오전 약 30분, 오후 약 56분 영상 데이터
* 영상 내 우회전 차량, 일시정지 위반 여부 및 시간 확인
* 위반여부 확인 위해 전방차량신호 시간별 라벨링

## 개발과정
### 위반 감지 모델
* 우회전 차량 인식
  * 영상내 우회전 차량 인식하기 위해 tracking 사용
  * 객체 인식 및 연산속도 비교를 통해 Yolov8s bot_sort 트래커 사용
    
  ![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/5b4e8120-e4a3-423b-94b2-ec5292d71623)
  
  * 객체 바운딩박스 좌표를 통해 우회전 차량 판단

* 차량 일시정지 인식
  
  ![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/ab8ad353-c7d3-4865-a65a-ba22a53cdd78)
  
  * 객체 바운딩박스의 변동을 통해 일시정지 판단
  * 일시정지의 상태에도 좌표의 변동 발생
  * 특이값의 영향을 줄이기 위해 좌표의 이동평균 사용

* 횡단보도 내 보행자 인식
  * 횡단보도 ROI 설정
  * 오토바이 라이더를 보행자로 인식하는 문제 발생
  * Yolo 커스텀 모델 학습하여 오토바이 라이더와 보행자 구분하여 인식
    
### 위반 차량 범칙금 분류 모델

![image](https://github.com/justdoit93/illegal_right_turn_detection/assets/129941418/0e3dc82b-ff05-41aa-ad81-d6c555fe7e61)

* 승용차, 승합차 범칙금 분류
* DenseNet 사용하여 104,465개 이미지 학습
* test accuracy : 99.22%

## 기대효과
* 우회전 교통사고 감소로 인명피해 방지
* 단속하는 인력 줄여 다른 곳에 배치 가능

