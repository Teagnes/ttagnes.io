# 使用vba下载outlook一批邮件的附件

需要下载outlook中一批邮件的附件，使用outlook自带的vba即可实现，微软牛逼！



1. #### 首先在收件箱下新建一个test目录

    ![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/1.PNG?raw=true>)

2. #### 然后在硬盘中新建一个用于保存文件的目录 ，这里使用e盘中的outlook目录来保存附件

3. #### 打开outlook的宏设置，点击outlook的右上角的  

   <b>文件</b> 

   ![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/3.PNG?raw=true>)

   <b>--->  选项 </b>  

   ![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/4.PNG?raw=true>)

   <b>--->  信任中心 ---> 信任中心设置  ---> </b>

   ![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/5.PNG?raw=true>)

    <b>宏设置  --->  启用所有宏  --->  确认</b>

   ![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/6.PNG?raw=true>)

   

   

4. #### 添加outlook的开发工具栏，点击outlook的右上角的文件 --->  选项   --->  自定义功能区     --->   在右边的栏目中勾选  <b>开发工具</b>

   ![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/7.PNG?raw=true>)

5. #### 点击开发工具进入vba中，或者按住 ctrl+f11，

   ![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/8.PNG?raw=true>)

6. #### 双击左侧的thisOutlookSession，在弹出的编辑框里输入下面的代码，注意如果outlook中的目录和保存文件的目录里如果和我的不一样，请相应的修改

   

   <b>保存文件的目录:</b> att.SaveAsFile "E:\outlook\" & att.FileName

   <b>收件箱中的子目录: </b>   myFolder.Folders("test")

![avatar](https://github.com/Teagnes/ttagnes.io/blob/master/images/2.PNG?raw=true>)



```
Sub Savethep_w_upload()
    Dim olApp As New Outlook.Application
    Dim nmsName As Outlook.NameSpace
    Dim vItem As Object
    Set nmsName = olApp.GetNamespace("MAPI")
    Set myFolder = nmsName.GetDefaultFolder(olFolderInbox)
    Set fldFolder = myFolder.Folders("test")
        
    For Each vItem In fldFolder.Items
       '-----Save Attachment-------
        For Each att In vItem.Attachments
            att.SaveAsFile "E:\outlook\" & att.FileName
        Next
        '------Save Attachment--------
    Next
    
    Set fldFolder = Nothing
    Set nmsName = Nothing
End Sub

```





6. #### 将代码贴到编辑框中后按ctrl+s 保存（或者点击保存按钮），再将你所有需要提取附件的邮件复制到test文件下 ，最后然后按f5 执行，等待程序运行完后，即可在保存目录下看到邮件中的附件