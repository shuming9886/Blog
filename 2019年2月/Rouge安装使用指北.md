# Rouge安装使用指北

1.在Linux服务器中，输入如下代码：

    pip install pyrouge

2.从Github上下载 ROUGE-1.5.5，地址为， https://github.com/andersjo/pyrouge

3.将pyrouge下载后解压到本地，在tools目录下，将文件ROUGE-1.5.5放置在Linux服务器中指定文件夹下，开始运行会出现

    OSError :[Errno 13] Permission denied

解决办法是，修改文件ROUGE-1.5.5权限

![pic1](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-15-08.png)

划红线的方框打勾。

4.再次运行，可能会出现如下错误，

    returned non-zero exit status 2

解决方法是，依次运行如下代码，

    cd ROUGE-1.5.5/data/
    rm WordNet-2.0.exc.db
    ./WordNet-2.0-Exceptions/buildExeptionDB.pl ./WordNet-2.0-Exceptions ./smart_common_words.txt ./WordNet-2.0.exc.db

5.但是再次运行，又出现了问题...

    Can't locate XML/Parser.pm in @INC (you may need to install the XML::Parser module) (@INC contains: /root/textrank/ROUGE-1.5.5 /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.26.1 /usr/local/share/perl/5.26.1 /usr/lib/x86_64-linux-gnu/perl5/5.26 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.26 /usr/share/perl/5.26 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base) at /root/textrank/ROUGE-1.5.5/XML/DOM.pm line 41.
    BEGIN failed--compilation aborted at /root/textrank/ROUGE-1.5.5/XML/DOM.pm line 70.
    Compilation failed in require at /root/textrank/ROUGE-1.5.5/ROUGE-1.5.5.pl line 177.
    BEGIN failed--compilation aborted at /root/textrank/ROUGE-1.5.5/ROUGE-1.5.5.pl line 177.
    Traceback (most recent call last):
      File "rouge_Q+Z.py", line 9, in <module>
        output = r.convert_and_evaluate()
      File "/usr/local/lib/python2.7/dist-packages/pyrouge/Rouge155.py", line 361, in convert_and_evaluate
        rouge_output = self.evaluate(system_id, rouge_args)
      File "/usr/local/lib/python2.7/dist-packages/pyrouge/Rouge155.py", line 336, in evaluate
        rouge_output = check_output(command).decode("UTF-8")
      File "/usr/lib/python2.7/subprocess.py", line 223, in check_output
        raise CalledProcessError(retcode, cmd, output=output)
    subprocess.CalledProcessError: Command '[u'/root/textrank/ROUGE-1.5.5/ROUGE-1.5.5.pl', '-e', '/root/textrank/ROUGE-1.5.5/data', '-c', '95', '-2', '-1', '-U', '-r', '1000', '-n', '4', '-w', '1.2', '-a', u'-m', u'/tmp/tmpIXA6xf/rouge_conf.xml']' 
    returned non-zero exit status 2

通过一番搜索，找到了解决办法

    sudo apt-get install libxml-parser-perl

It works!

![pic2](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-15-09.png)