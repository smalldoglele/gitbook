## jQuery Validation Plugin  使用纪要
[jQuery Validation Plugin  菜鸟教程](http://www.runoob.com/jquery/jquery-plugin-validate.html)

[jQuery Validation Plugin  官方仓库地址](https://github.com/jquery-validation/jquery-validation)

[jQuery Validation Plugin  官网地址](https://jqueryvalidation.org/)

##### 使用方法
```
$('#formId').validate();
```

#### 触发验证
1.submit表单触发

    + input type="submit" 自动
    
    + button 标签 默认类型是submit 自动
    
    + input type="button" 手动验证
    
> 因为button 有三种类型：submit button reset，且默认类型是submit
> 所以这里会有大坑，开发过程中建议用`<input type='button' value='提交'/>`
> 来代替`<button>提交</button>`

2.手动验证
```
var validator=$('#formId').validate();
validator.form(); // 触发验证表单
validator.focusInvalid();//焦点停在第一个验证出错的表单元素上
```

3.取消submit验证行为
```
$("#formId").validate({onsubmit:false});
```

