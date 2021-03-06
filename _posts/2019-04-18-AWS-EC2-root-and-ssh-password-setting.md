---
layout: post
title: "AWS EC2 인스턴스 비밀번호 활성화"
subtitle: "EC2 인스턴스 공개키(.pem)없이 간편하게 접속하기"
categories : AWS
tags: AWS
author: Nayeong Kim
comments : True
---
<div id='preview' class='display-none'>
vscode와 같은 에디터를 원격지 서버에 연결해서 사용할 때 공개키로 연결하는 것은 생각보다 까다롭다. EC2 인스턴스의 비밀번호를 활성화하여 ftp 및 ssh 접속을 간편하게 만들어보자.
</div>

## EC2 인스턴스 비밀번호 활성화
vscode와 같은 에디터를 원격지 서버에 연결해서 사용할 때, 공개키로 연결하는 것은 생각보다 까다롭다. 뿐만 아니라 외부 컴퓨터(공개키가 없는)에서 서버에 접속하는 것 역시 불가능해서 공개키 기반의 접속방식은 불편한 점이 여럿 있다. 

<br>

### 1) 비밀번호 설정변경
아래 작업은 root에서 진행된다. 
<br>
아직 root계정을 활성화하지 않았다면 [[aws]Django 서버 세팅2]({{ site.baseurl}}/2019/04/15/AWS-EC2-Ubuntu-인스터스-생성-및-Django-서버-세팅-2.html)를 참고하자

나노 에디터를 이용하여 아래 설정을 변경한다.
{% highlight shell %}
$sudo nano /etc/ssh/sshd_config

# sshd_config
# PasswordAuthentication을 찾아 yes로 변경한다.
PasswordAuthentication yes
{% endhighlight %}

<br>

### 2) ssh 서비스 재시작
{% highlight shell %}
sudo service ssh restart
{% endhighlight %}

<br>

### 3) 비밀번호로 EC2 접속
{% highlight shell %}
$ssh -i root@{IP}
'root@{IP}'s password: # 비밀번호 입력
{% endhighlight %}
이와 같이, 비밀번호를 활성화하면 vscode, pycharm과 같은 에디터에서 간편하게 서버 연동을 할 수 있다.

<br>