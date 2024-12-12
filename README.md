# **One-Click Detection Service**  
🌍 **위성 사진 활용 무단 방치 차량 디텍션** 🚗  

---

## 📖 **프로젝트 설명**  
위성 데이터는 국토지리정보원과 같은 기관에서 공개되고 있지만, 이를 실제로 활용하는 사람은 많지 않습니다. 이는 데이터 사용자와 제공 기관 간의 **기술적 간극**에서 비롯된 문제입니다.  
**One-Click Detection Service**는 이러한 간극을 좁히고, 누구나 데이터를 쉽게 활용할 수 있도록 설계된 서비스입니다. 특히, **무단 방치 차량** 탐지에 중점을 두어 위성 데이터를 실용적으로 활용할 수 있는 환경을 제공합니다.

---

### 💡 **문제 정의**  
- **위성 데이터의 활용 문제**: 공개된 데이터는 많지만, 대부분 제대로 활용되지 못합니다.  
- **사용자와 제공자 간의 간극**: 데이터를 활용하려면 전문적인 기술이 필요하지만, 일반 사용자는 접근하기 어렵습니다.

---

### 🌟 **해결책**  
**One-Click Detection Service**는 아래와 같은 기능을 통해 문제를 해결합니다:  
1. **사용자 친화적인 인터페이스**  
   - 클릭 한 번으로 데이터를 처리하고 분석할 수 있습니다.  
2. **무단 방치 차량 탐지**  
   - 위성 사진을 활용해 차량을 식별하고, 무단 방치된 차량을 탐지합니다.  
3. **데이터 활용성 증대**  
   - 복잡한 데이터 처리 과정을 간소화하여 누구나 데이터를 활용할 수 있도록 지원합니다.  

---

### 📌 **서비스 목표**  
- **모두를 위한 데이터 활용**  
  - 기술적 장벽을 제거하여 누구나 위성 데이터를 활용할 수 있도록 돕습니다.  
- **실용적 접근**  
  - 무단 방치 차량 탐지와 같은 구체적인 사례로 데이터 활용의 가치를 증명합니다.  

---

## ⚙️ **설치 방법**  
**Colab** 환경에서 프로젝트를 실행하는 방법입니다.

1. **GitHub 저장소 클론**  
   아래 명령어를 사용해 저장소를 복제합니다:
   ```bash
   !git clone https://github.com/lhg010524/Detection_Abandoned-vehicle

---

## 🚀 **사용 방법**

**One-Click Detection Service**는 아래 단계를 통해 위성 사진을 활용하여 무단 방치 차량을 탐지합니다.

### 1️⃣ **위성사진 수집**  
- **데이터 소스**: 국토지리정보원의 위성 데이터를 활용합니다.  
- **도구**: QGIS를 사용하여 필요한 위성 사진을 수집하고 적절히 편집합니다.  

### 2️⃣ **위성사진 전처리**  
- **모델**: SwinIR 모델을 사용하여 이미지 품질과 해상도를 향상시킵니다.  
- **결과**: 고해상도 이미지로 세부적인 객체 탐지가 가능해집니다.
- **학습** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lhg010524/Detection_Abandoned-vehicle/blob/main/TrainingSwinIR.ipynb)
- 📂 **Data Download** [Data Download Link](https://drive.google.com/drive/folders/1vFBLQ8Z7lBVCZ2qQgFzWSMkbLEdh2jmB?usp=sharing) <!-- 여기에 실제 데이터 다운로드 링크를 삽입하세요 -->



### 3️⃣ **차량 객체 세그멘테이션**  
- **알고리즘**: Mask R-CNN을 활용하여 차량 객체를 탐지하고 정확히 세그멘테이션합니다.  
- **결과물**: 탐지된 차량 객체가 이미지에서 시각적으로 구분됩니다.
- **학습** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lhg010524/Detection_Abandoned-vehicle/blob/main/mask_rcnn_train.ipynb)
- 📂 **Data Download** [Data Download Link](https://drive.google.com/drive/folders/1qkFEiILEDe9Tmyfc9jjP023kqG1XwLnd?usp=drive_link) <!-- 여기에 실제 데이터 다운로드 링크를 삽입하세요 -->

1. Annotation Files
```plaintext
/content/detectron2/
├── 1024_1.json
├── 1024_2.json
├── 1024_ver2_1.json
├── 1024_ver2_2.json
├── 1024_ver2_3.json
├── 1024_ver2_4.json
├── 256.json
├── 512.json
```

2. Image Directory
```plaintext
    /content/train
```

### 4️⃣ **중심 좌표 계산 및 변화 탐지**  
- 탐지된 객체들의 중심 좌표를 계산하여 정확한 위치 정보를 추출합니다.  
- 변화 탐지 알고리즘을 적용해 시간에 따른 객체 변화를 분석하고, 무단 방치 차량 여부를 판별합니다.
- **테스트** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lhg010524/Detection_Abandoned-vehicle/blob/main/mask_rcnn_test.ipynb)
  ```plaintext
      비교할 n-1 월 = "/content/drive/MyDrive/detectron2/n-1월" 에 사진 저장
      비교할 n 월 = "/content/drive/MyDrive/detectron2/n월" 에 사진 저장
      (각 폴더 내 사진 이름은 똑같아야 함.) 
      ex) 
      /content/drive/MyDrive/detectron2/5월
      ├── (37.483601°, 126.645470°).png
      ├── (37.483601°, 126.638490°).png
      
      /content/drive/MyDrive/detectron2/6월
      ├── (37.483601°, 126.645470°).png
      ├── (37.483601°, 126.638490°).png
   ```

✨ **이 4단계 프로세스**를 통해 위성 데이터를 효율적으로 활용하고, 무단 방치 차량을 간단히 탐지할 수 있습니다! 🚗🌍  

---

✨ **One-Click Detection Service**를 통해 누구나 위성 데이터를 활용할 수 있는 세상을 만들어갑니다! 🚀 


✨ [PPT](https://www.canva.com/design/DAGYDOfFGa8/iraMdiM5eu2H_2b8r8oecg/view?utm_content=DAGYDOfFGa8&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h1aafe4ed39)
