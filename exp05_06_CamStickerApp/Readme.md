# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 김정현 (6기 리서치)
- 리뷰어 : 김서연

# 프로젝트 루브릭
평가문항	상세기준
1. 자기만의 카메라앱 기능 구현을 완수하였다.	
[X] 얼굴 영역과 랜드마크를 정확하게 검출하고, 스티커 사진을 합성시키는 데 성공하였다.

2. 스티커 이미지를 정확한 원본 위치에 반영하였다.
[X] 정확한 좌표계산을 통해 고양이 수염의 위치가 원본 얼굴에 잘 어울리게 출력되었다.

3. 카메라 스티커앱을 다양한 원본이미지에 적용했을 때의 문제점을 체계적으로 분석하였다.
[ ] 얼굴각도, 이미지 밝기, 촬영거리 등 다양한 변수에 따른 영향도를 보고서에 체계적으로 분석하였다.

# PRT(Peer Review Template)
- [X] **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 루브릭 3개 기준 중 2개 만족. 여러 변수가 있을 때 어떻게 개선할 수 있을지도 고려해보면 좋을 것 같다.
    
- [X] **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - ```python
      import numpy as np
      # 좌표 순서가 y,x임에 유의한다. (y,x,rgb channel)
      sticker_area = img_show[refined_y:refined_y+img_sticker.shape[0], refined_x:refined_x+img_sticker.shape[1]]
      ```
    - 헷갈릴 수 있는 부분에 대한 주석 작성
    
- [X] **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” ”새로운 시도 또는 추가 실험을 수행”해봤나요?**
     - ```python
       # 수염 이미지
       sticker_area = img_bgr[refined_y:refined_y +img_sticker.shape[0], refined_x:refined_x+img_sticker.shape[1]]

       # 흰색 배경을 감지
       threshold = 240
       white_mask = np.all(img_sticker > threshold, axis=-1)

       # 흰색이 아닌 부분에서 원본 이미지와 스티커 이미지를 가중치를 이용해 합침
       blended_area = cv2.addWeighted(sticker_area, 0.5, img_sticker, 0.5, 0)
       img_bgr[refined_y:refined_y +img_sticker.shape[0], refined_x:refined_x+img_sticker.shape[1]] = \
         np.where(white_mask[..., None], sticker_area, blended_area)
    ```
    - 이미지를 반투명하게 만드는 코드를 추가하고 원리를 설명했다.
        
- [X] **4. 회고를 잘 작성했나요?**
    - <img width="889" alt="스크린샷 2023-10-04 오후 12 26 00" src="https://github.com/Seoyeon1129/AIFFEL_Research_6th_jh/assets/112914475/4baca543-7113-4db8-b703-1aed83c5c035">
    - 회고를 상세하게 잘 작성하였다.

          
- [X] **5. 코드가 간결하고 효율적인가요?**
    - 대체로 잘 작성되었다.
    - ```python
      refined_x = x - w // 2
      refined_y = y
      ```
      위 코드에서 refined_x, refined_y가 음수가 되거나, 값이 너무 커서 스티커 이미지 삽입 시 전체 이미지 프레임을 넘어갈 수 있다. 이 부분을 고려해서 좌표 수정 필요.


# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
