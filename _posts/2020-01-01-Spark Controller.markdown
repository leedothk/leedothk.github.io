---
layout: post
title:  "Spark Controller"
date:   2020-01-01 00:00:00 +0000
categories: Hadoop
---
![My helpful screenshot](/images/sparkcontroller_architectur.png)

- SAP에서 만든 SAP HANA DB와 HDFS(Hive) 데이터 연동 Adapter
- Spark 하고는 직접적인 관련이 없음
- 내장된 Spark Thrift, SparkSQL 를 사용하는 것으로 추정.  즉, 암바리에 Spark가 없어도 됨(?)
- Client-Server 구조(Client-HANA DB Client Side, Server-Hive Side)
- Hive 테이블 프록시 역할을 하는 Virtual Table을 통해 접근 – Cold Data
- Select만 가능, Procedure 만들어서 Hot Data 접근 가능(?)
- 하이브 메타스토어를 이용하여 HDFS에 접근하게 되므로 HDFS에 대한 권한 또는 Owner 설정이 필요함
- HBase는 현재 접근이 불가능한 것으로 추정됨

`암바리 서버 : util1.tipsbdsys (192.168.1.134)`

`스파크 컨트롤 설치 호스트 : sparkc.tipsbdsys (192.168.1.147) sparkc / sparkc!@ , root / WelcomeSparkc`



You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

이미지 삽입 테스트

이미지 시작
![My helpful screenshot](/images/shdi1593305169_360481421.jpg)
이미지 종료

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
