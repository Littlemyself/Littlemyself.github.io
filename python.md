![image-20210210215025674](https://qn.ymfgm.com/wp-content/uploads/2021/02/20210210215032.png)



```shell
WARNING: You are using pip version 20.2.3; however, version 21.0.1 is available.
You should consider upgrading via the 'd:\python3.9\python.exe -m pip install --upgrade pip' command.
```

```shell
python -m pip install -U --force-reinstall pip
```


```shell
pip install PyPDF2
```


![image-20210210215902923](https://qn.ymfgm.com/wp-content/uploads/2021/02/20210210215902.png)

提示上面错误关闭代理软件



```shell
from PyPDF2 import PdfFileReader, PdfFileWriter
 
ori="1.pdf"    #源文件
out="output.pdf"    #目标文件
 
pdfReader = PdfFileReader(open(ori, 'rb'))
pdfFileWriter = PdfFileWriter()
numPages = pdfReader.getNumPages()
remove=(1,3)    #要删除的页面，注意起始页为0   
for index in range(0, numPages):
    if index not in remove:
        pageObj = pdfReader.getPage(index)
        pdfFileWriter.addPage(pageObj)
pdfFileWriter.write(open(out, 'wb'))
```

