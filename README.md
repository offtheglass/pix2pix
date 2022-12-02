## pix2pix
# pix2pix
<img width="1213" alt="pix1" src="https://user-images.githubusercontent.com/86214286/205290281-b9f76507-9b3a-4132-8519-b12d5e6b628e.png">
*다양한 task를 image to image translation 관점에서 hyperparameter의 조정 없이 공통적인 approach로 좋은 결과를 냄.

# conditional GAN
<img width="939" alt="heisthebest" src="https://user-images.githubusercontent.com/86214286/205292769-d2a3925a-9e43-47f3-be06-9c96d3733b91.png">
* GAN과 비슷한 구조인데 조건(condition)을 주어서 조건에 맞게 학습할 수 있도록 함.(ex) 0-9까지의 클래스가 있다고 하면 7이라는 조건을 주고 그에 맞는 이미지를 생성)
* pix 2 pix는 일종의 conditional GAN으로 condition을 image로 주는 것으로 볼 수 있다.
# architecture
<img width="178" alt="pix 2 pix 2" src="https://user-images.githubusercontent.com/86214286/205290685-a819aa1f-cf43-42f0-872a-973d1b778803.png">
* U-net 기반의 네트워크 아키텍쳐 사용(input과 output의 크기를 맞추는 것은 다른 네트워크를 써도 되지만 U-net을 쓰는 게 성능이 좋았다고 함)
* 입력과 출력 모두 이미지이므로 입력과 출력의 차원을 맞춰줌
* -Skip connection을 사용해서 앞 쪽 layer에서 사용됐던 출력정보들을 뒤 쪽 layer에서도 사용할 수 있게 해 학습의 난이도를 낮춤
* 입력이미지와 출력이미지가 많은 정보를 공유하기 때문에 skip connection을 사용하는 것이 좋은 성능을 내는 데 도움이 된다고 할 수 있음.

# objective function


<img width="399" alt="pix2pix 3" src="https://user-images.githubusercontent.com/86214286/205290933-0ac73dd1-7aa1-453f-87b7-6b82e9c691c6.png">
* 왼쪽의 Lcgan은 현실적인 이미지를 만들도록하고, 오른쪽의 L1 loss는 실제 정답과 generator가 만든 image가 유사하도록 학습을 이끈다.
* L1 loss를 사용할 때 l2 loss를 사용할 때 보다 blurring 현상이 덜 발생한다고 함.
<img width="472" alt="pix12" src="https://user-images.githubusercontent.com/86214286/205291832-b481a62a-065c-405c-a6a7-c83293cce9d6.png">

<img width="380" alt="pix2 pix 4" src="https://user-images.githubusercontent.com/86214286/205291112-cc533ead-e1fa-419a-9f3a-c6d3db44693f.png">
<img width="357" alt="pix2pix 5" src="https://user-images.githubusercontent.com/86214286/205291194-f2353058-c6ad-4aa8-93ea-9c0eea8890f7.png">

# discriminator
* convolutional PatchGan 분류 모델을 사용해 이미지 전체에 대해 판별하지 않고, 이미지 내 패치 단위로 판별한다. —>상대적으로 적은 parameter를 사용하기 때문에 빠르고, 이미지의 크기가 크더라도 해당 이미지 전체를 보는 게 아니고 패치 단위로 보기 때문에 discrimnator 입장에서 부담이 덜하다.

# 한계점
* 학습 데이터가 실제 정답 y와 x가 한 쌍으로 묶여 있어야 한다. 
