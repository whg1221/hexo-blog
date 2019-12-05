---
title: getFieldDecorator无效
date: 2019-10-14 16:17:31
tags:
---
bug描述：getFieldDecorator无效
解决：需要 @Form.create() ，才能在this.props下面创建form对象