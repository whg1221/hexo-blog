---
title: 通过属性控制焦点，enter和blur执行同一函数会导致重复执行
date: 2017-10-10 16:13:31
tags:
---
bug描述：<input v-if="item.editable" type="text" name="" class="styleclass dargDiv" @keyup.enter="editComplete(index,$event);" @blur="editComplete(index,$event);" v-focus />此dom的获取焦点同是否显示相绑定，显示又同editable属性相绑定，失焦时能够顺利执行editComplete函数，但enter时会执行两次，因为editComplete函数改变了editable的属性。

解决方案：<input v-if="item.editable" type="text" name="" class="styleclass dargDiv" @keyup.enter="editCompleteEnter(index,$event);" @blur="editCompleteBlur(index,$event);" v-focus />绑定两个不同的函数，前一个仅仅是改变editable状态去触发后一个函数。

editCompleteEnter: function(index,$event) {
    // 触发blur
    this.selectedQuickFilterTagList[index].editable = false;
},

editCompleteBlur: function(index,$event) {
    this.nowEditing = $event.target.value;
    if(this.nowEditing) {
        this.selectedQuickFilterTagList[index].quickFilterTagName = this.selectedQuickFilterTagList[index].quickFilterTagAliasName;
        this.selectedQuickFilterTagList[index].quickFilterTagAliasName = $event.target.value;
    }
    this.selectedQuickFilterTagList[index].editable = false;
    this.nowEditing = "";
}