#### jquery-plugin-validate

[官网](https://jqueryvalidation.org/) [菜鸟教程](http://www.runoob.com/jquery/jquery-plugin-validate.html)

* 给表单加上验证事件
  ```js
  var validator=$("#formId").validate();
  ```
* 表单验证触发：

  1.默认验证会在表单元素失去焦点的时候触发  
  2.重要：验证会在表单提交的时候触发

  触发表单提交有两种方式:

  * form中的一个input\[type=submit\]按钮被点击了 
  * 使用form.submit\(\)提交

    上述两种方式都可以触发表单验证

* 手动触发表单验证
  ```js
  $("#formId").valid();
  ```
  
* 手动触发一个元素的验证

  ```js
  validator.element("#elementId");
  //或者
  $("#formId").validate().element("#elemnetId");
  ```



