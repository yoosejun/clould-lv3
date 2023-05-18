# 

## 기능적 요구사항
• 고객이 메뉴를 선택하여 주문한다.
• 고객이 선택한 메뉴에 대해 결제한다.
• 주문이 되면 주문 내역이 입점상점주인에게 주문정보가 전달된다.
• 상점주는 주문을 수락하거나 거절할 수 있다.
• 상점주는 요리시작때와 완료 시점에 시스템에 상태를 입력한다.
• 고객은 아직 요리가 시작되지 않은 주문은 취소할 수 있다.
• 요리가 완료되면 고객의 지역 인근의 라이더들에 의해 배송건 조회가 가능하다.
• 라이더가 해당 요리를 Pick한 후, 앱을 통해 통보한다.
• 고객이 주문상태를 중간중간 조회한다.
• 라이더의 배달이 끝나면 배송확인 버튼으로 모든 거래가 완료된다

## Model
www.msaez.io/#/storming/clouldlvsm
# 1. Eventstorming Model
# ![msaez](https://github.com/yoosejun/clould-lv3/assets/51141885/c7bdaa2d-030d-4dd6-be03-91018156d597)

# 2. Saga (Pub / Sub) 확인 (클러스터에 Kafka 설치 후)

# 3. Service Router 설치
# ![gitpod](https://github.com/yoosejun/clould-lv3/assets/51141885/30cdd4ea-c844-4e24-9433-e2dc3436fb25)

# 4. Zero downtime Deployment
# ![zerotime](https://github.com/yoosejun/clould-lv3/assets/51141885/cafe425c-425d-41ce-9b04-d708825a609d)


## Before Running Services
### Make sure there is a Kafka server running
```
cd kafka
docker-compose up
```
- Check the Kafka messages:
```
cd kafka
docker-compose exec -it kafka /bin/bash
cd /bin
./kafka-console-consumer --bootstrap-server localhost:9092 --topic cloudlv3
```

## Run the backend micro-services
See the README.md files inside the each microservices directory:

- app
- store
- delivery
- customerCenter


## Run API Gateway (Spring Gateway)
```
cd gateway
mvn spring-boot:run
```

## Test by API
- app
```
 http :8088/orders id="id" foodId="foodId" amount="amount" customerId="customerId" options="options" address="address" status="status" 
```
- store
```
 http :8088/orderManages id="id" foodId="foodId" orderId="orderId" amount="amount" options="options" address="address" status="status" 
```
- delivery
```
 http :8088/deliveries id="id" orderId="orderId" riderId="riderId" address="address" status="status" 
```
- customerCenter
```
```


## Run the frontend
```
cd frontend
npm i
npm run serve
```

## Test by UI
Open a browser to localhost:8088

## Required Utilities

- httpie (alternative for curl / POSTMAN) and network utils
```
sudo apt-get update
sudo apt-get install net-tools
sudo apt install iputils-ping
pip install httpie
```

- kubernetes utilities (kubectl)
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

- aws cli (aws)
```

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

- eksctl 
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

