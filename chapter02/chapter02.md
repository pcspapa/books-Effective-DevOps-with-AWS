AWS

AKIAZIM4R3UKYM57OSMY

8LlTykQqTLpLMWe/tDU326Ioenmzn1moslDVvpjm


# AWS 용어설명
* IAM (Identity and Access Management)
* AMI (Amazon Machine Image)
* VPC (Virtual Private Cloud)


# AWS 게정 구성
$ aws configure
$ aws iam list-users

# EC2 인스턴스
## AMI
$ aws ec2 describe-images
$ aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn2-ami-hvm-2.0.????????-x86_64-gp2" --query 'Images[*].[CreationDate, Description, ImageId]' --output text | sort -k 1 | tail

### 인스턴스 유형
* t2.micro

### 보안 그룹
* VPC ID 확인
$ aws ec2 describe-vpcs
* 보안 그룹 생성
$ aws ec2 create-security-group \
  --group-name HelloWorld \
  --description "Hello World Demo" \
  --vpc-id vpc-76f8081d
* 인바운드 트래팩 열기
$ aws ec2 authorize-security-group-ingress \
  --group-id sg-0f0558150e5b80a5c \
  --protocol tcp \
  --port 22 \
  --cidr 0.0.0.0/0
$ aws ec2 authorize-security-group-ingress \
  --group-id sg-0f0558150e5b80a5c \
  --protocol tcp \
  --port 3000 \
  --cidr 0.0.0.0/0
$ aws ec2 describe-security-groups \
  --group-id sg-0f0558150e5b80a5c \
  --output text

### ssh 키 생성하기
$ aws ec2 create-key-pair --key-name EffectiveDevOpsAWS
$ echo -e key-valu-붙이기 > ~/.ssh/EffectiveDevOpsAWS.pem
$ chmod 644 ~/.ssh/EffectiveDevOpsAWS.pem

___참고. aws ec2 describe-subnets___

### EC2 인스턴스 띄우기
$ aws ec2 run-instances \
  --instance-type t2.micro \
  --key-name EffectiveDevOpsAWS \
  --security-group-ids sg-0f0558150e5b80a5c \
  --image-id ami-047f7b46bd6dd5d84 \
  --subnet-id subnet-8403e1ef
$ aws ec2 describe-instance-status --instance-ids i-06c809c93cf320e42

### ssh를 이용해 ec2 인스턴스에 접속하기
$ aws ec2 describe-instances \
  --instance-ids i-06c809c93cf320e42 \
  --query "Reservations[*].Instances[*].PublicIpAddress"
$ sudo ssh -i ~/.ssh/EffectiveDevOpsAWS.pem ec2-user@13.125.214.109

### 간단한 Hello World 웹 응용프로그램 생성하기
#### node.js 설치하기
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash
$ . ~/.nvm/nvm.sh
$ nvm install 4.4.5
$ node -e "console.log('Running Node.js ' + process.version)"

#### node.js Hello World 실행하기
$ vi helloworld.js
$ node helloworld.js

* http://13.125.214.109:3000





$ aws ec2 run-instances
