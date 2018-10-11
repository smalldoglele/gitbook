```js
$("#memberId").combobox().next().children(":text").blur(function(){
    var val=$(this).val();
    console.log(">>>"+val);
    var storeId=$("#storeId").combobox("getValue");
     var comboxList=$("#memberId").combobox("getData");
    console.log(comboxList);
    var selectVal="";
    for(var i=0;i<comboxList.length;++i){
        var opt=comboxList[i];
        //storeId相等并且输入的val包含在所有的memNameList中
        if(opt.storeId=storeId && opt.memName.indexOf(val)>-1){
            selectVal=opt.id;
            break;
        }
    }
    console.log(selectVal);
    if(selectVal){
        $("#memberId").combobox("setValue",selectVal);
    }else{
        $("#memberId").combobox("setValue","");
    }
});
```