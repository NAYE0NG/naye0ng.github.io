---
layout: post
title: "AWS EC2 SSH 22번 포트 대신 80포트 사용하기"
subtitle: "방화벽, 포트차단 우회하기"
categories : AWS
tags: AWS
author: Nayeong Kim
comments : True
---

어제까지만 해도 22번 포트로 AWS EC2에 ssh 접속이 가능했는데, 오늘 ssh 접속하니 'port 22: Operation timed out'이 발생했다. EC2 보안 그룹에 22번 포트는 잘 열려 있어 혹시나 하고 핫스팟으로 접속하니 접속이 잘 된다. 아예 이 건물에서 22번 포트 접속을 막아놓은 것 같다. 이를 우회할 수 있는 방법을 고민하다가 인터넷은 안 막혀있으니 80 포트로 ssh 접속 하면 될것이라 생각했다.

<br>

## SSH 80포트로 접속하기
접속하려는 서버에 기본적으로 80포트가 열려있다는 가졍하에 진행한다. 

### 1) 80포트 설정 추가
{% highlight shell %}
$nano /etc/ssh/sshd_config 
{% endhighlight %}

<br>

### 2) sshd_config 파일 설정
80번 포트는 추가, 22번 포트는 주석으로 처리한다.
{% highlight shell %}
Port 80
#Port 22
{% endhighlight %}

<br>

### 3) ssh 서비스 재시작
{% highlight shell %}
$service sshd restart
{% endhighlight %}

<br>

### 4) 80포트로 ssh 접속
{% highlight shell %}
$ssh -p 80 root@{ip address}
{% endhighlight %}