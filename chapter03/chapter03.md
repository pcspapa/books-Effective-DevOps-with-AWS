AWS

# 3장 클라우드포메이션을 이용, 인프라 다루기

## 클라우드포메이션을 이용, helloworld 예제 다시 작성하기
$ pip3 install troposphere
* 템플릿 생성
$ python3 helloworld-cf-template.py > helloworld-cf.template

$ pip3 install ipify
$ pip3 install ipaddress


## 구성 관리 시스템 추가하기
### ansible 설치
```
$ pip3 install ansible
```

### 앤서블 플레이그라운드 생성하기
```
$ aws cloudformation create-stack \
  --capabilities CAPABILITY_IAM \
  --stack-name ansible \
  --template-body file://helloworld-cf-v2.template \
  --parameters ParameterKey=KeyPair,ParameterValue=EffectiveDevOpsAWS 
```

### 앤서블 저상소 생성하기
```
$ mkdir ansible

$ curl -Lo ec2.py https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py

$ chmod +x ec2.py

$ python3 ./ec2.py

$ vi ec2.ini

$ vi ansible.cfg
```

#### 앤서블 플레이북
##### nodejs
```
$ ansible-galaxy into nodejs

$ cd nodejs/tasks

$ vi main.yml
```

##### helloworld
```
$ ansible-galaxy into helloworld

$ cd helloworld/tasks

$ vi main.yml

$ cd helloworld/handlers

$ cd main.yml

$ cd helloworld/meta

$ vi main.yml

$ cd helloworld

$ vi helloworld.yml
```

#### 플레이북 실행하기
##### 검사
```
$ ansible-playbook helloworld.yml \
  --private-key ~/.ssh/EffectiveDevOpsAWS.pem \
  -e target=ec2 \
  --list-hosts
```

##### 실행 (dry-run 모드)
```
$ ansible-playbook helloworld.yml \
  --private-key ~/.ssh/EffectiveDevOpsAWS.pem \
  -e target={IP} \
  --check
```

##### 실행
```
$ ansible-playbook helloworld.yml \
  --private-key ~/.ssh/EffectiveDevOpsAWS.pem \
  -e target={IP} 
```





13.125.219.76

$ sudo ssh -i ~/.ssh/EffectiveDevOpsAWS.pem ec2-user@13.125.208.87
